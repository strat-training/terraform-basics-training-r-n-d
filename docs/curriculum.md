# Curriculum — scope by stage

Every topic each training stage covers, in the order the stage tackles it, so you can choose what stays. Each scope item becomes one build task in the stage's checklist. The stage's deliverable components, definition-of-done checks and write-up sections add the rest. The research prompts under each topic are answered in the write-up, so they are not tasks, but dropping a topic should still drop its research prompts and the checks that depended on it.

## How to choose

1. Every box starts ticked. Untick a topic you want to drop, or add one under the stage.
2. For each stage you changed, update the brief's scope first. Then drop or reword the research prompts and definition-of-done checks that depended on the dropped topics, and regenerate the write-up template and checklist (see "Keeping the stage files in step" in [README.md](README.md)).
3. A topic that a later stage relies on is flagged in that later stage's "Builds on" line, so check it before dropping a topic from an earlier stage.

## Overview

| Stage | Title | Scope items | Research prompts | Done checks | Tasks | Builds on |
| --- | --- | --- | --- | --- | --- | --- |
| M01 | Getting Started with Terraform | 7 | 7 | 7 | 29 | — (course entry point) |
| M02 | Configuring Providers and Connecting to AWS | 6 | 6 | 7 | 28 | M01 |
| M03 | Understanding the Terraform Workflow | 6 | 6 | 7 | 28 | M02 |
| M04 | Managing Terraform State | 6 | 6 | 7 | 28 | M03 |
| M05 | Terraform for Multi-Environment Deployments | 7 | 7 | 7 | 29 | M04 |
| M06 | Managing Resources with Network Provisioning | 5 | 5 | 7 | 26 | M03 |
| M07 | Defining Variables, Inputs and Outputs in Terraform | 9 | 9 | 7 | 32 | M06 (you may reuse that work) |
| M08 | Advanced Terraform Configuration | 8 | 8 | 7 | 30 | M04, M06, M07 |
| M09 | Designing Reusable Terraform Modules | 12 | 12 | 7 | 34 | M04, M05, M07, M08 |
| M10 | Change with Confidence: Safe Terraform Refactoring | 5 | 5 | 7 | 27 | M03, M04, M09 |
| M11 | Going Multi-Cloud with Terraform | 5 | 5 | 7 | 26 | M01, M02 |

The twelve stages generate 317 tasks between them. The capstone has its own checklist and is not listed here.

## M01 — Getting Started with Terraform

**Theme:** What Terraform is; install and verify Terraform, VS Code and the other lab tools on macOS and Windows  
**Builds on:** — (course entry point) · **Feeds into:** M02, M11

