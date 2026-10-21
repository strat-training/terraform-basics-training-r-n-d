# M04 Write-Up — Defining Variables, Inputs and Outputs in Terraform

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The parameterised AWS configuration with two sets of values that both plan cleanly, your precedence record, and the configuration's sensitive input and output (link your repository).

## Why it's built this way (key decisions)

- Which inputs should have defaults and which should be required, and what is the risk of each?
- How does each way of supplying a value show up in a plan?
- What does marking a value sensitive hide, and where can it still be seen?
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide to turning a hard-coded configuration into one that plans cleanly with two sets of values, using your own plan output to show the reasoning, not just the variable blocks.

## Concepts worth explaining

Pick 2–3 ideas — validation, value precedence, local values, or sensitive inputs and outputs — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-01 and DoD-02: a clean plan for each of your two sets of values, and the plan rejecting an invalid network address range with your validation message.
- DoD-04: your precedence record — one plan output per value source, then your combined run.
- DoD-05: your plan output with a sensitive input, and the output showing what is displayed for your sensitive output.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
