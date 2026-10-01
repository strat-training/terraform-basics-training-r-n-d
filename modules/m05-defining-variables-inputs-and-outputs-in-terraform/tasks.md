# M05 — Defining Variables, Inputs and Outputs in Terraform — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M04 (you may reuse that work)) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: Input variables — type, description and default *(scope 1)*
- [ ] **B2** Work on: Validation rules enforced at plan time *(scope 2)*
- [ ] **B3** Work on: Supplying values — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables *(scope 3)*
- [ ] **B4** Work on: Variable value precedence — which source wins when several supply the same variable, found by hands-on experiment *(scope 4)*
- [ ] **B5** Work on: Keeping environment-specific values out of the main configuration *(scope 5)*
- [ ] **B6** Work on: Local values — naming and reusing derived values within a configuration *(scope 6)*
- [ ] **B7** Work on: Sensitive input variables — marking them and getting their values into Terraform without committing them *(scope 7)*
- [ ] **B8** Work on: Output values — what to expose and how to mark an output sensitive *(scope 8)*
- [ ] **B9** Work on: What marking a value sensitive does and does not protect *(scope 9)*
- [ ] **B10** Work on: Reading validation errors as feedback *(scope 10)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): Which rules deserve plan-time validation, and which are better left for AWS to reject at apply time? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): Which inputs should have defaults and which should be required — what is the risk of each? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): Where does a typed variable stop being enough? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): What makes a validation error message useful to someone who did not write the rule? *(question 4)*
- [ ] **D5** Answer, with reasons, in write-up section 2 (Q5): If several sources can supply the same variable, why might a team still allow only one source per variable, and how would you enforce that? *(question 5)*
- [ ] **D6** Answer, with reasons, in write-up section 2 (Q6): How should a sensitive value reach Terraform, and what are the risks of each way you tried? *(question 6)*
- [ ] **D7** Answer, with reasons, in write-up section 2 (Q7): What does marking a value sensitive hide, and where can it still be seen? *(question 7)*
- [ ] **D8** Answer, with reasons, in write-up section 2 (Q8): Which outputs are worth exposing at all, and who is the audience for each? *(question 8)*
- [ ] **D9** Answer, with reasons, in write-up section 2 (Q9): When is a local value clearer than repeating an expression, and when does it hide too much? *(question 9)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: A parameterised AWS configuration in which region, network address ranges and the resource name prefix are inputs *(deliverable)*
- [ ] **C2** Have ready: two different sets of values that both plan cleanly *(deliverable)*
- [ ] **C3** Have ready: a record of your precedence experiments and a configuration that handles a sensitive input and a sensitive output *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: Formatting and validation checks pass with no errors. *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: An invalid network address range is rejected at plan time with your validation message and nothing is planned for creation (output pasted). *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: Both sets of values produce clean, error-free plans (output for each). *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: The main configuration file contains no hard-coded region, network address range or name prefix. *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: Every variable has a type and a description. *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: At least one value is derived once as a local value and used in more than one place (a reviewer reads the configuration). *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: Your precedence record has one isolated experiment for each source — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables — and each shows the single source supplying the variable and the value Terraform used (plan output per experiment). *(DoD-7)*
- [ ] **V8** Capture evidence in write-up section 6 for DoD-8: After the isolated experiments you combined sources deliberately, and your record states the order in which sources win, supported by your combined-run evidence. *(DoD-8)*
- [ ] **V9** Capture evidence in write-up section 6 for DoD-9: At least one sensitive input is marked sensitive, its value reaches Terraform without appearing in any committed file, and the plan output does not display it (output pasted). *(DoD-9)*
- [ ] **V10** Capture evidence in write-up section 6 for DoD-10: At least one output is marked sensitive, and your evidence shows what is displayed for it. *(DoD-10)*
- [ ] **V11** Capture evidence in write-up section 6 for DoD-11: Your write-up states what marking a value sensitive does and does not protect, supported by what you observed using placeholder values only. *(DoD-11)*
- [ ] **V12** Capture evidence in write-up section 6 for DoD-12: Everything created is destroyed, confirmed from the cloud side. *(DoD-12)*

## 5. Write up — one task per write-up section

- [ ] **W1** Complete write-up section 1, “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome. *(write-up section 1)*
- [ ] **W2** Complete write-up section 2, “Key decisions and tradeoffs”: One entry per open design question from the brief, then any further decision of your own worth recording. Say what you considered, what you chose, why, and what you gave up. *(write-up section 2)*
- [ ] **W3** Complete write-up section 3, “How to build it”: This section becomes the teaching content, so write it for a learner who has finished the previous stage and has not seen this one. They will follow it alone, with no trainer to ask. *(write-up section 3)*
- [ ] **W4** Complete write-up section 4, “Concepts in my own words”: For each concept: explain it as you would to a colleague, in your own words — no pasted definitions. Give one example from your build and one thing it is commonly confused with. *(write-up section 4)*
- [ ] **W5** Complete write-up section 5, “What tripped me up”: Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. *(write-up section 5)*
- [ ] **W6** Complete write-up section 6, “Checkpoint evidence”: One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. *(write-up section 6)*
- [ ] **W7** Complete write-up section 7, “Versions and sources”. *(write-up section 7)*
- [ ] **W8** Complete write-up section 8, “Before I submit”. *(write-up section 8)*

## 6. Close out

- [ ] **F1** Self-review: go back through this list and the brief's definition of done. Every item is ticked, or you have written down why not and told the trainer. *(close out)*
- [ ] **F2** Set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review. *(close out)*
