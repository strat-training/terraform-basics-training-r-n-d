# Curriculum — scope by stage

Every topic each training stage covers, in the order the stage tackles it, so you can choose what stays. Each scope item becomes one build task in the stage's checklist. The stage's deliverable components, definition-of-done checks and write-up sections add the rest. The research prompts under each topic are answered in the write-up, so they are not tasks, but dropping a topic should still drop its research prompts and the checks that depended on it. Each stage's lab is listed under its topics, so you can see the hands-on work that goes with them.

## How to choose

1. Every box starts ticked. Untick a topic you want to drop, or add one under the stage.
2. For each stage you changed, update the brief's scope first. Then drop or reword the research prompts, the lab and the definition-of-done checks that depended on the dropped topics, and regenerate the write-up template and checklist (see "Keeping the stage files in step" in [README.md](README.md)).
3. A topic that a later stage relies on is flagged in that later stage's "Builds on" line, so check it before dropping a topic from an earlier stage.

## Overview

| Stage | Title | Scope items | Research prompts | Done checks | Tasks | Builds on |
| --- | --- | --- | --- | --- | --- | --- |
| M01 | Getting Started with Terraform | 5 | 5 | 7 | 27 | — (course entry point) |
| M02 | Managing Terraform State | 6 | 6 | 7 | 28 | M01 |
| M03 | Managing Resources with Network Provisioning | 5 | 5 | 7 | 26 | M01 |
| M04 | Defining Variables, Inputs and Outputs in Terraform | 9 | 9 | 7 | 32 | M03 (you may reuse that work) |
| M05 | Terraform for Multi-Environment Deployments | 7 | 7 | 7 | 29 | M02, M04 |
| M06 | Advanced Terraform Configuration | 8 | 8 | 7 | 30 | M02, M03, M04 |
| M07 | Designing Reusable Terraform Modules | 12 | 12 | 7 | 34 | M02, M04, M05, M06 |
| M08 | Change with Confidence: Safe Terraform Refactoring | 5 | 5 | 7 | 27 | M01, M02, M07 |
| M09 | Going Multi-Cloud with Terraform | 5 | 5 | 7 | 26 | M01 |

The nine stages generate 259 tasks between them. The capstone has its own checklist and is not listed here.

## M01 — Getting Started with Terraform

**Theme:** Workstation, sign-in with no static keys, providers and the lock file, then one resource taken through init, plan, apply, update and destroy  
**Builds on:** — (course entry point) · **Feeds into:** M02, M03, M08, M09

