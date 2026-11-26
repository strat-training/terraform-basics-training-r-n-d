# Templates

Reusable starting points for new stages and capstones. Copy one into the folder it is for and replace every `<placeholder>`; each template carries its own guidance in an HTML comment at the top, which you delete when you are done. Nothing here is a live stage: the links inside these files are written for the folder the copy lands in.

| Template | Copy it to | Used for |
| --- | --- | --- |
| [brief-sample.md](brief-sample.md) | — | A sample brief from another course, kept as the model for the structure and tone of every stage brief |
| [brief.md](brief.md) | `modules/<stage-folder>/brief.md` | A stage brief, in the structure and tone of the sample: objective, scope with research prompts, stack constraints, named deliverable, definition of done, best practices, what to confirm with the trainer |
| [write-up-template.md](write-up-template.md) | `modules/<stage-folder>/write-up-template.md` | The blank write-up for a stage, generated from its brief |
| [tasks.md](tasks.md) | `modules/<stage-folder>/tasks.md` | The shape of a stage checklist. Generate it with the planner rather than filling it in by hand |
| [capstone-brief.md](capstone-brief.md) | `modules/m10-capstone/brief.md` | A capstone brief: AI-assisted development policy, requirements, presentation, rubric |
| [capstone-write-up-template.md](capstone-write-up-template.md) | `modules/m10-capstone/write-up-template.md` | The blank write-up for a capstone |
| [capstone-tasks.md](capstone-tasks.md) | `modules/m10-capstone/tasks.md` | The shape of a capstone checklist, written by hand |
| [course-readme.md](course-readme.md) | `README.md` (repository root) | The trainee-facing course README: how a stage works, the stages, the capstone, the rules and the stage rubric |
| [trainee-task-planner.md](trainee-task-planner.md) | `.claude/commands/trainee-task-planner.md` | The `/trainee-task-planner` command, which generates a stage checklist without leaking answers |
| [em-files-generator.md](em-files-generator.md) | `.claude/commands/em-files-generator.md` | The `/em-files-generator` command, which scaffolds the root `README.md` and a stage's `brief.md`, `write-up-template.md` and `tasks.md` by inferring the stage from the design documents in `docs/arch-docs/` |
| [em-files-generator-agent.md](em-files-generator-agent.md) | `.claude/agents/EM-files-generator.md` | The agent that `/em-files-generator` runs |
| [checkstage.md](checkstage.md) | `.claude/commands/checkstage.md` | The `/checkstage` command, a read-only check of a stage's template and files and of a trainee's write-up |
| [checkstage-agent.md](checkstage-agent.md) | `.claude/agents/learning-modules-and-writeup-checker.md` | The agent that `/checkstage` runs |
| [build-to-teach-playbook.md](build-to-teach-playbook.md) | — | The step-by-step prompt sequence for building a course repository like this one, for another trainer to reuse |

## The planner command

[trainee-task-planner.md](trainee-task-planner.md) is a copy of `.claude/commands/trainee-task-planner.md`. The command only runs from `.claude/commands/`, and that folder is not tracked in git, so this copy is the one that is kept. If you change the command, copy it here too, or the two will drift.

To use it on a new machine, copy it into `.claude/commands/`. It reads a stage's `brief.md` and `write-up-template.md` and writes `tasks.md` beside them. It covers stage briefs only.

## The generator and the checker

`/em-files-generator` scaffolds the course's root `README.md` and a stage's three files, `brief.md`, `write-up-template.md` and `tasks.md`, by inferring the stage from the design documents in `docs/arch-docs/` (the solution design and the ADRs) and the rest of `docs/`. Every inferred item is shown with its source, or marked for you to confirm. The README is cut from [course-readme.md](course-readme.md) and carries the stage list, the course-wide rules and the rubric. The write-up template is cut from the master, [write-up-template.md](write-up-template.md) in this folder, and `tasks.md` is written by `/trainee-task-planner`, which the command runs for you. It is shaped like `/scaffold`: it shows what it found and stops, shows its plan and stops, and only writes or overwrites a file after you approve. `/checkstage` checks that template against the master and the brief, checks that the brief and `tasks.md` agree with it, and checks a trainee's filled-in `write-up.md` if there is one. It reports and never edits, and follows the same cycle: it shows its plan, then waits for your go (add `go` to the command to skip the wait, since nothing is written). Each command runs an agent of its own, so install both files of a pair.

The four files here are copies, kept for the same reason as the planner copy above: `.claude/` is not tracked in git. If you change one in `.claude/`, copy it here too, or the two will drift.

To use them on a new machine or in another course, copy each file to the place the table gives. Both agents start with a "Course layout" section that names the stages folder, the master template, the course README, how the capstone is recognised and the planner command. Change those lines to match the new course; the commands follow the agents, and the rest needs no editing. The agents read the master fresh on every run, so editing the master is enough to change what they generate and check.

## Starting a course

Follow [build-to-teach-playbook.md](build-to-teach-playbook.md): it settles the decisions to make first, then takes you from the stage list to a validated repository, one prompt at a time, using the templates in this folder.

`/em-files-generator` writes the root `README.md` from `course-readme.md`, so you do not need to copy it by hand (copy it yourself only if you are not using the generator). It is written for the trainee, so keep trainer and maintainer notes out of it and put them in `docs/README.md`. Keep its "Rules for every stage" heading, because the stage checklists link to it.

## Adding a stage

1. Make sure `docs/arch-docs/` covers the stage. You do not need a README, a Stages table or a `modules/` folder first: with none of them, the generator proposes the stage list from the documents for you to confirm.
2. Run `/em-files-generator <stage>`. Read what it found and reply, read its plan and reply `apply`. It writes the root `README.md` (the Stages table, the rules for every stage and the rubric), then `brief.md` and `write-up-template.md` in a new folder under `modules/`, and then runs the task planner for `tasks.md`.
3. Read the brief. The objective, research prompts, constraints and definition of done are inferred from the design documents, so they are the generator's draft; anything marked inferred needs your confirmation. Check that no scope description, constraint or definition-of-done bullet answers one of the research prompts.
4. Run `/checkstage <stage-folder>` and fix anything it reports.
5. Check the root [README](../../README.md) the generator wrote: its Stages table, its rules for every stage and its rubric. It has no capstone section unless it already had one.

## Adding a capstone

Copy `capstone-brief.md`, `capstone-write-up-template.md` and `capstone-tasks.md` into `modules/m10-capstone/` and fill them in. The capstone is marked against its rubric and confirmed in a presentation, so its checklist is written by hand rather than generated.
