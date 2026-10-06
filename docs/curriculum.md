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
| M02 | Configuring Providers and Connecting to AWS | 6 | 5 | 8 | 29 | M01 |
| M03 | Understanding the Terraform Workflow | 6 | 5 | 6 | 27 | M02 |
| M04 | Managing Resources with Network Provisioning | 5 | 4 | 7 | 26 | M03 |
| M05 | Defining Variables, Inputs and Outputs in Terraform | 9 | 8 | 8 | 33 | M04 (you may reuse that work) |
| M06 | Managing Terraform State | 4 | 5 | 8 | 27 | M03 |
| M07 | Remote State and State Management Practices | 4 | 4 | 8 | 27 | M06 |
| M08 | Terraform for Multi-Environment Deployments | 7 | 5 | 6 | 28 | M05, M07 |
| M09 | Advanced Terraform Configuration | 8 | 7 | 8 | 31 | M04, M05, M06 |
| M10 | Designing Reusable Terraform Modules | 12 | 8 | 8 | 35 | M05, M06, M07, M08, M09 |
| M11 | Change with Confidence: Safe Terraform Refactoring | 5 | 5 | 8 | 28 | M03, M06, M07, M10 |
| M12 | Going Multi-Cloud with Terraform | 5 | 2 | 6 | 25 | M01, M02 |

The twelve stages generate 346 tasks between them. The capstone has its own checklist and is not listed here.

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

**If every topic is kept:** 29 tasks — Setup 3, Build 8 (6 topics and 2 deliverable components), Verify 8, Write-up 10.

**Topics**

- [x] 1. Authenticating to AWS (IAM Identity Center) and verifying Terraform identity
- [x] 2. Keeping static access keys off disk and out of the repository
- [x] 3. What a provider is and how Terraform finds and installs one
- [x] 4. Provider concepts, credential configuration, and default tags
- [x] 5. Dependency management: version constraints, lock files, and safe upgrades
- [x] 6. Using and inspecting multiple providers in a single configuration

**Topics to add:**

- [ ] <a topic to add>

## M03 — Understanding the Terraform Workflow

**Theme:** Declarative model, resource anatomy; plan, apply, destroy; plan review; in-place vs replace  
**Builds on:** M02 · **Leaves behind:** Nothing. Destroy everything.

**If every topic is kept:** 27 tasks — Setup 3, Build 8 (6 topics and 2 deliverable components), Verify 6, Write-up 10.

**Topics**

- [x] 1. Declarative versus imperative infrastructure — what it means that Terraform describes desired state
- [x] 2. Anatomy of a resource — type, name, arguments and attributes
- [x] 3. The core workflow — initialise, plan, apply, destroy
- [x] 4. What a plan shows — reading the action for each resource, In-place updates versus replacement
- [x] 5. Plan review as a habit — what to check before approving
- [x] 6. Destroying what you created

**Topics to add:**

- [ ] <a topic to add>

## M04 — Managing Resources with Network Provisioning

**Theme:** Dependencies, repetition, data sources, a small VPC  
**Builds on:** M03 · **Leaves behind:** Nothing. Destroy everything.

