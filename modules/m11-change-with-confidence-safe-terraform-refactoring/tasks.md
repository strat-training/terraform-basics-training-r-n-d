# M11 — Change with Confidence: Safe Terraform Refactoring — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M03, M06, M07, M10) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: Why refactoring must never mean destroy-and-recreate *(scope 1)*
- [ ] **B2** Work on: Renaming or re-addressing a resource without replacing it *(scope 2)*
- [ ] **B3** Work on: Adopting an existing, unmanaged resource into Terraform *(scope 3)*
- [ ] **B4** Work on: Tidying generated configuration *(scope 4)*
- [ ] **B5** Work on: Ceasing to manage a resource without destroying it *(scope 5)*
- [ ] **B6** Work on: Verifying every refactor with a plan — zero destroys, zero replacements *(scope 6)*
- [ ] **B7** Work on: Reading a saved plan as JSON with `jq` — checking the action on every resource mechanically *(scope 7)*
- [ ] **B8** Work on: Targeted operations — an emergency tool, never routine *(scope 8)*
- [ ] **B9** Work on: Reading legacy guidance that relies on imperative state commands *(scope 9)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): How can you tell, before applying, that a refactor will not touch real infrastructure? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): What did the generated configuration get wrong or leave out, and how did you decide what to keep? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): When a resource stops being managed, what is responsible for it afterwards, and how do you avoid orphaning cost? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): Why does the course prefer changes that appear in a plan over commands that edit state, and when might you still see those commands? *(question 4)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: Three refactors applied to a small configuration — a rename, an adoption and a stop-managing — each verified by a plan with no destroys and no replacements *(deliverable)*
- [ ] **C2** Have ready: a short note on legacy imperative commands *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: After each of the three refactors, a saved plan shows zero destroys and zero replacements (three plan summaries pasted). *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: At least one of the three plan checks reads the saved plan's JSON form with `jq` and reports the action on every resource (output pasted). *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: The renamed resource keeps its real-world identity (its cloud-side identifier is unchanged). *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: The adopted resource is in state and described by configuration, and a plan after adoption shows no changes. *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: The stop-managing resource still exists in AWS afterwards and Terraform no longer tracks it. *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: Each refactor is visible as a reviewable change in configuration (the diff is in your evidence). *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: Your write-up declares that no state-mutating command was used for any refactor. *(DoD-7)*
- [ ] **V8** Capture evidence in write-up section 6 for DoD-8: Your note on legacy imperative commands says when you will meet them and what the declarative equivalent is. *(DoD-8)*
- [ ] **V9** Capture evidence in write-up section 6 for DoD-9: No billable resource is left behind, including anything Terraform no longer manages; only the M07 bucket remains. *(DoD-9)*

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
