# M02 — Configuring Providers and Connecting to AWS — Tasks

**Objective:** By the end of this stage, you can sign in to the AWS sandbox with the access you were given and say, at any moment, which identity and account Terraform will act as — using your own caller-identity output as the evidence, not an assumption. You can pin Terraform and provider versions deliberately and explain how a configuration, the provider plugins it needs and the lock file fit together, well enough to say what a version bump would change and who should review it.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M01) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Authenticating to AWS (IAM Identity Center) and verifying Terraform identity
- [ ] Work on: Keeping static access keys off disk and out of the repository
- [ ] Work on: What a provider is and how Terraform finds and installs one
- [ ] Work on: Provider concepts, credential configuration, and default tags
- [ ] Work on: Dependency management: version constraints, lock files, and safe upgrades
- [ ] Work on: Using and inspecting multiple providers in a single configuration
- [ ] Have ready: A signed-in sandbox session and a minimal Terraform configuration that uses the `aws` and `random` providers
- [ ] Have ready: Terraform and provider versions pinned, the lock file committed, and default tags configured on the AWS provider

## Verify

- [ ] Confirm DoD-01: Your notes show a caller-identity query that returns the sandbox identity from your own signed-in session (output pasted, account details redacted as the trainer directs), not the identity you assumed you had. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-02: Your notes show the scan you ran for static access keys on disk and in your repository, and what it looked for, not a statement that there are none. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-03: Your configuration declares a required Terraform version and, for every provider it uses, a source and a version constraint, and the provider listing shows both `aws` and `random` (output pasted), not providers left to float. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-04: The lock file is committed (it appears in your commit), and your notes show one deliberate version change with the lock file before and after, not a description of what a version change would do. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-05: Formatting and validation pass with no errors, and the plan shows default tags on at least one taggable resource the configuration would create (plan excerpt), not tags you only set in the code. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-06: Your notes show that no resources exist in the sandbox as a result of this stage, confirmed from the cloud side, not from Terraform's output. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-07: Your write-up takes a first-time learner to a signed-in sandbox session and a pinned, plan-only configuration unaided — verified by you following it end to end from a clean state. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] Under “Why it's built this way (key decisions)”: One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
