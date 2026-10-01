# M02 — Configuring Providers and Connecting to AWS — tasks

Generated from [brief.md](brief.md) by `/trainee-task-planner`. Work top to bottom and tick each box when it is true. This list contains no answers, no code and no steps: how to do each item is yours to work out, and recording how is the point of the write-up. Do not edit `brief.md`.

Sections 1–4 are the work. Section 5 runs alongside them: update `write-up.md` as you finish each piece, not at the end, and tick each box only when that section is complete and accurate.

## 0. Set up

- [ ] **S1** Read `brief.md` from top to bottom, including its stack constraints and out-of-scope list, and the rules for every stage in the [README](../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build. *(set up)*
- [ ] **S2** Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched. *(set up)*
- [ ] **S3** Confirm that each stage named under "Builds on" in the brief (M01) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build. *(set up)*

## 1. Build — in the brief's scope order

Each task is a topic from the brief's scope. How to approach it is yours to work out.

- [ ] **B1** Work on: Signing in to the AWS sandbox with the access you were given — IAM Identity Center (SSO) through the AWS CLI *(scope 1)*
- [ ] **B2** Work on: Confirming which identity and account Terraform will act as *(scope 2)*
- [ ] **B3** Work on: Credential lifetime — session expiry, its symptoms, and recovering from it *(scope 3)*
- [ ] **B4** Work on: Browser-based sign-in from inside a container or remote workspace *(scope 4)*
- [ ] **B5** Work on: Keeping static access keys off disk and out of the repository *(scope 5)*
- [ ] **B6** Work on: What a provider is and how Terraform finds and installs one *(scope 6)*
- [ ] **B7** Work on: Version constraints — for Terraform itself and for each provider *(scope 7)*
- [ ] **B8** Work on: The dependency lock file — what it records and why it is committed *(scope 8)*
- [ ] **B9** Work on: Using more than one provider in a single configuration *(scope 9)*
- [ ] **B10** Work on: Provider configuration — how a provider obtains its credentials, and provider-level default tags *(scope 10)*
- [ ] **B11** Work on: Inspecting which providers and versions a configuration actually uses *(scope 11)*
- [ ] **B12** Work on: Upgrading a pinned version deliberately *(scope 12)*

## 2. Decide — the brief's open design questions

- [ ] **D1** Answer, with reasons, in write-up section 2 (Q1): What does a learner see when their session has expired, and how will you help them tell that apart from a genuine permissions problem? *(question 1)*
- [ ] **D2** Answer, with reasons, in write-up section 2 (Q2): What can go wrong when you sign in from inside a container rather than on the host? *(question 2)*
- [ ] **D3** Answer, with reasons, in write-up section 2 (Q3): How does the AWS provider decide which credentials to use, and how would you prove which identity a plan is using? *(question 3)*
- [ ] **D4** Answer, with reasons, in write-up section 2 (Q4): What is the difference between a version constraint you declare and what the lock file records, and why does the course want both? *(question 4)*
- [ ] **D5** Answer, with reasons, in write-up section 2 (Q5): How loose or tight should a provider constraint be, and who carries the risk of each choice? *(question 5)*
- [ ] **D6** Answer, with reasons, in write-up section 2 (Q6): Why set tags at the provider rather than on each resource, and what would make you tag a resource individually anyway? *(question 6)*
- [ ] **D7** Answer, with reasons, in write-up section 2 (Q7): What should a reviewer look for in a merge request that changes the lock file? *(question 7)*

## 3. Deliver — the named deliverable

- [ ] **C1** Have ready: A signed-in sandbox session and a minimal Terraform configuration that uses the `aws` and `random` providers *(deliverable)*
- [ ] **C2** Have ready: Terraform and provider versions pinned, the lock file committed, and default tags configured on the AWS provider *(deliverable)*

## 4. Verify — the definition of done

- [ ] **V1** Capture evidence in write-up section 6 for DoD-1: An authenticated AWS sandbox session exists and a caller-identity query returns the sandbox identity (output pasted, account details redacted as the trainer directs). *(DoD-1)*
- [ ] **V2** Capture evidence in write-up section 6 for DoD-2: You have caused a session to fail, captured the symptom, and recovered; the write-up records both. *(DoD-2)*
- [ ] **V3** Capture evidence in write-up section 6 for DoD-3: No static access keys are present in your AWS configuration on disk or in your repository; your evidence shows the scan you ran and what it looked for. *(DoD-3)*
- [ ] **V4** Capture evidence in write-up section 6 for DoD-4: Signing in also works from inside the dev container, or your write-up records exactly what blocked it (output pasted). *(DoD-4)*
- [ ] **V5** Capture evidence in write-up section 6 for DoD-5: The configuration declares a required Terraform version and, for every provider it uses, a source and a version constraint. *(DoD-5)*
- [ ] **V6** Capture evidence in write-up section 6 for DoD-6: The lock file exists and is committed to version control (it appears in your commit). *(DoD-6)*
- [ ] **V7** Capture evidence in write-up section 6 for DoD-7: The provider listing for the configuration shows both `aws` and `random` (output pasted). *(DoD-7)*
- [ ] **V8** Capture evidence in write-up section 6 for DoD-8: Formatting and validation checks pass with no errors (output pasted). *(DoD-8)*
- [ ] **V9** Capture evidence in write-up section 6 for DoD-9: Default tags are configured on the AWS provider and the plan shows them on at least one taggable resource the configuration would create (plan excerpt). *(DoD-9)*
- [ ] **V10** Capture evidence in write-up section 6 for DoD-10: One deliberate version change is shown with its effect on the lock file (before and after). *(DoD-10)*
- [ ] **V11** Capture evidence in write-up section 6 for DoD-11: No resources exist in the sandbox as a result of this stage, confirmed from the cloud side. *(DoD-11)*

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
