# M01 — Getting Started with Terraform — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that you have the access and tools the brief's stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: What Terraform is — infrastructure as code, and the problem Terraform solves *(scope 1)*
- [ ] **B2** Work on: The tools the labs need, and what each one is for *(scope 2)*
- [ ] **B3** Work on: Installing Terraform at the pinned version on macOS *(scope 3)*
- [ ] **B4** Work on: Installing Terraform at the pinned version on Windows *(scope 4)*
- [ ] **B5** Work on: Visual Studio Code for Terraform work — installation and the Terraform extension *(scope 5)*
- [ ] **B6** Work on: The AWS, Google Cloud and Azure command-line tools, plus Git, `jq` and `curl` *(scope 6)*
- [ ] **B7** Work on: A shell that can run the labs' shell scripts on Windows *(scope 7)*
- [ ] **B8** Work on: Switching between Terraform versions with a version manager *(scope 8)*
- [ ] **B9** Work on: The pinned dev container as an alternative to installing locally *(scope 9)*
- [ ] **B10** Work on: Verifying the toolchain end to end — versions, and formatting and validation of a configuration that creates nothing *(scope 10)*
- [ ] **B11** Work on: OpenTofu differences — an ungraded sidebar *(scope 11)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): Which install method would you choose for each tool on each operating system, and what does each choice cost in maintenance and support? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): Which parts of the toolchain must be identical for every learner, which can vary, and what does each choice cost in support? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): What fails differently on Windows than on macOS, and how will a learner tell a broken install from a misconfigured one? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): How will a learner know the toolchain is correct, rather than merely present? *(question 4)*
- [ ] **D5** Answer, with reasons, in write-up section 2 (Q5): Why might a team prefer the local install over the dev container, or the reverse, and what does each give up? *(question 5)*
- [ ] **D6** Answer, with reasons, in write-up section 2 (Q6): What problem does Terraform solve that a script or the cloud console does not, and where would you not use it? *(question 6)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: A verified lab toolchain for macOS and Windows — Terraform, Visual Studio Code with its Terraform extension, and the cloud and shell tools the labs use *(deliverable)*
- [ ] **C2** Have ready: your written installation guide for both systems (the write-up) *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: Terraform at the pinned version (1.11 or later) runs on macOS and on Windows (version output pasted for each). *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: Visual Studio Code with the Terraform extension is installed on both systems, and the editor flags a deliberately introduced error in a configuration (screenshot for each). *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: The AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` run on both systems (version output pasted for each). *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: A version manager switches between two Terraform versions on each system where one works; where none does, the write-up says so (output pasted). *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: The pinned dev container starts and runs the same Terraform version (version output pasted). *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: Formatting and validation checks pass on a configuration that creates nothing, on both systems (output pasted). *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: The steps for any operating system you do not own are verified on a second machine or by a second person, or are marked unverified in the write-up. *(DoD-7)*
- [ ] **V8** Capture evidence in write-up section 6 for DoD-8: Your write-up takes a first-time learner on either operating system to DoD-1 through DoD-3 unaided — verified by you following it end to end from a clean state. *(DoD-8)*
- [ ] **V9** Capture evidence in write-up section 6 for DoD-9: Your write-up explains, in your own words, what infrastructure as code is and what Terraform adds to it. *(DoD-9)*

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
