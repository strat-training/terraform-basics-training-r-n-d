# M05 — Terraform for Multi-Environment Deployments — Tasks

**Objective:** By the end of this stage, you can deploy dev and prod from one configuration with separate state, named and tagged so consistently that anyone can tell which environment a resource belongs to at a glance — using your own two environments as the evidence, not a diagram. You can say when you would use workspaces or a directory per environment instead.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M02, M04) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] **TASK-M05-B01** Work on: One configuration, many environments
- [ ] **TASK-M05-B02** Work on: Per-environment input values
- [ ] **TASK-M05-B03** Work on: Per-environment backend settings and separate state keys in the shared bucket
- [ ] **TASK-M05-B04** Work on: Managing blast radius through state separation
- [ ] **TASK-M05-B05** Work on: Enforcing naming conventions and default provider tags
- [ ] **TASK-M05-B06** Work on: Switching between environments safely
- [ ] **TASK-M05-B07** Work on: Alternative isolation methods: directories vs workspaces (theory)
- [ ] **TASK-M05-B08** Have ready: One configuration deployed as both dev and prod with separate state
- [ ] **TASK-M05-B09** Have ready: a note comparing three ways to separate environments

## Verify

- [ ] **TASK-M05-V01** Confirm DoD-01: Two state objects exist in the bucket under different keys (listing pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M05-V02** Confirm DoD-02: Both environments produce clean plans, with the output for each, not one plan reported as covering both. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M05-V03** Confirm DoD-03: Environment-specific inputs differ between your two environments and live outside the main configuration files. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M05-V04** Confirm DoD-04: Every resource follows the naming convention and carries the required tags, shown from the plan, the state or the cloud side, not from your code. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M05-V05** Confirm DoD-05: Your comparison note covers a directory per environment, workspaces and the per-environment files you used, and says when each fits. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M05-V06** Confirm DoD-06: Both environments are destroyed and the bucket is retained, confirmed from the cloud side. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M05-V07** Confirm DoD-07: Your write-up takes a first-time learner to one configuration deployed as dev and prod with separate state unaided — verified by you following it end to end from a clean state. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] **TASK-M05-W01** Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] **TASK-M05-W02** Under “Why it's built this way (key decisions)”: One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] **TASK-M05-W03** Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] **TASK-M05-W04** Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] **TASK-M05-W05** Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] **TASK-M05-W06** Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] **TASK-M05-W07** Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] **TASK-M05-W08** Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] **TASK-M05-W09** Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] **TASK-M05-W10** Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
