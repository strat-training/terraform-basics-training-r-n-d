# M09 — Advanced Terraform Configuration — write-up

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

### Q1. What should the keys of a repeated resource be, and what happens to the real infrastructure when a key changes?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q2. When does a dynamic block make a configuration clearer, and when does it make it harder to review than the repetition it replaced?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q3. Which values should be derived inside the configuration, and which should the caller supply?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q4. When is a condition in the configuration the wrong tool?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q5. Where did you have to state a dependency explicitly rather than rely on a reference, and how did you decide that was genuinely needed?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q6. Which resources, if any, should be protected from replacement or destruction, which changes should Terraform ignore, and what does each cost the next person who has to change them?

- Options considered:
- Chosen:
- Why:
- Trade-off accepted:

### Q7. What assumption about real infrastructure is worth checking in your configuration, where does the check belong, and what should happen when it fails?

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

### Composing built-in functions to derive values


### Conditional expressions — and when a condition belongs in configuration at all


### `for` expressions and splat expressions — reshaping collections


### `for_each` in depth — maps, sets and derived collections, and what makes a key stable


### Dynamic blocks — generating repeated nested blocks from data


### Data sources in depth — beyond the basic lookup introduced in M04


### Explicit dependencies with `depends_on` — when a reference cannot express the ordering


### The `lifecycle` block — controlling replacement, destruction and ignored changes


### Preconditions and postconditions — checking assumptions about real infrastructure


### When a feature costs more readability than it saves



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
| **DoD-2** At least one resource is repeated from a structured input — a map, or a collection derived from one — and your write-up justifies the keys you chose. | | |
| **DoD-3** At least one resource has repeated nested blocks generated from the same structured input, and the plan shows the expected number of them (plan excerpt). | | |
| **DoD-4** Adding an entry, removing an entry and changing a key in the input each produce a plan you have captured, and your write-up says exactly what each plan would do to the real infrastructure. | | |
| **DoD-5** Derived values are defined once and used in more than one place, and no expression is duplicated across files (a reviewer reads the configuration). | | |
| **DoD-6** At least one conditional changes what the configuration creates or sets, and the plan is shown for both outcomes of the condition (two plan excerpts). | | |
| **DoD-7** A data source supplies a value the configuration uses, and no equivalent value is hard-coded (a reviewer reads the configuration). | | |
| **DoD-8** Every explicit dependency in the configuration is justified in the write-up; if there are none, the write-up says why a reference was always enough. | | |
| **DoD-9** Every lifecycle setting you used is justified in the write-up, and its effect is shown from a plan or a deliberate attempt that it affects (output pasted). | | |
| **DoD-10** At least one precondition or postcondition is in place, and you have deliberately triggered it and captured the failure message (output pasted). | | |
| **DoD-11** Your readability note says, for each advanced feature you used, where it helped and where it made the configuration harder to follow. | | |
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
