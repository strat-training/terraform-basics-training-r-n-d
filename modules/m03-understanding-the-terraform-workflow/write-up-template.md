# M03 — Understanding the Terraform Workflow — write-up

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

### Q1. How does describing the desired state differ from scripting the steps, and what does that change about running the same configuration twice?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. How can you tell from the plan alone that a change will destroy something, before you apply it?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. For your chosen resource, which changes are made in place and which force replacement — how did you establish that, and how sure are you?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. What would you do if a plan showed a destroy you did not expect?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q5. What does a replacement cost when the resource holds data or other resources depend on it?

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

### Declarative versus imperative infrastructure — what it means that Terraform describes desired state


### Anatomy of a resource — type, name, arguments and attributes


### The core workflow — initialise, plan, apply, destroy


### What a plan shows — reading the action for each resource


### In-place updates versus replacement


### What causes a replacement


### Plan review as a habit — what to check before approving


### Destroying what you created



## 5. What tripped me up

<!-- Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. -->

| What happened (symptom or error text) | What I assumed | What it actually was | How I found out and fixed it |
| --- | --- | --- | --- |
| | | | |

## 6. Checkpoint evidence

<!-- One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. Redact anything sensitive. A row with no evidence is not done. -->

| Item | Evidence | Reviewer |
| --- | --- | --- |
| **DoD-1** Formatting and validation checks pass with no errors. | | |
| **DoD-2** You ran the same apply twice without changing the configuration; both outputs are pasted, and the write-up explains the difference between them in terms of desired state. | | |
| **DoD-3** Your write-up identifies the type, name, arguments and attributes of your resource, and shows an attribute whose value you did not set. | | |
| **DoD-4** You made at least one in-place change and at least one forced replacement; the plan output for each was captured before it was applied. | | |
| **DoD-5** Your plan-review note classifies every change you made as in-place or replacement, and the trainer's model answer agrees with each classification. | | |
| **DoD-6** For each classification the note explains the cause in terms of the resource itself, not just the plan's symbols. | | |
| **DoD-7** After destroy the resource is gone — confirmed from the cloud side, not only from Terraform's output. | | |

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
