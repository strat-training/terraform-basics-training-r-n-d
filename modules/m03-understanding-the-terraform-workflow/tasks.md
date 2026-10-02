# M03 — Understanding the Terraform Workflow — Tasks

**Objective:** Understand why Terraform describes the desired state of infrastructure instead of scripting steps, then run the core workflow end to end on a real resource and make reading the plan before applying a habit — to the point where you can predict, from a plan, whether a change updates a resource in place or replaces it.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M02) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Declarative versus imperative infrastructure — what it means that Terraform describes desired state
- [ ] Work on: Anatomy of a resource — type, name, arguments and attributes
- [ ] Work on: The core workflow — initialise, plan, apply, destroy
- [ ] Work on: What a plan shows — reading the action for each resource
- [ ] Work on: In-place updates versus replacement
- [ ] Work on: What causes a replacement
- [ ] Work on: Plan review as a habit — what to check before approving
- [ ] Work on: Destroying what you created
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: How does describing the desired state differ from scripting the steps, and what does that change about running the same configuration twice?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: How can you tell from the plan alone that a change will destroy something, before you apply it?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: For your chosen resource, which changes are made in place and which force replacement — how did you establish that, and how sure are you?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: What would you do if a plan showed a destroy you did not expect?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: What does a replacement cost when the resource holds data or other resources depend on it?
- [ ] Have ready: A configuration managing one small AWS resource, taken through create, in-place change, forced replacement and destroy
- [ ] Have ready: a written plan-review note

## Verify

- [ ] Confirm DoD-1: Formatting and validation checks pass with no errors. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: You ran the same apply twice without changing the configuration; both outputs are pasted, and the write-up explains the difference between them in terms of desired state. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Your write-up identifies the type, name, arguments and attributes of your resource, and shows an attribute whose value you did not set. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: You made at least one in-place change and at least one forced replacement; the plan output for each was captured before it was applied. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: Your plan-review note classifies every change you made as in-place or replacement, and your trainer confirms each classification on review. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: For each classification the note explains the cause in terms of the resource itself, not just the plan's symbols. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: After destroy the resource is gone — confirmed from the cloud side, not only from Terraform's output. Capture the evidence under “Checkpoint evidence”.

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
