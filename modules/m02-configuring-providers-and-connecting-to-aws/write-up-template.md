# M02 — Configuring Providers and Connecting to AWS — Write-up

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

- How does the AWS provider decide which credentials to use, and how would you prove which identity a plan is using?
- What is the difference between a version constraint you declare and what the lock file records, and why does the course want both?
- How loose or tight should a provider constraint be, and who carries the risk of each choice?
- Why set tags at the provider rather than on each resource, and what would make you tag a resource individually anyway?
- What should a reviewer look for in a merge request that changes the lock file?
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

- Authenticating to AWS (IAM Identity Center) and verifying Terraform identity
- Keeping static access keys off disk and out of the repository
- What a provider is and how Terraform finds and installs one
- Provider concepts, credential configuration, and default tags
- Dependency management: version constraints, lock files, and safe upgrades
- Using and inspecting multiple providers in a single configuration

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: An authenticated AWS sandbox session exists and a caller-identity query returns the sandbox identity (output pasted, account details redacted as the trainer directs).
- DoD-2: No static access keys are present in your AWS configuration on disk or in your repository; your evidence shows the scan you ran and what it looked for.
- DoD-3: The configuration declares a required Terraform version and, for every provider it uses, a source and a version constraint.
- DoD-4: The lock file exists and is committed to version control (it appears in your commit).
- DoD-5: The provider listing for the configuration shows both `aws` and `random` (output pasted).
- DoD-6: Formatting and validation checks pass with no errors (output pasted).
- DoD-7: Default tags are configured on the AWS provider and the plan shows them on at least one taggable resource the configuration would create (plan excerpt).
- DoD-8: One deliberate version change is shown with its effect on the lock file (before and after).
- DoD-9: No resources exist in the sandbox as a result of this stage, confirmed from the cloud side.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
