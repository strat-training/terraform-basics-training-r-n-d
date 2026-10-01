# M03 — Understanding the Terraform Workflow — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M02) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: Declarative versus imperative infrastructure — what it means that Terraform describes desired state *(scope 1)*
- [ ] **B2** Work on: Anatomy of a resource — type, name, arguments and attributes *(scope 2)*
- [ ] **B3** Work on: The core workflow — initialise, plan, apply, destroy *(scope 3)*
- [ ] **B4** Work on: What a plan shows — reading the action for each resource *(scope 4)*
- [ ] **B5** Work on: In-place updates versus replacement *(scope 5)*
- [ ] **B6** Work on: What causes a replacement *(scope 6)*
- [ ] **B7** Work on: Plan review as a habit — what to check before approving *(scope 7)*
- [ ] **B8** Work on: Destroying what you created *(scope 8)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): How does describing the desired state differ from scripting the steps, and what does that change about running the same configuration twice? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): How can you tell from the plan alone that a change will destroy something, before you apply it? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): For your chosen resource, which changes are made in place and which force replacement — how did you establish that, and how sure are you? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): What would you do if a plan showed a destroy you did not expect? *(question 4)*
- [ ] **D5** Answer, with reasons, in write-up section 2 (Q5): What does a replacement cost when the resource holds data or other resources depend on it? *(question 5)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: A configuration managing one small AWS resource, taken through create, in-place change, forced replacement and destroy *(deliverable)*
- [ ] **C2** Have ready: a written plan-review note *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: Formatting and validation checks pass with no errors. *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: You ran the same apply twice without changing the configuration; both outputs are pasted, and the write-up explains the difference between them in terms of desired state. *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: Your write-up identifies the type, name, arguments and attributes of your resource, and shows an attribute whose value you did not set. *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: You made at least one in-place change and at least one forced replacement; the plan output for each was captured before it was applied. *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: Your plan-review note classifies every change you made as in-place or replacement, and the trainer's model answer agrees with each classification. *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: For each classification the note explains the cause in terms of the resource itself, not just the plan's symbols. *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: After destroy the resource is gone — confirmed from the cloud side, not only from Terraform's output. *(DoD-7)*

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
