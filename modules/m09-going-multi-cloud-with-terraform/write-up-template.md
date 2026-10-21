# M09 Write-Up — Going Multi-Cloud with Terraform

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The two small configurations, one for GCP and one for Azure, each signing in with a short-lived login and outputting the identity it runs as (link your repository).

## Why it's built this way (key decisions)

- How do you confirm which project and subscription you are signed in to?
- What goes wrong if the ambient login points at a different project than you intended, and what in your configuration prevents it?
- What goes wrong if it points at a different subscription, and what in your configuration prevents it?
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide to a working sign-in and a successful plan on GCP and on Azure, using your own output to show the reasoning, not just the commands.

## Concepts worth explaining

Pick 2–3 ideas — GCP sign-in and project selection, Azure sign-in and subscription selection, state across clouds, or where this course stops — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-02: each cloud's plan output with its identity output and nothing to add.
- DoD-03: the output showing each configuration targets the intended project or subscription while the active login points elsewhere.
- DoD-04: the output of your scan for secrets and keys.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
