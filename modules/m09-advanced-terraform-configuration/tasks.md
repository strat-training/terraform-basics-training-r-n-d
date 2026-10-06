# M09 — Advanced Terraform Configuration — Tasks

**Objective:** Use Terraform's more advanced language features to describe infrastructure from data instead of by copy-paste: repeat resources and nested blocks from structured input, derive and reshape values, branch on conditions, look up what already exists, and control dependency and lifecycle behaviour.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M04, M05, M06) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Composing Values with Built-in Functions
- [ ] Work on: Making Configuration Conditional
- [ ] Work on: Reshaping Data with `for` and Splat Expressions
- [ ] Work on: Going Deeper with `for_each`
- [ ] Work on: Generating Nested Configuration with Dynamic Blocks
- [ ] Work on: Discovering Existing Infrastructure with Data Sources
- [ ] Work on: Controlling Dependencies and Resource Lifecycle
- [ ] Work on: Validating Infrastructure with Preconditions and Postconditions
- [ ] Have ready: A data-driven AWS configuration in which resources and nested blocks are generated from structured input instead of repeated by hand
- [ ] Have ready: derived values, a conditional, a data-source lookup, dependency and lifecycle controls, and checks on its own assumptions

## Verify

- [ ] Confirm DoD-1: Your training module shows formatting and validation checks passing with no errors. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: Your training module shows at least one resource repeated, and at least one resource with repeated nested blocks, generated from a structured input — a map, or a collection derived from one. It justifies the keys you chose, shows a plan with the expected number of nested blocks (plan excerpt), and shows adding an entry, removing an entry and changing a key, each with a captured plan and exactly what it would do to the real infrastructure. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Your training module shows derived values defined once and used in more than one place, with no expression duplicated across files (a reviewer reads the configuration). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: Your training module shows at least one conditional that changes what the configuration creates or sets, with the plan shown for both outcomes of the condition (two plan excerpts). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: Your training module shows a data source supplying a value the configuration uses, with no equivalent value hard-coded (a reviewer reads the configuration). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: Your training module justifies every explicit dependency in the configuration (or says why a reference was always enough) and every lifecycle setting you used, and shows each lifecycle setting's effect from a plan or a deliberate attempt that it affects (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: Your training module shows at least one precondition or postcondition in place that you deliberately triggered, with the failure message captured (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: A learner following your training module ends with everything destroyed except the M07 bucket, confirmed from the cloud side. Capture the evidence under “Checkpoint evidence”.

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
