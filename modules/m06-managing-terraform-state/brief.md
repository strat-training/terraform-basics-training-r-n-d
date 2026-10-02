# M06 — Managing Terraform State

| | |
| --- | --- |
| Stage | 6 of 12 |
| Cloud | AWS |
| Builds on | M03 |
| Cost | A few small, cheap resources. Look up what each one bills before you apply, and destroy them at the end of the stage. |
| Leaves behind | Nothing. Destroy everything. |

## Objective

Understand what Terraform's state is, why it must be treated as sensitive, and how the real world drifts away from it — and show that you can detect drift and decide how to reconcile it without ever editing state by hand.

## Scope

### In scope (in the order to tackle)

1. What state records and what Terraform uses it for
2. Secrets and state — what lands in state and who can read it
3. Keeping a secret out of state — ephemeral values and write-only arguments, where the provider supports them
4. Inspecting state, read-only
5. Drift — how it arises and how Terraform detects it
6. Reconciling drift — deciding whether the code or the real world wins
7. Why state is never edited by hand

### Out of scope

- Remote state and locking (M07)
- Marking inputs and outputs sensitive, and getting sensitive values into Terraform (M05)
- Moving, importing or removing resources from state (M11)
- Anything that changes state outside the plan/apply cycle

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- AWS only; a few small, cheap resources are enough.
- Terraform 1.11 or later. Write-only arguments depend on provider support, so your write-up says which resource and provider version you used and checks that support against the provider's documentation.
- State is local in this stage.
- State subcommands are for read-only inspection only.
- State files never go into version control.

## Deliverable

**A small configuration taken through an out-of-band change and back to a clean plan**, with your written answers to the stage's questions.

## Open design questions

1. What can leak a secret into state, and how would you demonstrate that safely, without using a real credential?
2. When Terraform reports drift, who decides whether the code or the real world is right, and on what basis?
3. What would you check before trusting a state file you did not create?
4. Why does the course treat a state file as sensitive even when the configuration contains no secrets?
5. When can a secret be kept out of state altogether, and what do you still have to protect when it is?

## Definition of done

- [ ] **DoD-1** The final plan shows no changes (output pasted).
- [ ] **DoD-2** The out-of-band change was detected by Terraform, not just noticed by you — the plan output from before reconciliation is captured.
- [ ] **DoD-3** The write-up records which side you let win (code or real world) and why.
- [ ] **DoD-4** Your evidence shows what state holds for a sensitive value, captured without exposing a real credential.
- [ ] **DoD-5** A secret reaches a resource through a write-only argument, and your evidence shows it is absent from state (output pasted, without exposing a real credential).
- [ ] **DoD-6** Your trainer confirms your written answers are correct on review.
- [ ] **DoD-7** State files are excluded from version control (the ignore rule and a clean commit history show it).
- [ ] **DoD-8** Everything created is destroyed, confirmed from the cloud side.

## Best practices this stage demonstrates

- State hygiene
- fmt and validate
