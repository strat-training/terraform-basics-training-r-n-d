---
name: checkstage
description: Run a read-only check of a Build-to-Teach stage — its write-up-template.md against the master and the brief, its brief and tasks.md for consistency, and a trainee's filled-in write-up.md if one exists — as an EVALUATE → PLAN → approval gate → APPLY → VALIDATE cycle run through the learning-modules-and-writeup-checker agent. Stages only, never the capstone.
argument-hint: <stage-folder> [path/to/write-up.md] [go] | all [go]
---

# /checkstage

**E→P→A→V** for checking a stage's learning material. It runs the same cycle as `/epav` — EVALUATE, PLAN, a gate, APPLY, VALIDATE — specialised to this one job. It is self-contained: it does not call `/evaluate`, `/plan`, `/apply` or `/validate`, which are for code tasks. Nothing is written at any step: APPLY runs the checks and VALIDATE re-verifies every finding.

## Course layout

Folder and file names (the stages folder, the master template, how the capstone is recognised, the task planner command) are set once, in the "Course layout" section at the top of the `learning-modules-and-writeup-checker` agent. When you copy this command to another course, change them there; this command follows the agent.

## Usage

- `/checkstage <stage-folder>` — run the cycle for one stage: its template against the master and the brief, how its brief and `tasks.md` agree with it, and a `write-up.md` in that folder if there is one.
- `/checkstage <stage-folder> <path-to-write-up.md>` — the same, with a trainee's write-up kept outside the repo.
- `/checkstage all` — every stage folder that has a `brief.md`, except the capstone. One plan and one gate cover all of them; each stage is then checked on its own and a summary table closes the run.
- Add `go` to any form to skip the wait at the gate (for example `/checkstage m05 go`). The EVALUATE SUMMARY and the PLAN are still shown. Because nothing is written, this is safe.

The folder may be given as a unique prefix of its name (for example `m05`), the full folder name, or its path. With no argument, ask which stage; do not guess.

## Cycle

```
EVALUATE → PLAN → [approval gate] → APPLY → VALIDATE
```

The agent cannot pause for approval, so this command holds the gate and runs the agent in two modes: **plan** (EVALUATE and PLAN, runs no check) and, after approval, **apply** (APPLY and VALIDATE).

## Steps

### 0 — Check the request

- The capstone is out of scope. If the argument is the capstone folder, stop and say so; `all` skips it.
- Confirm the stage's `brief.md` and `write-up-template.md` exist. If either is missing, stop and name it. Do not create it.
- If a path to a `write-up.md` was given, confirm the file exists.
- Confirm the master write-up template exists.

### 1 — EVALUATE

Launch the `learning-modules-and-writeup-checker` agent (Agent tool, `subagent_type: "learning-modules-and-writeup-checker"`) in **plan** mode. In the prompt, give the stage folder or `all`, the path to the trainee's `write-up.md` if one was given, the word "plan", and the instruction to read the master and the brief fresh. Output the agent's **EVALUATE SUMMARY**: what the master and brief contain, which of the stage's files exist, which parts will run, and anything it already knows it cannot verify.

### 2 — PLAN

Output the agent's **PLAN**: the checks that will run (template, file agreement, and the write-up if present), the files read, and "Writes: none".

**GATE: stop here. Do not run apply mode until the user approves.** Say:

> "Plan ready. Reply **go** to run the checks (nothing will be written), or give feedback to change what is checked."

If the user gave `go` in the arguments, say so and continue. If they give feedback, run plan mode again with it and show the new plan. Never edit the plan yourself.

### 3 — APPLY (only after approval)

Launch the agent again in **apply** mode, one run per stage; for `all`, the runs only read, so launch them together. Give each the stage folder, the word "apply", the write-up path if any, and the approved plan. The agent runs every planned check and records each one's result and evidence.

### 4 — VALIDATE

In the same run the agent re-verifies every finding: it reopens the file, re-quotes the line, re-runs the mechanical comparison for fixed text, rereads secret hits in context, and drops or downgrades anything that does not hold. Output each agent's **APPLY COMPLETE** and **VALIDATE COMPLETE** blocks, with its report, as they came back. Do not add findings the agent did not verify, and do not drop any it reported. For `all`, finish with a table of stages against fail and warn counts and the one thing to fix first.

Then, in one line each, point to the fix for what it found:
- A template that differs from the master, or has a weak question, concept or evidence item → `/em-files-generator <stage-folder>`.
- `tasks.md` drift → run the task planner again for that stage.
- A brief that answers its own research prompt, or a stale reference in a README → the EM edits it by hand.

> "Task complete."

## Abort at any step

If the user says "stop", "abort" or "cancel" at any point, stop immediately and summarise what was completed and what was not.

## Scope discipline

One stage at a time, or one pass with `all`. If something outside the checks turns up, report it in the summary and leave it alone. This command never edits any file, and never fixes what it finds.
