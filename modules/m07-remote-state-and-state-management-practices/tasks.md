# M07 — Remote State and State Management Practices — Tasks

**Objective:** Move state off your laptop into a remote backend that is versioned, encrypted, locked and access-controlled, and prove that locking works. The bucket you create here is reused by M08 to M11, so build it as something you would trust to hold every later stage's state.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M06) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Why state moves to a remote backend, and what locking prevents
- [ ] Work on: Bootstrapping, securing, and managing the lifecycle of the state bucket
- [ ] Work on: Configuring the backend and migrating existing local state into it
- [ ] Work on: Proving that native locking works and recovering abandoned locks
- [ ] Have ready: A protected S3 state bucket and a configuration that uses it as its remote backend
- [ ] Have ready: locking demonstrated

## Verify

- [ ] Confirm DoD-1: Your write-up shows a state object for your own configuration in the bucket (listing pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: Your write-up shows versioning and encryption at rest enabled and public access fully blocked on the bucket, shown from the cloud side, not from your configuration. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Your write-up shows a backend configuration that enables native locking, with no DynamoDB table used or created. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: Your write-up shows a plan after migrating local state with no changes, so nothing was recreated. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: Your write-up shows a second operation refused with a lock error while one is in progress (the error output pasted), not a description of what locking should do. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: Your write-up shows a lock you left behind deliberately and your recovery without losing or corrupting state (the error and the recovery output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: A learner following your training module ends with the bucket retained and everything else destroyed, confirmed from the cloud side, not only from Terraform's output. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: No static keys and no state file contents are committed to version control, shown by your commit history, not assumed. Capture the evidence under “Checkpoint evidence”.

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
