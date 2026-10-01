# Training modules — Terraform Concepts & Best Practices

These are the **Build-to-Teach** modules for the 4-week Terraform program described in [solution-design.md](../docs/arch-docs/solution-design.md). Each stage is built by a trainee, and the trainee writes it up as they go. The finished build and write-up become the teaching content for the next cohort. The framework is in [build-to-teach-framework.md](../docs/build-to-teach-framework/build-to-teach-framework.md).

These stages exist to teach Terraform itself. The capstone is a separate, standalone project that follows them; it does not shape them. It lives outside this folder, in [capstone/](../capstone/brief.md).

A note on words: in this folder a **module** is a *training stage*, not a Terraform module. Stage [M10](m10-designing-reusable-terraform-modules/brief.md) is the one that teaches Terraform modules; the solution design excludes that topic (ADR-015), so M10 is an addition that needs sign-off (see the open items below).

## The cycle

1. **The trainer hands over the brief.** Each stage's `brief.md` is the curriculum handoff: objective, scope, stack constraints, the named deliverable, open design questions and an observable definition of done. It contains no lesson, no steps, no code and no solutions. How to build it is yours to work out. (The framework calls the trainer the EM.)
2. **The trainee builds and writes up the stage together.** Copy `write-up-template.md` to `write-up.md` in the stage folder and fill it in *while* you build, not after the build works. The "how to build it" section is the teaching content, so write it for someone who will follow it with no trainer to ask.
3. **Both get reviewed together.** When you reach the definition of done, set Status to "In review". The trainer reviews the working system and the write-up side by side. The question is not only "does it work?" but "could someone else learn from this?"
4. **The trainee revises.** Fix what the review finds, in both the build and the write-up, before starting the next stage.
5. **The finished pair goes into the content library.** An accepted stage is the build plus its write-up. The trainer decides what carries into the next cohort's plan.

Review happens at the end of every stage, not just at the end of the course. A write-up produced after the system already works tends to be thin; reviewing as you go is what keeps it good.

## What is in each stage folder

| File | Owner | Purpose |
| --- | --- | --- |
| `brief.md` | Trainer | What to build and how you will know it is done. Do not edit it. |
| `write-up-template.md` | Trainer | A blank template. Leave it untouched so the next cohort starts clean. |
| `write-up.md` | Trainee | Your copy of the template, filled in as you build. |
| `tasks.md` | Trainer (generated) | An ordered checklist for the stage, one task per scope item, question, check and write-up section. You tick the boxes; it holds no answers and no steps. |

Your Terraform code lives outside this folder. Link it from the header of your write-up.

## Stages

| Stage | Title | Solution-design module | Theme | Leaves behind |
| --- | --- | --- | --- | --- |
| M01 | [Getting Started with Terraform](m01-getting-started-with-terraform/brief.md) | 1 (reworked) | What Terraform is; install and verify Terraform, VS Code and the other lab tools on macOS and Windows | Tools only |
| M02 | [Configuring Providers and Connecting to AWS](m02-configuring-providers-and-connecting-to-aws/brief.md) | 2 (extended) | Sign in to AWS, session expiry, no static keys; providers, version constraints, lock file (plan only) | Nothing |
| M03 | [Understanding the Terraform Workflow](m03-understanding-the-terraform-workflow/brief.md) | 3 (extended) | Declarative model, resource anatomy; plan, apply, destroy; plan review; in-place vs replace | Nothing |
| M04 | [Managing Resources with Network Provisioning](m04-managing-resources-with-network-provisioning/brief.md) | 4 (extended) | Dependencies, repetition, data sources, a small VPC | Nothing |
| M05 | [Defining Variables, Inputs and Outputs in Terraform](m05-defining-variables-inputs-and-outputs-in-terraform/brief.md) | 5 (extended) | Typed, validated inputs; value precedence; locals; sensitive inputs and outputs | Nothing |
| M06 | [Managing Terraform State](m06-managing-terraform-state/brief.md) | 6 | What state is, sensitive data in state, drift | Nothing |
| M07 | [Remote State and State Management Practices](m07-remote-state-and-state-management-practices/brief.md) | 7 | S3 backend, native locking | **The state bucket** |
| M08 | [Terraform for Multi-Environment Deployments](m08-terraform-for-multi-environment-deployments/brief.md) | 8 (extended) | Dev and prod from one configuration; directory vs workspaces vs per-environment files compared | Bucket only |
| M09 | [Advanced Terraform Configuration](m09-advanced-terraform-configuration/brief.md) | — (new) | `for_each` in depth, dynamic blocks, conditions, `for` expressions, data sources, dependency and lifecycle controls | Bucket only |
| M10 | [Designing Reusable Terraform Modules](m10-designing-reusable-terraform-modules/brief.md) | — (new) | Reusable modules: structure, naming, comments, interfaces, consuming published modules | Bucket only |
| M11 | [Change with Confidence: Safe Terraform Refactoring](m11-change-with-confidence-safe-terraform-refactoring/brief.md) | 9 (extended) | Rename, adopt, stop managing — no destroys; reading plans as JSON | Bucket only |
| M12 | [Going Multi-Cloud with Terraform](m12-going-multi-cloud-with-terraform/brief.md) | 10 | GCP and Azure sign-in and provider setup | Nothing |

