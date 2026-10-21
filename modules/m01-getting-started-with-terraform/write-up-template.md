# M01 Write-Up — Getting Started with Terraform

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The workstation you set up, the `versions.tf`, `providers.tf` and `main.tf` files that manage one AWS resource, and your plan-review note (link your repository).

## Why it's built this way (key decisions)

- How did you prove you were signed in to AWS without static keys, and what can a scan for static keys miss?
- How loose or tight did you make the provider version constraint, and what does the lock file record that the constraint does not?
- How can you tell from a plan whether a change updates a resource in place or replaces it, and what would you do if a plan showed a destroy you did not expect?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide that takes a learner on macOS or Windows from an empty folder to a destroyed resource, using your own output to show the reasoning, not just the commands.

## Concepts worth explaining

Pick 2–3 ideas — declarative versus imperative, providers and the lock file, default tags, or in-place update versus replacement — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-01 and DoD-02: your version output after switching between two Terraform versions, your redacted caller identity, and your static-key scan output.
- DoD-05 and DoD-06: your plan showing the default tags on the resource, and your plan showing the in-place update.
- DoD-06: the cloud-side query output showing the resource is gone after destroy.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
