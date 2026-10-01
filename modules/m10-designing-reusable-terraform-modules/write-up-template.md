# M10 — Designing Reusable Terraform Modules — write-up

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

### Q1. What belongs inside a module and what should stay in the root, and how did you draw that line?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. Which inputs did you expose, which did you fix, and what does each extra input cost the next person who has to understand the module?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. What does a caller need to be told by a module's outputs, and what should stay hidden?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. How should a module's files be laid out so a newcomer finds inputs, outputs and resources without being told?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q5. What deserves a comment in a module, and what should the code make obvious without one?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q6. How do resource addresses change when something moves into a module, and what would that mean for a configuration that is already deployed?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q7. How much do you trust a module you did not write, and what do you check before using it?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q8. When is a module the wrong answer?

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

### What a module is — the root module, child modules, and what a module call does


### Deciding what belongs in a module, and what does not


### A module's interface — inputs, outputs, and what it keeps private


### Standard module file structure — where inputs, outputs, resources and version requirements live, and why


### Naming conventions for a module's inputs, outputs and resources


### Comments and documentation — comment syntax, what deserves a comment, and descriptions on inputs and outputs


### Calling the same module more than once with different inputs


### How modules change resource addresses in a plan and in state


### Module sources and versions — local paths versus registry or Git sources, and pinning


### Consuming a published module — reading someone else's module before trusting it


### What a module may assume about provider configuration


### Module anti-patterns — thin wrappers, over-parameterisation, abstractions that hide cloud differences



## 5. What tripped me up

<!-- Add a row whenever you lose more than about ten minutes. These become the course's common-errors entries, so keep the exact error text. -->

| What happened (symptom or error text) | What I assumed | What it actually was | How I found out and fixed it |
| --- | --- | --- | --- |
| | | | |

## 6. Checkpoint evidence

<!-- One row per definition-of-done item in the brief. Paste real output, trimmed to the relevant lines, or link a screenshot. Redact anything sensitive. A row with no evidence is not done. -->

| Item | Evidence | Reviewer |
| --- | --- | --- |
| **DoD-1** Formatting and validation checks pass for both the module and the root configuration. | | |
| **DoD-2** The module has a documented interface: every input has a type and a description, inputs that can take a bad value are validated, and every output has a description (a reviewer reads the module). | | |
| **DoD-3** The module follows the standard module layout; a reviewer can find its inputs, outputs, resources and version requirements from file names alone. | | |
| **DoD-4** The names of the module's inputs, outputs and internal resources follow one convention, which your write-up states. | | |
| **DoD-5** The module's comments explain why rather than restate what, and your write-up states which comment syntax you chose and why (a reviewer reads the module). | | |
| **DoD-6** The module is called at least twice with different inputs and both calls produce clean plans (output pasted). | | |
| **DoD-7** The module configures no provider itself and hard-codes no region, account or environment name (a reviewer reads it). | | |
| **DoD-8** Resource addresses for the separate calls show distinct module paths (state listing pasted). | | |
| **DoD-9** Resources created through the module still follow M08's naming convention and carry the required tags (shown from the plan, state or cloud side). | | |
| **DoD-10** The write-up contains a review of one published module — its source, pinned version, inputs and outputs, and what you checked before trusting it. | | |
| **DoD-11** The decision note says what you put in the module, what you left out, and a case where you would not write a module. | | |
| **DoD-12** Everything is destroyed except the M07 bucket, confirmed from the cloud side. | | |

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
