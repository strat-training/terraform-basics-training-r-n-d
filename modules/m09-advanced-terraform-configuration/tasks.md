# M09 — Advanced Terraform Configuration — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M04, M05, M06) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: Composing built-in functions to derive values *(scope 1)*
- [ ] **B2** Work on: Conditional expressions — and when a condition belongs in configuration at all *(scope 2)*
- [ ] **B3** Work on: `for` expressions and splat expressions — reshaping collections *(scope 3)*
- [ ] **B4** Work on: `for_each` in depth — maps, sets and derived collections, and what makes a key stable *(scope 4)*
- [ ] **B5** Work on: Dynamic blocks — generating repeated nested blocks from data *(scope 5)*
- [ ] **B6** Work on: Data sources in depth — beyond the basic lookup introduced in M04 *(scope 6)*
- [ ] **B7** Work on: Explicit dependencies with `depends_on` — when a reference cannot express the ordering *(scope 7)*
- [ ] **B8** Work on: The `lifecycle` block — controlling replacement, destruction and ignored changes *(scope 8)*
- [ ] **B9** Work on: Preconditions and postconditions — checking assumptions about real infrastructure *(scope 9)*
- [ ] **B10** Work on: When a feature costs more readability than it saves *(scope 10)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): What should the keys of a repeated resource be, and what happens to the real infrastructure when a key changes? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): When does a dynamic block make a configuration clearer, and when does it make it harder to review than the repetition it replaced? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): Which values should be derived inside the configuration, and which should the caller supply? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): When is a condition in the configuration the wrong tool? *(question 4)*
- [ ] **D5** Answer, with reasons, in write-up section 2 (Q5): Where did you have to state a dependency explicitly rather than rely on a reference, and how did you decide that was genuinely needed? *(question 5)*
- [ ] **D6** Answer, with reasons, in write-up section 2 (Q6): Which resources, if any, should be protected from replacement or destruction, which changes should Terraform ignore, and what does each cost the next person who has to change them? *(question 6)*
- [ ] **D7** Answer, with reasons, in write-up section 2 (Q7): What assumption about real infrastructure is worth checking in your configuration, where does the check belong, and what should happen when it fails? *(question 7)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: A data-driven AWS configuration in which resources and nested blocks are generated from structured input instead of repeated by hand *(deliverable)*
- [ ] **C2** Have ready: derived values, a conditional, a data-source lookup, dependency and lifecycle controls, and checks on its own assumptions *(deliverable)*
- [ ] **C3** Have ready: a readability note on where each feature helped and where it hurt *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: Formatting and validation checks pass with no errors. *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: At least one resource is repeated from a structured input — a map, or a collection derived from one — and your write-up justifies the keys you chose. *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: At least one resource has repeated nested blocks generated from the same structured input, and the plan shows the expected number of them (plan excerpt). *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: Adding an entry, removing an entry and changing a key in the input each produce a plan you have captured, and your write-up says exactly what each plan would do to the real infrastructure. *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: Derived values are defined once and used in more than one place, and no expression is duplicated across files (a reviewer reads the configuration). *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: At least one conditional changes what the configuration creates or sets, and the plan is shown for both outcomes of the condition (two plan excerpts). *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: A data source supplies a value the configuration uses, and no equivalent value is hard-coded (a reviewer reads the configuration). *(DoD-7)*
- [ ] **V8** Capture evidence in write-up section 6 for DoD-8: Every explicit dependency in the configuration is justified in the write-up; if there are none, the write-up says why a reference was always enough. *(DoD-8)*
- [ ] **V9** Capture evidence in write-up section 6 for DoD-9: Every lifecycle setting you used is justified in the write-up, and its effect is shown from a plan or a deliberate attempt that it affects (output pasted). *(DoD-9)*
- [ ] **V10** Capture evidence in write-up section 6 for DoD-10: At least one precondition or postcondition is in place, and you have deliberately triggered it and captured the failure message (output pasted). *(DoD-10)*
- [ ] **V11** Capture evidence in write-up section 6 for DoD-11: Your readability note says, for each advanced feature you used, where it helped and where it made the configuration harder to follow. *(DoD-11)*
- [ ] **V12** Capture evidence in write-up section 6 for DoD-12: Everything is destroyed except the M07 bucket, confirmed from the cloud side. *(DoD-12)*

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
