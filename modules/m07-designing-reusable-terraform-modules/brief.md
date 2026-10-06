# M07 — Designing Reusable Terraform Modules Brief

**Stage:** 7 of 9 · **Builds on:** M02, M04, M05, M06 · **Feeds into:** M08

## Objective

By the end of this stage, you can package part of a configuration as a reusable Terraform module with a standard structure and a deliberate, documented interface, call it more than once, and explain what a module boundary does to inputs, outputs, resource addresses and blast radius — using your own module's plans and state as the evidence, not the documentation. You can say when a module is the wrong answer.

## Scope

You build and read your own module, not a worked example. Find out, and write down in your own words:

- **What a module is** — the root module, child modules, and what a module call does. Research: what a module call hands to the module and what it gets back.
- **Deciding what belongs in a module, and what does not** — drawing the line between the root configuration and the module. Research: what belongs inside a module and what should stay in the root, and how you drew that line.
- **A module's interface** — inputs, outputs, and what it keeps private. Research: which inputs you exposed and which you fixed, what each extra input costs the next person who has to understand the module, and what a caller needs to be told by a module's outputs.
- **Standard module file structure** — where inputs, outputs, resources and version requirements live. Research: how a module's files should be laid out so a newcomer finds inputs, outputs and resources without being told.
- **Naming conventions for a module's inputs, outputs and resources** — one convention that a newcomer can follow. Research: which naming convention you chose, and why.
- **Comments and documentation** — comment syntax, what deserves a comment, and descriptions on inputs and outputs. Research: what deserves a comment in a module, and what the code should make obvious without one.
- **Calling the same module more than once with different inputs** — the same module used twice, with different inputs. Research: what stays shared between the calls and what each call owns.
- **How modules change resource addresses in a plan and in state** — what moving resources into a module does to their addresses. Research: how resource addresses change when something moves into a module, and what that would mean for a configuration that is already deployed.
- **Module sources and versions** — local paths versus registry or Git sources, and pinning. Research: what pinning protects you from for each kind of source.
- **Consuming a published module** — reading someone else's module before trusting it. Research: how much you trust a module you did not write, and what you check before using it.
- **What a module may assume about provider configuration** — what the module can take for granted from its caller. Research: what a module assumes about provider configuration, and where it takes its region, account and environment name from.
- **Module anti-patterns** — patterns that make a module hard to use or maintain. Research: when a module is the wrong answer.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- You use AWS only, and a module you write in this stage must not abstract over several clouds.
- Terraform is 1.11 or later, with provider versions pinned from `versions.env`.
- The module you author lives in the same repository as its caller and is referenced by local path, and any registry or Git module you consume is pinned to an exact version.
- The public Terraform Registry is free, so use no paid tooling.
- State lives in the M02 bucket, keyed per environment as in M05.
- Every call of the module creates its own resources, so keep them small and cheap, look up what each one bills before you apply, and destroy everything except the bucket at the end.
- Publishing a module to a registry, testing modules, deeply nested module trees (one level of nesting is enough), the HCP Terraform private registry and Terraform Stacks are out of scope.

## Deliverable

**A reusable AWS module with a standard file structure and a documented, commented interface, and a root configuration that calls it at least twice with different inputs**, deployed with the M05 environment arrangement, plus a decision note on what you put in the module and what you left out.

## Lab

**Goal.** Package part of a configuration as a reusable Terraform module and use it more than once.

**You do, in the sandbox.**

1. Move part of an earlier configuration (the network from M03) into `modules/network/` with `main.tf`, `variables.tf`, `outputs.tf` and `versions.tf`.
2. Give every input a type and a description, give every output a description, add one `validation`, and write comments that explain why, not what.
3. In the root configuration, call the module twice with different inputs, as `module "dev"` and `module "prod"`, each with `source = "./modules/network"`.
4. Run `terraform init`, `terraform plan` and `terraform apply`, then run `terraform state list` to see the module paths in the resource addresses.
5. Find a published module on the Terraform Registry, read its source, and write down its pinned version, its inputs and outputs, and what you checked before trusting it.
6. Check that the names and tags follow the convention from M05, then destroy.

**You build and capture.** The module and the root configuration that calls it are your deliverable. Capture clean plans for both calls, the distinct module paths, the names and tags of what the module creates, and your review of a published module.

**Clean-up.** Destroy everything except the M02 bucket.

## Definition of done

- DoD-01: Formatting and validation pass for both the module and the root configuration, and the module is called at least twice with different inputs: both calls produce clean plans (output pasted) and resource addresses for the separate calls show distinct module paths (state listing pasted), not two copies of the same call.
- DoD-02: The module has a documented interface — every input has a type and a description, inputs that can take a bad value are validated, and every output has a description — and follows the standard module layout, so a reviewer can find what they need from file names alone (a reviewer reads the module).
- DoD-03: The names of the module's inputs, outputs and internal resources follow one convention, which your notes state, and your notes say which comment syntax you chose, what you chose to comment, and why (a reviewer reads the module).
- DoD-04: Your notes state what the module assumes about provider configuration and where it takes its region, account and environment name from, not that it “just works”, and resources created through the module still follow M05's naming convention and carry the required tags (shown from the plan, state or cloud side).
- DoD-05: Your notes review one published module — its source, pinned version, inputs and outputs, and what you checked before trusting it — and include a decision note that says what you put in the module, what you left out, and a case where you would not write a module.
- DoD-06: Everything is destroyed except the M02 bucket, confirmed from the cloud side.
- DoD-07: Your write-up takes a first-time learner to a reusable module called twice from a root configuration unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- Typed, validated inputs (the module interface)
- Layout and naming (module structure and naming conventions)
- Pinned versions (module sources)
- fmt and validate
- Reuse through documented, version-pinned modules

## Still open / ask your trainer

- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
