# M06 — Managing Terraform State

| | |
| --- | --- |
| Stage | 6 of 12 |
| Course reference | Module 6 / Activity 6 "State and drift" (solution-design §6.2) |
| Cloud | AWS |
| Builds on | M03 |
| Time box | TBC — see [README](../README.md#open-items-for-the-trainer) |
| Leaves behind | Nothing. Destroy everything. |

## Objective

Understand what Terraform's state is, why it must be treated as sensitive, and how the real world drifts away from it — and show that you can detect drift and decide how to reconcile it without ever editing state by hand.

## Scope

### In scope (in the order to tackle)

1. What state records and what Terraform uses it for
2. Secrets and state — what lands in state and who can read it
3. Inspecting state, read-only
4. Drift — how it arises and how Terraform detects it
5. Reconciling drift — deciding whether the code or the real world wins
6. Why state is never edited by hand

### Out of scope

- Remote state and locking (M07)
- Marking inputs and outputs sensitive, and getting sensitive values into Terraform (M05)
- Moving, importing or removing resources from state (M11)
- Anything that changes state outside the plan/apply cycle (ADR-008)

## Stack constraints

- Everything under [Rules for every stage](../README.md#rules-for-every-stage).
- AWS only; one or two small, cheap resources are enough.
- State is local in this stage.
- State subcommands are for read-only inspection only (ADR-008).
- State files never go into version control.

## Deliverable

**A small configuration taken through an out-of-band change and back to a clean plan**, with your written answers to the stage's questions.

## Open design questions

1. What can leak a secret into state, and how would you demonstrate that safely, without using a real credential?
2. When Terraform reports drift, who decides whether the code or the real world is right, and on what basis?
3. What would you check before trusting a state file you did not create?
4. Why does the course treat a state file as sensitive even when the configuration contains no secrets?

## Definition of done

- [ ] **DoD-1** The final plan shows no changes (output pasted).
- [ ] **DoD-2** The out-of-band change was detected by Terraform, not just noticed by you — the plan output from before reconciliation is captured.
- [ ] **DoD-3** The write-up records which side you let win (code or real world) and why.
- [ ] **DoD-4** Evidence shows that a sensitive value can be read from state, captured without exposing a real credential.
- [ ] **DoD-5** Your written answers agree with the trainer's model answers on review.
- [ ] **DoD-6** State files are excluded from version control (the ignore rule and a clean commit history show it).
- [ ] **DoD-7** Everything created is destroyed, confirmed from the cloud side.

## Best practices this stage demonstrates

- State hygiene (Activity 6 answers)
- fmt and validate
