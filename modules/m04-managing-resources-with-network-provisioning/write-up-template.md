# M04 — Managing Resources with Network Provisioning — write-up

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

### Q1. Where in your configuration did you rely on Terraform to infer ordering, and was there anywhere you felt you had to state it explicitly? Why?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. What are the trade-offs between the two ways of repeating a resource, and why does the course want one preferred?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. What happens to your existing subnets if you later add or remove one from the set you are repeating over?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. What distinguishes a public subnet from a private one in AWS, and how would you prove which is which?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q5. What is the difference between a resource and a data source in what Terraform manages, and what happens to each when you destroy?

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

### Resource references and the dependency graph Terraform builds from them


### Implicit versus explicit dependencies


### Repeating a resource — the two mechanisms Terraform offers and the course's preference


### Data sources — reading information that already exists, and how it differs from a resource


### A VPC, subnets in more than one availability zone, and the routing a public tier needs


### Public versus private subnets — what makes a subnet public


### Cost awareness — why some networking resources bill by the hour



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
| **DoD-2** The plan contains the VPC, subnets in at least two availability zones, and the routing for the public tier (resource addresses shown from the plan output or its JSON form). | | |
| **DoD-3** Subnets are created from a keyed collection; the `count` meta-argument is not used to repeat any resource (a reviewer reads the configuration to confirm). | | |
| **DoD-4** At least one value the configuration needs about the account or region is read with a data source rather than hard-coded (a reviewer reads the configuration). | | |
| **DoD-5** No NAT gateway appears in the plan or in state. | | |
| **DoD-6** Your note names the implicit dependencies in your configuration and where each one comes from. | | |
| **DoD-7** Everything is destroyed, confirmed from the cloud side. | | |

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
