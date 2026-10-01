# M07 — Remote State and State Management Practices — write-up

> **How to use this file.** Copy it to `write-up.md` in this folder and fill in the copy; leave this template blank for the next cohort. Write each section **while you build**, in the same sitting as the work — not after it works. The brief is in [brief.md](brief.md); do not edit it. Never paste credentials, tokens or key material anywhere in this file.

| | |
| --- | --- |
| Trainee | |
| Status | Draft <!-- Draft → In review → Revising → Accepted --> |
| Build location | <!-- repository and branch or merge request holding your Terraform code --> |
| Started / finished | |
| Hours spent | <!-- an honest total — the trainer uses it to set time boxes --> |

## 1. What I built

<!-- Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome. A reader should know what exists before they read how you got there. -->

## 2. Key decisions and tradeoffs

<!-- One entry per open design question from the brief, then any further decision of your own worth recording. Say what you considered, what you chose, why, and what you gave up. "The docs said so" is not a reason. -->

### Q1. Who and what needs access to the state bucket, and how narrow can you make that without breaking Terraform?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. How did you solve the problem of creating the thing that stores your state, and what would you do differently on a team?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. What happens if a lock is left behind, and what must you check before overriding one?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. Why is this bucket kept when everything else is destroyed, and what risk does that carry?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:


### Additional decisions

<!-- Add as many as you need, in the same shape. -->

## 3. How to build it

<!-- This section becomes the teaching content, so write it for a learner who has finished the previous stage and has not seen this one. They will follow it alone, with no trainer to ask. Include the commands and code they need, the reason for each step, what they should see afterwards, and where to stop and check before moving on. -->

### Before you start

<!-- What the learner needs in place: earlier stages, access, tools, versions. -->

### Steps

<!-- Numbered, in the order you would do them again. -->

### How you know it worked

<!-- What the learner can check to be sure, without asking you. -->

### Clean-up

<!-- Exactly what to destroy or retire, and how to confirm nothing is left. -->

## 4. Concepts in my own words

<!-- For each concept: explain it as you would to a colleague, in your own words — no pasted definitions. Give one example from your build and one thing it is commonly confused with. -->

### Why state moves to a remote backend, and what locking prevents


### The bootstrapping problem — where the state bucket itself comes from


### Protecting the bucket — versioning, encryption at rest, blocked public access, restricted access


### Configuring the backend and migrating existing local state into it


### Native S3 state locking, and why DynamoDB-based locking is no longer taught


### Proving that locking works


### A bucket that outlives its stage — lifecycle and eventual retirement



## 5. What tripped me up

<!-- Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. -->

| What happened (symptom or error text) | What I assumed | What it actually was | How I found out and fixed it |
| --- | --- | --- | --- |
| | | | |

## 6. Checkpoint evidence

<!-- One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. Redact anything sensitive. A row with no evidence is not done. -->

| Item | Evidence | Reviewer |
| --- | --- | --- |
| **DoD-1** A state object for your configuration exists in the bucket (listing pasted). | | |
| **DoD-2** Versioning is enabled on the bucket (shown from the cloud side). | | |
| **DoD-3** Encryption at rest is enabled and public access is fully blocked (shown from the cloud side). | | |
| **DoD-4** The backend configuration enables native locking and no DynamoDB table is used or created. | | |
| **DoD-5** A plan after migrating local state shows no changes — nothing was recreated. | | |
| **DoD-6** With one operation in progress, a second is refused with a lock error (the error output pasted). | | |
| **DoD-7** The bucket is retained and everything else is destroyed, confirmed from the cloud side. | | |
| **DoD-8** No static keys and no state file contents are committed to version control. | | |

## 7. Versions and sources

**Versions this was written for:** <!-- Terraform, each provider and each CLI, exact versions. -->

**Official documentation used:** <!-- Links, one per concept or step that relied on them. -->

## 8. Before I submit

- [ ] Every definition-of-done item has evidence in section 6
- [ ] I followed section 3 from a clean start and it worked as written
- [ ] Every concept in section 4 is in my own words
- [ ] Every open design question in section 2 has a reasoned answer, including what I gave up
- [ ] Section 5 records everything that cost me real time
- [ ] No credentials, tokens or key material appear anywhere in this file or my repository
- [ ] Status above is set to "In review"
