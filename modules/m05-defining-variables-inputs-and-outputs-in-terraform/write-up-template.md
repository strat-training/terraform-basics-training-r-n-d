# M05 — Defining Variables, Inputs and Outputs in Terraform — Write-up

> This write-up is meant to become part of the content library: write it so the next cohort could learn from it, not just as a record of what you did. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Write each section as you build, not after it works. Never paste credentials, tokens or key material anywhere in this file.

| | |
| --- | --- |
| Trainee | |
| Status | Draft <!-- Draft → In review → Revising → Accepted --> |
| Build location | <!-- your GitLab repository and branch or merge request holding your Terraform code --> |
| Hours spent | <!-- an honest total --> |

## What I built

Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.

## Why it's built this way (key decisions)

One entry per open design question in the brief, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.

- Which rules deserve plan-time validation, and which are better left for AWS to reject at apply time?
- Which inputs should have defaults and which should be required — what is the risk of each?
- Where does a typed variable stop being enough?
- If several sources can supply the same variable, why might a team still allow only one source per variable, and how would you enforce that?
- How should a sensitive value reach Terraform, and what are the risks of each way you tried?
- What does marking a value sensitive hide, and where can it still be seen?
- Which outputs are worth exposing at all, and who is the audience for each?
- When is a local value clearer than repeating an expression, and when does it hide too much?
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.

## Concepts worth explaining

Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.

- Input variables — type, description and default
- Validation rules enforced at plan time
- Supplying values — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables
- Variable value precedence — which source wins when several supply the same variable, found by hands-on experiment
- Keeping environment-specific values out of the main configuration
- Local values — naming and reusing derived values within a configuration
- Sensitive input variables — marking them and getting their values into Terraform without committing them
- Output values — what to expose and how to mark an output sensitive
- What marking a value sensitive does and does not protect

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: Formatting and validation checks pass with no errors, and both sets of values produce clean, error-free plans (output for each).
- DoD-2: Every variable has a type and a description, and an invalid network address range is rejected at plan time with your validation message and nothing is planned for creation (output pasted).
- DoD-3: The main configuration file contains no hard-coded region, network address range or name prefix, and at least one value is derived once as a local value and used in more than one place (a reviewer reads the configuration).
- DoD-4: Your precedence record has one isolated experiment for each source — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables — and each shows the single source supplying the variable and the value Terraform used (plan output per experiment); after them you combined sources deliberately, and your record states the order in which sources win, supported by your combined-run evidence.
- DoD-5: At least one sensitive input is marked sensitive, its value reaches Terraform without appearing in any committed file, and the plan output does not display it; at least one output is marked sensitive, and your evidence shows what is displayed for it. Your write-up states what marking a value sensitive does and does not protect, supported by what you observed using placeholder values only.
- DoD-6: Everything created is destroyed, confirmed from the cloud side.
- DoD-7: Your write-up takes a first-time learner to a parameterised configuration that plans cleanly with two sets of values unaided — verified by you following it end to end from a clean state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