Work the stages in order. Later stages build on earlier ones, and M07's bucket is reused by M08 to M11; retire it when M12 is accepted. M09 and M10 are additions, so for M11 and M12 the stage numbers here are two higher than the solution design's module numbers. M09 comes before modules so that module interfaces can rely on it, and modules come before refactoring so that extracting code into a module is something M11 can then refactor. Folder names are descriptive; the briefs refer to each other by stage ID (M01–M12).

## Rules for every stage

These apply to every brief. A brief repeats only what is specific to its stage.

- **Terraform CLI, 1.11 or later**, at the exact version in `versions.env`. OpenTofu is an ungraded sidebar only (ADR-002, ADR-006).
- **AWS first.** GCP and Azure appear only in M12, as setup and read-only checks (ADR-003).
- **Sandbox accounts only, short-lived sign-in only.** Never create, store or commit a static access key, service-account key or client secret (ADR-005).
- **Destroy at the end of every stage.** The M07 state bucket is the only thing kept, until M12 is accepted. Keep resources small and cheap, and use no NAT gateways (ADR-011).
- **Sandbox-compatible tooling only.** No Organizations or service control policies, billing APIs, tag-filtered budgets, paid SaaS or policy-as-code engines. No HCP Terraform, Stacks, Packer, Kubernetes providers or `terraform test` (ADR-015).
- **Pin everything and commit the lock file.** Formatting and validation checks must pass before you call a stage done.
- **Never edit state by hand.** Refactor declaratively (ADR-008).

## What review looks for

- Every definition-of-done item has real evidence — pasted output or a screenshot, not a claim.
- The "how to build it" section works for someone other than you. You have followed it from a clean start.
- Concepts are in your own words, with an example from your own build.
- Each open design question has a reasoned answer that says what you gave up.
- "What tripped me up" is honest and keeps the exact error text. These entries become the course's common-errors list.

## Open items for the trainer

These are gaps or choices the source documents leave open. They are listed here, not decided silently.

**Framework questions (unanswered in the framework doc)**
- Checkpoint cadence: these modules assume a review at the end of each stage. Whether to also hold weekly checkpoints is open.
- Who owns the content library over time, and where it lives.
- Whether the trainer's review notes are folded into the training material or stay private. Until this is settled, the write-up template has no place for review notes.

**Gaps in what these briefs could be built from**
- **The PRD is not in this repository.** Only the solution design and ADRs were available. Stage names for M02–M08 and M11–M12 come from the activity map (solution-design §6.2). Scope lists for the stages the architecture docs describe thinly (M01–M06) are inferred from that map and the 14-practice matrix (§7). M09 and M10 are additions that the design mentions only in passing (§7 names `for_each` over `count`; ADR-015 names preconditions and postconditions and excludes module authoring); their scope and definitions of done are a proposal for you to review. Check everything against PRD s.5–s.8. M01's rework, M02's sign-in material, M05's precedence and sensitive-value material, and M10's structure and comment material come from the trainer's direction, not from the design.
- **Time boxes** are not in the architecture docs except for M12. Every other brief says "TBC". The "Hours spent" field in each write-up will give you real figures to set them from. M09 and M10 add hours that the course's 37–42 hour budget does not include.
- **Assets the briefs assume but this repository does not have yet:** `versions.env`, the pinned dev container, and the model answers for M03, M06 and M12.
- **M04's expected resource list** is inferred from the solution design's network topology (§8.1); the design says only "expected resources".
- **OpenTofu sidebar placement:** the design allows Module 1 or 2. It is placed in M01.
- **Proposed ADRs:** 007 and 008 are not yet signed off. M08 and M11 rely on them and say so.
- **Scope of what a trainee builds:** each brief's deliverable is the working Terraform for that stage's activity. Starter code, graded hints, check scripts, cheat sheets and quizzes (solution-design §4) are not part of these briefs. Decide who produces them.

