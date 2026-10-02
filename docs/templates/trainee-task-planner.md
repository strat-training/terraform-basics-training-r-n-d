# /trainee-task-planner

Reads a Build-to-Teach stage's `brief.md` and `write-up-template.md` and writes `tasks.md` beside them, in the shape of the reusable template in `docs/templates/tasks.md`: an ordered checklist a solo trainee works through, in four sections — Setup, Build, Verify, Write-up. It restates what the brief already says as tasks and adds nothing to it. Use this instead of writing a stage checklist by hand — the order, the one-task-per-source-item coverage and, above all, the no-leaked-answers rule are each easy to break while trying to be helpful.

Follows the same EVALUATE → PLAN → APPLY → VALIDATE cycle as `/evaluate` `/plan` `/apply` `/validate`, self-contained in this one command (the same shape `/dev-tasks-planner` uses). **Stop at the end of EVALUATE and PLAN and wait for explicit approval before continuing** — do not run straight through to APPLY, unless the invoking prompt explicitly waives the pause (see "Unattended runs").

This command covers stage briefs, which have the numbered sections listed under Prerequisites. The capstone brief has its own capstone-shaped template (`docs/templates/capstone-brief.md`); write the capstone's `tasks.md` by hand from `docs/templates/capstone-tasks.md`.

## Arguments

`/trainee-task-planner <stage-folder>`

Example: `/trainee-task-planner modules/m04-managing-resources-with-network-provisioning`. A bare folder name, or just its stage prefix such as `m04`, resolves under `modules/` when it matches exactly one folder; if it matches none or several, stop and list the candidates.

`/trainee-task-planner re-plan <stage-folder>` regenerates an existing `tasks.md` from a brief that has since changed. It is a full rewrite, never a hand-patch: the same four steps run and APPLY overwrites the file.

One stage per invocation. To cover many stages, run one forked subagent per stage; each runs the whole cycle on its own.

### Unattended runs

The invoking prompt may also (a) name a precedent `tasks.md` to match the shape of, (b) name stage-specific sensitivities — open questions needing extra care, treated as additions to the leak rules below, and (c) say to run without pausing. If it says the request itself is the approval, still print the EVALUATE SUMMARY and the PLAN, then continue without waiting. Otherwise pause at both gates.

## Prerequisites — MANDATORY, check before doing anything else

Verify each with `ls` and a real read, not an assumption.

1. `<stage-folder>/brief.md` and `<stage-folder>/write-up-template.md` both exist.
2. The brief has, non-empty: an objective, a numbered in-scope list, a named deliverable, numbered open design questions, and a definition of done made of checkbox items with IDs. The template has `##` section headings, each opening with a plain-text paragraph.
3. `re-plan` only: `<stage-folder>/tasks.md` exists.

**If any check fails, STOP.** Do not guess the missing piece and do not write a brief or template here:

```
⚠ /trainee-task-planner cannot run for <stage-folder> yet.

Missing: <which file or section>

tasks.md is derived entirely from the brief and the write-up template, so there is nothing
to plan from. The brief is the trainer's document — fix <missing piece> there, then re-run.
```

---

## The rule that overrides everything: no leaked answers

The brief hands the trainee a problem on purpose. `tasks.md` keeps them moving through it; it must never solve any part of it. A task NEVER contains:

- **Code** of any kind: no code blocks, no commands with arguments, no config or file-content snippets, no pseudo-code.
- **A name the brief does not already use** — library, API, function, resource type, command, flag, setting, algorithm, tool or pattern. If a technical term is not in `brief.md` or `write-up-template.md`, it does not go in a task.
- **A design choice** — which option, approach, value, structure, ordering or trade-off — that resolves anything the brief poses as a question or phrases as "decide" or "work out".
- **A hint in disguise**: "consider using…", "you may want to…", "for example", "e.g.", "such as", "think about X" where X is the answer, a rhetorical question that names its own answer, or a ladder of leading sub-questions.
- **Explanation**: definitions, reasons, background. A task says what to produce, never why or how.

Allowed: the brief's and template's own words, verbatim; pointing at a brief section by name; the verbs *work on, have ready, confirm, capture*.

**Frames plus verbatim text.** To make this checkable, every task is one of the fixed frames in APPLY with only text lifted verbatim from the brief or template filling its blanks. "Verbatim" means the same words and punctuation; markdown emphasis markers (`**`) may be dropped. The frames are the only free text in the file. If a task seems to need a clarifying phrase of your own, that phrase is the leak — leave it out. If a verbatim line in the brief would itself resolve an open question, do not paraphrase around it and do not edit the brief: restate it exactly as written and report it under "Brief issues" for the trainer.

---

## EVALUATE — Read the source material in full

Read each of these end to end, not by grep:

