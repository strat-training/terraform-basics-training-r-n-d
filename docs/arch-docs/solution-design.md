# Solution Design: Terraform Concepts & Best Practices Training (4-Week Self-Paced)

| | |
| --- | --- |
| **Source** | PRD: Terraform Concepts & Best Practices Training (Oct 1, 2026, @Lee) |
| **Status** | Draft for review |
| **Date** | October 1, 2026 |
| **Related** | [ADR index](adrs/README.md) |
| **Revision** | 2026-10-01: source hosting and CI changed from GitHub to GitLab (see ADR-016) |

This document describes how the program in the PRD will be built and run: the content system, the learner environment, the check scripts, content CI, and the capstone architecture. Each significant choice links to an ADR. Items the PRD does not settle are listed in section 11 as assumptions or open items rather than silently decided.

---

## 1. Summary

The program is delivered as **11 Markdown modules in a GitLab starter repository**, run in a **pinned dev container** (local, or GitLab Workspaces if enabled), against **pre-made sandbox accounts** on AWS, GCP and Azure. Each activity has a **local check script** and a **reference solution**. A **content CI pipeline** tests every activity against the pinned Terraform and provider versions so the content cannot silently rot. There is no LMS and no instructor in the loop.

The capstone (Terraform Flashcard Quiz) is a single Terraform root configuration that provisions a 3-tier app on AWS Singapore, a backup bucket on GCP and an assets container on Azure with **one `terraform apply`**, using S3 remote state.

### Key design decisions at a glance

