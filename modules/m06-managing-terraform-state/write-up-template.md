# M06 — Managing Terraform State — Write-up

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

- What can leak a secret into state, and how would you demonstrate that safely, without using a real credential?
- When Terraform reports drift, who decides whether the code or the real world is right, and on what basis?
- What would you check before trusting a state file you did not create?
- Why does the course treat a state file as sensitive even when the configuration contains no secrets?
- When can a secret be kept out of state altogether, and what do you still have to protect when it is?
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

- What state records and what Terraform uses it for
- Secrets and state — what lands in state and who can read it
- Keeping a secret out of state — ephemeral values and write-only arguments, where the provider supports them
- Inspecting state, read-only
- Drift — how it arises and how Terraform detects it
- Reconciling drift — deciding whether the code or the real world wins
- Why state is never edited by hand

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: The final plan shows no changes (output pasted).
- DoD-2: The out-of-band change was detected by Terraform, not just noticed by you — the plan output from before reconciliation is captured.
- DoD-3: The write-up records which side you let win (code or real world) and why.
- DoD-4: Your evidence shows what state holds for a sensitive value, captured without exposing a real credential.
- DoD-5: A secret reaches a resource through a write-only argument, and your evidence shows it is absent from state (output pasted, without exposing a real credential).
- DoD-6: Your trainer confirms your written answers are correct on review.
- DoD-7: State files are excluded from version control (the ignore rule and a clean commit history show it).
- DoD-8: Everything created is destroyed, confirmed from the cloud side.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
