# M06 — Managing Terraform State — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M03) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: What state records and what Terraform uses it for *(scope 1)*
- [ ] **B2** Work on: Secrets and state — what lands in state and who can read it *(scope 2)*
- [ ] **B3** Work on: Inspecting state, read-only *(scope 3)*
- [ ] **B4** Work on: Drift — how it arises and how Terraform detects it *(scope 4)*
- [ ] **B5** Work on: Reconciling drift — deciding whether the code or the real world wins *(scope 5)*
- [ ] **B6** Work on: Why state is never edited by hand *(scope 6)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): What can leak a secret into state, and how would you demonstrate that safely, without using a real credential? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): When Terraform reports drift, who decides whether the code or the real world is right, and on what basis? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): What would you check before trusting a state file you did not create? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): Why does the course treat a state file as sensitive even when the configuration contains no secrets? *(question 4)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: A small configuration taken through an out-of-band change and back to a clean plan *(deliverable)*
- [ ] **C2** Have ready: your written answers to the stage's questions *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: The final plan shows no changes (output pasted). *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: The out-of-band change was detected by Terraform, not just noticed by you — the plan output from before reconciliation is captured. *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: The write-up records which side you let win (code or real world) and why. *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: Evidence shows that a sensitive value can be read from state, captured without exposing a real credential. *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: Your written answers agree with the trainer's model answers on review. *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: State files are excluded from version control (the ignore rule and a clean commit history show it). *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: Everything created is destroyed, confirmed from the cloud side. *(DoD-7)*

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
