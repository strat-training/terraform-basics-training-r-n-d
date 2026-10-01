# M10 — Designing Reusable Terraform Modules — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M05, M06, M07, M08, M09) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: What a module is — the root module, child modules, and what a module call does *(scope 1)*
- [ ] **B2** Work on: Deciding what belongs in a module, and what does not *(scope 2)*
- [ ] **B3** Work on: A module's interface — inputs, outputs, and what it keeps private *(scope 3)*
- [ ] **B4** Work on: Standard module file structure — where inputs, outputs, resources and version requirements live, and why *(scope 4)*
- [ ] **B5** Work on: Naming conventions for a module's inputs, outputs and resources *(scope 5)*
- [ ] **B6** Work on: Comments and documentation — comment syntax, what deserves a comment, and descriptions on inputs and outputs *(scope 6)*
- [ ] **B7** Work on: Calling the same module more than once with different inputs *(scope 7)*
- [ ] **B8** Work on: How modules change resource addresses in a plan and in state *(scope 8)*
- [ ] **B9** Work on: Module sources and versions — local paths versus registry or Git sources, and pinning *(scope 9)*
- [ ] **B10** Work on: Consuming a published module — reading someone else's module before trusting it *(scope 10)*
- [ ] **B11** Work on: What a module may assume about provider configuration *(scope 11)*
- [ ] **B12** Work on: Module anti-patterns — thin wrappers, over-parameterisation, abstractions that hide cloud differences *(scope 12)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): What belongs inside a module and what should stay in the root, and how did you draw that line? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): Which inputs did you expose, which did you fix, and what does each extra input cost the next person who has to understand the module? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): What does a caller need to be told by a module's outputs, and what should stay hidden? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): How should a module's files be laid out so a newcomer finds inputs, outputs and resources without being told? *(question 4)*
- [ ] **D5** Answer, with reasons, in write-up section 2 (Q5): What deserves a comment in a module, and what should the code make obvious without one? *(question 5)*
- [ ] **D6** Answer, with reasons, in write-up section 2 (Q6): How do resource addresses change when something moves into a module, and what would that mean for a configuration that is already deployed? *(question 6)*
- [ ] **D7** Answer, with reasons, in write-up section 2 (Q7): How much do you trust a module you did not write, and what do you check before using it? *(question 7)*
- [ ] **D8** Answer, with reasons, in write-up section 2 (Q8): When is a module the wrong answer? *(question 8)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: A reusable AWS module with a standard file structure and a documented, commented interface, and a root configuration that calls it at least twice with different inputs, deployed with the M08 environment arrangement *(deliverable)*
- [ ] **C2** Have ready: a decision note on what you put in the module and what you left out *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: Formatting and validation checks pass for both the module and the root configuration. *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: The module has a documented interface: every input has a type and a description, inputs that can take a bad value are validated, and every output has a description (a reviewer reads the module). *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: The module follows the standard module layout; a reviewer can find its inputs, outputs, resources and version requirements from file names alone. *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: The names of the module's inputs, outputs and internal resources follow one convention, which your write-up states. *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: The module's comments explain why rather than restate what, and your write-up states which comment syntax you chose and why (a reviewer reads the module). *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: The module is called at least twice with different inputs and both calls produce clean plans (output pasted). *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: The module configures no provider itself and hard-codes no region, account or environment name (a reviewer reads it). *(DoD-7)*
- [ ] **V8** Capture evidence in write-up section 6 for DoD-8: Resource addresses for the separate calls show distinct module paths (state listing pasted). *(DoD-8)*
- [ ] **V9** Capture evidence in write-up section 6 for DoD-9: Resources created through the module still follow M08's naming convention and carry the required tags (shown from the plan, state or cloud side). *(DoD-9)*
- [ ] **V10** Capture evidence in write-up section 6 for DoD-10: The write-up contains a review of one published module — its source, pinned version, inputs and outputs, and what you checked before trusting it. *(DoD-10)*
- [ ] **V11** Capture evidence in write-up section 6 for DoD-11: The decision note says what you put in the module, what you left out, and a case where you would not write a module. *(DoD-11)*
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
