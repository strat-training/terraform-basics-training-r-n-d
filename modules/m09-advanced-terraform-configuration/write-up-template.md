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

- Composing built-in functions to derive values
- Conditional expressions — and when a condition belongs in configuration at all
- `for` expressions and splat expressions — reshaping collections
- `for_each` in depth — maps, sets and derived collections, and what makes a key stable
- Dynamic blocks — generating repeated nested blocks from data
- Data sources in depth — beyond the basic lookup introduced in M04
- Explicit dependencies with `depends_on` — when a reference cannot express the ordering
- The `lifecycle` block — controlling replacement, destruction and ignored changes
- Preconditions and postconditions — checking assumptions about real infrastructure
- When a feature costs more readability than it saves

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: Formatting and validation checks pass with no errors.
- DoD-2: At least one resource is repeated from a structured input — a map, or a collection derived from one — and your write-up justifies the keys you chose.
- DoD-3: At least one resource has repeated nested blocks generated from the same structured input, and the plan shows the expected number of them (plan excerpt).
- DoD-4: Adding an entry, removing an entry and changing a key in the input each produce a plan you have captured, and your write-up says exactly what each plan would do to the real infrastructure.
- DoD-5: Derived values are defined once and used in more than one place, and no expression is duplicated across files (a reviewer reads the configuration).
- DoD-6: At least one conditional changes what the configuration creates or sets, and the plan is shown for both outcomes of the condition (two plan excerpts).
- DoD-7: A data source supplies a value the configuration uses, and no equivalent value is hard-coded (a reviewer reads the configuration).
- DoD-8: Every explicit dependency in the configuration is justified in the write-up; if there are none, the write-up says why a reference was always enough.
- DoD-9: Every lifecycle setting you used is justified in the write-up, and its effect is shown from a plan or a deliberate attempt that it affects (output pasted).
- DoD-10: At least one precondition or postcondition is in place, and you have deliberately triggered it and captured the failure message (output pasted).
- DoD-11: Your readability note says, for each advanced feature you used, where it helped and where it made the configuration harder to follow.
- DoD-12: Everything is destroyed except the M07 bucket, confirmed from the cloud side.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
