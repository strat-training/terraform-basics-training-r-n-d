# Build-to-Teach Playbook — building a course repository like this one

A reusable, step-by-step guide for a trainer who wants to run a Build-to-Teach research-and-development course for any technical subject: trainees build real things from briefs, write up how as they go, and the finished pairs become the next cohort's teaching material. Each prompt is in its own block. Replace every `<…>` placeholder, copy the whole block and send it as it is.

This playbook is the prompt sequence that produced this repository, with what that run taught us added.

## What you end up with

```
README.md                        — the trainee's guide: how a stage works, the stages, the capstone, the rules, how review works
modules/
  m01-<stage-title>/
    brief.md                     — your handoff: objective, scope, constraints, deliverable, questions, definition of done
    write-up-template.md         — blank; the trainee fills in a copy as they build
    tasks.md                     — a generated checklist that restates the brief and answers nothing
  m02-<stage-title>/ …
  capstone/
    brief.md  tasks.md  write-up-template.md
docs/
  README.md                      — trainer and maintainer notes
  templates/                     — the templates, the planner command and this playbook
knowledge/retros/                — findings worth keeping
.claude/commands/
  trainee-task-planner.md        — generates tasks.md without leaking answers
```

## The ideas it rests on

- **A brief hands over a problem, never a solution.** Objective, scope, constraints, a named deliverable, open design questions and an observable definition of done. No lesson, no steps, no code.
- **Build and write-up are one piece of work.** The trainee writes each stage up while building it, and you review both together, stage by stage.
- **Stages teach the subject. The capstone is separate.** Never shape a stage around what the capstone will need, and never let the capstone change a stage.
- **Nothing in a task or a brief may answer an open question.** A line that states the outcome a question asks the trainee to reason out is a leak, even if it looks like an ordinary requirement.
- **Trainees see a trainee's course.** Their README and `modules/` speak to "you", and carry no design-document citations, no maintenance notes and no "draft" flags. Trainer material lives under `docs/`.
- **Cost is part of the lesson.** Every stage says what it may bill, and the capstone can make cost a constraint.

## Settle these before you write anything

Answer them in writing, then keep the answers where trainers can find them. Each one saves a rewrite later.

| Decision | Why it matters |
| --- | --- |
| The source of truth: a design document, a topic list or a curriculum | The stages are cut from it. Say which document wins when they disagree |
| The stages: how many, in what order, with what titles | Titles are trainee-facing and should be easy to navigate. Fix them before you write briefs |
| What each stage leaves behind | Anything that survives a stage (a bucket, a repository) is a dependency for the next ones |
| Rules for every stage | Versions, credentials, cost, clean-up and tooling limits, stated once in the README instead of in every brief |
| Where trainees' work lives | A repository host outside this one, linked from each write-up |
| Cost and access | Who provides the sandbox, what may bill, and whether time boxes belong in the course at all |
| Capstone shape | What is fixed for everyone, what is the trainee's own design decision, the rubric, the pass mark and the AI policy |
| The review rubric | What "accepted" means for a stage, and what "pass" means for the capstone |

## Prompt 1 — Propose the stages

Run once per course. It writes nothing; you confirm the list before anything is created.

**Placeholders:** `<SOURCE_DOC_PATH>`, `<FRAMEWORK_DOC_PATH>`, `<SUBJECT>`

```
Read <SOURCE_DOC_PATH> and <FRAMEWORK_DOC_PATH>. Propose the training stages for a Build-to-Teach <SUBJECT>
course: for each stage, a descriptive title a trainee could navigate by, a one-line theme, what it builds on,
what it leaves behind, and what it must not cover. Check the order: does each stage rely only on earlier
ones? List anything the source document is silent on as a question for me. Do not create any files yet.
```

Answer the questions it raises in the chat. Reorder, rename, add and drop stages until the list is right.

## Prompt 2 — Write the stage briefs

**Placeholders:** `<STAGE_LIST>` (the confirmed list), `<RULES_FOR_EVERY_STAGE>`

