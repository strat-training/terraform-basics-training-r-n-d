# M03 — Understanding the Terraform Workflow

| | |
| --- | --- |
| Stage | 3 of 12 |
| Course reference | Module 3 / Activity 3 "Apply/change/replace" (solution-design §6.2) |
| Cloud | AWS |
| Builds on | M02 |
| Time box | TBC — see [README](../README.md#open-items-for-the-trainer) |
| Leaves behind | Nothing. Destroy everything. |

## Objective

Understand why Terraform describes the desired state of infrastructure instead of scripting steps, then run the core workflow end to end on a real resource and make reading the plan before applying a habit — to the point where you can predict, from a plan, whether a change updates a resource in place or replaces it.

## Scope

### In scope (in the order to tackle)

1. Declarative versus imperative infrastructure — what it means that Terraform describes desired state
2. Anatomy of a resource — type, name, arguments and attributes
3. The core workflow — initialise, plan, apply, destroy
4. What a plan shows — reading the action for each resource
5. In-place updates versus replacement
6. What causes a replacement
7. Plan review as a habit — what to check before approving
8. Destroying what you created

### Out of scope

- Variables and validation (M05)
- State internals and drift (M06)
- Remote state (M07)
- Lifecycle controls that change replacement behaviour (M09)
- Refactoring without replacement (M11)

## Stack constraints

- Everything under [Rules for every stage](../README.md#rules-for-every-stage).
- AWS only. Use one small, cheap resource such as an S3 bucket — the stage's check confirms "the bucket is gone" at the end.
- State is local in this stage; remote state arrives in M07.
- Every apply is preceded by a plan you have read.

## Deliverable

**A configuration managing one small AWS resource, taken through create, in-place change, forced replacement and destroy**, with a written plan-review note.

## Open design questions

1. How does describing the desired state differ from scripting the steps, and what does that change about running the same configuration twice?
2. How can you tell from the plan alone that a change will destroy something, before you apply it?
3. For your chosen resource, which changes are made in place and which force replacement — how did you establish that, and how sure are you?
4. What would you do if a plan showed a destroy you did not expect?
5. What does a replacement cost when the resource holds data or other resources depend on it?

## Definition of done

- [ ] **DoD-1** Formatting and validation checks pass with no errors.
- [ ] **DoD-2** You ran the same apply twice without changing the configuration; both outputs are pasted, and the write-up explains the difference between them in terms of desired state.
- [ ] **DoD-3** Your write-up identifies the type, name, arguments and attributes of your resource, and shows an attribute whose value you did not set.
- [ ] **DoD-4** You made at least one in-place change and at least one forced replacement; the plan output for each was captured before it was applied.
- [ ] **DoD-5** Your plan-review note classifies every change you made as in-place or replacement, and the trainer's model answer agrees with each classification.
- [ ] **DoD-6** For each classification the note explains the cause in terms of the resource itself, not just the plan's symbols.
- [ ] **DoD-7** After destroy the resource is gone — confirmed from the cloud side, not only from Terraform's output.

## Best practices this stage demonstrates

- Plan review (Activity 3 note)
- fmt and validate
