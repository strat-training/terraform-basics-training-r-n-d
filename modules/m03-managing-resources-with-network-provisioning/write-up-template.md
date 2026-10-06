# M03 — Managing Resources with Network Provisioning — Write-up

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

One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.

- Where in your configuration you relied on Terraform to infer ordering.
- Whether there was anywhere you had to state an ordering explicitly, and why.
- The trade-offs between the two ways of repeating a resource and why the course wants one preferred, and what happens to your existing subnets if you later add or remove one from the set you are repeating over.
- The difference between a resource and a data source in what Terraform manages, and what happens to each when you destroy.
- What the routing for a public tier needs, and how you would see it in the plan.
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

- Resource references and the dependency graph Terraform builds from them
- Implicit versus explicit dependencies
- Repeating a resource
- Data sources
- A VPC, subnets in more than one availability zone, and the routing a public tier needs

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-01: Formatting and validation pass with no errors, and the plan contains the VPC, subnets in at least two availability zones, and the routing for the public tier, with resource addresses taken from the plan output or its JSON form, not from your code.
- DoD-02: Subnets in more than one availability zone are created by repeating one resource block, not by writing each one out (a reviewer reads the configuration).
- DoD-03: At least one value your configuration needs about the account or region is read with a data source, not hard-coded (a reviewer reads the configuration).
- DoD-04: No NAT gateway appears in the plan or in state, shown from real output, not from the absence of one in your code.
- DoD-05: Your note names the implicit dependencies in your own configuration and where each one comes from, not a general definition of an implicit dependency.
- DoD-06: Everything is destroyed, confirmed from the cloud side, not only from Terraform's output.
- DoD-07: Your write-up takes a first-time learner to the same small AWS network unaided — verified by you following it end to end from a clean state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
