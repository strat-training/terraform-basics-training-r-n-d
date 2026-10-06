# M05 — Terraform for Multi-Environment Deployments — Write-up

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

- What makes it easy to apply one environment's values to the other's state, and what you will do to make that harder.
- Which inputs are the same in both environments and which must differ.
- How you would notice if both environments ended up in the same state.
- What separate state does and does not protect.
- Which tags a clean-up or cost report would need beyond `Environment`, and why.
- How you would notice that you are in the wrong environment.
- When workspaces would be the right tool and what you give up by not using them here, when a directory per environment would be the right tool and what you give up by not using it, and in what ways keeping both environments in one account misrepresents real practice.
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

- One configuration, many environments
- Per-environment input values
- Per-environment backend settings and separate state keys in the shared bucket
- Managing blast radius through state separation
- Enforcing naming conventions and default provider tags
- Switching between environments safely
- Alternative isolation methods: directories vs workspaces (theory)

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-01: Two state objects exist in the bucket under different keys (listing pasted).
- DoD-02: Both environments produce clean plans, with the output for each, not one plan reported as covering both.
- DoD-03: Environment-specific inputs differ between your two environments and live outside the main configuration files.
- DoD-04: Every resource follows the naming convention and carries the required tags, shown from the plan, the state or the cloud side, not from your code.
- DoD-05: Your comparison note covers a directory per environment, workspaces and the per-environment files you used, and says when each fits.
- DoD-06: Both environments are destroyed and the bucket is retained, confirmed from the cloud side.
- DoD-07: Your write-up takes a first-time learner to one configuration deployed as dev and prod with separate state unaided — verified by you following it end to end from a clean state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
