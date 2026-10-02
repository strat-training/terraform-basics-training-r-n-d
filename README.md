# Terraform Concepts & Best Practices — training stages and capstone

This is your Terraform course: twelve training stages in `modules/`, followed by a capstone project. For each stage your trainer gives you a brief. You build the stage and write it up as you go, your trainer reviews both together, you revise, and the finished pair becomes teaching material for the next cohort.

A note on words: a **module** in this repository is a *training stage*, not a Terraform module. Stage [M10](modules/m10-designing-reusable-terraform-modules/brief.md) is the one that teaches Terraform modules.

## What is in this repository

| Path | What it holds |
| --- | --- |
| `modules/` | The twelve stage folders (M01–M12), each with a brief, a checklist and a write-up template |
| `modules/capstone/` | The capstone, with its own brief, checklist and write-up template |

The other folders are trainer material. You do not need them to do the stages.

## How a stage works

1. **Your trainer hands you the brief.** Each stage's `brief.md` says what to build and how you will know it is done: objective, scope, stack constraints, the named deliverable, open design questions and a definition of done. It contains no lesson, no steps, no code and no solutions. How to build it is yours to work out.
2. **You build and write up the stage together.** Copy `write-up-template.md` to `write-up.md` in the stage folder and fill it in *while* you build, not after the build works. The "how to build it" section is the teaching content, so write it for someone who will follow it with no trainer to ask.
3. **Your trainer reviews both together.** When you reach the definition of done, set Status to "In review". Your trainer reviews the working system and the write-up side by side. The question is not only "does it work?" but "could someone else learn from this?"
4. **You revise.** Fix what the review finds, in both the build and the write-up, before starting the next stage.
5. **The finished pair goes into the content library.** An accepted stage is the build plus its write-up. Your trainer decides what carries into the next cohort's plan.

Review happens at the end of every stage, not just at the end of the course. A write-up produced after the system already works tends to be thin; reviewing as you go is what keeps it good.

### What is in each stage folder

| File | Who writes it | Purpose |
| --- | --- | --- |
| `brief.md` | Your trainer | What to build and how you will know it is done. Do not edit it. |
| `write-up-template.md` | Your trainer | A blank template. Leave it untouched so the next cohort starts clean. |
| `write-up.md` | You | Your copy of the template, filled in as you build. |
| `tasks.md` | Your trainer | An ordered checklist for the stage, one task per scope item, question, check and write-up section. You tick the boxes; it holds no answers and no steps. |

Your Terraform code lives outside this repository, in your own GitLab repository. Link it from the header of your write-up. The capstone folder has the same three files.

## Stages