```
Create one folder per stage under modules/, named m<NN>-<descriptive-title>, and write each stage's brief.md
from docs/templates/brief.md. The brief is the trainer's handoff only: objective, scope in the order to
tackle, out of scope, stack constraints, a named deliverable, open design questions, an observable
definition of done with stable IDs, written around the trainee's training module (the build plus the
write-up that teaches it) in the pattern of docs/templates/brief.md (an artifact, a specific observable
result, and a "not the weaker substitute" contrast), and a Cost row. No lesson content, no steps, no code, no solutions.
The stages are: <STAGE_LIST>. These rules apply to every stage and are stated once in the README, so do
not repeat them in the briefs: <RULES_FOR_EVERY_STAGE>.

When all the briefs are written, check each one: does any scope item, constraint or definition-of-done line
state the outcome an open design question asks the trainee to reason out? List every such line.
```

Reword the lines it finds before moving on. These are the briefs that answer their own questions; each one reaches the trainee as an instruction.

## Prompt 3 — Write the write-up templates

```
For every stage, write write-up-template.md from docs/templates/write-up-template.md. Copy the stage's open
design questions, scope items and definition-of-done items from its brief word for word into the sections
that list them. Keep the other sections exactly as the template has them.
```

The write-up lists are copied, not paraphrased. That is what lets the next prompt check coverage by machine.

## Prompt 4 — Add the task planner, then generate the checklists

Copy `docs/templates/trainee-task-planner.md` into `.claude/commands/` in the new repository. It has nothing course-specific in it. Generate one stage first to confirm the shape.

**Placeholder:** `<STAGE_FOLDER>` (for example `modules/m03-<stage-title>`)

```
/trainee-task-planner <STAGE_FOLDER>
```

Advance through the gates it stops at. Then generate the rest.

**Placeholders:** `<STAGE_FOLDER>`, `<PRECEDENT_TASKS_FILE>` (a generated `tasks.md` to match), `<STAGE_SENSITIVITY>` (optional: an open question in this brief that no task may answer)

```
Run `/trainee-task-planner <STAGE_FOLDER>` end to end — evaluate, plan, apply, validate, with no pausing for
approval (this request is the approval). Match <PRECEDENT_TASKS_FILE>: same sections, same task
granularity, same closing task. Tasks must never leak answers: no code, no name the brief does not use, no
design choice that resolves a question the brief leaves open. <STAGE_SENSITIVITY>

Write <STAGE_FOLDER>/tasks.md, then run the full coverage check against this stage's brief and write-up
template, fix any gap, and re-check until clean. Report in under 200 words: task count and section
breakdown, gaps found and fixed, and confirmation that the leaked-answer check passed.
```

Run it as one forked agent per stage if your tooling allows it. Afterwards, count the tasks:

```
grep -c '^\- \[ \]' modules/*/tasks.md
```

## Prompt 5 — Design the capstone

The capstone is its own project. Decide first what is fixed and what is the trainee's design, because that choice drives everything else in the brief.

**Placeholders:** `<WHAT_IS_FIXED>`, `<WHAT_IS_THE_TRAINEES>`, `<CONSTRAINTS>`, `<COST_LIMITS>`, `<RUBRIC_CRITERIA_AND_POINTS>`, `<PASS_MARK>`

```
Write modules/capstone/brief.md from docs/templates/capstone-brief.md, then write-up-template.md from
docs/templates/capstone-write-up-template.md and tasks.md from docs/templates/capstone-tasks.md. Fixed for
everyone: <WHAT_IS_FIXED>. The trainee's own design decisions, all collected in one section called "Your
design decisions": <WHAT_IS_THE_TRAINEES>. Constraints: <CONSTRAINTS>. Cost challenge: <COST_LIMITS>.
Include an AI-assisted development policy that asks for an explanation on the spot, design decisions the
trainee owns, and a log of at least one wrong AI suggestion. Rubric: <RUBRIC_CRITERIA_AND_POINTS>, with
Excellent, Satisfactory and Needs work for each criterion, scored in bands, pass mark <PASS_MARK>, and the
definition of done as a gate. Add a presentation section that says what the panel checks for each
criterion and that it will ask the trainee to explain a random block and change it live, unassisted.
State outcomes, not mechanisms, wherever the mechanism is the trainee's decision. Do not write any
solution into the brief.
```

