# M08 — Terraform for Multi-Environment Deployments — write-up

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

### Q1. What makes it easy to apply one environment's values to the other's state, and what will you do to make that harder?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. Which tags would a clean-up or cost report need beyond `Environment`, and why?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. How should the files be laid out so a newcomer finds each concern without being told?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. When would workspaces be the right tool, and what do you give up by not using them here?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q5. When would a directory per environment be the right tool, and what do you give up by not using it here?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q6. In what ways does keeping both environments in one account misrepresent real practice?

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

### One configuration, many environments — what is shared and what must be separate


### Per-environment input values


### Per-environment backend settings and separate state keys in the shared bucket


### Blast radius — what separate state does and does not protect


### The standard file layout for a root configuration


### A naming convention and required tags applied through provider defaults


### Switching between environments safely


### Other ways to separate environments — a directory per environment, and workspaces — and when each fits (explained, not used)



## 5. What tripped me up

<!-- Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. -->

| What happened (symptom or error text) | What I assumed | What it actually was | How I found out and fixed it |
| --- | --- | --- | --- |
| | | | |

## 6. Checkpoint evidence

<!-- One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. Redact anything sensitive. A row with no evidence is not done. -->

| Item | Evidence | Reviewer |
| --- | --- | --- |
| **DoD-1** Two state objects exist in the bucket under different keys (listing pasted). | | |
| **DoD-2** Both environments produce clean plans (output for each). | | |
| **DoD-3** Environment-specific inputs differ between the two environments and live outside the main configuration files. | | |
| **DoD-4** Every resource follows the naming convention and carries the required tags (shown from the plan, state or cloud side). | | |
| **DoD-5** The file layout follows the standard root-configuration layout; a reviewer can find each concern from file names alone. | | |
| **DoD-6** The comparison note is present and covers a directory per environment, workspaces, and the per-environment files you used, saying when each fits. | | |
| **DoD-7** Both environments are destroyed and the bucket is retained, confirmed from the cloud side. | | |

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
