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

1. Refactoring principles: renaming and removing resources without destruction
2. Adopting existing, unmanaged resources into Terraform
3. Verifying refactors mechanically: reading plans as JSON with `jq`
4. Emergency recovery: handling partial applies and failed destroys
5. Advanced troubleshooting: targeted operations and legacy state commands

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

Your training module — the build plus the write-up that teaches it — is done when each of these is true.

- [ ] **DoD-1** After each of the three refactors, your write-up shows a saved plan with zero destroys and zero replacements (three plan summaries pasted), and at least one check reads the saved plan's JSON form with `jq` and reports the action on every resource (output pasted), not a plan read by eye.
- [ ] **DoD-2** Your write-up shows the renamed resource keeping its real-world identity: its cloud-side identifier is unchanged.
- [ ] **DoD-3** Your write-up shows the adopted resource in state and described by configuration, and a plan after adoption with no changes.
- [ ] **DoD-4** Your write-up shows the stop-managing resource still existing in AWS afterwards and no longer tracked by Terraform.
- [ ] **DoD-5** Each refactor is a reviewable change in configuration (the diff is in your evidence), and your write-up lists every command you ran against state and what each one did, not only the ones that changed something.
- [ ] **DoD-6** Your note on legacy imperative commands says when you will meet them and what the declarative equivalent is.
- [ ] **DoD-7** Your write-up shows an apply you caused to stop part-way, the error and what state holds afterwards, and the configuration brought back to a clean plan without editing state by hand (output pasted), and explains what to do after a failed destroy.
- [ ] **DoD-8** A learner following your training module ends with no billable resource left behind; only the M07 bucket remains.

## Best practices this stage demonstrates

- Refactoring blocks
- Plan review
- fmt and validate