| # | Decision | ADR |
| --- | --- | --- |
| 1 | Markdown modules in a Git repo; no LMS or external grader | [ADR-001](adrs/ADR-001-delivery-as-markdown-in-starter-repo.md) |
| 2 | Teach Terraform CLI; OpenTofu is a sidebar only | [ADR-002](adrs/ADR-002-terraform-cli-with-opentofu-sidebar.md) |
| 3 | AWS first; GCP and Azure are setup-only plus one storage resource each | [ADR-003](adrs/ADR-003-aws-primary-gcp-azure-setup-only.md) |
| 4 | Pinned dev container, run locally; GitLab Workspaces optional | [ADR-004](adrs/ADR-004-pinned-dev-container.md) |
| 5 | Pre-made sandboxes; SSO / CLI logins, no static keys | [ADR-005](adrs/ADR-005-sandbox-accounts-and-short-lived-credentials.md) |
| 6 | S3 backend with native locking (`use_lockfile`), Terraform 1.11+ | [ADR-006](adrs/ADR-006-s3-remote-state-native-locking.md) |
| 7 | One configuration, per-environment `.tfvars` and backend config files | [ADR-007](adrs/ADR-007-environments-via-tfvars-and-backend-config.md) |
| 8 | Declarative refactoring (`moved`, `import`, `removed`) over `state mv` / `state rm` | [ADR-008](adrs/ADR-008-declarative-refactoring-blocks.md) |
| 9 | Local check scripts built on native Terraform commands | [ADR-009](adrs/ADR-009-local-check-scripts.md) |
| 10 | Content CI with pinned versions and scheduled runs | [ADR-010](adrs/ADR-010-content-ci-and-version-pinning.md) |
| 11 | Cost controls: destroy at the end of every activity, NAT only in capstone | [ADR-011](adrs/ADR-011-cost-and-destroy-controls.md) |
| 12 | Capstone is one root module, one apply, three clouds, one state | [ADR-012](adrs/ADR-012-capstone-single-root-multi-cloud.md) |
| 13 | Capstone app delivered as EC2 user-data templates, secrets via RDS-managed secret | [ADR-013](adrs/ADR-013-capstone-app-delivery-and-secrets.md) |
| 14 | Off-site backup to GCS uses federated identity, not exported keys | [ADR-014](adrs/ADR-014-offsite-backup-without-static-keys.md) |
| 15 | Sandbox-compatible tooling only (no OPA/Sentinel, no paid SaaS) | [ADR-015](adrs/ADR-015-sandbox-compatible-tooling-only.md) |
| 16 | Source hosting and content CI on GitLab (replaces the PRD's GitHub, Codespaces and Actions) | [ADR-016](adrs/ADR-016-gitlab-for-hosting-and-ci.md) |

ADR-001 to ADR-006, ADR-011 and ADR-015's exclusions come directly from PRD decisions. ADR-016 comes from stakeholder direction (code is kept in GitLab) and amends ADR-001, ADR-004 and ADR-010; the PRD wording needs a matching update. ADR-007 to ADR-010, ADR-012 to ADR-014 are **proposed** by this design and need owner sign-off.

---

## 2. Goals mapped to design

| PRD goal | How the design delivers it |
| --- | --- |
| Teach core concepts (providers, resources, state, plan/apply...) | 11 modules, one activity each, in a fixed order with a weekly checkpoint |
| Build best-practice habits | The 14-practice checklist (PRD s.10) is encoded as check-script assertions and capstone rubric lines; see section 7 |
| AWS first, then GCP and Azure | AWS in Modules 1-9; Module 10 and capstone add the other two clouds |
| Fully self-paced, auto-checked | Local check scripts plus answer keys; no instructor or LMS (ADR-001, ADR-009) |
| 70% completion | Graded hints, check-script feedback with hints, FAQ, community channel; see section 9 |

---

## 3. System context

```
                      +-----------------------------+
                      |  GitLab group               |
                      |  - starter repo (modules,   |
                      |    activities, data/, CI)   |
                      |  - CI/CD, container registry|
                      +--------------+--------------+
                                     |  clone / open in dev container
                                     v
 +-----------------------------------------------------------------+
 |  Learner workspace: dev container                               |
 |  Terraform >= 1.11 | AWS CLI | gcloud | az | check scripts      |
 +--------+----------------------+----------------------+----------+
          | aws sso login        | gcloud ADC login     | az login
          v                      v                      v
   AWS sandbox account    GCP sandbox project    Azure sandbox subscription
   (S3 state bucket kept  (Week 4 only)          (Week 4 only)
    from Activity 7)
```

Actors:

- **Learner**: works in the dev container, runs checks locally, keeps a "what broke" note in their own repo.
- **Content team**: writes modules, activities, solutions, check scripts, quiz banks; owns CI.
- **Capstone reviewer** (peer or mentor): scores against the 100-point rubric.
- **Platform owner of sandboxes** (outside this program): provisions accounts, budgets and guardrails.

---

## 4. Content architecture

### 4.1 Starter repository layout

```
terraform-training/
|-- README.md                      # how to start, progress checklist (FR-1)
|-- .devcontainer/                 # pinned toolchain (ADR-004)
|-- modules/                       # the 11 reading files
|   |-- 01-environment-setup.md
|   |-- ...
|   `-- 11-capstone.md
|-- quizzes/                       # weekly quizzes + answer keys (FR-2)
|-- cheatsheets/                   # one page per module (CR-2); PDF export is should-have (CR-7)
|-- activities/
|   |-- module-1/ ... module-10/
|   |   |-- starter/
|   |   |-- solution/
|   |   |-- hints.md               # graded hints, level 1 to 3
|   |   `-- check                  # check script (ADR-009)
|   `-- module-11/                 # capstone: starter + rubric + solution
|-- data/                          # capstone app payload (CR-8)
|   |-- templates/{web,app}.sh.tftpl
|   |-- assets/                    # theme and logo for Azure Blob
|   |-- seed.sql
|   |-- db-seed-and-dump.sh
|   `-- bad.tfvars
|-- tools/
|   |-- check-lib/                 # shared check helpers
|   `-- ci/                        # CI harness, scheduled tests
|-- FAQ.md                         # common errors (FR-6)
|-- .gitlab-ci.yml                 # merge request, scheduled and tag pipelines (ADR-010, ADR-016)
`-- .gitlab/                       # merge request templates (capstone review rubric)
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
| Runtime | Dev container run locally (Docker or Podman); optionally GitLab Workspaces if the instance offers them; Terraform 1.11+ pinned, AWS CLI, `gcloud`, Azure CLI | ADR-004, ADR-016 |
| Local install path | Documented alternative using `tfenv` or `mise` (Module 1 teaches it) | ADR-004 |
| Offline practice | Optional LocalStack for S3-only exercises; VPC/EC2 activities always use real AWS | ADR-004 |
| Credentials | AWS IAM Identity Center (SSO); `gcloud auth application-default login`; `az login` | ADR-005 |
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

Plan checks use `terraform show -json` on a saved plan and assert on the JSON (resource addresses, `actions` per change), so checks are stable against cosmetic output changes. Note that checks are run by the learner and are therefore **self-reported**; the PRD accepts this (section 12) and the capstone rubric review is the only externally verified element.

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
| 10 GCP/Azure setup | Both configs validate and plan with identity output, no secrets in repo |
| 11 Capstone | Rubric review (section 8) |

### 6.3 Pacing and unlocking

Weeks are followed in order, and progress to the next week follows passing the weekly checkpoint (PRD s.5). Because there is no LMS, "gating" is by convention and by the checklist, not enforced by software. The solution folders sit in the same repository; learners are asked to open them only after attempting hints. This is a trust-based design and is acceptable for the target audience (working engineers).

### 6.4 State bucket lifecycle across activities

Activity 7 creates the state bucket and **keeps it**. All later activities (8, 9 and the capstone) reuse it with separate state keys. The destroy check in later activities explicitly excludes it. Learners who finish the course can destroy it with a documented clean-up step in the capstone module.

---

## 7. Best-practice enforcement

The PRD lists 14 practices (s.10) and requires each to appear in at least one activity and one quiz question (CR-4). The design makes this verifiable by keeping a **coverage matrix** in `tools/ci/coverage.yaml`, mapping each practice to an activity check and a quiz question ID. CI fails if a practice has no mapped check or question.

| Practice | Where enforced (check or rubric) |
| --- | --- |
| Pinned versions, lock file | Activity 2 check; capstone "Terraform quality" |
| No static credentials | Activity 1, 10 checks; capstone "Security and cost" |
| fmt and validate | Every check script |
| Plan review | Activity 3 note; Activity 9 plan assertions |
| Implicit dependencies | Activity 4 note |
| `for_each` over `count` | Activity 4 check |
| Typed, validated inputs | Activity 5 check; capstone `bad.tfvars` proof |
| State hygiene | Activity 6 answers; Activity 7 bucket checks |
| Remote state with locking | Activity 7 check; capstone |
| Separate state per environment | Activity 8 check |
| Layout and naming | Activity 8 check; capstone |
| `default_tags` | Activity 2, 8 checks; capstone |
| Refactoring blocks | Activity 9 check |
| Cloud differences explicit | Activity 10 note; capstone provider config |

---

## 8. Capstone architecture: Terraform Flashcard Quiz

### 8.1 Topology

```
                         Internet
                            |
                            v
                  +--------------------+
                  |  Web tier (EC2)    |  Nginx + React (data/templates/web.sh.tftpl)
                  |  public subnet     |-----------------------------+
                  +---------+----------+                             |
                            | :8080                                  | browser loads theme/logo
                            v                                        v
                  +--------------------+                  +----------------------+
                  |  App tier (EC2)    |                  | Azure Storage Account |
                  |  private subnet    |                  | + Blob container      |
                  |  Node.js API       |                  | (theme, logo)         |
                  |  /health /db /cards|                  +----------------------+
                  |  /answers /stats   |
                  |  /config           |
                  +----+----------+----+
                       | :3306    | backup (federated identity)
                       v          v
              +----------------+  +-----------------------+
              | RDS MySQL 8.4  |  | GCS bucket            |
              | private subnet |  | (off-site DB backup)  |
              +----------------+  +-----------------------+

   AWS ap-southeast-1: VPC, 2 public + 2 private subnets, 1 NAT gateway (capstone only),
   security groups (internet -> web -> app -> db), IAM instance role, S3 remote state.
```

### 8.2 Terraform root configuration

One root module with three provider configurations (`aws`, `google`, `azurerm`), pinned in `required_providers`. File layout follows Module 8:

```
versions.tf      # required_version, required_providers, lock file committed
providers.tf     # aws (default_tags), google (explicit project), azurerm (features {}, explicit subscription_id)
variables.tf     # typed, described, validated
network.tf       # VPC, subnets, route tables, NAT, security groups
database.tf      # RDS MySQL 8.4, subnet group, managed secret
compute.tf       # web and app EC2, instance profiles, templatefile() of data/templates/*
backup.tf        # GCS bucket, federated identity wiring (ADR-014)
assets.tf        # Azure storage account, container, blobs from data/assets/
outputs.tf       # application URL, bucket name, container URL
backend.hcl      # S3 bucket, key, use_lockfile (supplied via -backend-config)
terraform.tfvars # plus data/bad.tfvars for the failure proof
```

### 8.3 Dependency order inside one apply

Terraform resolves this through references (implicit dependencies, as Module 4 teaches), but the intended order is:

1. Network and security groups, plus the Azure storage account and GCS bucket (independent of AWS).
2. RDS instance and managed secret.
3. Azure blobs from `data/assets/` (so the asset URL is known).
4. App tier (needs RDS endpoint, secret ARN, GCS bucket name).
5. Web tier (needs App tier private address and Azure asset URL, rendered into the template).
6. Outputs.

The app tier must wait for RDS to be reachable before seeding. This is handled in the boot script with a bounded retry loop, not with a Terraform `time_sleep` hack, so the plan stays clean and a re-apply is idempotent.

### 8.4 "Provision, prove, tear down" mapping to Terraform and checks

| Phase | Mechanism | Evidence learner submits |
| --- | --- | --- |
| Provision | `terraform apply` once; `terraform plan` afterwards shows no changes | Apply log tail and clean-plan output |
| Prove it works | Browser test plus `curl` of `/health` and `/db`; reload test; footer inspection; `gsutil ls` or `gcloud storage ls` of the bucket | Screenshots and command output |
| Prove it fails safely | `terraform plan -var-file=data/bad.tfvars` | Output showing the validation error and zero resources planned |
| Tear down | `terraform destroy`, then console or CLI checks per cloud | Output of "nothing left" checks per cloud |

The "nothing left behind" check is provided as a script (`activities/module-11/check-clean`) that lists tagged resources in AWS, labelled resources in GCP, and the resource group in Azure, and reports anything remaining. Resources use `default_tags` / labels / tags so they can be found.

### 8.5 Security design for the capstone

| Risk | Control |
| --- | --- |
| Public database | RDS in private subnets, security group allows port 3306 only from the App tier SG |
| Hard-coded DB password | RDS-managed master secret in Secrets Manager; App tier reads it via instance role (ADR-013) |
| Secrets in state | Avoid `random_password` for the DB; the Module 6 activity demonstrates why |
| Static cloud keys | None. AWS via SSO and instance role; GCP backup via federated identity (ADR-014); Azure uses `az login` for provisioning only |
| Overly open web tier | Security group allows 80/443 from internet only; SSH disabled, SSM Session Manager for access if needed |
| State exposure | S3 state bucket versioned, encrypted, public access blocked, access restricted to the learner role (ADR-006) |
| Public assets | Azure container allows anonymous read of the non-sensitive theme and logo only; nothing else is stored there |

### 8.6 Cost design

- Instance sizes: `t3.micro` or equivalent for both tiers; `db.t4g.micro` (or `db.t3.micro` where unavailable) for RDS, single-AZ, minimal storage, no Multi-AZ, backup retention minimal.
- One NAT gateway (allowed by PRD) so the private App tier can install packages. It is the main hourly cost; the documentation advises completing the "prove" phase in one sitting and destroying promptly.
- GCS bucket in a regional location with a lifecycle rule; Azure Storage Account on the cheapest redundancy tier (LRS).
- Learners are told the expected cost per hour and a "destroy now" reminder is in every capstone step.

---

## 9. Learner support and completion strategy

PRD target: 70% completion. The design addresses the main drop-off drivers.

| Drop-off driver | Design response |
| --- | --- |
| Stuck with no instructor | Three-level graded hints; check script messages that name the failing item and a hint; FAQ of common errors; community channel with a stated response time (FR-6) |
| Environment problems | Dev container with pinned tools; Module 1 is entirely about getting a working toolchain |
| Cloud account friction in Week 4 | Early-access checklist at the start of Week 3; Activity 10 uses read-only data sources; documented AWS-only capstone path as fallback (PRD s.14) |
| Time pressure | Recommended pace but modules stay available; pause and resume supported |
| Fear of cost | Explicit destroy steps and a clean-up check at every activity end |

**Measurement without an LMS.** Completion and pass data come from the post-course survey and capstone submissions (PRD s.2). This is weaker than telemetry. If the pilot shows low response rates, add an opt-in lightweight telemetry step to the check script (for example, writing a signed pass receipt the learner submits). This is an open item (section 11).

---

## 10. Quality, CI and maintenance

Summarised from ADR-010.

- **Pinned versions.** One file (`versions.env`) defines the Terraform version and the provider versions for the program. The dev container, activities and CI all read from it.
- **Per-merge-request CI** (GitLab merge request pipelines). For every activity: format and validate the starter and solution; run the check script against the solution and expect pass; run the check script against the starter and expect specific failures (so checks are not vacuous). Activities that need real cloud use a dedicated CI sandbox with a nightly teardown sweeper, authenticated through GitLab CI/CD ID tokens (OIDC federation) with no stored cloud keys (ADR-016).
- **Scheduled CI (weekly).** A GitLab scheduled pipeline re-runs everything against the pinned versions and, separately, against the latest provider versions in "canary" mode, so upcoming breakage is visible before a version bump (CR-1).
- **Triggered review.** After each Terraform minor release, and after an AWS, Google or AzureRM provider major release, the content owner reviews affected activities using the CI report (PRD s.13). A six-monthly full review is calendared.
- **Capstone `data/` tests (CR-8).** CI renders the boot-script templates, runs shell linting, boots the app against a local MySQL 8.4 container, hits all six endpoints, and validates `seed.sql`, the dump helper and `bad.tfvars` (which must fail validation with the expected message).
- **Verification note from the PRD.** Before content is built, re-check against release notes of the pinned Terraform version: native S3 locking, `moved`, `import` and `removed` blocks, and `-generate-config-out`.

---

## 11. Assumptions, open items and PRD observations

These are points the PRD leaves open or where the design had to choose. Each should be confirmed by the program owner before content build begins.

| # | Item | Why it matters | Proposed handling |
| --- | --- | --- | --- |
| A1 | **How the DB backup reaches GCS in one apply with no static keys.** The PRD requires the backup to be "present in the GCS bucket" after a single apply, with no keys in the repo. The database is private, so a laptop-run provisioner cannot reach it. | Core capstone feasibility | ADR-014 proposes GCP Workload Identity Federation from the App tier's AWS role. **Needs a spike**: sandbox policies may block creating workload identity pools. Fallback: dump seed data from `data/seed.sql` into the bucket from the provisioning host, documented as a reduced-fidelity proof. |
| A2 | **What `data/db-seed-and-dump.sh` does exactly** and where it runs. | Determines A1 | Assumed to seed the DB and produce a dump that can be uploaded. Content authors to confirm. |
| A3 | **Secrets approach for the provided app templates.** The PRD requires "password not hard-coded" but does not say how the app gets it. | App template contract | ADR-013 proposes RDS-managed secret read by the instance role. Templates must be written accordingly. |
| A4 | **Browser access to Azure Blob assets.** The front end loads assets in the browser, which needs anonymous read or SAS URLs, and a CORS rule. Storage accounts in some sandboxes disallow public blob access. | Capstone "footer shows assets loaded" proof | Default to anonymous read on the container for non-sensitive assets; fallback to a time-limited SAS URL generated by Terraform. Confirm sandbox policy. |
| A5 | **Capstone remote-state bucket.** The PRD says remote state in S3 but Activity 7 is the bucket's origin, and learners may skip or have destroyed it. | Capstone prerequisite | Capstone module includes a "verify or recreate state bucket" step reusing the Activity 7 solution. |
| A6 | **Starter repo folder naming.** `modules/` for reading files collides with Terraform's term. | Learner confusion | See note in 4.1. |
| A7 | **Hours per week.** Week 4 is 11-13 hours but the capstone alone is 7-9 hours plus Module 10's 45-60 minute activity, reading and checkpoint. | Completion risk in Week 4 | Keep as written; flag Week 4 as the heaviest and show the capstone in 2-3 sittings. Consider a 5th "capstone buffer" week for slower learners (pacing is a recommendation, per PRD). |
| A8 | **"Activities (10)" weight** in the assessment table. There are 11 activities, with Activity 11 weighted as the capstone. | Rubric clarity | Interpreted as Activities 1-10 at 40%, capstone at 40%. No change needed, just keep wording consistent in learner docs. |
| A9 | **Check-script integrity.** Checks run locally and are self-reported. | Credential and certification value | Acceptable per PRD (no certification goal). Capstone rubric review is the only external gate. |
| A10 | **Module 10 backends.** `gcs` and `azurerm` backends are reference-only. | Scope | Documented as read-only reference; no activity configures them. |
| A11 | **GitLab specifics are unknown**: gitlab.com or self-managed, tier, runner type, whether the runners can build container images, and whether GitLab Workspaces are enabled. | Browser-only access, CI cloud auth, dev container build | ADR-016 and ADR-004 are written to work without Workspaces. Confirm with the GitLab owner in weeks 1-2. If self-managed, check that AWS, GCP and Azure can reach its OIDC issuer URL. |
| A12 | **PRD still names GitHub, Codespaces and Actions** (s.3, s.13 FR-3 and FR-7, s.14 dependencies). | Source-of-truth drift between PRD and design | Update the PRD wording; add a Docker/Podman check to the pre-assessment, since without Workspaces there is no browser-only path. |

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
| CR-8 Capstone `data/` ships and is tested | `data/` folder, capstone CI | 8, 10, ADR-013 |
| FR-7 Peer review through merge requests (should) | Merge requests in a shared GitLab group, rubric as merge request template | 8.4, ADR-016 |
| CR-6 OpenTofu sidebar (should) | Sidebar in Module 1 or 2 | ADR-002 |
| CR-7 Cheat-sheet PDFs (should) | Markdown to PDF in CI | 4.1 |

---

## 13. Delivery plan alignment

The PRD launch plan (16 weeks) maps to the design as follows.

| PRD weeks | Design work |
| --- | --- |
| 1-2 | Confirm audience and metrics; create repo skeleton, `versions.env`, dev container, CI skeleton; **run the A1 and A4 spikes** |
| 3-8 | Author Weeks 1-4 content in order; each activity lands with starter, solution, hints, check script and CI job together; capstone `data/` built by week 6 so Week 4 content can reference it |
| 9 | Internal review: content, security (secret scan, IAM, SG review), cost (run a full capstone and record actual spend) |
| 10-15 | Pilot with 10-15 learners; collect survey data; watch for Week 4 time overrun and sandbox policy issues |
| 16 | Revise and launch |

## 14. Risks specific to this design

| Risk | Mitigation |
| --- | --- |
| Federated backup (ADR-014) blocked by sandbox policy | Spike in weeks 1-2, documented fallback |
| Check scripts produce false passes or false failures | CI runs each script against both solution (must pass) and starter (must fail on named items) |
| CI cloud sandbox cost or leaked resources | Nightly sweeper, budget alarm on the CI sandbox, small instance types |
| Learners skip the state bucket in Activity 7 | Capstone verify/recreate step (A5) |
| Provider canary breaks surface late | Weekly canary run, owner assigned, triage SLA |
| No browser-only option for learners whose laptops cannot run containers | Pre-assessment checks for Docker or Podman; GitLab Workspaces if enabled; local install path from Module 1 (ADR-004) |
| GitLab runners cannot build the dev container image, or cloud providers cannot trust the GitLab OIDC issuer | Confirm runner capability and issuer reachability in weeks 1-2 (A11); fall back to a pre-built image published manually |
