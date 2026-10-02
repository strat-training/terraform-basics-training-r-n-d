# <Course title> — training stages and capstone

<!--
TEMPLATE: course README. Copy to the repository root as README.md and replace every <placeholder>. Delete
these comments when you are done.

Write it for the trainee. Speak to "you": what you do, what you get, how you are reviewed. Keep trainer and
maintainer notes out of it (how files are generated, where design documents live, who supplies what, how to
change a template) and put those in docs/README.md. Do not cite internal design documents or decision numbers,
and do not flag anything as draft or unconfirmed: anything still open is for the trainee to "ask your trainer"
in the brief itself.

Keep these headings exactly, because other files link to them: "Rules for every stage" (the stage checklists
link to it as #rules-for-every-stage). Delete the capstone section if the course has no capstone, and replace
"stage" with your own word everywhere if you do not use it.
-->

This is your <subject> course: <n> training stages in `modules/`, followed by <a capstone project | no capstone>. For each stage your trainer gives you a brief. You build the stage and write it up as you go, your trainer reviews both together, you revise, and the finished pair becomes teaching material for the next cohort.

A note on words: <a term the course uses in two senses, and which sense this README means. Delete this paragraph if there is none.>

## What is in this repository

| Path | What it holds |
| --- | --- |
| `modules/` | The <n> stage folders (<first>–<last>), each with a brief, a checklist and a write-up template |
| `modules/capstone/` | The capstone, with its own brief, checklist and write-up template |

The other folders are trainer material. You do not need them to do the stages.

## How a stage works

1. **Your trainer hands you the brief.** Each stage's `brief.md` says what to build and how you will know it is done: objective, scope, stack constraints, the named deliverable, open design questions and a definition of done. It contains no lesson, no steps, no code and no solutions. How to build it is yours to work out.
2. **You build and write up the stage together.** Copy `write-up-template.md` to `write-up.md` in the stage folder and fill it in *while* you build, not after the build works. The "how to build it" section is the teaching content, so write it for someone who will follow it with no trainer to ask.
3. **Your trainer reviews both together.** When you reach the definition of done, set Status to "In review". Your trainer reviews the working system and the write-up side by side. The question is not only "does it work?" but "could someone else learn from this?"
4. **You revise.** Fix what the review finds, in both the build and the write-up, before starting the next stage.
5. **The finished pair goes into the content library.** An accepted stage is the build plus its write-up. Your trainer decides what carries into the next cohort's plan.

Review happens at the end of every stage, not just at the end of the course. A write-up produced after the system already works tends to be thin; reviewing as you go is what keeps it good.

### What is in each stage folder

| File | Who writes it | Purpose |
| --- | --- | --- |
| `brief.md` | Your trainer | What to build and how you will know it is done. Do not edit it. |
| `write-up-template.md` | Your trainer | A blank template. Leave it untouched so the next cohort starts clean. |
| `write-up.md` | You | Your copy of the template, filled in as you build. |
| `tasks.md` | Your trainer | An ordered checklist for the stage, one task per scope item, question, check and write-up section. You tick the boxes; it holds no answers and no steps. |

<Where your own work lives and how to link it, for example "Your code lives outside this repository, in your own <host> repository. Link it from the header of your write-up." Add that the capstone folder has the same three files.>

## Stages

<!-- Link each title to its brief.md and each checklist to its tasks.md. -->

| Stage | Title | Checklist | Theme | Leaves behind |
| --- | --- | --- | --- | --- |
| <ID> | [<Title>](<link to the stage's brief.md>) | [tasks](<link to the stage's tasks.md>) | <what the stage covers, in one line> | <what survives the stage, or "Nothing"> |

<Order note: work the stages in order, what later stages reuse from earlier ones, and why any stage sits where it does. Say the briefs refer to each other by stage ID.>

## The capstone — <name>

<!-- Delete this section if the course has no capstone. -->

<One paragraph: when it comes, that it is standalone, and what you build and show, in the trainee's voice.>

**What is fixed:** <the parts that are the same for everyone, so that the work can be compared>. **What is yours:** <the decisions you make and defend>. <Where the brief lists them.>

| | |
| --- | --- |
| Brief | [<path>](<link to the capstone brief.md>) |
| Checklist | [<path>](<link to the capstone tasks.md>) |
| Write-up template | [<path>](<link to the capstone write-up-template.md>) |
| Constraints | <the main rules, in one line> |
| Cost challenge | <the cost limits, or delete the row> |
| Proofs | <the evidence you must submit> |
| AI tools | <which tools are allowed, what you must log, what you must never paste, and that you must be able to explain and change your work without them> |
| Presentation | <length, questions, and what the panel asks for> |
| You hand in | <what, and where it lives> |
| Assessed by | <the rubric's total, the pass mark, and any condition that must also be met> |

| Rubric criterion | Points | What it covers |
| --- | --- | --- |
| <criterion> | <points> | <what it covers, in one line> |

<How each criterion is scored, what the presentation does and does not carry, and what the trainer supplies.>

## Rules for every stage

These apply to every stage brief, <first> to <last>. A brief repeats only what is specific to its stage. <The capstone restates its own rules in its brief.>

- **<Rule.>** <What it means for you.>
- **Destroy at the end of every stage.** <What is kept, until when.> <Keep resources small and cheap.>
- **Know what it costs before you apply.** Each brief has a Cost row. Look up what each resource in your plan bills and estimate the hourly cost before you apply. <How the estimate is evidence.>
- **Pin everything and commit the lock file.** <The checks that must pass before you call a stage done.>
- **<Rule.>** <What it means for you.>

## What review looks for

Your trainer reviews a stage's build and write-up together and rates each criterion below. <The capstone has its own rubric.>

| Criterion | Excellent | Satisfactory | Needs work |
| --- | --- | --- | --- |
| Definition of done | Every item has real evidence — pasted output or a screenshot, trimmed to the relevant lines and redacted — and the build matches what the write-up says | Every item is addressed, but some evidence is a claim or is hard to follow | An item is missing, unmet or has no evidence |
| Design decisions | Every open design question has a reasoned answer that says what you considered, what you chose and what you gave up | Questions are answered, but the reasons are thin or the trade-off is missing | A question is unanswered, or an answer only restates what you built |
| How to build it | Someone else could follow it from a clean start; you have followed it yourself and it works | It mostly works, with gaps or steps that assume knowledge the reader may not have | It is a summary of what you did rather than a guide, or it was never followed through |
| Concepts | Two or three ideas in your own words, each with an example from your own build | Explained correctly, but generic or close to the documentation's wording | Missing, or wrong |
| What tripped me up | Real obstacles with the exact error text, the cause and the fix. These entries become the course's common-errors list | Obstacles listed without the error text or the cause | Empty, or only polished successes |
| <Subject> practice | <Every rule for every stage is met, and the cost was looked up before applying and noted in the write-up> | <One slip against the rules, which is noted and fixed> | <A rule is broken, or the cost was never considered> |
| AI collaboration log | Specific: which tools, concrete examples, a suggestion that was wrong and how you caught it, and what you wrote yourself — or one line saying none was used | Generic, or no corrected suggestion | Missing |
| Understanding | You explain any part of your work when the trainer asks, without re-reading it | You explain most of it and need prompting on the rest | You cannot explain work you submitted |

**Accepted** means no criterion is Needs work and every item in the definition of done has evidence. Otherwise the stage goes back for revision before the next one starts. A write-up that is Excellent on "How to build it" and on "What tripped me up" is a candidate for the content library.

<One line saying how the capstone's write-up is reviewed and what else it is marked against.>
