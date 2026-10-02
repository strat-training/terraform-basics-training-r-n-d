# <Capstone title> Brief

<!--
TEMPLATE: capstone brief. Copy to modules/capstone/brief.md and replace every <placeholder>. Delete
these comments when you are done. This is NOT the stage brief template: a capstone is assessed
against a rubric and a presentation, and it carries an explicit policy on AI-assisted work.

Same rule as a stage brief: it states the problem, the constraints, the requirements and how the work
is judged. It does not hold the solution — no solution code, no design walk-through, no answers to the
design decisions the trainee has to make and defend.
-->

**Builds on:** <the stages this capstone assumes, and anything it extends>

## Objective

<One paragraph. What the trainee builds end to end, on their own, and the closing clause that keeps the bar on understanding: "...and be able to defend every decision in it, regardless of how the code got typed.">

## A note on AI-assisted development

You're expected to use AI tools for this capstone — that's realistic, not cheating. The bar this sets is understanding, not output:

1. **You must be able to explain any part of your work on the spot**, without looking it up or asking an AI tool again. During your presentation, your panel will pick <what: a stage, a task, a block of code> at random, ask you to walk through what it does and why, and ask you to make a small change to it live, unassisted.
2. **The design decisions are yours, not the tool's.** An AI tool can write an implementation; you decide <the decisions listed under "Your design decisions">. If you can't explain *why* a decision was made, it isn't actually your decision yet — go back and make it one.
3. **Keep a short log of at least one moment an AI tool's first suggestion was wrong, inefficient, or didn't fit your design**, and what you did instead. This is part of your write-up, not optional colour — catching and correcting a bad suggestion is the actual skill being assessed here, more than the code that resulted.

None of this means avoiding AI tools or second-guessing every line out of caution — it means treating suggested code the way you'd treat a teammate's pull request: read it, understand it, and be ready to defend keeping it.

## Scope / topic rule

<Fixed topic, or "default topic plus the rule for proposing your own". State what is too small to count, and what the trainer supplies. Add an architecture view here if the capstone has one — a Mermaid diagram of what must exist and where responsibilities end, not how to build it.>

## Your design decisions

<!--
Keep ALL of the trainee's freedom in this one section, so it can be seen in one place. Leave the
design open wherever the learning is in making the decision, and fix only what has to be the same for
every trainee so the work can be compared (a fixed use case in another cloud, a fixed release pattern,
the checks). Do not answer any of these decisions anywhere else in the brief.
-->

These are yours. Nothing in this brief or in `data/` decides them, and you defend each one in your write-up and in the presentation. The limits on them are the stack constraints and the cost challenge, and nothing else.

| Decision | What is open | What stays fixed |
| --- | --- | --- |
| <e.g. the topic or theme> | <what the trainee may choose> | <what must stay the same> |
| <e.g. what each tier runs on> | <the options left open> | <the limits that still apply> |
| <e.g. how the change is made safely> | <the mechanism is the trainee's> | <the outcome that is checked> |
| <e.g. how the result is demonstrated> | <the form is the trainee's> | <what it must make visible> |

## Stack constraints

Same as the rest of the course: <the course-wide rules that still apply>. On top of that, these are the constraints set for this capstone:

- **Tooling.** <what is not allowed; credentials rule>
- **Clouds and region.** <clouds, region, providers, version constraints, lock files>
- **State.** <backend, locking, one state per stack and environment>
- **Structure.** <stacks, modules, validation, formatting>
- **Releases or changes.** <how a change is made and what is forbidden>
- **Names and tags.** <naming pattern, required tags or labels>
- **Security.** <network, identity and secrets rules>
- **The supplied payload.** <what the trainer provides, what stays untouched and what the trainee may replace>
- **Sandbox limits.** <who to tell, and where the agreed fallbacks are>

### The cost challenge

<!--
When the design is open, cost is the constraint that keeps it honest. Set limits that can be checked
from the trainee's saved plan and estimate, and say where the figures come from and who confirms them.
-->

| Limit | Value | How it is checked |
| --- | --- | --- |
| Steady-state running cost | <hourly ceiling> | <how it is recomputed> |
| Total spend | <ceiling for the whole capstone> | <the estimate and the hours actually run> |
| Size ceiling | <largest allowed size per kind of resource> | <the checker, from the plan> |
| Count ceiling | <resources that are expensive to repeat> | <the checker, from the plan> |
| Teardown | <same-day destroy in one pass> | <the teardown scans> |

<Where the figures come from, whether they have been re-checked, and who confirms them.>

## Requirements (all required)

<!-- Tables work well: requirement, what it means, how it is checked. Group by theme. -->

| Requirement | What it means | How it is checked |
| --- | --- | --- |
| <requirement> | <what it means> | <evidence or check> |

### Inputs and guardrails

<Which inputs exist, what values are allowed, and that bad input must fail at plan time with a message that states the problem and the allowed values.>

### Stages or tasks

<The ordered stages: for each one, the one change, what the plan or result must show, and what to confirm before moving on. State the outcome, not the mechanism, wherever the mechanism is the trainee's decision.>

### Demonstrating the result

<What the trainee's demonstration must show and record, however they choose to build it, and where the record is kept so the panel can inspect it after the environment is gone.>

### Demo Challenge (the day-2 round)

<Changes that a live system gets after launch, each starting from the end of the stages. For each task: the change, and what the trainee must show. Written as outcomes, so that they hold whatever design the trainee chose.>

### Proofs you must submit

<Each proof, where it is run, and what it must show. Saved under `evidence/`.>

### What you hand in

| File or folder | What it holds |
| --- | --- |
| <path> | <contents> |
| `write-up.md` | Your filled-in `write-up-template.md` |

### Time, cost and teardown

<Effort, planning cost figures and whether they are verified, same-day destroy, and the read-only scan that proves nothing is left.>

### If the sandbox blocks something

| Blocked | Fallback | Waived |
| --- | --- | --- |
| <what the sandbox may block> | <the agreed fallback> | <the proofs it makes impossible> |

### Stretch goals / distinction work — optional

<Items that are optional and how they count, or "set by the trainer".>

## Presentation (raised bar)

<Format and length. State that the panel will pick one or two places at random and ask the trainee to (a) explain what it does and why and (b) make a small change live, without AI assistance — "This isn't a gotcha — it's the actual test of whether the capstone is yours.">

| Criterion | What the panel checks in the presentation |
| --- | --- |
| <rubric criterion> | <the questions or evidence the panel looks for> |

## Rubric (fixed — do not deviate from this when self-assessing)

**Scoring and pass mark.** <How each criterion is scored from 0 to its points, what Excellent, Satisfactory and Needs work are worth, the pass mark out of the total, and any condition that must also be met.>

| Criteria | Points | Excellent | Satisfactory | Needs work |
| --- | --- | --- | --- | --- |
| <criterion> | <points> | <what the best work shows> | <partly there> | <what is missing or broken> |

> **Note:** <where the weights come from, and what the trainer must confirm before a cohort is scored against it.>

## Definition of done

- <Observable result: a clean checkout builds and runs from the documented steps. A capstone that doesn't meet this bar doesn't pass, regardless of rubric score elsewhere.>
- <Observable result>
- You pass the live walkthrough component of the presentation — if you can't explain or change work you submitted, that part of the capstone doesn't count as done regardless of whether it applied.

## What goes into the content library

Both your working repository and your `write-up-template.md` (filled in) are the deliverable — the write-up is what the next cohort's capstone brief and training content get built from. Write it as teaching material, not a retrospective.

## Still open / ask your trainer

- <question the trainee should put to the trainer before starting>
