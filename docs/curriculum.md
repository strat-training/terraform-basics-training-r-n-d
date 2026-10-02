# Curriculum — scope by stage

Every topic each training stage covers, in the order the stage tackles it, so you can choose what stays. Each scope item becomes one build task in the stage's checklist. The stage's deliverable components, definition-of-done checks and write-up sections add the rest. Open design questions are answered in the write-up, so they are not tasks, but dropping a topic should still drop the questions and checks that depended on it.

## How to choose

1. Every box starts ticked. Untick a topic you want to drop, or add one under the stage.
2. For each stage you changed, update the brief's scope first. Then drop or reword the open design questions and definition-of-done checks that depended on the dropped topics, and regenerate the write-up template and checklist (see "Keeping the stage files in step" in [README.md](README.md)).
3. A topic that a later stage relies on is flagged in that later stage's "Builds on" line, so check it before dropping a topic from an earlier stage.

## Overview

| Stage | Title | Scope items | Design questions | Done checks | Tasks | Builds on |
| --- | --- | --- | --- | --- | --- | --- |
| M01 | Getting Started with Terraform | 7 | 5 | 8 | 30 | Nothing |
| M02 | Configuring Providers and Connecting to AWS | 8 | 5 | 9 | 32 | M01 |
| M03 | Understanding the Terraform Workflow | 7 | 5 | 6 | 28 | M02 |
| M04 | Managing Resources with Network Provisioning | 7 | 5 | 7 | 28 | M03 |
| M05 | Defining Variables, Inputs and Outputs in Terraform | 10 | 9 | 12 | 38 | M04 (you may reuse that work) |
| M06 | Managing Terraform State | 7 | 5 | 8 | 30 | M03 |
| M07 | Remote State and State Management Practices | 8 | 4 | 9 | 32 | M06 |
| M08 | Terraform for Multi-Environment Deployments | 8 | 6 | 7 | 30 | M05, M07 |
| M09 | Advanced Terraform Configuration | 10 | 7 | 12 | 38 | M04, M05, M06 |
| M10 | Designing Reusable Terraform Modules | 12 | 8 | 12 | 39 | M05, M06, M07, M08, M09 |
| M11 | Change with Confidence: Safe Terraform Refactoring | 10 | 5 | 11 | 36 | M03, M06, M07, M10 |
| M12 | Going Multi-Cloud with Terraform | 7 | 4 | 7 | 29 | M01, M02 |

The twelve stages generate 390 tasks between them. The capstone has its own checklist and is not listed here.

## M01 — Getting Started with Terraform

**Theme:** What Terraform is; install and verify Terraform, VS Code and the other lab tools on macOS and Windows  
**Builds on:** Nothing · **Leaves behind:** A working toolchain on your machine. No cloud resources.

**If every topic is kept:** 30 tasks — Setup 3, Build 9 (7 topics and 2 deliverable components), Verify 8, Write-up 10.

**Topics**

- [x] 1. What Terraform is — infrastructure as code, and the problem Terraform solves
- [x] 2. The core toolchain — AWS/GCP/Azure CLIs, Git, jq, curl, and their purposes
- [x] 3. Installing Terraform (macOS/Windows) and managing versions
- [x] 4. Configuring Visual Studio Code for Terraform work
- [x] 5. A shell that can run the labs' shell scripts on Windows
- [x] 6. Verifying the toolchain end to end — versions, and formatting and validation of a configuration that creates nothing
- [x] 7. OpenTofu differences — optional; you decide whether to include it

**Topics to add:**

- [ ] <a topic to add>

## M02 — Configuring Providers and Connecting to AWS

**Theme:** Sign in to AWS, no static keys; providers, version constraints, lock file (plan only)  
**Builds on:** M01 · **Leaves behind:** Nothing. This stage plans only; it creates no resources.

**If every topic is kept:** 32 tasks — Setup 3, Build 10 (8 topics and 2 deliverable components), Verify 9, Write-up 10.

**Topics**

- [x] 1. Authenticating to AWS (IAM Identity Center) and verifying Terraform identity
- [x] 2. Keeping static access keys off disk and out of the repository
- [x] 3. What a provider is and how Terraform finds and installs one, checking Provider version
- [x] 4. Version constraints — for Terraform itself and for each provider
- [x] 5. The dependency lock file — what it records and why it is committed
- [x] 6. Using more than one provider in a single configuration
- [x] 7. Provider configuration — how a provider obtains its credentials, and provider-level default tags
- [x] 8. Upgrading a pinned version deliberately

**Topics to add:**

- [ ] <a topic to add>

## M03 — Understanding the Terraform Workflow

**Theme:** Declarative model, resource anatomy; plan, apply, destroy; plan review; in-place vs replace  
**Builds on:** M02 · **Leaves behind:** Nothing. Destroy everything.

**If every topic is kept:** 28 tasks — Setup 3, Build 9 (7 topics and 2 deliverable components), Verify 6, Write-up 10.

