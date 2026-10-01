# M11 — Change with Confidence: Safe Terraform Refactoring — write-up

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

### Q1. How can you tell, before applying, that a refactor will not touch real infrastructure?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. What did the generated configuration get wrong or leave out, and how did you decide what to keep?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. When a resource stops being managed, what is responsible for it afterwards, and how do you avoid orphaning cost?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. Why does the course prefer changes that appear in a plan over commands that edit state, and when might you still see those commands?

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

### Why refactoring must never mean destroy-and-recreate


### Renaming or re-addressing a resource without replacing it


### Adopting an existing, unmanaged resource into Terraform


### Tidying generated configuration


### Ceasing to manage a resource without destroying it


### Verifying every refactor with a plan — zero destroys, zero replacements


### Reading a saved plan as JSON with `jq` — checking the action on every resource mechanically


### Targeted operations — an emergency tool, never routine


### Reading legacy guidance that relies on imperative state commands



## 5. What tripped me up

<!-- Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. -->

| What happened (symptom or error text) | What I assumed | What it actually was | How I found out and fixed it |
| --- | --- | --- | --- |
| | | | |

## 6. Checkpoint evidence

<!-- One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. Redact anything sensitive. A row with no evidence is not done. -->

| Item | Evidence | Reviewer |
| --- | --- | --- |
| **DoD-1** After each of the three refactors, a saved plan shows zero destroys and zero replacements (three plan summaries pasted). | | |
| **DoD-2** At least one of the three plan checks reads the saved plan's JSON form with `jq` and reports the action on every resource (output pasted). | | |
| **DoD-3** The renamed resource keeps its real-world identity (its cloud-side identifier is unchanged). | | |
| **DoD-4** The adopted resource is in state and described by configuration, and a plan after adoption shows no changes. | | |
| **DoD-5** The stop-managing resource still exists in AWS afterwards and Terraform no longer tracks it. | | |
| **DoD-6** Each refactor is visible as a reviewable change in configuration (the diff is in your evidence). | | |
| **DoD-7** Your write-up declares that no state-mutating command was used for any refactor. | | |
| **DoD-8** Your note on legacy imperative commands says when you will meet them and what the declarative equivalent is. | | |
| **DoD-9** No billable resource is left behind, including anything Terraform no longer manages; only the M07 bucket remains. | | |

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
