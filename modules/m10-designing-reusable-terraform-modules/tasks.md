# M10 — Designing Reusable Terraform Modules — Tasks

**Objective:** Package part of a configuration as a reusable Terraform module with a standard structure and a deliberate, documented interface. Call it more than once, comment it so the next person can maintain it, and explain what a module boundary does to inputs, outputs, resource addresses and blast radius — including when a module is the wrong answer.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M05, M06, M07, M08, M09) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: What a module is — the root module, child modules, and what a module call does
- [ ] Work on: Deciding what belongs in a module, and what does not
- [ ] Work on: A module's interface — inputs, outputs, and what it keeps private
- [ ] Work on: Standard module file structure
- [ ] Work on: Naming conventions for a module's inputs, outputs and resources
- [ ] Work on: Comments and documentation — comment syntax, what deserves a comment, and descriptions on inputs and outputs
- [ ] Work on: Calling the same module more than once with different inputs
- [ ] Work on: How modules change resource addresses in a plan and in state
- [ ] Work on: Module sources and versions — local paths versus registry or Git sources, and pinning
- [ ] Work on: Consuming a published module — reading someone else's module before trusting it
- [ ] Work on: What a module may assume about provider configuration
- [ ] Work on: Module anti-patterns
- [ ] Have ready: A reusable AWS module with a standard file structure and a documented, commented interface, and a root configuration that calls it at least twice with different inputs, deployed with the M08 environment arrangement
- [ ] Have ready: a decision note on what you put in the module and what you left out

## Verify

- [ ] Confirm DoD-1: Formatting and validation checks pass for both the module and the root configuration. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: The module has a documented interface: every input has a type and a description, inputs that can take a bad value are validated, and every output has a description (a reviewer reads the module). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: The module follows the standard module layout; a reviewer can find what they need from file names alone. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: The names of the module's inputs, outputs and internal resources follow one convention, which your write-up states. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: Your write-up states which comment syntax you chose, what you chose to comment, and why (a reviewer reads the module). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: The module is called at least twice with different inputs and both calls produce clean plans (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: Your write-up states what the module assumes about provider configuration and where it takes its region, account and environment name from (a reviewer reads the module). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: Resource addresses for the separate calls show distinct module paths (state listing pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-9: Resources created through the module still follow M08's naming convention and carry the required tags (shown from the plan, state or cloud side). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-10: The write-up contains a review of one published module — its source, pinned version, inputs and outputs, and what you checked before trusting it. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-11: The decision note says what you put in the module, what you left out, and a case where you would not write a module. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-12: Everything is destroyed except the M07 bucket, confirmed from the cloud side. Capture the evidence under “Checkpoint evidence”.

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
