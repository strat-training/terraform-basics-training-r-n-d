---
name: em-files-generator
description: Scaffold a Build-to-Teach course's EM files — the root README.md and a stage's brief.md, write-up-template.md and tasks.md — by inferring the stage, and the stage list if the repo has none yet, from the course's design documents (docs/arch-docs and the rest of docs/), as an EVALUATE → stop → PLAN → stop → APPLY → VALIDATE cycle run through the EM-files-generator agent and the task planner. Creates a new stage folder or regenerates an existing one. Stages only, never the capstone.
argument-hint: <stage> | all
---

# /em-files-generator

**Stage scaffold** — generates the files the EM owns — the course's root `README.md`, and for a stage its `brief.md`, `write-up-template.md` and `tasks.md` — by inferring the stage from the course's design documents: the solution design, PRD and ADRs in `docs/arch-docs/`, the framework, and whatever else under `docs/` bears on it. It works in a repo that has only `docs/`: with no README, no `modules/` and no Stages table, it infers the stage list too and writes the README that carries it. It is shaped like `/scaffold`: EVALUATE, stop for confirmation, PLAN, stop for approval, APPLY, VALIDATE. It is self-contained: it does not call `/evaluate`, `/plan`, `/apply` or `/validate`, which are for code tasks.

**Goal: structure and standards, not lessons.** Every file is written for the trainee and hands them a problem and never a solution. No lesson content, no steps beyond the lab, no code, no answers to a research prompt.

**Inference is shown, never hidden.** Every item in the EVALUATE summary and the PLAN carries where it came from (a design-document section, an ADR, the existing README or brief) or is marked `[inferred — confirm]` and raised as a question. Nothing inferred is written until you approve it.

## Course layout

Folder and file names (the source documents, the stage list, the stages folder, the templates, how the capstone is recognised, the task planner command) are set once, in the "Course layout" section at the top of the `EM-files-generator` agent. When you copy this command to another course, change them there; this command follows the agent. `docs/curriculum.md` is not a source.

## Usage

- `/em-files-generator <stage>` — scaffold one stage. `<stage>` is its ID (`M05`), a unique prefix of its folder name, its folder name, or its title. With no Stages table and no stage folders, the stage list is inferred from the design documents and `M01` is the first stage in it; a title and theme after the argument (for example `/em-files-generator "Using Secrets Safely" — keeping credentials out of state and code`) override the inference. A stage that has no folder yet gets one, and `modules/` if needed; a stage that has files gets them regenerated.
- `/em-files-generator all` — every stage in the Stages table, or in the inferred stage list, except the capstone. One combined EVALUATE and PLAN, one stop for each, then the stages are applied one at a time.

With no argument, ask which stage; do not guess. Existing files are overwritten only after you approve the PLAN, which lists each file as new or regenerate. To keep an existing file (for example a README or brief you have edited by hand), say so at the PLAN stop and it becomes a source, not an output. An existing README is updated narrowly (its Stages table, order note and any rule an ADR contradicts), and any capstone section in it is never touched.

## Prerequisites — check before doing anything else

Only two are hard:

1. `docs/arch-docs/` holds a design document (a solution design, a PRD or both). If it does not, stop: "Add the solution design to `docs/arch-docs/` first — there is nothing to infer from."
2. The README template (`docs/templates/course-readme.md`), the brief template, the sample brief and the master write-up template exist. If one is missing, stop and name it.

Everything else is **soft**: report it in the EVALUATE summary under "Missing inputs", use the fallback, and carry on. Do not stop, and do not ask for a title before the EVALUATE stop. **The README is not a prerequisite: it is one of the files this command writes.**

| Missing | Fallback |
| --- | --- |
| Stages table and stage folders | The stage list is inferred from the design documents and confirmed by the EM at the EVALUATE stop. |
| `modules/` | Created with the stage folder. |
| Root `README.md` | Generated from `docs/templates/course-readme.md`, with the stage list, the course-wide rules from the ADRs and the stage rubric, before the brief that links to it. |
| `/trainee-task-planner` in `.claude/commands/` | Read its tracked copy, `docs/templates/trainee-task-planner.md`, and follow it directly for step 3.2 below. If neither exists, skip `tasks.md` and say so. |
| Framework document, PRD, ADRs | Read what exists, and say what was missing. |

