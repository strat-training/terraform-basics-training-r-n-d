# M01 — Getting Started with Terraform — Write-up

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

- What problem Terraform solves that a script or the cloud console does not and where you would not use it, how describing the desired state differs from scripting the steps, which install method fits each tool on each operating system and what each choice costs in maintenance and support, how a version manager keeps Terraform at the version you pinned, what fails differently on Windows than on macOS, how you prove you are connected to AWS without static keys, and what a scan for static keys has to look at and what it can miss.
- What Terraform downloads when you initialise and where it puts it, the difference between a version constraint you declare and what the lock file records, how loose or tight a provider constraint should be and who carries the risk of each choice, and what a reviewer should look for in a merge request that changes the lock file.
- How the AWS provider decides which credentials to use and how you would prove which identity a plan is using, and why tags are set at the provider rather than on each resource and what would make you tag a resource individually anyway.
- Which parts of a resource you set and which Terraform reports back, what to check in a plan before you approve it, how you can tell from the plan alone what a change will do, and what you would do if a plan showed a destroy you did not expect.
- Which changes to your resource are made in place and which force replacement and how sure you are, what a replacement costs when the resource holds data or other resources depend on it, and how you confirm from the cloud side that everything is gone.
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader is new to Terraform and to this course.

## Concepts worth explaining

Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.

- Step 1 — The workstation (zero code)
- Step 2 — Dependencies: the `versions.tf` file
- Step 3 — Configuration: the `providers.tf` file
- Step 4 — Resources and planning: the `main.tf` file
- Step 5 — Apply and destroy

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-01: Your notes show the actual Terraform version, installed through a version manager and switched between two versions (output pasted), and a caller-identity query from your own signed-in session (output pasted, account details redacted as the trainer directs), not the version or the identity you assumed you had.
- DoD-02: Your notes show the scan you ran for static access keys on disk and in your repository, and what it looked for, not a statement that there are none.
- DoD-03: `terraform init` created the `.terraform` folder and the `.terraform.lock.hcl` file from your own `versions.tf`, the lock file is committed (it appears in your commit), and your notes say in your own words what it recorded, not what the documentation says.
- DoD-04: Formatting and validation pass with no errors on your `providers.tf` and `main.tf`, shown as pasted output, not described from memory.
- DoD-05: Your plan output is pasted and read: it shows the default tags on your resource, and your plan-review note classifies every change you made as create, in-place update or replacement, and your trainer confirms each classification on review.
- DoD-06: The plan before your one-attribute change shows an in-place update (output pasted), and after destroy nothing exists in the sandbox, confirmed from the cloud side, not only from Terraform's output.
- DoD-07: Your write-up takes a first-time learner on either operating system from an empty folder to a destroyed resource unaided — verified by you following it end to end from a clean state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
