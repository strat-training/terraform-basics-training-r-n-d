# M07 — Remote State and State Management Practices — Tasks

**Objective:** Move state off your laptop into a remote backend that is versioned, encrypted, locked and access-controlled, and prove that locking works. The bucket you create here is reused by M08 to M11, so build it as something you would trust to hold every later stage's state.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M06) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: Why state moves to a remote backend, and what locking prevents
- [ ] Work on: The bootstrapping problem — where the state bucket itself comes from
- [ ] Work on: Protecting the bucket — versioning, encryption at rest, blocked public access, restricted access
- [ ] Work on: Configuring the backend and migrating existing local state into it
- [ ] Work on: Native S3 state locking, and why DynamoDB-based locking is no longer taught
- [ ] Work on: Proving that locking works
- [ ] Work on: A bucket that outlives its stage — lifecycle and eventual retirement
- [ ] Work on: A lock left behind — what it means, what to check, and recovering safely
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: Who and what needs access to the state bucket, and how narrow can you make that without breaking Terraform?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: How did you solve the problem of creating the thing that stores your state, and what would you do differently on a team?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: What happens if a lock is left behind, and what must you check before overriding one?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: Why is this bucket kept when everything else is destroyed, and what risk does that carry?
- [ ] Have ready: A protected S3 state bucket and a configuration that uses it as its remote backend
- [ ] Have ready: locking demonstrated

## Verify

- [ ] Confirm DoD-1: A state object for your configuration exists in the bucket (listing pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: Versioning is enabled on the bucket (shown from the cloud side). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Encryption at rest is enabled and public access is fully blocked (shown from the cloud side). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: The backend configuration enables native locking and no DynamoDB table is used or created. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: A plan after migrating local state shows no changes — nothing was recreated. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: With one operation in progress, a second is refused with a lock error (the error output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: A lock has been left behind deliberately, and you recovered without losing or corrupting state (the error and the recovery output pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: The bucket is retained and everything else is destroyed, confirmed from the cloud side. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-9: No static keys and no state file contents are committed to version control. Capture the evidence under “Checkpoint evidence”.

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
