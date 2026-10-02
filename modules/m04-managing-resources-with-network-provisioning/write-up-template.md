# M04 — Managing Resources with Network Provisioning — Write-up

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

One entry per open design question in the brief, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.

- Where in your configuration did you rely on Terraform to infer ordering, and was there anywhere you felt you had to state it explicitly? Why?
- What are the trade-offs between the two ways of repeating a resource, and why does the course want one preferred?
- What happens to your existing subnets if you later add or remove one from the set you are repeating over?
- What distinguishes a public subnet from a private one in AWS, and how would you prove which is which?
- What is the difference between a resource and a data source in what Terraform manages, and what happens to each when you destroy?
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
- Repeating a resource — the two mechanisms Terraform offers
- Data sources — reading information that already exists, and how it differs from a resource
- A VPC, subnets in more than one availability zone, and the routing a public tier needs
- Public versus private subnets — what makes a subnet public
- Cost awareness — why some networking resources bill by the hour

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: Formatting and validation checks pass with no errors.
- DoD-2: The plan contains the VPC, subnets in at least two availability zones, and the routing for the public tier (resource addresses shown from the plan output or its JSON form).
- DoD-3: Subnets in more than one availability zone are created by repeating one resource block rather than writing each one out (a reviewer reads the configuration).
- DoD-4: At least one value the configuration needs about the account or region is read with a data source rather than hard-coded (a reviewer reads the configuration).
- DoD-5: No NAT gateway appears in the plan or in state.
- DoD-6: Your note names the implicit dependencies in your configuration and where each one comes from.
- DoD-7: Everything is destroyed, confirmed from the cloud side.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
