# Capstone Write-up

> This is the most important write-up of the course — it's meant to become part of the content library. Write it so the next cohort could use it as a model for their own capstone, not just as a record of what you did. Copy this file to `write-up.md` in your capstone repository and fill in the copy; leave this template untouched. Write each section as you build, not after it works. Never paste credentials, tokens or key material anywhere in this file.

| | |
| --- | --- |
| Trainee | |
| Status | Draft <!-- Draft → In review → Revising → Accepted --> |
| Build location | <!-- your GitLab capstone repository and branch --> |
| Hours spent | <!-- an honest total --> |

## What I built

Your platform: the shop you chose, what each tier runs on, what each stack holds, how your modules divide, how a release moves through it, how you demonstrate that, and where the off-site backup and the Azure assets fit. A diagram is welcome.

## Why it's built this way (key decisions)

One entry per question, then your cost estimate. Say what you considered, what you chose, why, and what you gave up. The design decisions in the brief are yours, so each answer should name the alternatives you rejected.

- What shop did you choose, and what did you change from the starter catalogue, theme and images?
- What does each tier run on, and what did you consider and reject?
- How many servers or tasks, subnets, balancers and other resources did you choose, and why those numbers? Where did the cost challenge force a trade-off?
- Where did you draw the stack boundary, and how did you divide the modules?
- How does a new version replace the old one without a failed request — what shifts the traffic, and what extra capacity does it use — and what does your approach cost in extra capacity, time and complexity compared with the alternatives?
- What decides that a server is ready to take traffic, and what does your readiness check prove — and fail to prove?
- How does the platform keep a faulty release away from customers, which signal other than the health check catches a bad one, and how did you roll back?
- How did you demonstrate the release, and what does your demonstration prove — and fail to prove?
- What does a schema change need so that the old and new versions can both run against the same database?
- How does each App server get its database credential without it passing through your code, variables, state or repository, and what does each alternative leak?
- How does the backup reach GCP, and how do the assets reach Azure, without a stored key — and what did you do where the sandbox blocked an approach?
- How did you express the dependencies between tiers and clouds so that one apply works, a release is a small plan, and the next plan is clean?
- What does "zero downtime" not cover in this design, and what would a production team add — including why this state would normally be split by cloud or tier?
- What could survive a destroy, and how did you find it in each cloud?
- What did your sizing, your release capacity and your cost choices come to per hour and in total? Include your own estimate — every billed resource, its hourly rate and the hours you expect it to run — and how it compares with the limits in the cost challenge and with what you observed.
- Where did you spend the most time, and why?

## AI collaboration log

Be specific, not a vague "I used AI to help write some code":

- Which AI tool(s) did you use, and for roughly what portion of the work (a stack, a module, the guardrails, the proofs, the demonstration, debugging, something else)?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead. Defects of the kinds `check.sh` looks for are the obvious candidates: over-broad IAM, open ports, `count` where `for_each` was needed, a reachable database, missing default tags. If you genuinely can't think of one, that's worth questioning: were you checking closely enough?
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write this as a guide someone could actually follow to build something like your capstone from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed M01–M12 but hasn't built a capstone before.

## Concepts worth explaining

Pick 2–3 ideas from across the whole course that this capstone made concrete for you, and explain each one in your own words as if teaching it for the first time.

## What tripped me up

The real obstacles — errors, design mistakes, failed plans, anything that cost you real time. Keep the exact error text. Include what the sandbox allowed and what it blocked: roles, load balancers, scaling, containers, the Storage Transfer API, anonymous Blob access. These are usually the most valuable part of a capstone write-up.

## Checkpoint evidence

Show: both stacks applying and the clean plan after each apply; failure proofs 1 to 3 and the distinction proof; stages 0 to 6 with each plan's summary line, your release demonstration record, the manifest versions on GCP and your failure signal's state at stage 5; Demo Challenge tasks 1 to 5; identity and backup proofs A to E; the stock checks; the `check.sh` result; your cost estimate against the cost challenge; and the teardown scans from all three clouds. Put the saved plans, the demonstration record and command output in `evidence/` and point to them from here.

## Rubric self-assessment

Score yourself honestly against all six criteria in the fixed rubric in `brief.md` before your panel reviews it — where do you think you land, and why? For understanding specifically: is there any part of your own work you'd struggle to explain cold, without re-reading it first? Name it here rather than hoping it doesn't come up in the presentation.

## What I'd do differently

If you started the capstone over today, what would you change?
