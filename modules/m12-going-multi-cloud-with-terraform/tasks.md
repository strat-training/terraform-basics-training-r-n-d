# M12 — Going Multi-Cloud with Terraform — Tasks

**Objective:** See that the core Terraform workflow carries over to GCP and Azure while provider setup does not: sign in with short-lived logins, make the project or subscription explicit, and prove each provider works with a read-only check.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M01, M02) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Confirming access to the GCP and Azure sandboxes
- [ ] Work on: GCP — Application Default Credentials sign-in, project selection, provider configuration
- [ ] Work on: Azure — CLI sign-in, subscription selection, provider configuration
- [ ] Work on: State management across clouds: `gcs` and `azurerm` backends
- [ ] Work on: Where this course stops — HCP Terraform and Sentinel, named and not taught
- [ ] Have ready: Two small Terraform configurations, one per cloud, each authenticating with a short-lived login and outputting the identity it runs as

## Verify

- [ ] Confirm DoD-1: Your training module shows both configurations passing formatting and validation checks. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: Your training module shows both configurations planning successfully, with the plan output including an identity output for each cloud (output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Your training module shows each configuration targeting the intended GCP project or Azure subscription even when the active login points elsewhere (evidence shown), or records why that was not possible. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: Your training module shows no secrets or keys in the repository or on disk (the scan you ran is in your evidence). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: Your training module shows neither configuration creating a resource (the plan shows nothing to add). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: Your training module closes with a short next-steps note that names HCP Terraform and Sentinel and says in one line what each is for. Capture the evidence under “Checkpoint evidence”.

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
