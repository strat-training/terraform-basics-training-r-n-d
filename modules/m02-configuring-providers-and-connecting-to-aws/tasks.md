# M02 — Configuring Providers and Connecting to AWS — Tasks

**Objective:** Sign in to the AWS sandbox with the access you were given, and know at any moment which identity and account Terraform will act as. Then pin Terraform and provider versions deliberately, and explain how a configuration, the provider plugins it needs and the lock file fit together — well enough to say what a version bump would change and who should review it.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M01) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Signing in to the AWS sandbox with the access you were given — IAM Identity Center (SSO) through the AWS CLI
- [ ] Work on: Confirming which identity and account Terraform will act as
- [ ] Work on: Credential lifetime — session expiry, its symptoms, and recovering from it
- [ ] Work on: Keeping static access keys off disk and out of the repository
- [ ] Work on: What a provider is and how Terraform finds and installs one
- [ ] Work on: Version constraints — for Terraform itself and for each provider
- [ ] Work on: The dependency lock file — what it records and why it is committed
- [ ] Work on: Using more than one provider in a single configuration
- [ ] Work on: Provider configuration — how a provider obtains its credentials, and provider-level default tags
- [ ] Work on: Inspecting which providers and versions a configuration actually uses
- [ ] Work on: Upgrading a pinned version deliberately
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: What does a learner see when their session has expired, and how will you help them tell that apart from a genuine permissions problem?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: How does the AWS provider decide which credentials to use, and how would you prove which identity a plan is using?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: What is the difference between a version constraint you declare and what the lock file records, and why does the course want both?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: How loose or tight should a provider constraint be, and who carries the risk of each choice?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: Why set tags at the provider rather than on each resource, and what would make you tag a resource individually anyway?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: What should a reviewer look for in a merge request that changes the lock file?
- [ ] Have ready: A signed-in sandbox session and a minimal Terraform configuration that uses the `aws` and `random` providers
- [ ] Have ready: Terraform and provider versions pinned, the lock file committed, and default tags configured on the AWS provider

## Verify

- [ ] Confirm DoD-1: An authenticated AWS sandbox session exists and a caller-identity query returns the sandbox identity (output pasted, account details redacted as the trainer directs). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: You have caused a session to fail, captured the symptom, and recovered; the write-up records both. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: No static access keys are present in your AWS configuration on disk or in your repository; your evidence shows the scan you ran and what it looked for. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: The configuration declares a required Terraform version and, for every provider it uses, a source and a version constraint. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: The lock file exists and is committed to version control (it appears in your commit). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: The provider listing for the configuration shows both `aws` and `random` (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: Formatting and validation checks pass with no errors (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: Default tags are configured on the AWS provider and the plan shows them on at least one taggable resource the configuration would create (plan excerpt). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-9: One deliberate version change is shown with its effect on the lock file (before and after). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-10: No resources exist in the sandbox as a result of this stage, confirmed from the cloud side. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] Under “Why it's built this way (key decisions)”: One entry per open design question in the brief, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
