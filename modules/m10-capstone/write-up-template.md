# Capstone Write-Up

Fill this in as you go, not after the fact. Write it so a trainee starting the capstone next cohort could use it as a model. Copy this file to `write-up.md` in your capstone repository and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The shop platform you chose — what it sells, what each tier runs on, what each stack holds, how a release moves through it, and where the GCP backup and the Azure assets fit (link your repository).

## Why it's built this way (key decisions)

- What does each tier run on, and what did you consider and reject?
- How does a new version replace the old one without a failed request, and what does that cost compared with the alternatives?
- How does each App server get its database credential without it passing through your code, variables, state or repository?
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide to building something like your capstone, assuming the reader has finished M01–M09 but has never built a capstone — the order you tackled things in and why.

## Concepts worth explaining

Pick 2–3 ideas from across the whole course that this capstone made concrete for you, other than the three design decisions above, and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time, including what the sandbox blocked. Keep the exact error text.

## Checkpoint evidence

Put the saved plans, logs and command output in `evidence/` and point to them from here. The definition of done in `brief.md` still applies in full.

- Definition of done 1 and 2: the apply and clean-plan output for both stacks, and stages 0 to 6 with each plan's summary line and your release demonstration record.
- Definition of done 3 and 4: your `check.sh` result, and the saved plans and proofs for the failure, identity and backup proofs and Demo Challenge tasks 1 to 5.
- Definition of done 5 and 6: your cost estimate against your saved plan, and the teardown scans from AWS, GCP and Azure.

## Rubric self-assessment

Score yourself honestly against all 3 criteria in the fixed rubric in `brief.md` before your panel reviews it — where do you think you land, and why? For understanding specifically: is there any part of your own work you'd struggle to explain cold, without re-reading it first? Name it here rather than hoping it doesn't come up in the presentation.

## What I'd do differently

If you started the capstone over, what would you do differently?
