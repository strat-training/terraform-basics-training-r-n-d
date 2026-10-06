# M09 — Advanced Terraform Configuration — Write-up

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

- What should the keys of a repeated resource be, and what happens to the real infrastructure when a key changes?
- When does a dynamic block make a configuration clearer, and when does it make it harder to review than the repetition it replaced?
- Which values should be derived inside the configuration, and which should the caller supply?
- When is a condition in the configuration the wrong tool?
- Where did you have to state a dependency explicitly rather than rely on a reference, and how did you decide that was genuinely needed?
- Which resources, if any, should be protected from replacement or destruction, which changes should Terraform ignore, and what does each cost the next person who has to change them?
- What assumption about real infrastructure is worth checking in your configuration, where does the check belong, and what should happen when it fails?
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

- DoD-1: Your training module shows formatting and validation checks passing with no errors.
- DoD-2: Your training module shows at least one resource repeated, and at least one resource with repeated nested blocks, generated from a structured input — a map, or a collection derived from one. It justifies the keys you chose, shows a plan with the expected number of nested blocks (plan excerpt), and shows adding an entry, removing an entry and changing a key, each with a captured plan and exactly what it would do to the real infrastructure.
- DoD-3: Your training module shows derived values defined once and used in more than one place, with no expression duplicated across files (a reviewer reads the configuration).
- DoD-4: Your training module shows at least one conditional that changes what the configuration creates or sets, with the plan shown for both outcomes of the condition (two plan excerpts).
- DoD-5: Your training module shows a data source supplying a value the configuration uses, with no equivalent value hard-coded (a reviewer reads the configuration).
- DoD-6: Your training module justifies every explicit dependency in the configuration (or says why a reference was always enough) and every lifecycle setting you used, and shows each lifecycle setting's effect from a plan or a deliberate attempt that it affects (output pasted).
- DoD-7: Your training module shows at least one precondition or postcondition in place that you deliberately triggered, with the failure message captured (output pasted).
- DoD-8: A learner following your training module ends with everything destroyed except the M07 bucket, confirmed from the cloud side.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
