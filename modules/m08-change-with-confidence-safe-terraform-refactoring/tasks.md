# M08 — Change with Confidence: Safe Terraform Refactoring — Tasks

**Objective:** By the end of this stage, you can rename, adopt and stop managing resources without destroying anything, by changing configuration rather than editing state — using a plan for each change as the evidence, not confidence that nothing real was touched. You verify every change with a plan that shows no destroys and no replacements.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M01, M02, M07) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] **TASK-M08-B01** Work on: Refactoring principles: renaming and removing resources without destruction
- [ ] **TASK-M08-B02** Work on: Adopting existing, unmanaged resources into Terraform
- [ ] **TASK-M08-B03** Work on: Verifying refactors mechanically: reading plans as JSON with `jq`
- [ ] **TASK-M08-B04** Work on: Emergency recovery: handling partial applies and failed destroys
- [ ] **TASK-M08-B05** Work on: Advanced troubleshooting: targeted operations and legacy state commands
- [ ] **TASK-M08-B06** Have ready: Three refactors applied to a small configuration — a rename, an adoption and a stop-managing — each verified by a plan with no destroys and no replacements
- [ ] **TASK-M08-B07** Have ready: a short note on legacy imperative commands

## Verify

- [ ] **TASK-M08-V01** Confirm DoD-01: After each of the three refactors, a saved plan shows zero destroys and zero replacements (three plan summaries pasted), and at least one of the three checks reads the saved plan's JSON form with `jq` and reports the action on every resource (output pasted), not a plan read by eye. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M08-V02** Confirm DoD-02: The renamed resource keeps its real-world identity (its cloud-side identifier is unchanged); the adopted resource is in state and described by configuration, and a plan after adoption shows no changes; the stop-managing resource still exists in AWS afterwards and Terraform no longer tracks it. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M08-V03** Confirm DoD-03: Each refactor is a reviewable change in configuration (the diff is in your evidence), and your notes list every command you ran against state and what each one did, not only the ones that changed something. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M08-V04** Confirm DoD-04: Your note on legacy imperative commands says when you will meet them and what the declarative equivalent is. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M08-V05** Confirm DoD-05: You caused an apply to stop part-way, captured the error and what state holds afterwards, and brought the configuration back to a clean plan without editing state by hand (output pasted); your notes also say what to do after a failed destroy. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M08-V06** Confirm DoD-06: No billable resource is left behind, and only the M02 bucket remains. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M08-V07** Confirm DoD-07: Your write-up takes a first-time learner to a rename, an adoption and a stop-managing with no destroys unaided — verified by you following it end to end from a clean state. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] **TASK-M08-W01** Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] **TASK-M08-W02** Under “Why it's built this way (key decisions)”: One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] **TASK-M08-W03** Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] **TASK-M08-W04** Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] **TASK-M08-W05** Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] **TASK-M08-W06** Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] **TASK-M08-W07** Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] **TASK-M08-W08** Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] **TASK-M08-W09** Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] **TASK-M08-W10** Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
