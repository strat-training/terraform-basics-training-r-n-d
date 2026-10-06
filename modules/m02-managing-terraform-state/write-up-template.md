# M02 — Managing Terraform State — Write-up

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

One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.

- What you would check before trusting a state file you did not create, and what goes wrong when state is edited by hand.
- What can leak a secret into state and how you would demonstrate that safely without a real credential, and why the course treats a state file as sensitive even when the configuration contains no secrets.
- What a remote backend gives a team that local state cannot.
- How you solved the problem of creating the thing that stores your state and what you would do differently on a team, who and what needs access to the bucket and how narrow you can make that without breaking Terraform, and why the bucket is kept when everything else is destroyed and what risk that carries.
- How you know that nothing was recreated.
- What locking prevents, and what it does not.
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

- Understanding and inspecting local state (read-only)
- Secrets and state
- Why state moves to a remote backend
- Bootstrapping and securing the state bucket
- Configuring the backend and migrating existing local state into it
- Native state locking

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-01: Your notes show where your local state lives and what it records for one of your own resources, captured read-only from your own state (output pasted), not described from the documentation.
- DoD-02: Your notes show what state holds for a sensitive value, captured from your own state without exposing a real credential, not a claim taken from the documentation.
- DoD-03: A state object for your configuration exists in the bucket (listing pasted), and a plan after migrating local state shows no changes — nothing was recreated.
- DoD-04: Versioning is enabled on the bucket, encryption at rest is enabled and public access is fully blocked, shown from the cloud side, not from your configuration.
- DoD-05: The backend configuration enables native locking and no DynamoDB table is used or created, and with one operation in progress a second is refused with a lock error (the error output pasted), not described from what locking should do.
- DoD-06: The bucket is retained and everything else is destroyed, confirmed from the cloud side, and no static keys, state files or state file contents are committed to version control, shown by the ignore rule and a clean commit history.
- DoD-07: Your write-up takes a first-time learner from local state to a protected remote backend, with locking demonstrated, unaided — verified by you following it end to end from a clean state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
