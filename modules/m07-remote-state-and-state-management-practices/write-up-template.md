# M07 — Remote State and State Management Practices — Write-up

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

- Who and what needs access to the state bucket, and how narrow can you make that without breaking Terraform?
- How did you solve the problem of creating the thing that stores your state, and what would you do differently on a team?
- What happens if a lock is left behind, and what must you check before overriding one?
- Why is this bucket kept when everything else is destroyed, and what risk does that carry?
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

- Why state moves to a remote backend, and what locking prevents
- Bootstrapping, securing, and managing the lifecycle of the state bucket
- Configuring the backend and migrating existing local state into it
- Proving that native locking works and recovering abandoned locks

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: Your write-up shows a state object for your own configuration in the bucket (listing pasted).
- DoD-2: Your write-up shows versioning and encryption at rest enabled and public access fully blocked on the bucket, shown from the cloud side, not from your configuration.
- DoD-3: Your write-up shows a backend configuration that enables native locking, with no DynamoDB table used or created.
- DoD-4: Your write-up shows a plan after migrating local state with no changes, so nothing was recreated.
- DoD-5: Your write-up shows a second operation refused with a lock error while one is in progress (the error output pasted), not a description of what locking should do.
- DoD-6: Your write-up shows a lock you left behind deliberately and your recovery without losing or corrupting state (the error and the recovery output pasted).
- DoD-7: A learner following your training module ends with the bucket retained and everything else destroyed, confirmed from the cloud side, not only from Terraform's output.
- DoD-8: No static keys and no state file contents are committed to version control, shown by your commit history, not assumed.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
