# M07 — Remote State and State Management Practices — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M06) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: Why state moves to a remote backend, and what locking prevents *(scope 1)*
- [ ] **B2** Work on: The bootstrapping problem — where the state bucket itself comes from *(scope 2)*
- [ ] **B3** Work on: Protecting the bucket — versioning, encryption at rest, blocked public access, restricted access *(scope 3)*
- [ ] **B4** Work on: Configuring the backend and migrating existing local state into it *(scope 4)*
- [ ] **B5** Work on: Native S3 state locking, and why DynamoDB-based locking is no longer taught *(scope 5)*
- [ ] **B6** Work on: Proving that locking works *(scope 6)*
- [ ] **B7** Work on: A bucket that outlives its stage — lifecycle and eventual retirement *(scope 7)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): Who and what needs access to the state bucket, and how narrow can you make that without breaking Terraform? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): How did you solve the problem of creating the thing that stores your state, and what would you do differently on a team? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): What happens if a lock is left behind, and what must you check before overriding one? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): Why is this bucket kept when everything else is destroyed, and what risk does that carry? *(question 4)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: A protected S3 state bucket and a configuration that uses it as its remote backend *(deliverable)*
- [ ] **C2** Have ready: locking demonstrated *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: A state object for your configuration exists in the bucket (listing pasted). *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: Versioning is enabled on the bucket (shown from the cloud side). *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: Encryption at rest is enabled and public access is fully blocked (shown from the cloud side). *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: The backend configuration enables native locking and no DynamoDB table is used or created. *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: A plan after migrating local state shows no changes — nothing was recreated. *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: With one operation in progress, a second is refused with a lock error (the error output pasted). *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: The bucket is retained and everything else is destroyed, confirmed from the cloud side. *(DoD-7)*
- [ ] **V8** Capture evidence in write-up section 6 for DoD-8: No static keys and no state file contents are committed to version control. *(DoD-8)*

## 5. Write up — one task per write-up section

- [ ] **W1** Complete write-up section 1, “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome. *(write-up section 1)*
- [ ] **W2** Complete write-up section 2, “Key decisions and tradeoffs”: One entry per open design question from the brief, then any further decision of your own worth recording. Say what you considered, what you chose, why, and what you gave up. *(write-up section 2)*
- [ ] **W3** Complete write-up section 3, “How to build it”: This section becomes the teaching content, so write it for a learner who has finished the previous stage and has not seen this one. They will follow it alone, with no trainer to ask. *(write-up section 3)*
- [ ] **W4** Complete write-up section 4, “Concepts in my own words”: For each concept: explain it as you would to a colleague, in your own words — no pasted definitions. Give one example from your build and one thing it is commonly confused with. *(write-up section 4)*
- [ ] **W5** Complete write-up section 5, “What tripped me up”: Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. *(write-up section 5)*
- [ ] **W6** Complete write-up section 6, “Checkpoint evidence”: One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. *(write-up section 6)*
- [ ] **W7** Complete write-up section 7, “Versions and sources”. *(write-up section 7)*
- [ ] **W8** Complete write-up section 8, “Before I submit”. *(write-up section 8)*

## 6. Close out

- [ ] **F1** Self-review: go back through this list and the brief's definition of done. Every item is ticked, or you have written down why not and told the trainer. *(close out)*
- [ ] **F2** Set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review. *(close out)*
