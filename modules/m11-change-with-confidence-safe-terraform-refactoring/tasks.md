# M11 — Change with Confidence: Safe Terraform Refactoring — Tasks

**Objective:** Rename, adopt and stop managing resources without destroying anything, by changing configuration rather than editing state — and verify every change with a plan that shows no destroys and no replacements.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M03, M06, M07, M10) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Why refactoring must never mean destroy-and-recreate
- [ ] Work on: Renaming or re-addressing a resource without replacing it
- [ ] Work on: Adopting an existing, unmanaged resource into Terraform
- [ ] Work on: Tidying generated configuration
- [ ] Work on: Ceasing to manage a resource without destroying it
- [ ] Work on: Verifying every refactor with a plan
- [ ] Work on: Reading a saved plan as JSON with `jq` — checking the action on every resource mechanically
- [ ] Work on: Targeted operations — an emergency tool, never routine
- [ ] Work on: Reading legacy guidance that relies on imperative state commands
- [ ] Work on: When an apply goes wrong — a partial apply, a failed destroy, and reading provider errors
- [ ] Have ready: Three refactors applied to a small configuration — a rename, an adoption and a stop-managing — each verified by a plan with no destroys and no replacements
- [ ] Have ready: a short note on legacy imperative commands

## Verify

- [ ] Confirm DoD-1: After each of the three refactors, a saved plan shows zero destroys and zero replacements (three plan summaries pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: At least one of the three plan checks reads the saved plan's JSON form with `jq` and reports the action on every resource (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: The renamed resource keeps its real-world identity (its cloud-side identifier is unchanged). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: The adopted resource is in state and described by configuration, and a plan after adoption shows no changes. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: The stop-managing resource still exists in AWS afterwards and Terraform no longer tracks it. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: Each refactor is visible as a reviewable change in configuration (the diff is in your evidence). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: Your write-up lists every command you ran against state and what each one did. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: Your note on legacy imperative commands says when you will meet them and what the declarative equivalent is. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-9: You have caused an apply to stop part-way, captured the error and what state holds afterwards, and brought the configuration back to a clean plan without editing state by hand (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-10: Your write-up explains how to read a provider error, and what to do after a failed destroy. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-11: No billable resource is left behind; only the M07 bucket remains. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] Under “Why it's built this way (key decisions)”: One entry per open design question in the brief, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
