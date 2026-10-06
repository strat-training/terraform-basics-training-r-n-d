# M06 — Managing Terraform State — Tasks

**Objective:** Understand what Terraform's state is, why it must be treated as sensitive, and how the real world drifts away from it — and show that you can detect drift and decide how to reconcile it without ever editing state by hand.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M03) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Understanding and inspecting Terraform state (read-only)
- [ ] Work on: Secrets and state — what lands in state and who can read it and keeping a secret out of state
- [ ] Work on: Infrastructure drift: detection, causes, and reconciliation
- [ ] Work on: The golden rule: why state is never edited by hand
- [ ] Have ready: A small configuration taken through an out-of-band change and back to a clean plan
- [ ] Have ready: your written answers to the stage's questions

## Verify

- [ ] Confirm DoD-1: Your training module shows the final plan with no changes (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: Your training module shows the out-of-band change detected by Terraform, not just noticed by you, with the plan output from before reconciliation captured. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Your training module records which side you let win (code or real world) and why. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: Your training module shows what state holds for a sensitive value, captured without exposing a real credential. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: Your training module shows a secret reaching a resource through a write-only argument and absent from state (output pasted, without exposing a real credential). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: Your trainer confirms the written answers in your training module are correct on review. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: Your training module shows state files excluded from version control (the ignore rule and a clean commit history show it). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: A learner following your training module ends with everything created destroyed, confirmed from the cloud side. Capture the evidence under “Checkpoint evidence”.

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
