# M12 — Going Multi-Cloud with Terraform — Write-up

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

- What can go wrong if the ambient login points at a different project or subscription than you intended, and what in your configuration prevents it?
- Where should state live for a configuration that creates nothing, and does your answer change once it does?
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

- Confirming access to the GCP and Azure sandboxes
- GCP — Application Default Credentials sign-in, project selection, provider configuration
- Azure — CLI sign-in, subscription selection, provider configuration
- State management across clouds: `gcs` and `azurerm` backends
- Where this course stops — HCP Terraform and Sentinel, named and not taught

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: Your write-up shows both configurations passing formatting and validation checks, as pasted output.
- DoD-2: Your write-up shows both configurations planning successfully, with an identity output for each cloud (output pasted), not the identity you expected.
- DoD-3: Each configuration targets the intended GCP project or Azure subscription even when the active login points elsewhere (evidence shown), or your write-up records why that was not possible.
- DoD-4: Your write-up shows the scan that found no secrets or keys in your repository or on disk, and what it looked for, not a statement that there are none.
- DoD-5: Your write-up shows neither configuration creating a resource: the plan shows nothing to add.
- DoD-6: Your write-up closes with a short next-steps note that names HCP Terraform and Sentinel and says in one line what each is for, in your own words.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
