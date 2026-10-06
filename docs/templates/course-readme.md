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
| `modules/m10-capstone/` | The capstone, with its own brief, checklist and write-up template |

The other folders are trainer material. You do not need them to do the stages.

## How a stage works

1. **Your trainer hands you the brief.** Each stage's `brief.md` says what to build and how you will know it is done: objective, scope, stack constraints, the named deliverable, a lab, a definition of done, and what to confirm with your trainer before you start. It contains no lesson, no steps, no code and no solutions. How to build it is yours to work out.
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
| `tasks.md` | Your trainer | An ordered checklist for the stage, one task per scope topic, deliverable component, check and write-up section. You tick the boxes; it holds no answers and no steps. |

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
- **Know what it costs before you apply.** Each brief's stack constraints say what the stage may bill. Look up what each resource in your plan bills and estimate the hourly cost before you apply. <How the estimate is evidence.>
- **Pin everything and commit the lock file.** <The checks that must pass before you call a stage done.>
- **<Rule.>** <What it means for you.>

## What review looks for

Your trainer reviews what you built and what you wrote together, against one rubric. <The capstone has its own rubric.>

<!-- Keep one table for the build and the write-up together, with between three and six criteria, and the points adding up to 100 (or change the pass mark below to match your total). -->

| Criterion | Graded on | Points | Excellent | Satisfactory | Needs work |
| --- | --- | --- | --- | --- | --- |
| Deliverable and definition of done | Build and write-up | <25> | Everything the brief names is there and works as described, and a reviewer can run it from a clean start and get what your write-up says. Every definition-of-done item is met and shown in the write-up with real evidence — pasted output or a screenshot, trimmed to the relevant lines and redacted | The deliverable is mostly there, or it works only after a fix you made during review. Every item is addressed, but some evidence is a claim or is hard to follow | Parts of the deliverable are missing, or it does not run. An item is unmet, or has no evidence |
| <Subject> quality, security and cost | Build | <20> | <Clear and well organised, follows the brief's constraints, and the checks the stage requires pass. No stored credentials. Everything the brief says to destroy is gone, confirmed from the provider's side. You looked up what each resource bills before you applied, and your estimate is in the write-up> | <It works but is untidy, or has one slip against the constraints or the safety rules, which you caught and fixed. Or the cost estimate was made after applying> | <It is hard to follow or breaks a constraint. Or there is a stored credential or a resource left running, or the cost was never considered> |
| Design decisions | Write-up | <15> | Every research prompt in the brief has a reasoned answer that says what you considered, what you chose and what you gave up, and the answers match what you built | Questions are answered, but the reasons are thin or the trade-off is missing | A question is unanswered, or an answer only restates what you built |
| How to build it | Write-up | <20> | Someone else could follow it from a clean start and end up with your build; you have followed it yourself and it works | It mostly works, with gaps or steps that assume knowledge the reader may not have | It is a summary of what you did rather than a guide, or it was never followed through |
| Concepts, obstacles and AI log | Write-up | <10> | Two or three concepts in your own words, each with an example from your own build. "What tripped me up" lists real obstacles with the exact error text, the cause and the fix; these entries become the course's common-errors list. The AI log is specific: which tools, concrete examples, a suggestion that was wrong and how you caught it, and what you wrote yourself — or one line saying none was used | Concepts are correct but generic or close to the documentation's wording, or the obstacles are listed without the error text or the cause, or the AI log is generic or has no corrected suggestion | A section is missing or wrong, the obstacles are only polished successes, or there is no AI log |
| Understanding | Build and write-up | <10> | You explain any part of your build and your write-up when the trainer asks, without re-reading it | You explain most of it and need prompting on the rest | You cannot explain work you submitted |

### How a stage is graded

1. Your trainer runs your build from a clean start and reads your write-up.
2. Each criterion is scored from 0 to its points. Excellent is <80%> or more of the points, Satisfactory is <50% to 79%>, and Needs work is under <50%>.
3. The scores are added up to a total out of <100>.
4. The stage is **accepted** when the total is <70> or more and both of these are true: <the deliverable works and every item in the definition of done is met and evidenced>; and <the safety conditions that always fail a stage, such as a stored credential or a resource left running>.
5. Otherwise the stage goes back to you with the criteria to fix, and you revise it before starting the next one.

A stage that scores <90> or more is a candidate for the content library.

<One line saying how the capstone's build and write-up are marked and what else it is checked against.>
