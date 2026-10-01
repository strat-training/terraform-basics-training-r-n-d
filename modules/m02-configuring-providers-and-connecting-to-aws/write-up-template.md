# M02 — Configuring Providers and Connecting to AWS — write-up

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

### Q1. What does a learner see when their session has expired, and how will you help them tell that apart from a genuine permissions problem?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. What can go wrong when you sign in from inside a container rather than on the host?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. How does the AWS provider decide which credentials to use, and how would you prove which identity a plan is using?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. What is the difference between a version constraint you declare and what the lock file records, and why does the course want both?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q5. How loose or tight should a provider constraint be, and who carries the risk of each choice?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q6. Why set tags at the provider rather than on each resource, and what would make you tag a resource individually anyway?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q7. What should a reviewer look for in a merge request that changes the lock file?

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

### Signing in to the AWS sandbox with the access you were given — IAM Identity Center (SSO) through the AWS CLI


### Confirming which identity and account Terraform will act as


### Credential lifetime — session expiry, its symptoms, and recovering from it


### Browser-based sign-in from inside a container or remote workspace


### Keeping static access keys off disk and out of the repository


### What a provider is and how Terraform finds and installs one


### Version constraints — for Terraform itself and for each provider


### The dependency lock file — what it records and why it is committed


### Using more than one provider in a single configuration


### Provider configuration — how a provider obtains its credentials, and provider-level default tags


### Inspecting which providers and versions a configuration actually uses


### Upgrading a pinned version deliberately



## 5. What tripped me up

<!-- Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. -->

| What happened (symptom or error text) | What I assumed | What it actually was | How I found out and fixed it |
| --- | --- | --- | --- |
| | | | |

## 6. Checkpoint evidence

<!-- One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. Redact anything sensitive. A row with no evidence is not done. -->

| Item | Evidence | Reviewer |
| --- | --- | --- |
| **DoD-1** An authenticated AWS sandbox session exists and a caller-identity query returns the sandbox identity (output pasted, account details redacted as the trainer directs). | | |
| **DoD-2** You have caused a session to fail, captured the symptom, and recovered; the write-up records both. | | |
| **DoD-3** No static access keys are present in your AWS configuration on disk or in your repository; your evidence shows the scan you ran and what it looked for. | | |
| **DoD-4** Signing in also works from inside the dev container, or your write-up records exactly what blocked it (output pasted). | | |
| **DoD-5** The configuration declares a required Terraform version and, for every provider it uses, a source and a version constraint. | | |
| **DoD-6** The lock file exists and is committed to version control (it appears in your commit). | | |
| **DoD-7** The provider listing for the configuration shows both `aws` and `random` (output pasted). | | |
| **DoD-8** Formatting and validation checks pass with no errors (output pasted). | | |
| **DoD-9** Default tags are configured on the AWS provider and the plan shows them on at least one taggable resource the configuration would create (plan excerpt). | | |
| **DoD-10** One deliberate version change is shown with its effect on the lock file (before and after). | | |
| **DoD-11** No resources exist in the sandbox as a result of this stage, confirmed from the cloud side. | | |

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