**If every topic is kept:** 27 tasks — Setup 3, Build 7 (5 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Step 1 — The workstation (zero code) — what Terraform is (declarative versus imperative), the core toolchain including a version manager, and keeping static access keys off disk; the environment and the mental model come before any editor
- [x] 2. Step 2 — Dependencies: the `versions.tf` file — what a provider is, version constraints, dependency management and the lock file, introduced before any infrastructure is written
- [x] 3. Step 3 — Configuration: the `providers.tf` file — provider concepts, how Terraform finds the AWS session you signed in with, and default tags, kept in a file of its own; checking syntax on a small, safe file before the configuration gets complex
- [x] 4. Step 4 — Resources and planning: the `main.tf` file — the anatomy of a resource (type, name, arguments and attributes), and plan review as a habit
- [x] 5. Step 5 — Apply and destroy — in-place updates versus replacement, and destroying what you created

**Lab**

- [x] **Goal:** Take one simple AWS resource through the whole Terraform lifecycle, from an empty folder to a clean destroy, on a workstation you set up yourself.
  - **You do:**
    1. The workstation: install Terraform through a version manager (`tfenv` or `asdf`) and the AWS CLI, configure VS Code, sign in to AWS through IAM Identity Center, and prove the connection without static keys with `aws sts get-caller-identity` and `terraform -version`.
    2. Dependencies: create `versions.tf` with the required providers block, run `terraform init`, and watch the `.terraform` folder and the `.terraform.lock.hcl` file appear.
    3. Configuration: create `providers.tf` with the AWS provider and a default tags block, then run `terraform fmt` and `terraform validate`.
    4. Resources and planning: create `main.tf` with a single resource, run `terraform plan`, read the output, and check that the default tags from step 3 are attached to the resource in the plan.
    5. Apply and destroy: run `terraform apply`, change one attribute to trigger an update, run `terraform plan` and look for the in-place update, apply again, then run `terraform destroy`.
  - **You build and capture:** The three files and the workstation are your deliverable. Capture the version output (including a switch between two Terraform versions), the caller-identity output, the scan for static keys, the files that `terraform init` created, the plan with the default tags on the resource, the plan that shows the in-place update, and the destroy confirmed from the cloud side.
  - **Clean-up:** Destroy the resource and confirm from the cloud side that it is gone.

**Topics to add:**

- [ ] <a topic to add>

## M02 — Managing Terraform State

**Theme:** What local state is and why it is sensitive; moving it into a protected S3 backend with native locking  
**Builds on:** M01 · **Feeds into:** M05, M06, M07, M08

**If every topic is kept:** 28 tasks — Setup 3, Build 8 (6 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Understanding and inspecting local state (read-only) — what state records, where it lives and what Terraform uses it for, looked at without changing anything
- [x] 2. Secrets and state — what lands in state and who can read it
- [x] 3. Why state moves to a remote backend — what a team loses when state stays on one machine
- [x] 4. Bootstrapping and securing the state bucket — where the bucket itself comes from, how it is protected, and why it outlives the stage
- [x] 5. Configuring the backend and migrating existing local state into it — moving the state you already have, without recreating anything
- [x] 6. Native state locking — holding one operation while a second tries to run

**Lab**

- [x] **Goal:** See what local state records, then move it into a protected S3 backend and prove that locking works.
  - **You do:**
    1. Local state: write a small configuration with one `aws_ssm_parameter` whose value is a made-up placeholder password, run `terraform init` and `terraform apply`, and see `terraform.tfstate` appear.
    2. Inspect it read-only: run `terraform state list` and `terraform state show` on the parameter, open `terraform.tfstate` to see where the placeholder value sits, and add `terraform.tfstate*` to `.gitignore`.
    3. The bucket: in a separate folder, write a configuration with an `aws_s3_bucket` and its versioning, encryption and public access block settings, and apply it with local state.
    4. The backend: in the first configuration, add a `backend "s3"` block that points at that bucket with native locking turned on (`use_lockfile = true`), run `terraform init -migrate-state`, then run `terraform plan` and check it shows no changes.
    5. Locking: start `terraform apply` and leave it at the approval prompt, run `terraform plan` in a second terminal, and read the lock error.
  - **You build and capture:** The bucket and the configuration that now uses it as its backend are your deliverable. Capture the read-only inspection, what state holds for a sensitive value (a placeholder only), the state object in the bucket, the protections shown from the cloud side, the plan after migration, and the lock error.
  - **Clean-up:** Keep the bucket and destroy everything else.

**Topics to add:**

- [ ] <a topic to add>

## M03 — Managing Resources with Network Provisioning

**Theme:** Dependencies, repetition, data sources, a small VPC  
**Builds on:** M01 · **Feeds into:** M04, M06

**If every topic is kept:** 26 tasks — Setup 3, Build 6 (5 topics and 1 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Resource references and the dependency graph Terraform builds from them — where your own configuration refers to one resource from another
- [x] 2. Implicit versus explicit dependencies — which ordering Terraform infers, and which you would have to state
- [x] 3. Repeating a resource — the two mechanisms Terraform offers
- [x] 4. Data sources — reading information that already exists, and how it differs from a resource
- [x] 5. A VPC, subnets in more than one availability zone, and the routing a public tier needs — the small network you build

**Lab**

- [x] **Goal:** Build a small AWS network and watch Terraform work out what depends on what.
  - **You do:**
    1. Start `main.tf` with an `aws_vpc` resource, and read the available zones with a `data "aws_availability_zones"` data source.
    2. Add two public subnets in different zones by repeating one `aws_subnet` block over the zones (`count` or `for_each`; write down which you used and why).
    3. Add an `aws_internet_gateway`, an `aws_route_table` with a default route to it, and an association between the route table and the subnets.
    4. Run `terraform plan` and `terraform graph`, find one dependency Terraform worked out from a reference, and add one `depends_on` where a reference cannot say what you need.
    5. Run `terraform apply`, look at the network in the console, then run `terraform destroy`.
  - **You build and capture:** The network configuration is your deliverable. Capture the plan showing the VPC, the subnets and the public routing, where your dependencies come from, the data source in use, and the destroy confirmed from the cloud side.
  - **Clean-up:** Destroy everything; no NAT gateway is created.

**Topics to add:**

- [ ] <a topic to add>

## M04 — Defining Variables, Inputs and Outputs in Terraform

**Theme:** Typed, validated inputs; value precedence; locals; sensitive inputs and outputs  
**Builds on:** M03 (you may reuse that work) · **Feeds into:** M05, M06, M07

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

**Lab**

- [x] **Goal:** Turn a hard-wired configuration into a parameterised one, and find out by experiment which source of a value wins.
  - **You do:**
    1. Take the network from M03 and replace the hard-coded region, address range and name prefix with `variable` blocks, each with a type, a description and a default.
    2. Add a `validation` block that rejects a bad address range, and test it with `terraform plan -var vpc_cidr=10.0.0.0/33`.
    3. Add a `locals` block for a name you use in more than one place.
    4. Run the precedence experiments: supply one variable from one source at a time — its default, `terraform.tfvars`, a `*.auto.tfvars` file, `-var`, `-var-file` and a `TF_VAR_` environment variable — run `terraform plan` for each, then combine sources and see which one wins.
    5. Add a variable marked `sensitive = true` with a placeholder value and a sensitive output, and run `terraform plan` and `terraform output` to see what is hidden.
    6. Plan with two different `.tfvars` files, then destroy anything you applied.
  - **You build and capture:** The parameterised configuration is your deliverable. Capture an invalid range rejected at plan time, clean plans for both sets of values, one plan per experiment and one for the combined run, and what is displayed for the sensitive input and output.
  - **Clean-up:** Destroy everything you created.

**Topics to add:**

- [ ] <a topic to add>

## M05 — Terraform for Multi-Environment Deployments

**Theme:** Dev and prod from one configuration; directory vs workspaces vs per-environment files compared  
**Builds on:** M02, M04 · **Feeds into:** M07

**If every topic is kept:** 29 tasks — Setup 3, Build 9 (7 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. One configuration, many environments — what is shared and what must be separate
- [x] 2. Per-environment input values — which values differ between dev and prod, and where they live
- [x] 3. Per-environment backend settings and separate state keys in the shared bucket — how the state key keeps one environment's state apart from the other's
- [x] 4. Managing blast radius through state separation — what separate state protects, and what it does not
- [x] 5. Enforcing naming conventions and default provider tags — a convention for names, and tags applied through the provider
- [x] 6. Switching between environments safely — what you check before every apply so you are in the environment you meant
- [x] 7. Alternative isolation methods: directories vs workspaces (theory) — explained in your comparison note, not built

**Lab**

- [x] **Goal:** Deploy dev and prod from one configuration with separate state, named and tagged consistently.
  - **You do:**
    1. Take one small configuration (the network from M03, or a single `aws_ssm_parameter`) and add `dev.tfvars` and `prod.tfvars` with different values.
    2. Add `dev.s3.tfbackend` and `prod.s3.tfbackend` files that point at the bucket from M02, each with its own state `key`.
    3. Name every resource `<app>-<env>-<resource>` and set `default_tags` in the provider block, including `Environment`.
    4. For dev, run `terraform init -backend-config=dev.s3.tfbackend -reconfigure` and `terraform apply -var-file=dev.tfvars`; then do the same for prod.
    5. List the bucket to see the two state objects, and run `terraform plan` for each environment to check it is clean.
    6. Write your comparison note on workspaces, a directory per environment and the per-environment files you used.
  - **You build and capture:** The one configuration deployed twice is your deliverable. Capture two state objects, a clean plan for each environment, the names and tags, and your comparison note.
  - **Clean-up:** Destroy both environments and keep the bucket.

**Topics to add:**

- [ ] <a topic to add>

## M06 — Advanced Terraform Configuration

**Theme:** `for_each` in depth, dynamic blocks, conditions, `for` expressions, data sources, dependency and lifecycle controls  
**Builds on:** M02, M03, M04 · **Feeds into:** M07

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

**Lab**

- [x] **Goal:** Describe infrastructure from data and see exactly what each change does to the real resources.
  - **You do:**
    1. Define one structured input in `variables.tf`: a map of rules, each with a port and a description.
    2. Create an `aws_vpc` and an `aws_security_group` whose ingress rules come from a `dynamic "ingress"` block over the map, and build the names with `locals` and built-in functions.
    3. Create one `aws_ssm_parameter` per map entry with `for_each`, and use a `for` expression to turn the map into an output list.
    4. Add a conditional so the parameters are created only when a flag is true, and run `terraform plan` with the flag on and off.
    5. Look up your account with a `data "aws_caller_identity"` data source and use it in a name, then add one `depends_on` and one `lifecycle` setting and read what each does in the plan.
    6. Add a `precondition` or `postcondition` and trigger it on purpose; then add an entry to the map, remove one and change a key, running `terraform plan` each time, and destroy.
  - **You build and capture:** The data-driven configuration is your deliverable. Capture the plan for each input change, the plan for both outcomes of the conditional, the effect of each lifecycle setting, and the failure message you triggered.
  - **Clean-up:** Destroy everything except the M02 bucket.

**Topics to add:**

- [ ] <a topic to add>

## M07 — Designing Reusable Terraform Modules

**Theme:** Reusable modules: structure, naming, comments, interfaces, consuming published modules  
**Builds on:** M02, M04, M05, M06 · **Feeds into:** M08

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

**Lab**

- [x] **Goal:** Package part of a configuration as a reusable Terraform module and use it more than once.
  - **You do:**
    1. Move part of an earlier configuration (the network from M03) into `modules/network/` with `main.tf`, `variables.tf`, `outputs.tf` and `versions.tf`.
    2. Give every input a type and a description, give every output a description, add one `validation`, and write comments that explain why, not what.
    3. In the root configuration, call the module twice with different inputs, as `module "dev"` and `module "prod"`, each with `source = "./modules/network"`.
    4. Run `terraform init`, `terraform plan` and `terraform apply`, then run `terraform state list` to see the module paths in the resource addresses.
    5. Find a published module on the Terraform Registry, read its source, and write down its pinned version, its inputs and outputs, and what you checked before trusting it.
    6. Check that the names and tags follow the convention from M05, then destroy.
  - **You build and capture:** The module and the root configuration that calls it are your deliverable. Capture clean plans for both calls, the distinct module paths, the names and tags of what the module creates, and your review of a published module.
  - **Clean-up:** Destroy everything except the M02 bucket.

**Topics to add:**

- [ ] <a topic to add>

## M08 — Change with Confidence: Safe Terraform Refactoring

**Theme:** Rename, adopt, stop managing — no destroys; reading plans as JSON; recovering from a failed apply  
**Builds on:** M01, M02, M07 · **Feeds into:** the capstone

**If every topic is kept:** 27 tasks — Setup 3, Build 7 (5 topics and 2 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Refactoring principles: renaming and removing resources without destruction — changing configuration, not state, so that nothing real is destroyed or replaced
- [x] 2. Adopting existing, unmanaged resources into Terraform — bringing something that already exists under Terraform's management
- [x] 3. Verifying refactors mechanically: reading plans as JSON with `jq` — checking the action on every resource in a saved plan rather than by eye
- [x] 4. Emergency recovery: handling partial applies and failed destroys — what to do when an apply or destroy stops part-way
- [x] 5. Advanced troubleshooting: targeted operations and legacy state commands — what these are, and when you would meet them

**Lab**

- [x] **Goal:** Rename, adopt and stop managing resources without destroying anything.
  - **You do:**
    1. Apply a small configuration with two `aws_ssm_parameter` resources, and create a third parameter by hand in the console.
    2. Rename one parameter in the configuration and add a `moved` block, then run `terraform plan -out=rename.tfplan` and check that it shows no destroys or replacements.
    3. Adopt the hand-made parameter: add an `import` block, run `terraform plan -generate-config-out=generated.tf`, tidy the generated file, and check that the next plan shows no changes.
    4. Stop managing one parameter with a `removed` block (`lifecycle { destroy = false }`), apply, and check from the cloud side that it still exists.
    5. For each saved plan, run `terraform show -json` and use `jq` to list the action on every resource.
    6. Break an apply on purpose with an invalid value, read the error and what state holds, then fix it and re-run to a clean plan without editing state by hand.
  - **You build and capture:** The three refactors are your deliverable. Capture the plan summaries, the check that reads a saved plan's JSON, the identity of the renamed resource, the error and what state holds afterwards, and the recovery.
  - **Clean-up:** No billable resource is left behind; only the M02 bucket remains.

**Topics to add:**

- [ ] <a topic to add>

## M09 — Going Multi-Cloud with Terraform

**Theme:** GCP and Azure sign-in and provider setup  
**Builds on:** M01 · **Feeds into:** the capstone

**If every topic is kept:** 26 tasks — Setup 3, Build 6 (5 topics and 1 deliverable components), Verify 7, Write-up 10.

**Topics**

- [x] 1. Installing the CLIs and confirming access to the GCP and Azure sandboxes — installing the Google Cloud and Azure command-line tools and checking that you can reach both sandboxes before you write anything
- [x] 2. GCP — Application Default Credentials sign-in, project selection, provider configuration — signing in with a short-lived login and pointing the configuration at the right project
- [x] 3. Azure — CLI sign-in, subscription selection, provider configuration — signing in with a short-lived login and pointing the configuration at the right subscription
- [x] 4. State management across clouds: `gcs` and `azurerm` backends — reference only: you do not configure them
- [x] 5. Where this course stops — HCP Terraform and Sentinel, named and not taught

**Lab**

- [x] **Goal:** Sign in to GCP and Azure with short-lived logins and prove each provider works without creating anything.
  - **You do:**
    1. Install the Google Cloud CLI and the Azure CLI, then sign in with `gcloud auth application-default login` and `az login`.
    2. Confirm where you are signed in with `gcloud config get-value project` and `az account show`.
    3. In a `gcp/` folder, write a configuration with the `google` provider and an explicit `project`, a read-only data source and an output for the identity; in an `azure/` folder, do the same with the `azurerm` provider and an explicit `subscription_id`.
    4. In each folder run `terraform init`, `terraform fmt`, `terraform validate` and `terraform plan`, and read the identity output.
    5. Switch your active login to another project or subscription if you have one, run `terraform plan` again, and check that each configuration still targets the one you intended.
    6. Scan the repository and your disk for secrets and keys, and check that each plan shows nothing to add.
  - **You build and capture:** The two configurations are your deliverable. Capture the identity output for each cloud, evidence that the intended project or subscription is used even when the login points elsewhere, the scan for secrets and keys, and a plan with nothing to add.
  - **Clean-up:** Nothing is created, so there is nothing to destroy.

**Topics to add:**

- [ ] <a topic to add>
