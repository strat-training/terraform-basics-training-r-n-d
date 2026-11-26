# Solution Design: Terraform Concepts & Best Practices Training (4-Week Self-Paced)

| | |
| --- | --- |
| **Source** | PRD: Terraform Concepts & Best Practices Training (Oct 1, 2026, @Lee) |
| **Status** | Draft for review |
| **Date** | October 1, 2026 |
| **Related** | [ADR index](adrs/README.md) |
| **Revision** | 2026-10-01: source hosting and CI changed from GitHub to GitLab (see ADR-016). 2026-11-26: the GCP and Azure module and the capstone were removed; the course is AWS only (see [ADR-017](adrs/ADR-017-aws-only-no-capstone.md)) |

This document describes how the program in the PRD will be built and run: the content system, the learner environment, the check scripts and content CI. Each significant choice links to an ADR. Items the PRD does not settle are listed in section 11 as assumptions or open items rather than silently decided.

---

## 1. Summary

The program is delivered as **9 Markdown modules in a GitLab starter repository**, run in a **pinned dev container** (local, or GitLab Workspaces if enabled), against **pre-made AWS sandbox accounts**. Each activity has a **local check script** and a **reference solution**. A **content CI pipeline** tests every activity against the pinned Terraform and provider versions so the content cannot silently rot. There is no LMS and no instructor in the loop.

The course is **AWS only and has no capstone project** ([ADR-017](adrs/ADR-017-aws-only-no-capstone.md)). The earlier design of a GCP and Azure setup module and a three-cloud capstone was removed on 2026-11-26.

### Key design decisions at a glance