**Topics**

- [x] 1. Declarative versus imperative infrastructure — what it means that Terraform describes desired state
- [x] 2. Anatomy of a resource — type, name, arguments and attributes
- [x] 3. The core workflow — initialise, plan, apply, destroy
- [x] 4. What a plan shows — reading the action for each resource
- [x] 5. In-place updates versus replacement
- [x] 6. Plan review as a habit — what to check before approving
- [x] 7. Destroying what you created

**Topics to add:**

- [ ] <a topic to add>

## M04 — Managing Resources with Network Provisioning

**Theme:** Dependencies, repetition, data sources, a small VPC  
**Builds on:** M03 · **Leaves behind:** Nothing. Destroy everything.

**If every topic is kept:** 28 tasks — Setup 3, Build 8 (7 topics and 1 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Resource references and the dependency graph Terraform builds from them
- [x] 2. Implicit versus explicit dependencies
- [x] 3. Repeating a resource — the two mechanisms Terraform offers
- [x] 4. Data sources — reading information that already exists, and how it differs from a resource
- [x] 5. A VPC, subnets in more than one availability zone, and the routing a public tier needs
- [x] 6. Public versus private subnets — what makes a subnet public
- [x] 7. Cost awareness — why some networking resources bill by the hour

**Topics to add:**

- [ ] <a topic to add>

## M05 — Defining Variables, Inputs and Outputs in Terraform

**Theme:** Typed, validated inputs; value precedence; locals; sensitive inputs and outputs  
**Builds on:** M04 (you may reuse that work) · **Leaves behind:** Nothing. Destroy everything.

**If every topic is kept:** 38 tasks — Setup 3, Build 13 (10 topics and 3 deliverable components), Verify 12, Write-up 10.

**Topics**

- [x] 1. Input variables — type, description and default
- [x] 2. Validation rules enforced at plan time
- [x] 3. Supplying values — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables
- [x] 4. Variable value precedence — which source wins when several supply the same variable, found by hands-on experiment
- [x] 5. Keeping environment-specific values out of the main configuration
- [x] 6. Local values — naming and reusing derived values within a configuration
- [x] 7. Sensitive input variables — marking them and getting their values into Terraform without committing them
- [x] 8. Output values — what to expose and how to mark an output sensitive
- [x] 9. What marking a value sensitive does and does not protect
- [x] 10. Reading validation errors as feedback

**Topics to add:**

- [ ] <a topic to add>

## M06 — Managing Terraform State

**Theme:** What state is, sensitive data in state and keeping secrets out of it, drift  
**Builds on:** M03 · **Leaves behind:** Nothing. Destroy everything.

**If every topic is kept:** 30 tasks — Setup 3, Build 9 (7 topics and 2 deliverable components), Verify 8, Write-up 10.

**Topics**

- [x] 1. What state records and what Terraform uses it for
- [x] 2. Secrets and state — what lands in state and who can read it
- [x] 3. Keeping a secret out of state — ephemeral values and write-only arguments, where the provider supports them
- [x] 4. Inspecting state, read-only
- [x] 5. Drift — how it arises and how Terraform detects it
- [x] 6. Reconciling drift — deciding whether the code or the real world wins
- [x] 7. Why state is never edited by hand

**Topics to add:**

- [ ] <a topic to add>

## M07 — Remote State and State Management Practices

**Theme:** S3 backend, native locking, recovering a lock left behind  
**Builds on:** M06 · **Leaves behind:** **The state bucket** — the only thing kept. Everything else is destroyed.

**If every topic is kept:** 32 tasks — Setup 3, Build 10 (8 topics and 2 deliverable components), Verify 9, Write-up 10.

**Topics**

- [x] 1. Why state moves to a remote backend, and what locking prevents
- [x] 2. The bootstrapping problem — where the state bucket itself comes from
- [x] 3. Protecting the bucket — versioning, encryption at rest, blocked public access, restricted access
- [x] 4. Configuring the backend and migrating existing local state into it
- [x] 5. Native S3 state locking, and why DynamoDB-based locking is no longer taught
- [x] 6. Proving that locking works
- [x] 7. A bucket that outlives its stage — lifecycle and eventual retirement
- [x] 8. A lock left behind — what it means, what to check, and recovering safely

**Topics to add:**

- [ ] <a topic to add>

## M08 — Terraform for Multi-Environment Deployments

**Theme:** Dev and prod from one configuration; directory vs workspaces vs per-environment files compared  
**Builds on:** M05, M07 · **Leaves behind:** Nothing except the M07 state bucket. Destroy both environments.

**If every topic is kept:** 30 tasks — Setup 3, Build 10 (8 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. One configuration, many environments — what is shared and what must be separate
- [x] 2. Per-environment input values
- [x] 3. Per-environment backend settings and separate state keys in the shared bucket
- [x] 4. Blast radius — what separate state does and does not protect
- [x] 5. The standard file layout for a root configuration
- [x] 6. A naming convention and required tags applied through provider defaults
- [x] 7. Switching between environments safely
- [x] 8. Other ways to separate environments — a directory per environment, and workspaces — and when each fits (explained, not used)

**Topics to add:**

- [ ] <a topic to add>

## M09 — Advanced Terraform Configuration

**Theme:** `for_each` in depth, dynamic blocks, conditions, `for` expressions, data sources, dependency and lifecycle controls  
**Builds on:** M04, M05, M06 · **Leaves behind:** Nothing except the M07 state bucket. Destroy everything else.

**If every topic is kept:** 38 tasks — Setup 3, Build 13 (10 topics and 3 deliverable components), Verify 12, Write-up 10.

**Topics**

- [x] 1. Composing built-in functions to derive values
- [x] 2. Conditional expressions — and when a condition belongs in configuration at all
- [x] 3. `for` expressions and splat expressions — reshaping collections
- [x] 4. `for_each` in depth — maps, sets and derived collections, and what makes a key stable
- [x] 5. Dynamic blocks — generating repeated nested blocks from data
- [x] 6. Data sources in depth — beyond the basic lookup introduced in M04
- [x] 7. Explicit dependencies with `depends_on` — when a reference cannot express the ordering
- [x] 8. The `lifecycle` block — controlling replacement, destruction and ignored changes
- [x] 9. Preconditions and postconditions — checking assumptions about real infrastructure
- [x] 10. When a feature costs more readability than it saves

**Topics to add:**

- [ ] <a topic to add>

## M10 — Designing Reusable Terraform Modules

**Theme:** Reusable modules: structure, naming, comments, interfaces, consuming published modules  
**Builds on:** M05, M06, M07, M08, M09 · **Leaves behind:** Nothing except the M07 state bucket. Destroy everything else.

**If every topic is kept:** 39 tasks — Setup 3, Build 14 (12 topics and 2 deliverable components), Verify 12, Write-up 10.

**Topics**

- [x] 1. What a module is — the root module, child modules, and what a module call does
- [x] 2. Deciding what belongs in a module, and what does not
- [x] 3. A module's interface — inputs, outputs, and what it keeps private
- [x] 4. Standard module file structure
- [x] 5. Naming conventions for a module's inputs, outputs and resources
- [x] 6. Comments and documentation — comment syntax, what deserves a comment, and descriptions on inputs and outputs
- [x] 7. Calling the same module more than once with different inputs
- [x] 8. How modules change resource addresses in a plan and in state
- [x] 9. Module sources and versions — local paths versus registry or Git sources, and pinning
- [x] 10. Consuming a published module — reading someone else's module before trusting it
- [x] 11. What a module may assume about provider configuration
- [x] 12. Module anti-patterns

**Topics to add:**

- [ ] <a topic to add>

## M11 — Change with Confidence: Safe Terraform Refactoring

**Theme:** Rename, adopt, stop managing — no destroys; reading plans as JSON; recovering from a failed apply  
**Builds on:** M03, M06, M07, M10 · **Leaves behind:** Nothing except the M07 state bucket.

**If every topic is kept:** 36 tasks — Setup 3, Build 12 (10 topics and 2 deliverable components), Verify 11, Write-up 10.

**Topics**

- [x] 1. Why refactoring must never mean destroy-and-recreate
- [x] 2. Renaming or re-addressing a resource without replacing it
- [x] 3. Adopting an existing, unmanaged resource into Terraform
- [x] 4. Tidying generated configuration
- [x] 5. Ceasing to manage a resource without destroying it
- [x] 6. Verifying every refactor with a plan
- [x] 7. Reading a saved plan as JSON with `jq` — checking the action on every resource mechanically
- [x] 8. Targeted operations — an emergency tool, never routine
- [x] 9. Reading legacy guidance that relies on imperative state commands
- [x] 10. When an apply goes wrong — a partial apply, a failed destroy, and reading provider errors

**Topics to add:**

- [ ] <a topic to add>

## M12 — Going Multi-Cloud with Terraform

**Theme:** GCP and Azure sign-in and provider setup  
**Builds on:** M01, M02 · **Leaves behind:** Nothing. No resources are created.

**If every topic is kept:** 29 tasks — Setup 3, Build 9 (7 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Confirming access to the GCP and Azure sandboxes
- [x] 2. GCP — Application Default Credentials sign-in, project selection, provider configuration
- [x] 3. Azure — CLI sign-in, subscription selection, provider configuration
- [x] 4. Read-only data sources as a safe proof of identity
- [x] 5. Where the clouds differ, stated explicitly
- [x] 6. The `gcs` and `azurerm` state backends — reference only
- [x] 7. Where this course stops — HCP Terraform and Sentinel, named and not taught

**Topics to add:**

- [ ] <a topic to add>
