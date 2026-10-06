# M06 — Managing Resources with Network Provisioning — Tasks

**Objective:** By the end of this stage, you can explain how Terraform works out what depends on what, create several similar resources without writing each one out by hand, and read information that already exists instead of hard-coding it — using the small AWS network you built as the evidence, not a diagram.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M03) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Resource references and the dependency graph Terraform builds from them
- [ ] Work on: Implicit versus explicit dependencies
- [ ] Work on: Repeating a resource
- [ ] Work on: Data sources
- [ ] Work on: A VPC, subnets in more than one availability zone, and the routing a public tier needs
- [ ] Have ready: A small AWS network configuration — one VPC with public and private subnets across more than one availability zone and the routing the public tier needs — with no NAT gateway

## Verify

- [ ] Confirm DoD-01: Formatting and validation pass with no errors, and the plan contains the VPC, subnets in at least two availability zones, and the routing for the public tier, with resource addresses taken from the plan output or its JSON form, not from your code. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-02: Subnets in more than one availability zone are created by repeating one resource block, not by writing each one out (a reviewer reads the configuration). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-03: At least one value your configuration needs about the account or region is read with a data source, not hard-coded (a reviewer reads the configuration). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-04: No NAT gateway appears in the plan or in state, shown from real output, not from the absence of one in your code. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-05: Your note names the implicit dependencies in your own configuration and where each one comes from, not a general definition of an implicit dependency. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-06: Everything is destroyed, confirmed from the cloud side, not only from Terraform's output. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-07: Your write-up takes a first-time learner to the same small AWS network unaided — verified by you following it end to end from a clean state. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] Under “Why it's built this way (key decisions)”: One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
