# M05 — Defining Variables, Inputs and Outputs in Terraform — write-up

> **How to use this file.** Copy it to `write-up.md` in this folder and fill in the copy; leave this template blank for the next cohort. Write each section **while you build**, in the same sitting as the work — not after it works. The brief is in [brief.md](brief.md); do not edit it. Never paste credentials, tokens or key material anywhere in this file.

| | |
| --- | --- |
| Trainee | |
| Status | Draft <!-- Draft → In review → Revising → Accepted --> |
| Build location | <!-- repository and branch or merge request holding your Terraform code --> |
| Started / finished | |
| Hours spent | <!-- an honest total — the trainer uses it to set time boxes --> |

## 1. What I built

<!-- Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome. A reader should know what exists before they read how you got there. -->

## 2. Key decisions and tradeoffs

<!-- One entry per open design question from the brief, then any further decision of your own worth recording. Say what you considered, what you chose, why, and what you gave up. "The docs said so" is not a reason. -->

### Q1. Which rules deserve plan-time validation, and which are better left for AWS to reject at apply time?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. Which inputs should have defaults and which should be required — what is the risk of each?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. Where does a typed variable stop being enough?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. What makes a validation error message useful to someone who did not write the rule?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q5. If several sources can supply the same variable, why might a team still allow only one source per variable, and how would you enforce that?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q6. How should a sensitive value reach Terraform, and what are the risks of each way you tried?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q7. What does marking a value sensitive hide, and where can it still be seen?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q8. Which outputs are worth exposing at all, and who is the audience for each?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q9. When is a local value clearer than repeating an expression, and when does it hide too much?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:


### Additional decisions

<!-- Add as many as you need, in the same shape. -->

## 3. How to build it

<!-- This section becomes the teaching content, so write it for a learner who has finished the previous stage and has not seen this one. They will follow it alone, with no trainer to ask. Include the commands and code they need, the reason for each step, what they should see afterwards, and where to stop and check before moving on. -->

### Before you start

<!-- What the learner needs in place: earlier stages, access, tools, versions. -->

### Steps

<!-- Numbered, in the order you would do them again. -->

### How you know it worked

<!-- What the learner can check to be sure, without asking you. -->

### Clean-up

<!-- Exactly what to destroy or retire, and how to confirm nothing is left. -->

## 4. Concepts in my own words

<!-- For each concept: explain it as you would to a colleague, in your own words — no pasted definitions. Give one example from your build and one thing it is commonly confused with. -->

### Input variables — type, description and default


### Validation rules enforced at plan time


### Supplying values — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables


### Variable value precedence — which source wins when several supply the same variable, found by hands-on experiment


### Keeping environment-specific values out of the main configuration


### Local values — naming and reusing derived values within a configuration


### Sensitive input variables — marking them and getting their values into Terraform without committing them


### Output values — what to expose and how to mark an output sensitive


### What marking a value sensitive does and does not protect


### Reading validation errors as feedback



## 5. What tripped me up

<!-- Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. -->

| What happened (symptom or error text) | What I assumed | What it actually was | How I found out and fixed it |
| --- | --- | --- | --- |
| | | | |

## 6. Checkpoint evidence

<!-- One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. Redact anything sensitive. A row with no evidence is not done. -->

| Item | Evidence | Reviewer |
| --- | --- | --- |
| **DoD-1** Formatting and validation checks pass with no errors. | | |
| **DoD-2** An invalid network address range is rejected at plan time with your validation message and nothing is planned for creation (output pasted). | | |
| **DoD-3** Both sets of values produce clean, error-free plans (output for each). | | |
| **DoD-4** The main configuration file contains no hard-coded region, network address range or name prefix. | | |
| **DoD-5** Every variable has a type and a description. | | |
| **DoD-6** At least one value is derived once as a local value and used in more than one place (a reviewer reads the configuration). | | |
| **DoD-7** Your precedence record has one isolated experiment for each source — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables — and each shows the single source supplying the variable and the value Terraform used (plan output per experiment). | | |
| **DoD-8** After the isolated experiments you combined sources deliberately, and your record states the order in which sources win, supported by your combined-run evidence. | | |
| **DoD-9** At least one sensitive input is marked sensitive, its value reaches Terraform without appearing in any committed file, and the plan output does not display it (output pasted). | | |
| **DoD-10** At least one output is marked sensitive, and your evidence shows what is displayed for it. | | |
| **DoD-11** Your write-up states what marking a value sensitive does and does not protect, supported by what you observed using placeholder values only. | | |
| **DoD-12** Everything created is destroyed, confirmed from the cloud side. | | |

## 7. Versions and sources

**Versions this was written for:** <!-- Terraform, each provider and each CLI, exact versions. -->

**Official documentation used:** <!-- Links, one per concept or step that relied on them. -->

## 8. Before I submit

- [ ] Every definition-of-done item has evidence in section 6
- [ ] I followed section 3 from a clean start and it worked as written
- [ ] Every concept in section 4 is in my own words
- [ ] Every open design question in section 2 has a reasoned answer, including what I gave up
- [ ] Section 5 records everything that cost me real time
- [ ] No credentials, tokens or key material appear anywhere in this file or my repository
- [ ] Status above is set to "In review"
