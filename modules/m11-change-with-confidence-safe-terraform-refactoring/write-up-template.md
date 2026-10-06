# M11 — Change with Confidence: Safe Terraform Refactoring — Write-up

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

- How can you tell, before applying, that a refactor will not touch real infrastructure?
- What did the generated configuration get wrong or leave out, and how did you decide what to keep?
- When a resource stops being managed, what is responsible for it afterwards, and how do you avoid orphaning cost?
- Why does the course prefer changes that appear in a plan over commands that edit state, and when might you still see those commands?
- How do you recover when an apply stops part-way, and what do you check before you run it again?
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

- Refactoring principles: renaming and removing resources without destruction
- Adopting existing, unmanaged resources into Terraform
- Verifying refactors mechanically: reading plans as JSON with `jq`
- Emergency recovery: handling partial applies and failed destroys
- Advanced troubleshooting: targeted operations and legacy state commands

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: After each of the three refactors, a saved plan shows zero destroys and zero replacements (three plan summaries pasted), and at least one of the three plan checks reads the saved plan's JSON form with `jq` and reports the action on every resource (output pasted).
- DoD-2: The renamed resource keeps its real-world identity (its cloud-side identifier is unchanged); the adopted resource is in state and described by configuration, and a plan after adoption shows no changes; the stop-managing resource still exists in AWS afterwards and Terraform no longer tracks it.
- DoD-3: Each refactor is visible as a reviewable change in configuration (the diff is in your evidence), and your write-up lists every command you ran against state and what each one did.
- DoD-4: Your note on legacy imperative commands says when you will meet them and what the declarative equivalent is.
- DoD-5: You have caused an apply to stop part-way, captured the error and what state holds afterwards, and brought the configuration back to a clean plan without editing state by hand (output pasted), and your write-up explains what to do after a failed destroy.
- DoD-6: No billable resource is left behind; only the M07 bucket remains.
- DoD-7: Your write-up takes a first-time learner to a rename, an adoption and a stop-managing with no destroys unaided — verified by you following it end to end from a clean state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