**If every topic is kept:** 26 tasks — Setup 3, Build 6 (5 topics and 1 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Resource references and the dependency graph Terraform builds from them
- [x] 2. Implicit versus explicit dependencies
- [x] 3. Repeating a resource — the two mechanisms Terraform offers
- [x] 4. Data sources — reading information that already exists, and how it differs from a resource
- [x] 5. A VPC, subnets in more than one availability zone, and the routing a public tier needs

**Topics to add:**

- [ ] <a topic to add>

## M05 — Defining Variables, Inputs and Outputs in Terraform

**Theme:** Typed, validated inputs; value precedence; locals; sensitive inputs and outputs  
**Builds on:** M04 (you may reuse that work) · **Leaves behind:** Nothing. Destroy everything.

**If every topic is kept:** 33 tasks — Setup 3, Build 12 (9 topics and 3 deliverable components), Verify 8, Write-up 10.

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

**Topics to add:**

- [ ] <a topic to add>

## M06 — Managing Terraform State

**Theme:** What state is, sensitive data in state and keeping secrets out of it, drift  
**Builds on:** M03 · **Leaves behind:** Nothing. Destroy everything.

**If every topic is kept:** 27 tasks — Setup 3, Build 6 (4 topics and 2 deliverable components), Verify 8, Write-up 10.

**Topics**

- [x] 1. Understanding and inspecting Terraform state (read-only)
- [x] 2. Secrets and state — what lands in state and who can read it and keeping a secret out of state
- [x] 3. Infrastructure drift: detection, causes, and reconciliation
- [x] 4. The golden rule: why state is never edited by hand

**Topics to add:**

- [ ] <a topic to add>

## M07 — Remote State and State Management Practices

**Theme:** S3 backend, native locking, recovering a lock left behind  
**Builds on:** M06 · **Leaves behind:** **The state bucket** — the only thing kept. Everything else is destroyed.

**If every topic is kept:** 27 tasks — Setup 3, Build 6 (4 topics and 2 deliverable components), Verify 8, Write-up 10.

**Topics**

- [x] 1. Why state moves to a remote backend, and what locking prevents
- [x] 2. Bootstrapping, securing, and managing the lifecycle of the state bucket
- [x] 3. Configuring the backend and migrating existing local state into it
- [x] 4. Proving that native locking works and recovering abandoned locks

**Topics to add:**

- [ ] <a topic to add>

## M08 — Terraform for Multi-Environment Deployments

**Theme:** Dev and prod from one configuration; directory vs workspaces vs per-environment files compared  
**Builds on:** M05, M07 · **Leaves behind:** Nothing except the M07 state bucket. Destroy both environments.

**If every topic is kept:** 28 tasks — Setup 3, Build 9 (7 topics and 2 deliverable components), Verify 6, Write-up 10.

**Topics**

- [x] 1. One configuration, many environments — what is shared and what must be separate
- [x] 2. Per-environment input values
- [x] 3. Per-environment backend settings and separate state keys in the shared bucket
- [x] 4. Managing blast radius through state separation
- [x] 5. Enforcing naming conventions and default provider tags
- [x] 6. Switching between environments safely
- [x] 7. Alternative isolation methods: directories vs workspaces (theory)

**Topics to add:**

- [ ] <a topic to add>

## M09 — Advanced Terraform Configuration

**Theme:** `for_each` in depth, dynamic blocks, conditions, `for` expressions, data sources, dependency and lifecycle controls  
**Builds on:** M04, M05, M06 · **Leaves behind:** Nothing except the M07 state bucket. Destroy everything else.

**If every topic is kept:** 31 tasks — Setup 3, Build 10 (8 topics and 2 deliverable components), Verify 8, Write-up 10.

**Topics**

- [x] 1. Composing Values with Built-in Functions
- [x] 2. Making Configuration Conditional
- [x] 3. Reshaping Data with `for` and Splat Expressions
- [x] 4. Going Deeper with `for_each`
- [x] 5. Generating Nested Configuration with Dynamic Blocks
- [x] 6. Discovering Existing Infrastructure with Data Sources
- [x] 7. Controlling Dependencies and Resource Lifecycle
- [x] 8. Validating Infrastructure with Preconditions and Postconditions

**Topics to add:**

- [ ] <a topic to add>

## M10 — Designing Reusable Terraform Modules

**Theme:** Reusable modules: structure, naming, comments, interfaces, consuming published modules  
**Builds on:** M05, M06, M07, M08, M09 · **Leaves behind:** Nothing except the M07 state bucket. Destroy everything else.

**If every topic is kept:** 35 tasks — Setup 3, Build 14 (12 topics and 2 deliverable components), Verify 8, Write-up 10.

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

**If every topic is kept:** 28 tasks — Setup 3, Build 7 (5 topics and 2 deliverable components), Verify 8, Write-up 10.

**Topics**

- [x] 1. Refactoring principles: renaming and removing resources without destruction
- [x] 2. Adopting existing, unmanaged resources into Terraform
- [x] 3. Verifying refactors mechanically: reading plans as JSON with `jq`
- [x] 4. Emergency recovery: handling partial applies and failed destroys
- [x] 5. Advanced troubleshooting: targeted operations and legacy state commands

**Topics to add:**

- [ ] <a topic to add>

## M12 — Going Multi-Cloud with Terraform

**Theme:** GCP and Azure sign-in and provider setup  
**Builds on:** M01, M02 · **Leaves behind:** Nothing. No resources are created.

**If every topic is kept:** 25 tasks — Setup 3, Build 6 (5 topics and 1 deliverable components), Verify 6, Write-up 10.

**Topics**

- [x] 1. Confirming access to the GCP and Azure sandboxes
- [x] 2. GCP — Application Default Credentials sign-in, project selection, provider configuration
- [x] 3. Azure — CLI sign-in, subscription selection, provider configuration
- [x] 4. State management across clouds: `gcs` and `azurerm` backends
- [x] 5. Where this course stops — HCP Terraform and Sentinel, named and not taught

**Topics to add:**

- [ ] <a topic to add>