| # | Decision | ADR |
| --- | --- | --- |
| 1 | Markdown modules in a Git repo; no LMS or external grader | [ADR-001](adrs/ADR-001-delivery-as-markdown-in-starter-repo.md) |
| 2 | Teach Terraform CLI; OpenTofu is a sidebar only | [ADR-002](adrs/ADR-002-terraform-cli-with-opentofu-sidebar.md) |
| 3 | ~~AWS first; GCP and Azure are setup-only plus one storage resource each~~ Superseded: AWS only | [ADR-003](adrs/ADR-003-aws-primary-gcp-azure-setup-only.md), [ADR-017](adrs/ADR-017-aws-only-no-capstone.md) |
| 4 | Pinned dev container, run locally; GitLab Workspaces optional | [ADR-004](adrs/ADR-004-pinned-dev-container.md) |
| 5 | Pre-made sandboxes; SSO / CLI logins, no static keys | [ADR-005](adrs/ADR-005-sandbox-accounts-and-short-lived-credentials.md) |
| 6 | S3 backend with native locking (`use_lockfile`), Terraform 1.11+ | [ADR-006](adrs/ADR-006-s3-remote-state-native-locking.md) |
| 7 | One configuration, per-environment `.tfvars` and backend config files | [ADR-007](adrs/ADR-007-environments-via-tfvars-and-backend-config.md) |
| 8 | Declarative refactoring (`moved`, `import`, `removed`) over `state mv` / `state rm` | [ADR-008](adrs/ADR-008-declarative-refactoring-blocks.md) |
| 9 | Local check scripts built on native Terraform commands | [ADR-009](adrs/ADR-009-local-check-scripts.md) |
| 10 | Content CI with pinned versions and scheduled runs | [ADR-010](adrs/ADR-010-content-ci-and-version-pinning.md) |
| 11 | Cost controls: destroy at the end of every activity, no NAT gateways | [ADR-011](adrs/ADR-011-cost-and-destroy-controls.md) |
| 12 | ~~Capstone is one root module, one apply, three clouds, one state~~ Superseded: no capstone | [ADR-012](adrs/ADR-012-capstone-single-root-multi-cloud.md) |
| 13 | ~~Capstone app delivered as EC2 user-data templates, secrets via RDS-managed secret~~ Superseded: no capstone | [ADR-013](adrs/ADR-013-capstone-app-delivery-and-secrets.md) |
| 14 | ~~Off-site backup to GCS uses federated identity, not exported keys~~ Superseded: no capstone | [ADR-014](adrs/ADR-014-offsite-backup-without-static-keys.md) |
| 15 | Sandbox-compatible tooling only (no OPA/Sentinel, no paid SaaS) | [ADR-015](adrs/ADR-015-sandbox-compatible-tooling-only.md) |
| 16 | Source hosting and content CI on GitLab (replaces the PRD's GitHub, Codespaces and Actions) | [ADR-016](adrs/ADR-016-gitlab-for-hosting-and-ci.md) |
| 17 | AWS only: remove the GCP and Azure module and the capstone | [ADR-017](adrs/ADR-017-aws-only-no-capstone.md) |

ADR-001 to ADR-006, ADR-011 and ADR-015's exclusions come directly from PRD decisions. ADR-016 comes from stakeholder direction (code is kept in GitLab) and amends ADR-001, ADR-004 and ADR-010; the PRD wording needs a matching update. ADR-007 to ADR-010 are **proposed** by this design and need owner sign-off. ADR-017 records the removal of the GCP and Azure module and the capstone: it supersedes ADR-003 and ADR-012 to ADR-014 and amends ADR-001, ADR-004, ADR-005, ADR-006, ADR-009, ADR-010, ADR-011, ADR-015 and ADR-016. The PRD still assumes them (A13).

---

## 2. Goals mapped to design

| PRD goal | How the design delivers it |
| --- | --- |
| Teach core concepts (providers, resources, state, plan/apply...) | 9 modules, one activity each, in a fixed order with a weekly checkpoint |
| Build best-practice habits | The 14-practice checklist (PRD s.10) is encoded as check-script assertions; see section 7 |
| AWS first, then GCP and Azure | Descoped: AWS only, in Modules 1-9. The PRD goal needs updating (A13) |
| Fully self-paced, auto-checked | Local check scripts plus answer keys; no instructor or LMS (ADR-001, ADR-009) |
| 70% completion | Graded hints, check-script feedback with hints, FAQ, community channel; see section 9 |

---

## 3. System context

```
                      +-----------------------------+
                      |  GitLab group               |
                      |  - starter repo (modules,   |
                      |    activities, CI)          |
                      |  - CI/CD, container registry|
                      +--------------+--------------+
                                     |  clone / open in dev container
                                     v
 +-----------------------------------------------------------------+
 |  Learner workspace: dev container                               |
 |  Terraform >= 1.11 | AWS CLI | check scripts                    |
 +------------------------------+----------------------------------+
                                | aws sso login
                                v
                         AWS sandbox account
                         (S3 state bucket kept
                          from Activity 7)
```

Actors:

- **Learner**: works in the dev container, runs checks locally, keeps a "what broke" note in their own repo.
- **Content team**: writes modules, activities, solutions, check scripts, quiz banks; owns CI.
- **Platform owner of sandboxes** (outside this program): provisions accounts, budgets and guardrails.

---

## 4. Content architecture

### 4.1 Starter repository layout

```
terraform-training/
|-- README.md                      # how to start, progress checklist (FR-1)
|-- .devcontainer/                 # pinned toolchain (ADR-004)
|-- modules/                       # the 9 reading files
|   |-- 01-environment-setup.md
|   `-- ...
|-- quizzes/                       # weekly quizzes + answer keys (FR-2)
|-- cheatsheets/                   # one page per module (CR-2); PDF export is should-have (CR-7)
|-- activities/
|   `-- module-1/ ... module-9/
|       |-- starter/
|       |-- solution/
|       |-- hints.md               # graded hints, level 1 to 3
|       `-- check                  # check script (ADR-009)
|-- tools/
|   |-- check-lib/                 # shared check helpers
|   `-- ci/                        # CI harness, scheduled tests
|-- FAQ.md                         # common errors (FR-6)
`-- .gitlab-ci.yml                 # merge request, scheduled and tag pipelines (ADR-010, ADR-016)
```

> Note: the PRD calls the reading files "module Markdown files" and also uses `activities/module-N/`. To avoid a name clash with Terraform "modules", the reading folder is named `lessons/` in the final repo if the team prefers. Content authors should decide before authoring starts; the structure above is otherwise unchanged.

### 4.2 Module template (CR-2, CR-3, CR-5)

Every module file contains, in order: learning objectives, prerequisites, estimated time, the 30-45 minute reading, link to the one-page cheat sheet, a "versions this was written for" line, links to official docs, and a pointer to the activity folder. Every activity folder contains a goal statement, starter code, graded hints, a check script and a solution.

### 4.3 Progress tracking

Progress is a Markdown checklist in the repo README that learners tick in their own fork or local copy (FR-1). Weekly quizzes are self-checked against answer keys (FR-2, PRD s.12). This is deliberately low-tech; consequences, including no central completion data, are in ADR-001 and section 9.

---

## 5. Learner environment

| Element | Design | ADR |
| --- | --- | --- |
| Runtime | Dev container run locally (Docker or Podman); optionally GitLab Workspaces if the instance offers them; Terraform 1.11+ pinned, AWS CLI | ADR-004, ADR-016 |
| Local install path | Documented alternative using `tfenv` or `mise` (Module 1 teaches it) | ADR-004 |
| Offline practice | Optional LocalStack for S3-only exercises; VPC/EC2 activities always use real AWS | ADR-004 |
| Credentials | AWS IAM Identity Center (SSO) | ADR-005 |
| Static keys | Check script fails if `~/.aws/credentials` holds access keys or if repo contains key patterns | ADR-005, ADR-009 |
| Accounts | Pre-made sandboxes, provided outside this program | ADR-005 |
| Source hosting and CI | GitLab group and project, GitLab CI/CD, Container Registry | ADR-016 |

Why SSO is the learner default: it is the best practice the course teaches, it produces short-lived credentials, and it makes the "no static keys" check meaningful.

---

## 6. Activity design

### 6.1 Check scripts

Each activity has a `check` script the learner runs locally (FR-4). Shared helpers live in `tools/check-lib/`. A check script:

1. Runs `terraform fmt -check -recursive` and `terraform validate`.
2. Runs the plan checks specific to the activity (for example, "no hard-coded CIDR in `main.tf`", "plan shows zero destroys and zero replacements").
3. Where state is involved, queries the sandbox (for example, confirms the S3 state object exists and versioning is on) using the learner's own credentials.
4. Confirms the stack is destroyed (except Activity 7's state bucket).
5. Scans for secrets and static keys.
6. Prints pass or fail per item, with a one-line hint on failure.

Plan checks use `terraform show -json` on a saved plan and assert on the JSON (resource addresses, `actions` per change), so checks are stable against cosmetic output changes. Note that checks are run by the learner and are therefore **self-reported**; the PRD accepts this (section 12). Nothing in the program is externally verified.

### 6.2 Activity map and what the check asserts

| Activity | Key technical assertion |
| --- | --- |
| 1 Toolchain | Terraform >= 1.11, `aws sts get-caller-identity` works, no static keys on disk |
| 2 Providers | `required_version` and `required_providers` set, lock file committed, `terraform providers` lists `aws` and `random` |
| 3 Apply/change/replace | fmt/validate pass, note names in-place vs replace correctly, bucket gone |
| 4 Network | Plan contains expected resources, subnets use `for_each`, destroyed afterwards |
| 5 Variables | Invalid CIDR rejected at plan time, both `.tfvars` plan clean, no hard-coded region/CIDR/instance type in `main.tf` |
| 6 State and drift | Final plan clean, written answers match model answer |
| 7 Remote state | State object exists in bucket, versioning on, backend sets `use_lockfile` |
| 8 Environments | Two state objects under different keys, both plans clean, required tags on all resources |
| 9 Refactor | After each of three steps: zero destroys and zero replacements |

### 6.3 Pacing and unlocking

Weeks are followed in order, and progress to the next week follows passing the weekly checkpoint (PRD s.5). Because there is no LMS, "gating" is by convention and by the checklist, not enforced by software. The solution folders sit in the same repository; learners are asked to open them only after attempting hints. This is a trust-based design and is acceptable for the target audience (working engineers).

### 6.4 State bucket lifecycle across activities

Activity 7 creates the state bucket and **keeps it**. All later activities (8 and 9) reuse it with separate state keys. The destroy check in later activities explicitly excludes it. Learners who finish the course can destroy it with a documented clean-up step at the end of the last module (Module 9).

---

## 7. Best-practice enforcement

The PRD lists 14 practices (s.10) and requires each to appear in at least one activity and one quiz question (CR-4). The design makes this verifiable by keeping a **coverage matrix** in `tools/ci/coverage.yaml`, mapping each practice to an activity check and a quiz question ID. CI fails if a practice has no mapped check or question. Practice 14 (cloud differences explicit) lost its only activity when Module 10 was removed, so it has to be dropped from the matrix or covered another way (A13).

| Practice | Where enforced (check or rubric) |
| --- | --- |
| Pinned versions, lock file | Activity 2 check |
| No static credentials | Activity 1 check |
| fmt and validate | Every check script |
| Plan review | Activity 3 note; Activity 9 plan assertions |
| Implicit dependencies | Activity 4 note |
| `for_each` over `count` | Activity 4 check |
| Typed, validated inputs | Activity 5 check |
| State hygiene | Activity 6 answers; Activity 7 bucket checks |
| Remote state with locking | Activity 7 check |
| Separate state per environment | Activity 8 check |
| Layout and naming | Activity 8 check |
| `default_tags` | Activity 2, 8 checks |
| Refactoring blocks | Activity 9 check |
| Cloud differences explicit | **Not enforced anywhere** since Module 10 was removed (A13) |

---

## 8. Capstone (removed)

The capstone (Terraform Flashcard Quiz) and the GCP and Azure module were removed on 2026-11-26 ([ADR-017](adrs/ADR-017-aws-only-no-capstone.md)). This section held its topology, root-module layout, dependency order, "provision, prove, tear down" mapping, security design and cost design. They are no longer part of the design; the earlier text is in git history, and the reasoning is kept in the superseded ADR-012, ADR-013 and ADR-014. The section number is kept so references to sections 9 to 14 stay valid.

---

## 9. Learner support and completion strategy

PRD target: 70% completion. The design addresses the main drop-off drivers.

| Drop-off driver | Design response |
| --- | --- |
| Stuck with no instructor | Three-level graded hints; check script messages that name the failing item and a hint; FAQ of common errors; community channel with a stated response time (FR-6) |
| Environment problems | Dev container with pinned tools; Module 1 is entirely about getting a working toolchain |
| Time pressure | Recommended pace but modules stay available; pause and resume supported |
| Fear of cost | Explicit destroy steps and a clean-up check at every activity end |

**Measurement without an LMS.** Completion and pass data come from the post-course survey (PRD s.2). This is weaker than telemetry. If the pilot shows low response rates, add an opt-in lightweight telemetry step to the check script (for example, writing a signed pass receipt the learner submits). This is an open item (section 11).

---

## 10. Quality, CI and maintenance

Summarised from ADR-010.

- **Pinned versions.** One file (`versions.env`) defines the Terraform version and the provider versions for the program. The dev container, activities and CI all read from it.
- **Per-merge-request CI** (GitLab merge request pipelines). For every activity: format and validate the starter and solution; run the check script against the solution and expect pass; run the check script against the starter and expect specific failures (so checks are not vacuous). Activities that need real cloud use a dedicated CI sandbox with a nightly teardown sweeper, authenticated through GitLab CI/CD ID tokens (OIDC federation) with no stored cloud keys (ADR-016).
- **Scheduled CI (weekly).** A GitLab scheduled pipeline re-runs everything against the pinned versions and, separately, against the latest provider versions in "canary" mode, so upcoming breakage is visible before a version bump (CR-1).
- **Triggered review.** After each Terraform minor release, and after an AWS provider major release, the content owner reviews affected activities using the CI report (PRD s.13). A six-monthly full review is calendared.
- **Verification note from the PRD.** Before content is built, re-check against release notes of the pinned Terraform version: native S3 locking, `moved`, `import` and `removed` blocks, and `-generate-config-out`.

---

## 11. Assumptions, open items and PRD observations

These are points the PRD leaves open or where the design had to choose. Each should be confirmed by the program owner before content build begins.

| # | Item | Why it matters | Proposed handling |
| --- | --- | --- | --- |
| A1 | ~~How the DB backup reaches GCS in one apply with no static keys.~~ | | **Withdrawn**: the capstone was removed (ADR-017). ADR-014 is superseded and the spike is no longer needed. |
| A2 | ~~What `data/db-seed-and-dump.sh` does exactly.~~ | | **Withdrawn**: no capstone `data/` folder. |
| A3 | ~~Secrets approach for the provided app templates.~~ | | **Withdrawn**: no capstone app. ADR-013 is superseded. |
| A4 | ~~Browser access to Azure Blob assets.~~ | | **Withdrawn**: no Azure content. |
| A5 | **Remote-state bucket prerequisite for later activities.** Activities 8 and 9 reuse the bucket that Activity 7 creates, and learners may skip or have destroyed it. | Prerequisite for Activities 8 and 9 | Carried over from the capstone: Activities 8 and 9 include a "verify or recreate state bucket" step reusing the Activity 7 solution. |
| A6 | **Starter repo folder naming.** `modules/` for reading files collides with Terraform's term. | Learner confusion | See note in 4.1. |
| A7 | ~~Hours per week.~~ | | **Withdrawn**: it was about Week 4 and the capstone. The week plan is now open (A13). |
| A8 | ~~"Activities (10)" weight in the assessment table.~~ | | **Withdrawn**: it split the assessment between Activities 1-10 and the capstone. The assessment is now open (A13). |
| A9 | **Check-script integrity.** Checks run locally and are self-reported. | Credential and certification value | Acceptable per PRD (no certification goal). There is no external gate now that the capstone is removed. |
| A10 | ~~Module 10 backends.~~ | | **Withdrawn**: no GCP or Azure content. |
| A11 | **GitLab specifics are unknown**: gitlab.com or self-managed, tier, runner type, whether the runners can build container images, and whether GitLab Workspaces are enabled. | Browser-only access, CI cloud auth, dev container build | ADR-016 and ADR-004 are written to work without Workspaces. Confirm with the GitLab owner in weeks 1-2. If self-managed, check that AWS can reach its OIDC issuer URL. |
| A12 | **PRD still names GitHub, Codespaces and Actions** (s.3, s.13 FR-3 and FR-7, s.14 dependencies). | Source-of-truth drift between PRD and design | Update the PRD wording; add a Docker/Podman check to the pre-assessment, since without Workspaces there is no browser-only path. |
| A13 | **The PRD and plan still assume GCP, Azure and the capstone** ([ADR-017](adrs/ADR-017-aws-only-no-capstone.md)): the "AWS first, then GCP and Azure" goal, Week 4 and its hours, the assessment weights (activities 40%, capstone 40%), the 100-point capstone rubric, FR-7 (peer review of the capstone), CR-8 (capstone `data/`), and best practice 14 (cloud differences explicit), which now has no activity. | PRD and design disagree; CI's coverage matrix fails on practice 14 | Program owner to update the PRD and decide the week plan for 9 modules, what (if anything) is the summative assessment, and whether to drop practice 14. Open. |

---

## 12. Requirements traceability

| PRD requirement | Design element | Section / ADR |
| --- | --- | --- |
| FR-1 Markdown modules and progress checklist | Starter repo, README checklist | 4, ADR-001 |
| FR-2 Ordered weeks, quizzes with answer keys | `quizzes/` with answer keys | 4, 6.3 |
| FR-3 Activities run from dev container with pinned tools | Dev container, `versions.env` | 5, ADR-004 |
| FR-4 Local check script with pass/fail and hint | `check` scripts, `check-lib` | 6.1, ADR-009 |
| FR-5 Pre-made sandboxes, not managed here | Out of scope; documented prerequisite | 3, ADR-005 |
| FR-6 Community channel and FAQ with response time | `FAQ.md`, channel, stated SLA | 9 |
| CR-1 Activity code tested in CI against pinned version | Content CI | 10, ADR-010 |
| CR-2 Objectives, prerequisites, time, cheat sheet | Module template | 4.2 |
| CR-3 One activity per module with starter, hints, check, solution | Activity folder structure | 4.1, 6 |
| CR-4 Each best practice in an activity and a quiz question | Coverage matrix enforced in CI | 7 |
| CR-5 Official docs links and version notes | Module template | 4.2 |
| CR-8 Capstone `data/` ships and is tested | Removed with the capstone. Open (A13) | ADR-017 |
| FR-7 Peer review through merge requests (should) | Not applicable now: it reviewed the capstone. Open (A13) | ADR-016, ADR-017 |
| CR-6 OpenTofu sidebar (should) | Sidebar in Module 1 or 2 | ADR-002 |
| CR-7 Cheat-sheet PDFs (should) | Markdown to PDF in CI | 4.1 |

---

## 13. Delivery plan alignment

The PRD launch plan (16 weeks) maps to the design as follows.

| PRD weeks | Design work |
| --- | --- |
| 1-2 | Confirm audience and metrics; create repo skeleton, `versions.env`, dev container, CI skeleton; confirm sandbox permissions (A11) |
| 3-8 | Author Weeks 1-4 content in order; each activity lands with starter, solution, hints, check script and CI job together |
| 9 | Internal review: content, security (secret scan, IAM, SG review), cost (run every activity and record actual spend) |
| 10-15 | Pilot with 10-15 learners; collect survey data; watch for time overruns and sandbox policy issues |
| 16 | Revise and launch |

## 14. Risks specific to this design

| Risk | Mitigation |
| --- | --- |
| Check scripts produce false passes or false failures | CI runs each script against both solution (must pass) and starter (must fail on named items) |
| CI cloud sandbox cost or leaked resources | Nightly sweeper, budget alarm on the CI sandbox, small instance types |
| Learners skip the state bucket in Activity 7 | Verify/recreate step in Activities 8 and 9 (A5) |
| Provider canary breaks surface late | Weekly canary run, owner assigned, triage SLA |
| No browser-only option for learners whose laptops cannot run containers | Pre-assessment checks for Docker or Podman; GitLab Workspaces if enabled; local install path from Module 1 (ADR-004) |
| GitLab runners cannot build the dev container image, or cloud providers cannot trust the GitLab OIDC issuer | Confirm runner capability and issuer reachability in weeks 1-2 (A11); fall back to a pre-built image published manually |
