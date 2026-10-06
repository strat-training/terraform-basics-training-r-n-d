# Capstone Tasks

**Objective:** Design, build and release a three-tier online shop of your own choosing on AWS, with a blue/green release you can prove, an off-site copy of its inventory in GCP and its theme and images served from Azure — inside a cost ceiling and with no stored key — on your own, and be able to defend every decision in it, regardless of how the code got typed.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints, the AI-assisted development policy, the rubric, the presentation checks and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Confirm with your trainer: who is on your panel.
- [ ] Confirm with your trainer: the distinction rule for the (D) items, the confirmed Satisfactory and Needs work wording in the rubric, and the cost challenge figures.
- [ ] Confirm with your trainer: where your `data/` folder is.
- [ ] Confirm with your trainer: whether the sandbox allows what your design needs — roles, load balancers, scaling, containers, Storage Transfer, anonymous Blob access — and which fallback applies if it does not.
- [ ] Set up a new GitLab repository for the capstone, separate from your stage practice work.
- [ ] Copy `write-up-template.md` to `write-up.md` in your repository and fill in the header table. Leave the template itself untouched.
- [ ] Read “A note on AI-assisted development” in `brief.md` and decide how you'll log AI interactions as you build, not retroactively at the end.
- [ ] Read the stack constraints in `brief.md` from top to bottom, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.

## Build

- [ ] **TASK-M10-B01** Work on: your cost estimate against the cost challenge, before you build and again when you finish — every billed resource, its hourly rate and the hours you expect it to run.
- [ ] **TASK-M10-B02** Work on: the `foundation` stack, as the brief says what it holds and reads from.
- [ ] **TASK-M10-B03** Work on: the `release` stack, as the brief says what it holds and reads from.
- [ ] **TASK-M10-B04** Work on: your local modules, with typed, validated inputs and documented outputs.
- [ ] **TASK-M10-B05** Work on: the App colours, built from one module called with `for_each`.
- [ ] **TASK-M10-B06** Work on: the `dev` and `prod` variable files, and a backend configuration file for each stack and environment, each with its own state.
- [ ] **TASK-M10-B07** Work on: the input guardrails, so that each variable in the brief's table fails at plan time with a message that states the problem and the allowed values.
- [ ] **TASK-M10-B08** Work on: the cross-variable rules, so that a failing plan reports every broken rule together.
- [ ] **TASK-M10-B09** Work on: failure proofs 1 to 3 and the distinction proof, before the first apply of the environment.
- [ ] **TASK-M10-B10** Work on: the S3 exports bucket, the GCP backup bucket and transfer job, and the Azure storage for the theme and images.
- [ ] **TASK-M10-B11** Work on: the release manifest published to GCP and Azure at every stage.
- [ ] **TASK-M10-B12** Work on: one variable file per stage in `stages/`, release variables only.
- [ ] **TASK-M10-B13** Work on: your release demonstration, running through all seven stages and leaving a record in `evidence/`.
- [ ] **TASK-M10-B14** Work on: stage 0 (Baseline), stage 1 (Warm green), stage 2 (Canary), stage 3 (Half and half) and stage 4 (Cutover), each saved as a plan, applied from the saved plan and confirmed before you move on.
- [ ] **TASK-M10-B15** Work on: stage 5 (Bad release) and stage 6 (Rollback), including the saved state of your failure signal.
- [ ] **TASK-M10-B16** Work on: Demo Challenge tasks 1 to 5, each starting from the end of stage 6.
- [ ] **TASK-M10-B17** Work on: identity and backup proofs A to E.
- [ ] **TASK-M10-B18** Work on: the stock checks.
- [ ] **TASK-M10-B19** Work on: `check.sh`, and fix whatever it fails.
- [ ] **TASK-M10-B20** (Optional) Work on: the (D) items — the traffic-with-nothing-running failure proof, Demo Challenge task 2, and applying `prod` for one hour — once everything required above is solid.
- [ ] **TASK-M10-B21** Commit in stages as you go — not as one commit at the end.
- [ ] **TASK-M10-B22** Destroy the stack the same day you build it, in one pass, then run the teardown scans in all three clouds.

## Verify

- [ ] **TASK-M10-V01** From a clean checkout, confirm both stacks apply with no manual step, and the plan after each apply shows no changes.
- [ ] **TASK-M10-V02** Confirm stages 0 to 6 are evidenced: zero failed requests in stages 0 to 4 and 6, the stage 5 failures confined to v3 orders with your failure signal's state saved, and stage 6 rolled back with one change.
- [ ] **TASK-M10-V03** Confirm the failure proofs, the identity and backup proofs A to E, and the stock checks all pass.
- [ ] **TASK-M10-V04** Confirm Demo Challenge tasks 1 to 5 each have a saved plan and their proof.
- [ ] **TASK-M10-V05** Confirm `check.sh` passes, and no stored key exists anywhere.
- [ ] **TASK-M10-V06** Confirm your platform is inside the cost challenge: the estimate in your write-up agrees with your saved plan.
- [ ] **TASK-M10-V07** Confirm destroy completes in one pass, and the teardown scans show nothing left in AWS, GCP or Azure.
- [ ] **TASK-M10-V08** Before your presentation: pick a few blocks of your own code and evidence at random and practice explaining and changing them unassisted — this is what your panel will do live.

## Write-up

- [ ] **TASK-M10-W01** Under “What I built”, describe your platform: what each stack holds, how your modules divide, how a release moves through it, and where the off-site backup and the Azure assets fit.
- [ ] **TASK-M10-W02** Under “Why it's built this way (key decisions)”, answer every question in the template, including your own cost estimate and where you spent the most time.
- [ ] **TASK-M10-W03** Under “AI collaboration log”, document which tools you used, 2–3 concrete examples of what you asked for, at least one corrected bad suggestion, and what you accepted versus rewrote — capture this as you go, not retroactively.
- [ ] **TASK-M10-W04** Under “How to build it (teach it to the next engineer)”, write a from-scratch guide for the next trainee.
- [ ] **TASK-M10-W05** Under “Concepts worth explaining”, pick 2–3 ideas from across the course and explain them in your own words.
- [ ] **TASK-M10-W06** Under “What tripped me up”, capture the real obstacles, including what the sandbox allowed and what it blocked.
- [ ] **TASK-M10-W07** Under “Checkpoint evidence”, show the evidence the template lists, and keep the saved plans, your release demonstration record and command output in `evidence/`.
- [ ] **TASK-M10-W08** Under “Rubric self-assessment”, score yourself against all three criteria; name any part of your work you'd struggle to explain cold.
- [ ] **TASK-M10-W09** Under “What I'd do differently”, reflect on what you'd change.
- [ ] **TASK-M10-W10** Final self-review: re-read your capstone and write-up against the definition of done and the full six-criteria rubric — confirm you're ready for the live walkthrough, not just that it runs.
