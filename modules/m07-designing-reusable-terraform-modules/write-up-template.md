# M07 Write-Up — Designing Reusable Terraform Modules

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The reusable AWS module with its documented interface, the root configuration that calls it twice with different inputs, and your decision note (link your repository).

## Why it's built this way (key decisions)

- What belongs inside the module and what stays in the root, and how did you draw the line?
- Which inputs did you expose and which did you fix, what does each extra input cost, and what must the outputs tell a caller?
- How do resource addresses change when something moves into a module, and what would that mean for a configuration that is already deployed?
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide to turning repeated configuration into a reusable module called twice, using your own plans and state listing to show the reasoning, not just the module block.

## Concepts worth explaining

Pick 2–3 ideas — what belongs in a module, a module's interface, how modules change resource addresses, or pinned module sources — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-01: clean plans for both module calls, and the state listing showing distinct module paths.
- DoD-02: your module's file listing and its input and output declarations with types and descriptions.
- DoD-05: your review of one published module and your decision note on what you put in the module, what you left out, and when you would not write a module.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
