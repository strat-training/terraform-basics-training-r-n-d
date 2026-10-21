# M06 Write-Up — Advanced Terraform Configuration

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The data-driven AWS configuration — resources and nested blocks generated from structured input, with a conditional, a data-source lookup, dependency and lifecycle controls and checks on its own assumptions (link your repository).

## Why it's built this way (key decisions)

- When is a condition the wrong tool?
- What should the keys of a repeated resource be, and what happens to real infrastructure when a key changes?
- Where did you state a dependency explicitly, and what do lifecycle protections and ignored changes cost the next person who edits it?
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide to turning a configuration repeated by hand into one driven by structured input, using your own plans to show the reasoning, not just the expressions.

## Concepts worth explaining

Pick 2–3 ideas — `for_each` keys, dynamic blocks, `for` expressions, dependencies and lifecycle controls, or preconditions and postconditions — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-02: your plans for adding an entry, removing an entry and changing a key, with what each does to the real infrastructure.
- DoD-03: your conditional's plan for both outcomes.
- DoD-04: your plan, or your deliberate attempt, showing what each lifecycle setting does.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
