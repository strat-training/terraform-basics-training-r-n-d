# M01 — Getting Started with Terraform — write-up

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

### Q1. Which install method would you choose for each tool on each operating system, and what does each choice cost in maintenance and support?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. Which parts of the toolchain must be identical for every learner, which can vary, and what does each choice cost in support?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. What fails differently on Windows than on macOS, and how will a learner tell a broken install from a misconfigured one?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. How will a learner know the toolchain is correct, rather than merely present?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q5. Why might a team prefer the local install over the dev container, or the reverse, and what does each give up?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q6. What problem does Terraform solve that a script or the cloud console does not, and where would you not use it?

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

### What Terraform is — infrastructure as code, and the problem Terraform solves


### The tools the labs need, and what each one is for


### Installing Terraform at the pinned version on macOS


### Installing Terraform at the pinned version on Windows


### Visual Studio Code for Terraform work — installation and the Terraform extension


### The AWS, Google Cloud and Azure command-line tools, plus Git, `jq` and `curl`


### A shell that can run the labs' shell scripts on Windows


### Switching between Terraform versions with a version manager


### The pinned dev container as an alternative to installing locally


### Verifying the toolchain end to end — versions, and formatting and validation of a configuration that creates nothing


### OpenTofu differences — an ungraded sidebar



## 5. What tripped me up

<!-- Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. -->

| What happened (symptom or error text) | What I assumed | What it actually was | How I found out and fixed it |
| --- | --- | --- | --- |
| | | | |

## 6. Checkpoint evidence

<!-- One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. Redact anything sensitive. A row with no evidence is not done. -->

| Item | Evidence | Reviewer |
| --- | --- | --- |
| **DoD-1** Terraform at the pinned version (1.11 or later) runs on macOS and on Windows (version output pasted for each). | | |
| **DoD-2** Visual Studio Code with the Terraform extension is installed on both systems, and the editor flags a deliberately introduced error in a configuration (screenshot for each). | | |
| **DoD-3** The AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` run on both systems (version output pasted for each). | | |
| **DoD-4** A version manager switches between two Terraform versions on each system where one works; where none does, the write-up says so (output pasted). | | |
| **DoD-5** The pinned dev container starts and runs the same Terraform version (version output pasted). | | |
| **DoD-6** Formatting and validation checks pass on a configuration that creates nothing, on both systems (output pasted). | | |
| **DoD-7** The steps for any operating system you do not own are verified on a second machine or by a second person, or are marked unverified in the write-up. | | |
| **DoD-8** Your write-up takes a first-time learner on either operating system to DoD-1 through DoD-3 unaided — verified by you following it end to end from a clean state. | | |
| **DoD-9** Your write-up explains, in your own words, what infrastructure as code is and what Terraform adds to it. | | |

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
