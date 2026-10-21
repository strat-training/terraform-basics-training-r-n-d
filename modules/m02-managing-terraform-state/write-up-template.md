# M02 Write-Up — Managing Terraform State

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The protected S3 state bucket and the small configuration whose local state you inspected and then migrated into it (link your repository).

## Why it's built this way (key decisions)

- What can leak a secret into state, and why does the course treat a state file as sensitive even when the configuration contains no secrets?
- What did you do to protect the bucket that holds your state, and how narrow could you make access to it without breaking Terraform?
- What does native locking prevent, and what does it not?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide from local state to a protected remote backend with locking demonstrated, using your own state output to show the reasoning, not just the commands.

## Concepts worth explaining

Pick 2–3 ideas — what state records, secrets in state, bootstrapping the bucket, migrating local state, or native locking — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-01 and DoD-02: your read-only local state output for one of your own resources, including what it holds for a sensitive value.
- DoD-03 and DoD-04: the bucket listing showing your migrated state, and the bucket's versioning, encryption and public-access settings from the cloud side.
- DoD-05: the lock error you got when a second operation ran while the first was in progress.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
