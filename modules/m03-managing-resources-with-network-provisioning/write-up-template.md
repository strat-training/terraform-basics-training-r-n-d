# M03 Write-Up — Managing Resources with Network Provisioning

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The small AWS network — a VPC, subnets in more than one availability zone, the routing the public tier needs and no NAT gateway (link your repository).

## Why it's built this way (key decisions)

- Where did Terraform work out the order of your resources on its own, and where did you have to state an ordering explicitly?
- What are the trade-offs between the two ways of repeating a resource, and what happens to your existing subnets if you add or remove one from the set?
- What is the difference between a resource and a data source in what Terraform manages, and what happens to each on destroy?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide to building a small multi-zone network, using your own plan output to show the reasoning, not just the configuration.

## Concepts worth explaining

Pick 2–3 ideas — the dependency graph, repeating a resource, data sources, or the routing a public tier needs — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-01 and DoD-04: your plan showing the VPC, subnets in two or more zones and the public routing, with no NAT gateway.
- DoD-05: your note naming the implicit dependencies in your configuration and where each one comes from.
- DoD-02 and DoD-03: your plan or state listing showing the subnets created from one repeated block, and the value your data source read.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
