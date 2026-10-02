# M11 — Change with Confidence: Safe Terraform Refactoring

| | |
| --- | --- |
| Stage | 11 of 12 |
| Cloud | AWS |
| Builds on | M03, M06, M07, M10 |
| Cost | Look up what each resource in your plan bills before you apply, and destroy everything except the M07 bucket at the end of the stage. |
| Leaves behind | Nothing except the M07 state bucket. |

## Objective

Rename, adopt and stop managing resources without destroying anything, by changing configuration rather than editing state — and verify every change with a plan that shows no destroys and no replacements.

## Scope

### In scope (in the order to tackle)

1. Why refactoring must never mean destroy-and-recreate
2. Renaming or re-addressing a resource without replacing it
3. Adopting an existing, unmanaged resource into Terraform
4. Tidying generated configuration
5. Ceasing to manage a resource without destroying it
6. Verifying every refactor with a plan
7. Reading a saved plan as JSON with `jq` — checking the action on every resource mechanically
8. Targeted operations — an emergency tool, never routine
9. Reading legacy guidance that relies on imperative state commands
10. When an apply goes wrong — a partial apply, a failed destroy, and reading provider errors

### Out of scope

- Imperative state mutation as the method for any refactor
- Editing state by hand

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- Every refactor is a declarative change in configuration. State subcommands are for inspection only and are not how any refactor here is performed.
- State lives in the M07 bucket under its own key.
- Terraform 1.11 or later. Verify the refactoring features you rely on against the release notes of the pinned version before you write them up.
- The resource you adopt must genuinely exist outside Terraform's management beforehand.
- Adopting a resource involves generated configuration that needs manual tidying; that tidying is part of the work.

## Deliverable

**Three refactors applied to a small configuration — a rename, an adoption and a stop-managing — each verified by a plan with no destroys and no replacements**, plus a short note on legacy imperative commands.

## Open design questions

1. How can you tell, before applying, that a refactor will not touch real infrastructure?
2. What did the generated configuration get wrong or leave out, and how did you decide what to keep?
3. When a resource stops being managed, what is responsible for it afterwards, and how do you avoid orphaning cost?
4. Why does the course prefer changes that appear in a plan over commands that edit state, and when might you still see those commands?
5. How do you recover when an apply stops part-way, and what do you check before you run it again?

## Definition of done

- [ ] **DoD-1** After each of the three refactors, a saved plan shows zero destroys and zero replacements (three plan summaries pasted).
- [ ] **DoD-2** At least one of the three plan checks reads the saved plan's JSON form with `jq` and reports the action on every resource (output pasted).
- [ ] **DoD-3** The renamed resource keeps its real-world identity (its cloud-side identifier is unchanged).
- [ ] **DoD-4** The adopted resource is in state and described by configuration, and a plan after adoption shows no changes.
- [ ] **DoD-5** The stop-managing resource still exists in AWS afterwards and Terraform no longer tracks it.
- [ ] **DoD-6** Each refactor is visible as a reviewable change in configuration (the diff is in your evidence).
- [ ] **DoD-7** Your write-up lists every command you ran against state and what each one did.
- [ ] **DoD-8** Your note on legacy imperative commands says when you will meet them and what the declarative equivalent is.
- [ ] **DoD-9** You have caused an apply to stop part-way, captured the error and what state holds afterwards, and brought the configuration back to a clean plan without editing state by hand (output pasted).
- [ ] **DoD-10** Your write-up explains how to read a provider error, and what to do after a failed destroy.
- [ ] **DoD-11** No billable resource is left behind; only the M07 bucket remains.

## Best practices this stage demonstrates

- Refactoring blocks
- Plan review
- fmt and validate
