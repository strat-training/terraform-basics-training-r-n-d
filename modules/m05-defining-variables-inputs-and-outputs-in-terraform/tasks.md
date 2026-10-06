# M05 — Defining Variables, Inputs and Outputs in Terraform — Tasks

**Objective:** Turn a hard-wired configuration into a parameterised one with typed, described and validated inputs. Use local values to derive a value once. Work out by experiment which source of a variable's value wins when several are present. Handle sensitive inputs and outputs so that secrets reach Terraform and leave it without being committed or casually displayed.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M04 (you may reuse that work)) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Input variables — type, description and default
- [ ] Work on: Validation rules enforced at plan time
- [ ] Work on: Supplying values — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables
- [ ] Work on: Variable value precedence — which source wins when several supply the same variable, found by hands-on experiment
- [ ] Work on: Keeping environment-specific values out of the main configuration
- [ ] Work on: Local values — naming and reusing derived values within a configuration
- [ ] Work on: Sensitive input variables — marking them and getting their values into Terraform without committing them
- [ ] Work on: Output values — what to expose and how to mark an output sensitive
- [ ] Work on: What marking a value sensitive does and does not protect
- [ ] Have ready: A parameterised AWS configuration in which region, network address ranges and the resource name prefix are inputs
- [ ] Have ready: two different sets of values that both plan cleanly
- [ ] Have ready: a record of your precedence experiments and a configuration that handles a sensitive input and a sensitive output

## Verify

- [ ] Confirm DoD-1: Your write-up shows formatting and validation passing with no errors and both sets of values producing clean, error-free plans, with the output for each, not one run reported as covering both. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: Your write-up shows an invalid network address range rejected at plan time with your own validation message and nothing planned for creation (output pasted), not a rule you wrote but never triggered. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Your main configuration file contains no hard-coded region, network address range or name prefix, and every variable has a type and a description. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: At least one value in your configuration is derived once as a local value and used in more than one place (a reviewer reads the configuration), not repeated as the same expression. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: Your precedence record has one isolated experiment for each source — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables — each showing the single source supplying the variable and the value Terraform used (plan output per experiment), followed by a deliberate combined run that states the order in which sources win, backed by that run's output rather than by documentation. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: At least one sensitive input is marked sensitive, its value reaches Terraform without appearing in any committed file, and the plan output does not display it; at least one output is marked sensitive, and your write-up shows what is displayed for it (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: Your write-up states what marking a value sensitive does and does not protect, backed by what you observed with placeholder values, not by what the documentation says. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: A learner following your training module ends with everything created destroyed, confirmed from the cloud side, not only from Terraform's output. Capture the evidence under “Checkpoint evidence”.

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