1. `brief.md` and `write-up-template.md`.
2. The project `README.md` at the repository root (its rules for every stage apply to the trainee but are not restated in tasks; the brief's own constraints are restated only as the brief words them).
3. If a precedent `tasks.md` was named, read it and note its headings, task granularity and closing task. Otherwise the default shape below applies.
4. `re-plan` only: read the existing `tasks.md`. For every task record whether it is ticked and which source item its text came from.

Build the **source inventory**, which everything later is checked against:

- **Objective** — the paragraph under "Objective", text exact.
- **Scope items** — the numbered list under "In scope", in order, text exact.
- **Open design questions** — numbered, text exact.
- **Deliverable components** — the Deliverable text split at its own joins ("and", "plus", ", with"), each piece kept in the brief's words. If a split is ambiguous, prefer fewer, larger components and show the split in PLAN for approval.
- **Definition-of-done checks** — each ID with its text exact.
- **Write-up sections** — each `##` heading in the template, with the template's own guidance for it: the first two sentences of the plain-text paragraph that opens the section.
- **Builds on** and the stack constraints — used for the Setup tasks only.

Then the **sensitivity pass**. For each open question, write one line saying what the trainee must reach on their own: the option chosen, the name of the mechanism, the reason. This list is for you and the trainer; it never goes into `tasks.md`. Add any caller-supplied sensitivities.

Finally check the brief and template themselves, and report — do not fix — what you find:

- Does any scope item, constraint or definition-of-done line already resolve an open question?
- Does each definition-of-done item appear in the template's "Checkpoint evidence" section, one for one?
- Is any scope item a step rather than a topic?

### Output — EVALUATE SUMMARY

```
EVALUATE SUMMARY
────────────────
Stage:        <folder> — <brief title>   (mode: new | re-plan)
Source items: scope <n> · open questions <n> · deliverable components <n> · DoD checks <n> · write-up sections <n>
Shape:        <named precedent, or "default shape from this command">
Sensitive:    <per open question: what the trainee must reach alone — never copied into tasks.md>
Caller notes: <stage-specific sensitivities from the invoking prompt, or "none">
Brief issues: <self-resolving lines, missing evidence entries, step-like scope items — or "none">
Existing:     <re-plan only: tasks ticked / carried over / invalidated>
```

Do NOT plan task wording or write any file yet. End with:

> "Ready to plan. Reply to proceed with PLAN, or give feedback to redo EVALUATE."

---

## PLAN — Decide the checklist's content

**Default shape** (a named precedent overrides it): four sections, in this order.

| Section | Holds | One task per |
| --- | --- | --- |
| Setup | Read the brief, make the write-up copy, confirm access | fixed: three tasks |
| Build | The brief's scope in the brief's order, then its deliverable | scope item, deliverable component |
| Verify | The definition of done | DoD check |
| Write-up | The write-up template, then a closing self-review | template section, plus one closing task |

Rules, all mandatory:

- **One task per source item.** No merging, no splitting, no extra tasks, no task without a source item.
- **Source order.** Tasks follow the order of the brief and the template.
- **Open design questions are not tasks.** The trainee answers them in the write-up's "Why it's built this way" section, which has a task of its own, so the checklist stays short. Each question must still appear in the write-up template, and the leak checks still treat every question as sensitive.
- **`re-plan` carry-over.** Keep a task ticked only if its source text is word-for-word unchanged. Changed and new items come back unticked; items no longer in the brief are dropped. List all three in PLAN.

### Output — PLAN blueprint

```
PLAN
────
File:      <stage-folder>/tasks.md — <new | full rewrite>
Sections:  Setup 3 · Build <n> (scope <a> · components <b>) · Verify <n> · Write-up <n> (sections <m> + closing review)
Coverage:  every scope item, component, DoD check and write-up section → one task, in source order; every question → the write-up template
Split:     <the deliverable split into components, in the brief's words>
Frames:    <the frames from APPLY that will be used, unmodified>
Leak watch: <per sensitive question, the temptations to avoid — by category, not by answer>
Carry-over: <re-plan only: ticks kept / reset / dropped>
```

Output as a blueprint. No file writes yet. End with:

> "Waiting for approval. Reply to apply, or give feedback to revise the plan."

---

## APPLY — Write `tasks.md`

Write `<stage-folder>/tasks.md` and nothing else. Do not touch `brief.md` or `write-up-template.md`. Follow PLAN exactly; if something PLAN did not anticipate turns up, stop, flag it, and confirm before deviating.

Use this structure verbatim. Angle brackets are the only blanks; each is filled with text copied exactly from the brief or template.

```
# <brief's H1> — Tasks

**Objective:** <the brief's Objective paragraph>

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (<Builds on value>) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: <scope item n>
- [ ] Have ready: <deliverable component n>

## Verify

- [ ] Confirm <DoD-n>: <DoD text> Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “<heading>”: <template guidance>
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
```

Frame notes:

- **Setup, third task** — when "Builds on" is "Nothing", drop everything from "that each stage" to "has been accepted, and that you have", leaving: "Confirm that you have the access and tools the brief's stack constraints require. Raise anything missing with the trainer before you build."
- **Write-up tasks** — use the template's own guidance for that section, verbatim, shortened to its first two sentences if longer. If the section has no opening paragraph, end the task after the heading, with a full stop.
- **Task lines** are single lines that begin exactly `- [ ] ` (a carried-over task in `re-plan` begins `- [x] `). No nested checkboxes, so `grep -c '^\- \[ \]'` counts tasks.
- Do not add a "Done when", a hint line, an estimate, a sub-bullet or a note to any task.

### Output — APPLY COMPLETE

```
APPLY COMPLETE
──────────────
Written:  <stage-folder>/tasks.md — <task count> tasks (Setup 3 · Build <n> · Verify <n> · Write-up <n>)
Carried:  <re-plan only: ticks kept / reset / dropped>
Skipped:  <anything intentionally deferred>
```

Then prompt to continue to VALIDATE.

---

## VALIDATE — Prove coverage, then prove nothing leaked

Run all three checks. Do not rely on eyeballing, and do not trust the EVALUATE notes: re-read `brief.md`, `write-up-template.md` and `tasks.md` fresh from disk.

### 1 — Coverage script

Write a short script in a scratch location outside the stage folder (the session scratchpad if one is provided), run it, then delete it. It re-parses all three files and asserts:

- The sections Setup, Build, Verify and Write-up are present, in that order, and every task sits under one.
- Every task line starts `- [ ] ` or, in `re-plan`, `- [x] `.
- **Counts and order:** Setup has 3 tasks; Build has one task per scope item, then one per deliverable component; Verify has one per DoD ID; Write-up has one per template section plus the closing task. Each task's blank is the source text, verbatim.
- **Deliverable:** every component fragment is a verbatim substring of the Deliverable text, and together they cover all of it except the joining words used to split it.
- **Frames:** regenerating the whole file from the brief and template reproduces it byte for byte, so every task is its frame with only verbatim text in the blanks.

Fix anything it finds and re-run until clean.

### 2 — Mechanical leak screen

A second script, run before the dedicated re-read, over the text that fills each frame's blanks. The frames themselves are fixed and already approved, so they are not screened. Flag:

- any code fence or indented code block;
- any backticked token that is neither a file name in the stage folder nor a substring of `brief.md` or `write-up-template.md`;
- any identifier-like token (digits, underscores, hyphenated or camel-cased) missing from both source files;
- any of these as whole words or phrases — "for example", "e.g.", "such as", "consider", "you may want", "you could", "try", "hint", "tip", "think about". Match on word boundaries, so "entry", "registry" and "considered" do not trigger.

A flag in your own wording: remove it. A flag inside verbatim brief text: leave it, and list it under Brief issues. Re-run until only the latter remain.

### 3 — Dedicated re-read for leaked answers

Not a script. Read `tasks.md` top to bottom as the trainee would, with the EVALUATE sensitivity list beside it, and answer each of these in writing:

- **Cross-leaks:** for each open question, scan every other task — Work on, Have ready, Confirm and Under — for wording that would answer it. A scope item or DoD line that names the very mechanism, approach or reason a question asks the trainee to reach is a leak even though no task states it.
- **Topics, not steps:** is every "Work on" task still a topic, or has any become an instruction?
- **No stowaways:** is every sentence in the file either a frame or verbatim brief or template text?

State the result per item with the evidence — the tasks examined, quoting their first words, and what you found — not a bare "passed". Fix anything in your own wording. For a leak that lives in the brief's own text, do not change the brief or paraphrase the task; report it.

If a leak pattern keeps recurring across briefs, append it to `knowledge/retros/` the way `/validate` does.

### Output — VALIDATE COMPLETE

```
VALIDATE COMPLETE
─────────────────
File:         <stage-folder>/tasks.md
Tasks:        <total> (Setup 3 · Build <n> · Verify <n> · Write-up <n>)
Coverage:     scope <n>/<n> · components <n>/<n> · questions in write-up <n>/<n> · DoD <n>/<n> · write-up <n>/<n> · frames OK
Leak screen:  <clean | list of flags, each marked own-wording (fixed) or brief text (reported)>
Re-read:      <per check: tasks examined and the finding>
Brief issues: <lines in the brief that resolve a question, for the trainer — or "none">
Issues fixed: <list, if any>
```

> "Task complete."
