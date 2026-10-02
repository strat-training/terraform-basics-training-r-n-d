# Trainer and maintainer notes

Material for the people who run and maintain the course. Trainees do not need it: their guide is the [root README](../README.md).

| Path | What it holds |
| --- | --- |
| [templates/](templates/README.md) | Reusable templates for a stage brief, a capstone brief, the write-ups and the checklists, and a copy of the planner command |
| `arch-docs/` | The design documents behind the course (trainers only) |
| `build-to-teach-framework/`, [build-to-teach-playbook.md](build-to-teach-playbook.md) | The framework and the original prompt playbook that produced this structure. The framework calls the trainer the EM. The updated, reusable playbook for other trainers is [templates/build-to-teach-playbook.md](templates/build-to-teach-playbook.md) |
| [../knowledge/retros/](../knowledge/retros/2026-10-02-briefs-that-answer-their-own-questions.md) | Findings worth keeping, such as briefs that answer their own questions |
| `../.claude/commands/` | Project commands, including `/trainee-task-planner`. This folder is not tracked in git, so the planner is also kept as [a copy in `templates/`](templates/trainee-task-planner.md) |

## Keeping the stage files in step

- A stage's `tasks.md` is generated from its brief. After a brief changes, regenerate it with `/trainee-task-planner re-plan <stage>`. The capstone's checklist is written by hand, from the capstone templates.
- A stage's `write-up-template.md` is generated from its brief too: its design questions, scope items and definition-of-done items are copied word for word.
- The briefs say nothing about how to build a stage. Before you change one, check that no scope item, constraint or definition-of-done line answers one of its open design questions.
- The capstone's `data/` folder (the application in three versions, a starter catalogue, a starter theme and images, an optional `probe.sh`, and `check.sh`) and `versions.env` are supplied by the trainer and are not in this repository yet.
