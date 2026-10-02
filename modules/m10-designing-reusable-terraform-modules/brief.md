# M10 — Designing Reusable Terraform Modules

| | |
| --- | --- |
| Stage | 10 of 12 |
| Cloud | AWS |
| Builds on | M05, M06, M07, M08, M09 |
| Cost | Small, cheap resources, and every call of the module creates its own. Look up what each one bills before you apply, and destroy everything except the M07 bucket at the end of the stage. |
| Leaves behind | Nothing except the M07 state bucket. Destroy everything else. |

## Objective

Package part of a configuration as a reusable Terraform module with a standard structure and a deliberate, documented interface. Call it more than once, comment it so the next person can maintain it, and explain what a module boundary does to inputs, outputs, resource addresses and blast radius — including when a module is the wrong answer.

## Scope

### In scope (in the order to tackle)

1. What a module is — the root module, child modules, and what a module call does
2. Deciding what belongs in a module, and what does not
3. A module's interface — inputs, outputs, and what it keeps private
4. Standard module file structure
5. Naming conventions for a module's inputs, outputs and resources
6. Comments and documentation — comment syntax, what deserves a comment, and descriptions on inputs and outputs
7. Calling the same module more than once with different inputs
8. How modules change resource addresses in a plan and in state
9. Module sources and versions — local paths versus registry or Git sources, and pinning
10. Consuming a published module — reading someone else's module before trusting it
11. What a module may assume about provider configuration
12. Module anti-patterns

### Out of scope

- Modules that wrap more than one cloud or hide provider differences
- Publishing a module to a registry
- Testing modules (`terraform test` is excluded)
- Deeply nested module trees; one level of nesting is enough
- HCP Terraform private registry and Terraform Stacks

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- AWS only. A module written in this stage must not abstract over several clouds.
- Terraform 1.11 or later, provider versions pinned from `versions.env`.
- The module you author lives in the same repository as its caller and is referenced by local path.
- Any registry or Git module you consume is pinned to an exact version. The public Terraform Registry is free; no paid tooling.
- State lives in the M07 bucket, keyed per environment as in M08.
- Keep resources small and cheap; destroy everything except the bucket at the end.

## Deliverable

**A reusable AWS module with a standard file structure and a documented, commented interface, and a root configuration that calls it at least twice with different inputs**, deployed with the M08 environment arrangement, plus a decision note on what you put in the module and what you left out.

## Open design questions

1. What belongs inside a module and what should stay in the root, and how did you draw that line?
2. Which inputs did you expose, which did you fix, and what does each extra input cost the next person who has to understand the module?
3. What does a caller need to be told by a module's outputs, and what should stay hidden?
4. How should a module's files be laid out so a newcomer finds inputs, outputs and resources without being told?
5. What deserves a comment in a module, and what should the code make obvious without one?
6. How do resource addresses change when something moves into a module, and what would that mean for a configuration that is already deployed?
7. How much do you trust a module you did not write, and what do you check before using it?
8. When is a module the wrong answer?

## Definition of done

- [ ] **DoD-1** Formatting and validation checks pass for both the module and the root configuration.
- [ ] **DoD-2** The module has a documented interface: every input has a type and a description, inputs that can take a bad value are validated, and every output has a description (a reviewer reads the module).
- [ ] **DoD-3** The module follows the standard module layout; a reviewer can find what they need from file names alone.
- [ ] **DoD-4** The names of the module's inputs, outputs and internal resources follow one convention, which your write-up states.
- [ ] **DoD-5** Your write-up states which comment syntax you chose, what you chose to comment, and why (a reviewer reads the module).
- [ ] **DoD-6** The module is called at least twice with different inputs and both calls produce clean plans (output pasted).
- [ ] **DoD-7** Your write-up states what the module assumes about provider configuration and where it takes its region, account and environment name from (a reviewer reads the module).
- [ ] **DoD-8** Resource addresses for the separate calls show distinct module paths (state listing pasted).
- [ ] **DoD-9** Resources created through the module still follow M08's naming convention and carry the required tags (shown from the plan, state or cloud side).
- [ ] **DoD-10** The write-up contains a review of one published module — its source, pinned version, inputs and outputs, and what you checked before trusting it.
- [ ] **DoD-11** The decision note says what you put in the module, what you left out, and a case where you would not write a module.
- [ ] **DoD-12** Everything is destroyed except the M07 bucket, confirmed from the cloud side.

## Best practices this stage demonstrates

- Typed, validated inputs (the module interface)
- Layout and naming (module structure and naming conventions)
- Pinned versions (module sources)
- fmt and validate
- Reuse through documented, version-pinned modules
