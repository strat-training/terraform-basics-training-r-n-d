# M03 — Understanding the Terraform Workflow

| | |
| --- | --- |
| Stage | 3 of 12 |
| Cloud | AWS |
| Builds on | M02 |
| Cost | One small, cheap resource. Look up what it bills before you apply, and destroy it at the end of the stage. |
| Leaves behind | Nothing. Destroy everything. |

## Objective

Understand why Terraform describes the desired state of infrastructure instead of scripting steps, then run the core workflow end to end on a real resource and make reading the plan before applying a habit — to the point where you can predict, from a plan, whether a change updates a resource in place or replaces it.

## Scope

### In scope (in the order to tackle)

1. Declarative versus imperative infrastructure — what it means that Terraform describes desired state
2. Anatomy of a resource — type, name, arguments and attributes
3. The core workflow — initialise, plan, apply, destroy
4. What a plan shows — reading the action for each resource, In-place updates versus replacement
5. Plan review as a habit — what to check before approving
6. Destroying what you created

### Out of scope

- Variables and validation (M05)
- State internals and drift (M06)
- Remote state (M07)
- Lifecycle controls that change replacement behaviour (M09)
- Refactoring without replacement (M11)

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
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

Your training module — the build plus the write-up that teaches it — is done when each of these is true.

- [ ] **DoD-1** Your write-up shows formatting and validation passing with no errors, as pasted output.
- [ ] **DoD-2** Your write-up shows the same apply run twice on an unchanged configuration, with both outputs pasted, and explains the difference between them in terms of desired state, not as “it did nothing the second time”.
- [ ] **DoD-3** Your write-up identifies the type, name, arguments and attributes of your own resource and shows an attribute whose value you did not set, from real output.
- [ ] **DoD-4** Your write-up shows at least one in-place change and at least one forced replacement, each with the plan output captured before it was applied, not afterwards.
- [ ] **DoD-5** Every change in your plan-review note is classified as in-place or replacement, and your trainer confirms each classification on review.
- [ ] **DoD-6** A learner following your training module ends with the resource gone after destroy, confirmed from the cloud side, not only from Terraform's output.

## Best practices this stage demonstrates

- Plan review
- fmt and validate