Keep any reference solution you have out of the trainee-facing files. The brief states requirements, proofs and marking; the solution stays with the trainers.

## Prompt 6 — Write the READMEs

```
Write README.md at the repository root from docs/templates/course-readme.md, for the trainee: speak to
"you", list the stages with links to their briefs and checklists, state the rules for every stage once,
describe the stage rubric, and summarise the capstone from its brief. Then write docs/README.md for
trainers and maintainers: the folder map, how the stage files are kept in step with the briefs, and what
the trainer must supply.
```

## Prompt 7 — Validate for the trainee's view

Run it after any large change and before you hand the repository over.

```
/validate make sure modules/ and README.md are tailored for trainee view
```

The criteria it should check:

| Check | Pass when |
| --- | --- |
| Voice | The README and every file under `modules/` speak to the trainee |
| Internal references | No decision numbers, no design-document or activity citations, no mention of a reference solution, no planner or template maintenance notes |
| Flags | No "draft" or "unconfirmed" markers; open items appear only as "ask your trainer" in the brief |
| Links | Every link and every anchor resolves, including `#rules-for-every-stage` |
| Coverage | Every stage's `tasks.md` and write-up template match its brief, and the leaked-answer screen is clean |
| Counts | The task counts match what the planner reported |

## Prompt 8 — Spot-check the riskiest stages

No prompt needed: read the generated files yourself. For any stage whose brief leaves a genuinely open design question, read its `tasks.md` directly rather than trusting an agent's report. Record any pattern you find in `knowledge/retros/`, so the next course avoids it.

## Prompt 9 — Change a stage later

A stage's `tasks.md` and write-up template are generated from its brief. Change the brief first, then regenerate; never patch them by hand.

**Placeholders:** `<STAGE_FOLDER>`, `<CHANGE>` (for example "add a topic", "reword a definition-of-done line", "raise the bar for AI-assisted work")

```
Update <STAGE_FOLDER>/brief.md to <CHANGE>. Then update write-up-template.md so its lists still match the
brief word for word, and run `/trainee-task-planner re-plan <STAGE_FOLDER>` as a full rewrite of tasks.md.
Check the new brief for lines that answer its own open questions.
```

## Prompt 10 — Add a stage

```
Add a stage <ID> — <TITLE> after <PREVIOUS_STAGE>. Write brief.md from docs/templates/brief.md, then
write-up-template.md from docs/templates/write-up-template.md, then run /trainee-task-planner on it. Add it
to the Stages table in README.md and say what it builds on and what it leaves behind.
```

## Habits that kept this course out of trouble

- **Ask for scope decisions in the chat.** When the source document is silent or contradicts another, ask the trainer rather than inferring. A wrong inference in a brief reaches every trainee.
- **Keep stage and capstone separate.** If a stage exists only to prepare for the capstone, the stages are drifting.
- **State a rule once.** Put course-wide rules in the README and have each brief link to them, so a change is made in one place.
- **Prefer a narrow change.** When asked to remove something, remove that thing and fix its direct consequences. Do not restore or rewrite broad areas.
- **Regenerate, don't patch.** Checklists and write-up lists come from the brief; editing them by hand makes them drift.
- **Check numbering after every removal.** Definition-of-done IDs, scope items and question numbers are referenced by the generated files.
- **Run commands from the repository root.** Some tools write output into whichever folder they run from.

## Minimum assets to start a new course

1. The Build-to-Teach framework document, unchanged: [build-to-teach-framework.md](../build-to-teach-framework/build-to-teach-framework.md).
2. `.claude/commands/trainee-task-planner.md`, copied from [trainee-task-planner.md](trainee-task-planner.md).
3. The templates in this folder.
4. This playbook, for the prompts.

Everything else (`modules/` and each stage's three files, the capstone, the READMEs) is generated for the new course from its own source document, using Prompts 1–6.
