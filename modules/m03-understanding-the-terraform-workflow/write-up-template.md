# M03 — Understanding the Terraform Workflow — Write-up

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

- How does describing the desired state differ from scripting the steps, and what does that change about running the same configuration twice?
- How can you tell from the plan alone that a change will destroy something, before you apply it?
- For your chosen resource, which changes are made in place and which force replacement — how did you establish that, and how sure are you?
- What would you do if a plan showed a destroy you did not expect?
- What does a replacement cost when the resource holds data or other resources depend on it?
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

- Declarative versus imperative infrastructure — what it means that Terraform describes desired state
- Anatomy of a resource — type, name, arguments and attributes
- The core workflow — initialise, plan, apply, destroy
- What a plan shows — reading the action for each resource
- In-place updates versus replacement
- What causes a replacement
- Plan review as a habit — what to check before approving
- Destroying what you created

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: Formatting and validation checks pass with no errors.
- DoD-2: You ran the same apply twice without changing the configuration; both outputs are pasted, and the write-up explains the difference between them in terms of desired state.
- DoD-3: Your write-up identifies the type, name, arguments and attributes of your resource, and shows an attribute whose value you did not set.
- DoD-4: You made at least one in-place change and at least one forced replacement; the plan output for each was captured before it was applied.
- DoD-5: Your plan-review note classifies every change you made as in-place or replacement, and your trainer confirms each classification on review.
- DoD-6: For each classification the note explains the cause in terms of the resource itself, not just the plan's symbols.
- DoD-7: After destroy the resource is gone — confirmed from the cloud side, not only from Terraform's output.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