**If every topic is kept:** 29 tasks — Setup 3, Build 9 (7 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. What Terraform is — infrastructure as code, and the problem Terraform solves
- [x] 2. The core toolchain — AWS/GCP/Azure CLIs, Git, jq, curl, and their purposes
- [x] 3. Installing Terraform (macOS/Windows) and managing versions — at the pinned version on each system, and switching between Terraform versions with a version manager
- [x] 4. Configuring Visual Studio Code for Terraform work — installing the editor and the Terraform extension, and an editor that flags your mistakes
- [x] 5. A shell that can run the labs' shell scripts on Windows — making the labs' shell scripts run on a Windows machine
- [x] 6. Verifying the toolchain end to end — versions, and formatting and validation of a configuration that creates nothing
- [x] 7. OpenTofu differences — optional; you decide whether to include it

**Topics to add:**

- [ ] <a topic to add>

## M02 — Configuring Providers and Connecting to AWS

**Theme:** Sign in to AWS, no static keys; providers, version constraints, lock file (plan only)  
**Builds on:** M01 · **Feeds into:** M03, M11

**If every topic is kept:** 28 tasks — Setup 3, Build 8 (6 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Authenticating to AWS (IAM Identity Center) and verifying Terraform identity — signing in with the access you were given and confirming which identity and account Terraform will act as
- [x] 2. Keeping static access keys off disk and out of the repository — where keys end up by accident, and how you check that none are there
- [x] 3. What a provider is and how Terraform finds and installs one — the plugins a configuration needs, and where they come from
- [x] 4. Provider concepts, credential configuration, and default tags — how a provider obtains its credentials, and tags set at the provider
- [x] 5. Dependency management: version constraints, lock files, and safe upgrades — what you declare, what the lock file records, and how to move a pinned version deliberately
- [x] 6. Using and inspecting multiple providers in a single configuration — seeing which providers and versions a configuration actually uses

**Topics to add:**

- [ ] <a topic to add>

## M03 — Understanding the Terraform Workflow

**Theme:** Declarative model, resource anatomy; plan, apply, destroy; plan review; in-place vs replace  
**Builds on:** M02 · **Feeds into:** M04, M06, M10

**If every topic is kept:** 28 tasks — Setup 3, Build 8 (6 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Declarative versus imperative infrastructure — what it means that Terraform describes desired state
- [x] 2. Anatomy of a resource — type, name, arguments and attributes
- [x] 3. The core workflow — initialise, plan, apply, destroy
- [x] 4. What a plan shows — reading the action for each resource, and the difference between in-place updates and replacement
- [x] 5. Plan review as a habit — what to check before approving
- [x] 6. Destroying what you created — removing what you built, and proving it is gone

**Topics to add:**

- [ ] <a topic to add>

## M04 — Managing Terraform State

**Theme:** What local state is and why it is sensitive; moving it into a protected S3 backend with native locking  
**Builds on:** M03 · **Feeds into:** M05, M08, M09, M10

**If every topic is kept:** 28 tasks — Setup 3, Build 8 (6 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Understanding and inspecting local state (read-only) — what state records, where it lives and what Terraform uses it for, looked at without changing anything
- [x] 2. Secrets and state — what lands in state and who can read it
- [x] 3. Why state moves to a remote backend — what a team loses when state stays on one machine
- [x] 4. Bootstrapping and securing the state bucket — where the bucket itself comes from, how it is protected, and why it outlives the stage
- [x] 5. Configuring the backend and migrating existing local state into it — moving the state you already have, without recreating anything
- [x] 6. Native state locking — holding one operation while a second tries to run

**Topics to add:**

- [ ] <a topic to add>

## M05 — Terraform for Multi-Environment Deployments

**Theme:** Dev and prod from one configuration; directory vs workspaces vs per-environment files compared  
**Builds on:** M04 · **Feeds into:** M09

**If every topic is kept:** 29 tasks — Setup 3, Build 9 (7 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. One configuration, many environments — what is shared and what must be separate
- [x] 2. Per-environment input values — which values differ between dev and prod, and where they live
- [x] 3. Per-environment backend settings and separate state keys in the shared bucket — how the state key keeps one environment's state apart from the other's
- [x] 4. Managing blast radius through state separation — what separate state protects, and what it does not
- [x] 5. Enforcing naming conventions and default provider tags — a convention for names, and tags applied through the provider
- [x] 6. Switching between environments safely — what you check before every apply so you are in the environment you meant
- [x] 7. Alternative isolation methods: directories vs workspaces (theory) — explained in your comparison note, not built

**Topics to add:**

- [ ] <a topic to add>

## M06 — Managing Resources with Network Provisioning

**Theme:** Dependencies, repetition, data sources, a small VPC  
**Builds on:** M03 · **Feeds into:** M07, M08

**If every topic is kept:** 26 tasks — Setup 3, Build 6 (5 topics and 1 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Resource references and the dependency graph Terraform builds from them — where your own configuration refers to one resource from another
- [x] 2. Implicit versus explicit dependencies — which ordering Terraform infers, and which you would have to state
- [x] 3. Repeating a resource — the two mechanisms Terraform offers
- [x] 4. Data sources — reading information that already exists, and how it differs from a resource
- [x] 5. A VPC, subnets in more than one availability zone, and the routing a public tier needs — the small network you build

**Topics to add:**

- [ ] <a topic to add>

## M07 — Defining Variables, Inputs and Outputs in Terraform

**Theme:** Typed, validated inputs; value precedence; locals; sensitive inputs and outputs  
**Builds on:** M06 (you may reuse that work) · **Feeds into:** M08, M09

**If every topic is kept:** 32 tasks — Setup 3, Build 12 (9 topics and 3 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Input variables — what a variable declares, and the defaults you give it
- [x] 2. Validation rules enforced at plan time — rules that reject a bad value before anything is planned
- [x] 3. Supplying values — the ways to give a variable a value
- [x] 4. Variable value precedence — which source wins when several supply the same variable, found by hands-on experiment
- [x] 5. Keeping environment-specific values out of the main configuration — what belongs in the main configuration and what does not
- [x] 6. Local values — naming and reusing derived values within a configuration
- [x] 7. Sensitive input variables — marking them and getting their values into Terraform without committing them
- [x] 8. Output values — what to expose and how to mark an output sensitive
- [x] 9. What marking a value sensitive does and does not protect — what the marking does and does not protect, shown with placeholder values

**Topics to add:**

- [ ] <a topic to add>

## M08 — Advanced Terraform Configuration

**Theme:** `for_each` in depth, dynamic blocks, conditions, `for` expressions, data sources, dependency and lifecycle controls  
**Builds on:** M04, M06, M07 · **Feeds into:** M09

**If every topic is kept:** 30 tasks — Setup 3, Build 10 (8 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Composing Values with Built-in Functions — deriving a value with functions instead of repeating it
- [x] 2. Making Configuration Conditional — creating or setting something only when a condition holds
- [x] 3. Reshaping Data with `for` and Splat Expressions — turning one collection into another, in your own plan output
- [x] 4. Going Deeper with `for_each` — repeating resources from a map or a set, and what makes a key stable
- [x] 5. Generating Nested Configuration with Dynamic Blocks — generating repeated nested blocks from data
- [x] 6. Discovering Existing Infrastructure with Data Sources — looking up what already exists instead of hard-coding it
- [x] 7. Controlling Dependencies and Resource Lifecycle — ordering that a reference cannot express, and controlling replacement, destruction and ignored changes
- [x] 8. Validating Infrastructure with Preconditions and Postconditions — checking assumptions about real infrastructure

**Topics to add:**

- [ ] <a topic to add>

## M09 — Designing Reusable Terraform Modules

**Theme:** Reusable modules: structure, naming, comments, interfaces, consuming published modules  
**Builds on:** M04, M05, M07, M08 · **Feeds into:** M10

**If every topic is kept:** 34 tasks — Setup 3, Build 14 (12 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. What a module is — the root module, child modules, and what a module call does
- [x] 2. Deciding what belongs in a module, and what does not — drawing the line between the root configuration and the module
- [x] 3. A module's interface — inputs, outputs, and what it keeps private
- [x] 4. Standard module file structure — where inputs, outputs, resources and version requirements live
- [x] 5. Naming conventions for a module's inputs, outputs and resources — one convention that a newcomer can follow
- [x] 6. Comments and documentation — comment syntax, what deserves a comment, and descriptions on inputs and outputs
- [x] 7. Calling the same module more than once with different inputs — the same module used twice, with different inputs
- [x] 8. How modules change resource addresses in a plan and in state — what moving resources into a module does to their addresses
- [x] 9. Module sources and versions — local paths versus registry or Git sources, and pinning
- [x] 10. Consuming a published module — reading someone else's module before trusting it
- [x] 11. What a module may assume about provider configuration — what the module can take for granted from its caller
- [x] 12. Module anti-patterns — patterns that make a module hard to use or maintain

**Topics to add:**

- [ ] <a topic to add>

## M10 — Change with Confidence: Safe Terraform Refactoring

**Theme:** Rename, adopt, stop managing — no destroys; reading plans as JSON; recovering from a failed apply  
**Builds on:** M03, M04, M09 · **Feeds into:** the capstone

**If every topic is kept:** 27 tasks — Setup 3, Build 7 (5 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Refactoring principles: renaming and removing resources without destruction — changing configuration, not state, so that nothing real is destroyed or replaced
- [x] 2. Adopting existing, unmanaged resources into Terraform — bringing something that already exists under Terraform's management
- [x] 3. Verifying refactors mechanically: reading plans as JSON with `jq` — checking the action on every resource in a saved plan rather than by eye
- [x] 4. Emergency recovery: handling partial applies and failed destroys — what to do when an apply or destroy stops part-way
- [x] 5. Advanced troubleshooting: targeted operations and legacy state commands — what these are, and when you would meet them

**Topics to add:**

- [ ] <a topic to add>

## M11 — Going Multi-Cloud with Terraform

**Theme:** GCP and Azure sign-in and provider setup  
**Builds on:** M01, M02 · **Feeds into:** the capstone

**If every topic is kept:** 26 tasks — Setup 3, Build 6 (5 topics and 1 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Confirming access to the GCP and Azure sandboxes — checking that you can reach both sandboxes before you write anything
- [x] 2. GCP — Application Default Credentials sign-in, project selection, provider configuration — signing in with a short-lived login and pointing the configuration at the right project
- [x] 3. Azure — CLI sign-in, subscription selection, provider configuration — signing in with a short-lived login and pointing the configuration at the right subscription
- [x] 4. State management across clouds: `gcs` and `azurerm` backends — reference only: you do not configure them
- [x] 5. Where this course stops — HCP Terraform and Sentinel, named and not taught

**Topics to add:**

- [ ] <a topic to add>
