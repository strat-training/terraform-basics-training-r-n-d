# M01 — Getting Started with Terraform — Tasks

**Objective:** By the end of this stage, you can set up your own workstation, sign in to AWS without static keys, and take one simple resource through the whole Terraform lifecycle — initialise, plan, apply, update and destroy — using your own terminal output and plans as the evidence, not a diagram from a slide. You can explain what Terraform is, what a provider is and why versions are pinned, and predict from a plan whether a change updates a resource in place or replaces it.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that you have the access and tools the brief's stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Step 1 — The workstation (zero code)
- [ ] Work on: Step 2 — Dependencies: the `versions.tf` file
- [ ] Work on: Step 3 — Configuration: the `providers.tf` file
- [ ] Work on: Step 4 — Resources and planning: the `main.tf` file
- [ ] Work on: Step 5 — Apply and destroy
- [ ] Have ready: A configuration made of `versions.tf`, `providers.tf` and `main.tf` that manages one simple AWS resource, taken through create, in-place update and destroy from a workstation you set up yourself
- [ ] Have ready: a written plan-review note

## Verify

- [ ] Confirm DoD-01: Your notes show the actual Terraform version, installed through a version manager and switched between two versions (output pasted), and a caller-identity query from your own signed-in session (output pasted, account details redacted as the trainer directs), not the version or the identity you assumed you had. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-02: Your notes show the scan you ran for static access keys on disk and in your repository, and what it looked for, not a statement that there are none. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-03: `terraform init` created the `.terraform` folder and the `.terraform.lock.hcl` file from your own `versions.tf`, the lock file is committed (it appears in your commit), and your notes say in your own words what it recorded, not what the documentation says. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-04: Formatting and validation pass with no errors on your `providers.tf` and `main.tf`, shown as pasted output, not described from memory. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-05: Your plan output is pasted and read: it shows the default tags on your resource, and your plan-review note classifies every change you made as create, in-place update or replacement, and your trainer confirms each classification on review. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-06: The plan before your one-attribute change shows an in-place update (output pasted), and after destroy nothing exists in the sandbox, confirmed from the cloud side, not only from Terraform's output. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-07: Your write-up takes a first-time learner on either operating system from an empty folder to a destroyed resource unaided — verified by you following it end to end from a clean state. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] Under “Why it's built this way (key decisions)”: One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader is new to Terraform and to this course.
- [ ] Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
