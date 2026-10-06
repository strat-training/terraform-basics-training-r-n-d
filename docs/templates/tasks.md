# <Stage ID> — <Stage title> — Tasks

<!--
TEMPLATE: stage checklist. Do not fill this in by hand for a stage: run `/trainee-task-planner
<stage-folder>` (see trainee-task-planner.md in this folder), which fills it from the stage's brief
and write-up template and checks it for leaked answers.

Every line below that is not a heading, a frame or a placeholder is fixed text. Placeholders are
filled only with text copied word for word from the brief or the write-up template. A task never
holds code, a name the brief does not use, a design choice, a hint or an explanation.

Every task outside Setup starts with an ID, TASK-<stage>-<letter><nn>: B for Build, V for Verify and W for
Write-up, counting up from 01 within each section (the closing self-review is the last W). Setup tasks have no ID.
-->

**Objective:** <the brief's Objective paragraph, verbatim>

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (<Builds on value>) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] **TASK-<Stage ID>-B01** Work on: <scope topic title, verbatim — one task per scope bullet, in the brief's order>
- [ ] **TASK-<Stage ID>-B02** Have ready: <deliverable component, verbatim — one task per component>

## Verify

- [ ] **TASK-<Stage ID>-V01** Confirm <DoD-nn>: <definition-of-done bullet, verbatim, with the label the brief gives it> Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] **TASK-<Stage ID>-W01** Under “<template heading>”: <the template's guidance for that section, verbatim, shortened to its first two sentences if longer — one task per `##` section of the write-up template, in the template's order>
- [ ] **TASK-<Stage ID>-W02** Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
