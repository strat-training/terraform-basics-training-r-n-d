# M04 — Defining Variables, Inputs and Outputs in Terraform — Tasks

**Objective:** By the end of this stage, you can turn a hard-wired configuration into a parameterised one, work out by experiment which source of a variable's value wins, and handle a sensitive input and a sensitive output so that secrets reach Terraform and leave it without being committed or casually displayed — using your own plans as the evidence, not the documentation's description. You use local values to derive a value once.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M03 (you may reuse that work)) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] **TASK-M04-B01** Work on: Input variables
- [ ] **TASK-M04-B02** Work on: Validation rules enforced at plan time
- [ ] **TASK-M04-B03** Work on: Supplying values
- [ ] **TASK-M04-B04** Work on: Variable value precedence
- [ ] **TASK-M04-B05** Work on: Keeping environment-specific values out of the main configuration
- [ ] **TASK-M04-B06** Work on: Local values
- [ ] **TASK-M04-B07** Work on: Sensitive input variables
- [ ] **TASK-M04-B08** Work on: Output values
- [ ] **TASK-M04-B09** Work on: What marking a value sensitive does and does not protect
- [ ] **TASK-M04-B10** Have ready: A parameterised AWS configuration in which region, network address ranges and the resource name prefix are inputs
- [ ] **TASK-M04-B11** Have ready: two different sets of values that both plan cleanly
- [ ] **TASK-M04-B12** Have ready: a record of your precedence experiments and a configuration that handles a sensitive input and a sensitive output

## Verify

- [ ] **TASK-M04-V01** Confirm DoD-01: Formatting and validation pass with no errors, and both sets of values produce clean, error-free plans (output for each), not one run reported as covering both. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M04-V02** Confirm DoD-02: Every variable has a type and a description, and an invalid network address range is rejected at plan time with your validation message and nothing planned for creation (output pasted), not a rule you wrote but never triggered. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M04-V03** Confirm DoD-03: The main configuration file contains no hard-coded region, network address range or name prefix, and at least one value is derived once as a local value and used in more than one place (a reviewer reads the configuration). Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M04-V04** Confirm DoD-04: Your precedence record has one isolated experiment for each source — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables — each showing the single source supplying the variable and the value Terraform used (plan output per experiment); after them you combined sources deliberately, and your record states the order in which sources win, backed by your combined-run evidence, not by the documentation. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M04-V05** Confirm DoD-05: At least one sensitive input is marked sensitive, its value reaches Terraform without appearing in any committed file, and the plan output does not display it; at least one output is marked sensitive, and your evidence shows what is displayed for it. Your notes state what marking a value sensitive does and does not protect, backed by what you observed with placeholder values only. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M04-V06** Confirm DoD-06: Everything you created is destroyed, confirmed from the cloud side, not only from Terraform's output. Capture the evidence under “Checkpoint evidence”.
- [ ] **TASK-M04-V07** Confirm DoD-07: Your write-up takes a first-time learner to a parameterised configuration that plans cleanly with two sets of values unaided — verified by you following it end to end from a clean state. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] **TASK-M04-W01** Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] **TASK-M04-W02** Under “Why it's built this way (key decisions)”: One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] **TASK-M04-W03** Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] **TASK-M04-W04** Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] **TASK-M04-W05** Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] **TASK-M04-W06** Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] **TASK-M04-W07** Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] **TASK-M04-W08** Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] **TASK-M04-W09** Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] **TASK-M04-W10** Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
