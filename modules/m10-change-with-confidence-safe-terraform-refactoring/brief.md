# M10 — Change with Confidence: Safe Terraform Refactoring Brief

**Stage:** 10 of 11 · **Builds on:** M03, M04, M09 · **Feeds into:** the capstone

## Objective

By the end of this stage, you can rename, adopt and stop managing resources without destroying anything, by changing configuration rather than editing state — using a plan for each change as the evidence, not confidence that nothing real was touched. You verify every change with a plan that shows no destroys and no replacements.

## Scope

You refactor your own configuration, not a worked example. Find out, and write down in your own words:

- **Refactoring principles: renaming and removing resources without destruction** — changing configuration, not state, so that nothing real is destroyed or replaced. Research: how you can tell, before applying, that a refactor will not touch real infrastructure, and what is responsible for a resource that stops being managed and how you avoid orphaning cost.
- **Adopting existing, unmanaged resources into Terraform** — bringing something that already exists under Terraform's management. Research: what the generated configuration got wrong or left out, and how you decided what to keep.
- **Verifying refactors mechanically: reading plans as JSON with `jq`** — checking the action on every resource in a saved plan rather than by eye. Research: what the action on every resource looks like in a saved plan's JSON form.
- **Emergency recovery: handling partial applies and failed destroys** — what to do when an apply or destroy stops part-way. Research: how you recover when an apply stops part-way, and what you check before you run it again.
- **Advanced troubleshooting: targeted operations and legacy state commands** — what these are, and when you would meet them. Research: why the course prefers changes that appear in a plan over commands that edit state, and when you might still see those commands.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- Every refactor is a declarative change in configuration.
- State subcommands are for inspection only and are not how any refactor here is performed, and editing state by hand is out of scope.
- State lives in the M04 bucket under its own key, and Terraform is 1.11 or later.
- Check the refactoring features you rely on against the release notes of the pinned version before you write them up.
- The resource you adopt must genuinely exist outside Terraform's management beforehand, and adopting it involves generated configuration that needs manual tidying, which is part of the work.
- Look up what each resource in your plan bills before you apply, and destroy everything except the M04 bucket at the end.

## Deliverable

**Three refactors applied to a small configuration — a rename, an adoption and a stop-managing — each verified by a plan with no destroys and no replacements**, plus a short note on legacy imperative commands.

## Lab

**Goal.** Rename, adopt and stop managing resources without destroying anything.

**You do, in the sandbox.** Rename a resource, adopt one that already exists outside Terraform, stop managing another, and check each change with a saved plan; then cause an apply to stop part-way and bring the configuration back to a clean plan without editing state by hand.

**You build and capture.** The three refactors are your deliverable. Capture the plan summaries, the check that reads a saved plan's JSON, the identity of the renamed resource, the error and what state holds afterwards, and the recovery.

**Clean-up.** No billable resource is left behind; only the M04 bucket remains.

## Definition of done

- DoD-01: After each of the three refactors, a saved plan shows zero destroys and zero replacements (three plan summaries pasted), and at least one of the three checks reads the saved plan's JSON form with `jq` and reports the action on every resource (output pasted), not a plan read by eye.
- DoD-02: The renamed resource keeps its real-world identity (its cloud-side identifier is unchanged); the adopted resource is in state and described by configuration, and a plan after adoption shows no changes; the stop-managing resource still exists in AWS afterwards and Terraform no longer tracks it.
- DoD-03: Each refactor is a reviewable change in configuration (the diff is in your evidence), and your notes list every command you ran against state and what each one did, not only the ones that changed something.
- DoD-04: Your note on legacy imperative commands says when you will meet them and what the declarative equivalent is.
- DoD-05: You caused an apply to stop part-way, captured the error and what state holds afterwards, and brought the configuration back to a clean plan without editing state by hand (output pasted); your notes also say what to do after a failed destroy.
- DoD-06: No billable resource is left behind, and only the M04 bucket remains.
- DoD-07: Your write-up takes a first-time learner to a rename, an adoption and a stop-managing with no destroys unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- Refactoring blocks
- Plan review
- fmt and validate

## Still open / ask your trainer

- Which existing resource you will adopt, and where it comes from.
- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
