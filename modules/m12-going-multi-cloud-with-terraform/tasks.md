# M12 — Going Multi-Cloud with Terraform — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M01, M02) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: Confirming access to the GCP and Azure sandboxes *(scope 1)*
- [ ] **B2** Work on: GCP — Application Default Credentials sign-in, explicit project, provider configuration *(scope 2)*
- [ ] **B3** Work on: Azure — CLI sign-in, explicit subscription, provider configuration *(scope 3)*
- [ ] **B4** Work on: Read-only data sources as a safe proof of identity *(scope 4)*
- [ ] **B5** Work on: Sign-in modes for when no browser is available — inside a container or remote workspace *(scope 5)*
- [ ] **B6** Work on: Where the clouds differ, stated explicitly — no abstraction layer *(scope 6)*
- [ ] **B7** Work on: The `gcs` and `azurerm` state backends — reference only *(scope 7)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): What can go wrong if the ambient login points at a different project or subscription than you intended, and what in your configuration prevents it? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): What stays the same across all three clouds in the Terraform workflow, and what changes? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): Why does the course refuse to hide cloud differences behind a common wrapper? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): Where should state live for a configuration that creates nothing, and does your answer change once it does? *(question 4)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: Two small Terraform configurations, one per cloud, each authenticating with a short-lived login and outputting the identity it runs as *(deliverable)*
- [ ] **C2** Have ready: a written comparison of how the clouds differ in setup *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: Both configurations pass formatting and validation checks. *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: Both configurations plan successfully and the plan output includes an identity output for each cloud (output pasted). *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: The GCP project and the Azure subscription are set explicitly in configuration. *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: No secrets or keys exist in the repository or on disk (the scan you ran is in your evidence). *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: Neither configuration creates a resource (the plan shows nothing to add). *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: Your written comparison of cloud differences agrees with the trainer's model answer on review. *(DoD-6)*

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
