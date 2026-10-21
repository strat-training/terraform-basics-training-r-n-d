# M05 Write-Up — Terraform for Multi-Environment Deployments

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

One configuration deployed as both dev and prod with separate state, and your note comparing three ways to separate environments (link your repository).

## Why it's built this way (key decisions)

- Which name parts and tags let anyone tell at a glance which environment a resource belongs to, and what else would a clean-up or cost report need?
- What does separate state protect, what does it not, and what makes it easy to apply one environment's values to the other's state?
- When would workspaces or a directory per environment be the right tool, and what do you give up by not using them here?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide to deploying one configuration as dev and prod with separate state, using your own plans to show the reasoning, not just the commands.

## Concepts worth explaining

Pick 2–3 ideas — per-environment values and state keys, limiting blast radius with separate state, naming conventions and default tags, or directories versus workspaces — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-01 and DoD-02: the listing showing two state objects under different keys, and a clean plan for each environment.
- DoD-04: a plan, state listing or cloud-side output showing the naming convention and required tags on your resources.
- DoD-05: your note comparing a directory per environment, workspaces and per-environment files, and when each fits.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