| Stage | Title | Checklist | Theme | Leaves behind |
| --- | --- | --- | --- | --- |
| M01 | [Getting Started with Terraform](modules/m01-getting-started-with-terraform/brief.md) | [tasks](modules/m01-getting-started-with-terraform/tasks.md) | What Terraform is; install and verify Terraform, VS Code and the other lab tools on macOS and Windows | Tools only |
| M02 | [Configuring Providers and Connecting to AWS](modules/m02-configuring-providers-and-connecting-to-aws/brief.md) | [tasks](modules/m02-configuring-providers-and-connecting-to-aws/tasks.md) | Sign in to AWS, session expiry, no static keys; providers, version constraints, lock file (plan only) | Nothing |
| M03 | [Understanding the Terraform Workflow](modules/m03-understanding-the-terraform-workflow/brief.md) | [tasks](modules/m03-understanding-the-terraform-workflow/tasks.md) | Declarative model, resource anatomy; plan, apply, destroy; plan review; in-place vs replace | Nothing |
| M04 | [Managing Resources with Network Provisioning](modules/m04-managing-resources-with-network-provisioning/brief.md) | [tasks](modules/m04-managing-resources-with-network-provisioning/tasks.md) | Dependencies, repetition, data sources, a small VPC | Nothing |
| M05 | [Defining Variables, Inputs and Outputs in Terraform](modules/m05-defining-variables-inputs-and-outputs-in-terraform/brief.md) | [tasks](modules/m05-defining-variables-inputs-and-outputs-in-terraform/tasks.md) | Typed, validated inputs; value precedence; locals; sensitive inputs and outputs | Nothing |
| M06 | [Managing Terraform State](modules/m06-managing-terraform-state/brief.md) | [tasks](modules/m06-managing-terraform-state/tasks.md) | What state is, sensitive data in state and keeping secrets out of it, drift | Nothing |
| M07 | [Remote State and State Management Practices](modules/m07-remote-state-and-state-management-practices/brief.md) | [tasks](modules/m07-remote-state-and-state-management-practices/tasks.md) | S3 backend, native locking, recovering a lock left behind | **The state bucket** |
| M08 | [Terraform for Multi-Environment Deployments](modules/m08-terraform-for-multi-environment-deployments/brief.md) | [tasks](modules/m08-terraform-for-multi-environment-deployments/tasks.md) | Dev and prod from one configuration; directory vs workspaces vs per-environment files compared | Bucket only |
| M09 | [Advanced Terraform Configuration](modules/m09-advanced-terraform-configuration/brief.md) | [tasks](modules/m09-advanced-terraform-configuration/tasks.md) | `for_each` in depth, dynamic blocks, conditions, `for` expressions, data sources, dependency and lifecycle controls | Bucket only |
| M10 | [Designing Reusable Terraform Modules](modules/m10-designing-reusable-terraform-modules/brief.md) | [tasks](modules/m10-designing-reusable-terraform-modules/tasks.md) | Reusable modules: structure, naming, comments, interfaces, consuming published modules | Bucket only |
| M11 | [Change with Confidence: Safe Terraform Refactoring](modules/m11-change-with-confidence-safe-terraform-refactoring/brief.md) | [tasks](modules/m11-change-with-confidence-safe-terraform-refactoring/tasks.md) | Rename, adopt, stop managing — no destroys; reading plans as JSON; recovering from a failed apply | Bucket only |
| M12 | [Going Multi-Cloud with Terraform](modules/m12-going-multi-cloud-with-terraform/brief.md) | [tasks](modules/m12-going-multi-cloud-with-terraform/tasks.md) | GCP and Azure sign-in and provider setup | Nothing |

Work the stages in order. Later stages build on earlier ones, and M07's bucket is reused by M08 to M11 and kept until the capstone ends. M09 comes before modules so that module interfaces can rely on it, and modules come before refactoring so that extracting code into a module is something M11 can then refactor. Folder names are descriptive; the briefs refer to each other by stage ID (M01–M12).

## The capstone — Terraform Shop

The capstone follows M12. It is a standalone project that assumes everything the stages teach and does not change them. You build a **Terraform Shop**, a three-tier online shop on AWS (`ap-southeast-1`): three app versions released to live traffic with zero failed checkouts, a bad release rolled back with one change, an off-site copy of the item inventory in GCP, and the shop's theme and images served from Azure — with no stored key anywhere and inside a cost ceiling. What the shop sells, what each tier runs on, how many resources there are, how zero downtime is achieved and how the release is demonstrated are your own decisions, all listed in one section of the brief. The GCP and Azure use cases are fixed.

| | |
| --- | --- |
| Brief | [modules/capstone/brief.md](modules/capstone/brief.md) |
| Checklist | [modules/capstone/tasks.md](modules/capstone/tasks.md) |
| Write-up template | [modules/capstone/write-up-template.md](modules/capstone/write-up-template.md) |
| Presentation | 15 minutes of presenting and 15 minutes of questions |
| Shape | Two stacks (`foundation` and `release`) built from local modules; blue and green app colours with traffic moved between them; release stages 0 to 6; a Demo Challenge of five day-2 tasks; failure, identity and backup proofs; a cost challenge; a supplied `check.sh` |
| Your design | The shop and its theme; what each tier runs on (servers, Fargate or other); resource counts; network and access; the zero-downtime mechanism; how a bad release is detected and rolled back; how the release is demonstrated. See "Your design decisions" in the brief |
| You hand in | A GitLab repository, an `evidence/` folder and `write-up.md` |
| Assessed by | A 100-point rubric with a pass mark of 70, confirmed in a presentation |

