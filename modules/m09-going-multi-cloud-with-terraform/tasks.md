# M09 — Going Multi-Cloud with Terraform — Tasks

**Objective:** By the end of this stage, you can sign in to GCP and Azure with short-lived logins, make the project or subscription explicit, and prove each provider works with a read-only check — using your own identity output as the evidence, not the identity you expected. You can see that the core Terraform workflow carries over to GCP and Azure while provider setup does not.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M01) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] **TASK-M09-B01** Work on: Installing the CLIs and confirming access to the GCP and Azure sandboxes
- [ ] **TASK-M09-B02** Work on: GCP — Application Default Credentials sign-in, project selection, provider configuration
- [ ] **TASK-M09-B03** Work on: Azure — CLI sign-in, subscription selection, provider configuration
- [ ] **TASK-M09-B04** Work on: State management across clouds: `gcs` and `azurerm` backends
- [ ] **TASK-M09-B05** Work on: Where this course stops
- [ ] **TASK-M09-B06** Have ready: Two small Terraform configurations, one per cloud, each authenticating with a short-lived login and outputting the identity it runs as

## Verify

- [ ] **TASK-M09-V01** Confirm DoD-01: Both configurations pass formatting and validation checks, shown as pasted output. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M09-V02** Confirm DoD-02: Both configurations plan successfully, and the plan output includes an identity output for each cloud (output pasted), not the identity you expected. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M09-V03** Confirm DoD-03: Each configuration targets the intended GCP project or Azure subscription even when the active login points elsewhere (evidence shown), or your notes record why that was not possible. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M09-V04** Confirm DoD-04: No secrets or keys exist in the repository or on disk, and the scan you ran is in your evidence, not a statement that there are none. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M09-V05** Confirm DoD-05: Neither configuration creates a resource: the plan shows nothing to add. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M09-V06** Confirm DoD-06: Your notes close with a short next-steps note that names HCP Terraform and Sentinel and says in one line what each is for. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M09-V07** Confirm DoD-07: Your write-up takes a first-time learner to a working sign-in and a successful plan for GCP and for Azure unaided — verified by you following it end to end from a clean state. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] **TASK-M09-W01** Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] **TASK-M09-W02** Under “Why it's built this way (key decisions)”: One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] **TASK-M09-W03** Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] **TASK-M09-W04** Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] **TASK-M09-W05** Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] **TASK-M09-W06** Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] **TASK-M09-W07** Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] **TASK-M09-W08** Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] **TASK-M09-W09** Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] **TASK-M09-W10** Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
