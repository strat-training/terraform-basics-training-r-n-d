# M07 — Designing Reusable Terraform Modules — Write-up

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

- What a module call hands to the module and what it gets back.
- What belongs inside a module and what should stay in the root, and how you drew that line.
- Which inputs you exposed and which you fixed, what each extra input costs the next person who has to understand the module, and what a caller needs to be told by a module's outputs.
- How a module's files should be laid out so a newcomer finds inputs, outputs and resources without being told.
- Which naming convention you chose, and why.
- What deserves a comment in a module, and what the code should make obvious without one.
- What stays shared between the calls and what each call owns.
- How resource addresses change when something moves into a module, and what that would mean for a configuration that is already deployed.
- What pinning protects you from for each kind of source.
- How much you trust a module you did not write, and what you check before using it.
- What a module assumes about provider configuration, and where it takes its region, account and environment name from.
- When a module is the wrong answer.
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

- What a module is
- Deciding what belongs in a module, and what does not
- A module's interface
- Standard module file structure
- Naming conventions for a module's inputs, outputs and resources
- Comments and documentation
- Calling the same module more than once with different inputs
- How modules change resource addresses in a plan and in state
- Module sources and versions
- Consuming a published module
- What a module may assume about provider configuration
- Module anti-patterns

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-01: Formatting and validation pass for both the module and the root configuration, and the module is called at least twice with different inputs: both calls produce clean plans (output pasted) and resource addresses for the separate calls show distinct module paths (state listing pasted), not two copies of the same call.
- DoD-02: The module has a documented interface — every input has a type and a description, inputs that can take a bad value are validated, and every output has a description — and follows the standard module layout, so a reviewer can find what they need from file names alone (a reviewer reads the module).
- DoD-03: The names of the module's inputs, outputs and internal resources follow one convention, which your notes state, and your notes say which comment syntax you chose, what you chose to comment, and why (a reviewer reads the module).
- DoD-04: Your notes state what the module assumes about provider configuration and where it takes its region, account and environment name from, not that it “just works”, and resources created through the module still follow M05's naming convention and carry the required tags (shown from the plan, state or cloud side).
- DoD-05: Your notes review one published module — its source, pinned version, inputs and outputs, and what you checked before trusting it — and include a decision note that says what you put in the module, what you left out, and a case where you would not write a module.
- DoD-06: Everything is destroyed except the M02 bucket, confirmed from the cloud side.
- DoD-07: Your write-up takes a first-time learner to a reusable module called twice from a root configuration unaided — verified by you following it end to end from a clean state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