| Rubric criterion | Points |
| --- | --- |
| Provision | 15 |
| Release proofs | 25 |
| Structure and quality | 20 |
| Demo Challenge (the day-2 round) | 15 |
| AI review log and design note | 15 |
| Security, cost, teardown | 10 |

The presentation carries no separate points. It is where the panel confirms the evidence behind each criterion; the brief lists what is checked for each one. Your trainer gives you a `data/` folder (the application in three versions, a starter catalogue, a starter theme and images, an optional `probe.sh` and `check.sh`); you may replace the catalogue and theme with your own.

## Rules for every stage

These apply to every stage brief, M01 to M12. A brief repeats only what is specific to its stage. The capstone restates its own rules in its brief.

- **Terraform CLI, 1.11 or later**, at the exact version in `versions.env`. OpenTofu is an optional topic in M01; you decide whether to include it.
- **AWS first.** GCP and Azure appear only in M12, as setup and read-only checks.
- **Sandbox accounts only, short-lived sign-in only.** Never create, store or commit a static access key, service-account key or client secret.
- **Destroy at the end of every stage.** The M07 state bucket is the only thing kept, until the capstone ends. Keep resources small and cheap, and use no NAT gateways.
- **Know what it costs before you apply.** Each brief has a Cost row. Look up what each resource in your plan bills and estimate the hourly cost before you apply. Billing APIs are not used, so your estimate is your evidence.
- **Sandbox-compatible tooling only.** No Organizations or service control policies, billing APIs, tag-filtered budgets, paid SaaS or policy-as-code engines. No HCP Terraform, Stacks, Packer, Kubernetes providers or `terraform test`.
- **Pin everything and commit the lock file.** Formatting and validation checks must pass before you call a stage done.
- **Never edit state by hand.** Refactor declaratively.

## What review looks for

Your trainer reviews a stage's build and write-up together and rates each criterion below. The capstone has its own rubric.

| Criterion | Excellent | Satisfactory | Needs work |
| --- | --- | --- | --- |
| Definition of done | Every item has real evidence — pasted output or a screenshot, trimmed to the relevant lines and redacted — and the build matches what the write-up says | Every item is addressed, but some evidence is a claim or is hard to follow | An item is missing, unmet or has no evidence |
| Design decisions | Every open design question has a reasoned answer that says what you considered, what you chose and what you gave up | Questions are answered, but the reasons are thin or the trade-off is missing | A question is unanswered, or an answer only restates what you built |
| How to build it | Someone else could follow it from a clean start; you have followed it yourself and it works | It mostly works, with gaps or steps that assume knowledge the reader may not have | It is a summary of what you did rather than a guide, or it was never followed through |
| Concepts | Two or three ideas in your own words, each with an example from your own build | Explained correctly, but generic or close to the documentation's wording | Missing, or wrong |
| What tripped me up | Real obstacles with the exact error text, the cause and the fix. These entries become the course's common-errors list | Obstacles listed without the error text or the cause | Empty, or only polished successes |
| Terraform practice | The rules for every stage are met: formatting and validation pass, versions are pinned and the lock file committed, no static credentials and no state in version control, and everything the brief says to destroy is gone. The cost was looked up before applying and is noted in the write-up | One slip against the rules, which is noted and fixed | A rule is broken — a stored key, a committed state file, a resource left running — or the cost was never considered |
| AI collaboration log | Specific: which tools, concrete examples, a suggestion that was wrong and how you caught it, and what you wrote yourself — or one line saying none was used | Generic, or no corrected suggestion | Missing |
| Understanding | You explain any part of your work when the trainer asks, without re-reading it | You explain most of it and need prompting on the rest | You cannot explain work you submitted |

**Accepted** means no criterion is Needs work and every item in the definition of done has evidence. Otherwise the stage goes back for revision before the next one starts. A write-up that is Excellent on "How to build it" and on "What tripped me up" is a candidate for the content library.

The capstone's write-up is reviewed the same way. The capstone is also marked against its own rubric, which has points and a pass mark of 70 out of 100, and confirmed in its presentation.
