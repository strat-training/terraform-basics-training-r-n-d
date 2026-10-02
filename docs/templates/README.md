# Templates

Reusable starting points for new stages and capstones. Copy one into the folder it is for and replace every `<placeholder>`; each template carries its own guidance in an HTML comment at the top, which you delete when you are done. Nothing here is a live stage: the links inside these files are written for the folder the copy lands in.

| Template | Copy it to | Used for |
| --- | --- | --- |
| [brief.md](brief.md) | `modules/<stage-folder>/brief.md` | A stage brief: objective, scope, stack constraints, named deliverable, open design questions, definition of done |
| [write-up-template.md](write-up-template.md) | `modules/<stage-folder>/write-up-template.md` | The blank write-up for a stage, generated from its brief |
| [tasks.md](tasks.md) | `modules/<stage-folder>/tasks.md` | The shape of a stage checklist. Generate it with the planner rather than filling it in by hand |
| [capstone-brief.md](capstone-brief.md) | `modules/capstone/brief.md` | A capstone brief: AI-assisted development policy, requirements, presentation, rubric |
| [capstone-write-up-template.md](capstone-write-up-template.md) | `modules/capstone/write-up-template.md` | The blank write-up for a capstone |
| [capstone-tasks.md](capstone-tasks.md) | `modules/capstone/tasks.md` | The shape of a capstone checklist, written by hand |
| [course-readme.md](course-readme.md) | `README.md` (repository root) | The trainee-facing course README: how a stage works, the stages, the capstone, the rules and the stage rubric |
| [trainee-task-planner.md](trainee-task-planner.md) | `.claude/commands/trainee-task-planner.md` | The `/trainee-task-planner` command, which generates a stage checklist without leaking answers |
| [build-to-teach-playbook.md](build-to-teach-playbook.md) | — | The step-by-step prompt sequence for building a course repository like this one, for another trainer to reuse |

## The planner command

[trainee-task-planner.md](trainee-task-planner.md) is a copy of `.claude/commands/trainee-task-planner.md`. The command only runs from `.claude/commands/`, and that folder is not tracked in git, so this copy is the one that is kept. If you change the command, copy it here too, or the two will drift.

To use it on a new machine, copy it into `.claude/commands/`. It reads a stage's `brief.md` and `write-up-template.md` and writes `tasks.md` beside them. It covers stage briefs only.

## Starting a course

Follow [build-to-teach-playbook.md](build-to-teach-playbook.md): it settles the decisions to make first, then takes you from the stage list to a validated repository, one prompt at a time, using the templates in this folder.

Copy `course-readme.md` to the repository root as `README.md` and fill it in. It is written for the trainee, so keep trainer and maintainer notes out of it and put them in `docs/README.md`. Keep its "Rules for every stage" heading, because the stage checklists link to it.

## Adding a stage

1. Copy `brief.md` into a new folder under `modules/` and fill it in. Check that no scope item, constraint or definition-of-done line answers one of the open design questions.
2. Copy `write-up-template.md` beside it and fill it in from the brief: its open design questions, scope items and definition-of-done items, word for word.
3. Run `/trainee-task-planner <stage-folder>` to generate `tasks.md`.
4. Add the stage to the table in the root [README](../../README.md).

## Adding a capstone

Copy `capstone-brief.md`, `capstone-write-up-template.md` and `capstone-tasks.md` into `modules/capstone/` and fill them in. The capstone is marked against its rubric and confirmed in a presentation, so its checklist is written by hand rather than generated.
