# M10 — Designing Reusable Terraform Modules — Write-up

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

- What belongs inside a module and what should stay in the root, and how did you draw that line?
- Which inputs did you expose, which did you fix, and what does each extra input cost the next person who has to understand the module?
- What does a caller need to be told by a module's outputs, and what should stay hidden?
- How should a module's files be laid out so a newcomer finds inputs, outputs and resources without being told?
- What deserves a comment in a module, and what should the code make obvious without one?
- How do resource addresses change when something moves into a module, and what would that mean for a configuration that is already deployed?
- How much do you trust a module you did not write, and what do you check before using it?
- When is a module the wrong answer?
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

- What a module is — the root module, child modules, and what a module call does
- Deciding what belongs in a module, and what does not
- A module's interface — inputs, outputs, and what it keeps private
- Standard module file structure
- Naming conventions for a module's inputs, outputs and resources
- Comments and documentation — comment syntax, what deserves a comment, and descriptions on inputs and outputs
- Calling the same module more than once with different inputs
- How modules change resource addresses in a plan and in state
- Module sources and versions — local paths versus registry or Git sources, and pinning
- Consuming a published module — reading someone else's module before trusting it
- What a module may assume about provider configuration
- Module anti-patterns

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: Your training module shows formatting and validation checks passing for both the Terraform module and the root configuration.
- DoD-2: Your training module shows a Terraform module with a documented interface and the standard module layout: every input has a type and a description, inputs that can take a bad value are validated, every output has a description, and a reviewer can find what they need from file names alone (a reviewer reads the Terraform module).
- DoD-3: Your training module states the one convention that the names of the Terraform module's inputs, outputs and internal resources follow, and which comment syntax you chose, what you chose to comment, and why (a reviewer reads the Terraform module).
- DoD-4: Your training module shows the Terraform module called at least twice with different inputs, both calls producing clean plans (output pasted) and the separate calls having distinct module paths in their resource addresses (state listing pasted).
- DoD-5: Your training module states what the Terraform module assumes about provider configuration and where it takes its region, account and environment name from (a reviewer reads the Terraform module).
- DoD-6: Your training module shows resources created through the Terraform module still following M08's naming convention and carrying the required tags (shown from the plan, state or cloud side).
- DoD-7: Your training module contains a review of one published module — its source, pinned version, inputs and outputs, and what you checked before trusting it — and a decision note that says what you put in the Terraform module, what you left out, and a case where you would not write a module.
- DoD-8: A learner following your training module ends with everything destroyed except the M07 bucket, confirmed from the cloud side.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