**Decisions created by adding M09 and M10**
- **ADR-015 needs superseding.** M10 teaches authoring reusable modules, which ADR-015 (Accepted) excludes; ADR-003 and ADR-007 also treat module reuse as out of scope. The ADR index says an accepted decision is superseded by a new ADR, not edited, so M10's brief says it departs from ADR-015 until one exists. M09 also touches ADR-015 lightly: it teaches preconditions and postconditions, which the ADR names but no stage covered.
- **The numbers have drifted.** M09 and M10 are new, so for M11 and M12 the stage numbers here differ from the solution design's: refactoring is Module 9 there and M11 here, GCP/Azure is Module 10 and M12. The solution design, ADRs and PRD also still say there are 11 modules, the eleventh being the capstone. Each affected brief's "Course reference" row records the difference.
- **M09 is large.** It has ten scope items and twelve definition-of-done checks, and it deliberately overlaps M04: M04 introduces repetition and a basic data-source lookup, and M09 goes deeper. If a trainee's hours show it overruns, split it — expressions, `for_each` and dynamic blocks first; data sources, dependencies, lifecycle controls and conditions second.

**Decisions created by reworking M01 and M02 and extending M05**
- **Sign-in moved from M01 to M02.** Sandbox access is provided before the course, so M01 installs tools only and M02 teaches signing in, session expiry and the static-key check. The solution design puts all three in Module 1 (ADR-005, ADR-009), and its Activity 1 check for "no static credentials" now belongs to M02 (§7).
- **M01 makes local installation the main path (confirmed).** Installing on macOS and Windows is the core of the stage and the dev container is an alternative. ADR-004 (Accepted) says the reverse: container supported, local install secondary. It still needs amending or superseding.
- **M02 now carries two themes.** It has twelve scope items, seven open questions and eleven definition-of-done checks. If it overruns, split sign-in from versioning.
- **M05 is large.** It has ten scope items, nine open questions and twelve definition-of-done checks. If it overruns, split it: variables, locals and validation first; value precedence and sensitive inputs and outputs second.

**Decisions created by the order review**
- **M02 is plan-only.** It required creating and destroying a resource before M03 teaches the workflow, so it now stops at `init` and `plan`.
- **M05 no longer sizes an instance.** No stage creates a compute instance, so the variables stage parameterises the network's region, address ranges and name prefix instead.
- **M11 reads saved plans as JSON.** M01 installs `jq` but no stage used it, and reading a plan's JSON is how "zero destroys" is checked mechanically.
- **M03 and M04 gained the basics.** M03 teaches the declarative model and the anatomy of a resource; M04 introduces data sources and M09 goes deeper.
- **M01 gained an introduction and M05 took over local values.** M01 gained a short "what Terraform is" item to fit "Getting Started with Terraform", and M05 took over local values from M09 so that locals sit with variables and outputs.
- **M08 compares three ways to separate environments** — a directory per environment, workspaces and per-environment files — as an explained-not-built note. ADR-007 still holds.
- **Considered and rejected (trainer decision):** a compute and security-group stage to prepare trainees for the capstone. The stages teach Terraform concepts; the capstone is standalone and does not drive their content.
- **The rest of the order stands:** variables before state, state before remote state before environments, modules before refactoring, GCP and Azure last.

## Proposed additions (not yet scaffolded)

Found when reviewing M01–M12 for Terraform concepts a trainee would otherwise miss. Nothing here is built. If you adopt more than one, decide the order together before renumbering again.

1. **When apply goes wrong.** Partial applies, a lock left behind, a failed destroy, reading provider errors. M07's design questions ask about a stuck lock, but nothing teaches recovery. This could run as a thread through M07 and M11, or be a short stage after M11.
2. **Secrets that never reach state.** M06 shows secrets landing in state. Newer Terraform releases also have ephemeral values and write-only arguments. I have not verified which the pinned version supports, so check the release notes and provider documentation before deciding whether to teach them.
3. **An open-source static-analysis sidebar.** Formatting and validation are the only automated quality gates in any stage. ADR-015 permits open-source linters as ungraded sidebars.
4. **A fifteenth best practice.** If M10 stays, add "reuse through documented, version-pinned modules" to the PRD's practice list (s.10) and to the coverage matrix. M09's conditions that check assumptions are in the same position: ADR-015 names them, but the matrix has no practice for them. CI fails any practice that lacks a mapped check and quiz question (ADR-010), so the matrix has to change with it.
5. **A next-steps note for HCP Terraform and Sentinel.** ADR-015 says the course should name them as next steps without teaching them; no stage has a next-steps section yet.
