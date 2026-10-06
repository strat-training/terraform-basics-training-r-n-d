# M06 — Advanced Terraform Configuration — Write-up

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

- Which values should be derived inside the configuration and which the caller should supply.
- When a condition in the configuration is the wrong tool.
- How a collection looks before and after you reshape it.
- What the keys of a repeated resource should be, and what happens to the real infrastructure when a key changes.
- When a dynamic block makes a configuration clearer, and when it makes it harder to review than the repetition it replaced.
- What a data source supplies that you would otherwise hard-code.
- Where you had to state a dependency explicitly and how you decided that was needed, and which resources should be protected from replacement or destruction, which changes Terraform should ignore, and what each costs the next person who has to change them.
- What assumption about real infrastructure is worth checking in your configuration, where the check belongs, and what should happen when it fails.
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

- Composing Values with Built-in Functions
- Making Configuration Conditional
- Reshaping Data with `for` and Splat Expressions
- Going Deeper with `for_each`
- Generating Nested Configuration with Dynamic Blocks
- Discovering Existing Infrastructure with Data Sources
- Controlling Dependencies and Resource Lifecycle
- Validating Infrastructure with Preconditions and Postconditions

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-01: Formatting and validation pass with no errors, and derived values are defined once and used in more than one place, with no expression duplicated across files (a reviewer reads the configuration).
- DoD-02: At least one resource is repeated from a structured input — a map, or a collection derived from one — and your notes justify the keys you chose; at least one resource has repeated nested blocks generated from the same structured input, and the plan shows the expected number of them (plan excerpt); adding an entry, removing an entry and changing a key each produce a plan you captured, and your notes say exactly what each plan would do to the real infrastructure, not what you expect it to do.
- DoD-03: At least one conditional changes what the configuration creates or sets, and the plan is shown for both outcomes (two plan excerpts), not only the outcome you expected; a data source supplies a value the configuration uses, and no equivalent value is hard-coded (a reviewer reads the configuration).
- DoD-04: Every explicit dependency and every lifecycle setting in your configuration is justified in your notes (or they say why a reference was always enough), and each lifecycle setting's effect is shown from a plan or a deliberate attempt that it affects (output pasted), not assumed from its name.
- DoD-05: At least one precondition or postcondition is in place and you deliberately triggered it, with the real failure message captured (output pasted).
- DoD-06: Everything is destroyed except the M02 bucket, confirmed from the cloud side.
- DoD-07: Your write-up takes a first-time learner to a data-driven configuration like yours unaided — verified by you following it end to end from a clean state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