The capstone is out of scope. If the argument is the capstone, stop and say so; `all` skips it.

---

## Steps

### 1 — EVALUATE

Launch the `EM-files-generator` agent (Agent tool, `subagent_type: "EM-files-generator"`) in **plan** mode and ask for the EVALUATE SUMMARY. Output it as it came back: what it read, the stage's identity, the stage map (content, constraints and evidence seeds, each with its source), Proposed ADRs it would depend on, how any existing files differ, documents that disagree, everything marked inferred, and its questions.

**Stop. Do not plan.** End with:

> "Ready to plan. Reply to proceed with PLAN, or give feedback to redo EVALUATE."

Answer each question from the EM's reply, or ask the EM. Never guess a scope decision.

### 2 — PLAN

Run the agent again in plan mode with the EM's answers and ask for the PLAN blueprint. Output it as it came back: all the files, each marked new, regenerate or keep, section by section for the README and the brief with their provenance, the write-up template's fill-ins, the planner's task counts, the overlap check, the inferred items and the blast radius. Nothing has been written.

**Stop. Do not apply.** End with:

> "Waiting for approval. Reply to apply, or give feedback to revise the plan."

Feedback means run plan mode again with it and show the new blueprint. Never edit the blueprint yourself. For `all`, show one blueprint per stage in the same message.

### 3 — APPLY (only after approval)

1. Launch the agent in **apply** mode with the stage and the approved blueprint exactly as shown, including any change the EM asked for. It writes `README.md`, then `brief.md`, then `write-up-template.md`, and stops. The files carry no ADR numbers or citations: those stay in the plan. Output its APPLY COMPLETE block.
2. Run the task planner for the stage: `/trainee-task-planner <stage-folder>`, or `/trainee-task-planner re-plan <stage-folder>` if `tasks.md` already exists. If the command is not installed, read `docs/templates/trainee-task-planner.md` and follow its four steps yourself, in the same unattended way; do not copy it into `.claude/commands/` unless the EM asks. Tell it the EM has approved the scaffold plan, that `brief.md` and `write-up-template.md` are the files just written, and that it should run all four of its steps without pausing and report. If the planner stops on a prerequisite, report why and go no further.

For `all`, repeat both steps for one stage at a time, in the order of the Stages table.

### 4 — VALIDATE

Launch the agent in **validate** mode. It re-reads all the files from disk, runs its mechanical checks first (README headings, Stages table, links and rubric; brief sections, scope against the plan, definition-of-done labels, no citations in the brief, template headings and fixed text, tasks coverage), then reviews the brief for lines that answer their own research prompts or contradict an Accepted ADR, the template for overlap between questions and concepts, and `tasks.md` against the master. It classifies issues as [BLOCKER], [FIX NOW] or [BACKLOG], and fixes the first two in `brief.md` and `write-up-template.md`. Output its VALIDATE COMPLETE block as it came back, without adding claims it did not verify.

If it finds a problem in `tasks.md`, report it and offer to re-run the planner. Do not patch the file.

Then tell the EM, one line each:
- The README was written or updated, with its Stages table carrying the stage list, so later runs use the same list. Stages not yet scaffolded show plain titles and no links until they are.
- Any Proposed ADR the brief relies on, which still needs the program owner's sign-off.
- Anything that needs a template or planner change: README or task wording that describes the write-up differently from the master, such as a Status field or a header table.
- Trainer and maintainer notes belong in `docs/README.md`, which this command does not write.
- The README has no capstone section unless it already had one: the capstone is not generated here.
- Nothing has been committed.

> "Task complete."

## Abort at any step

If the user says "stop", "abort" or "cancel" at any point, stop immediately and summarise what was written and what was not.

## Scope discipline

One stage at a time. This command never edits the design documents, the framework, a template, the curriculum, `docs/README.md`, a trainee's `write-up.md`, or any other stage's files. If something outside its files turns up (a gap in the design documents, a neighbouring stage that needs a change), report it and leave it alone.
