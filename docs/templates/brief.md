# <Stage ID> — <Stage title>

<!--
TEMPLATE: stage brief. Copy to modules/<stage-folder>/brief.md and replace every <placeholder>.
Delete these comments when you are done. The brief is the trainer's handoff to the trainee, and
nothing else: objective, scope, stack constraints, a named deliverable, open design questions and an
observable definition of done.

It contains NO lesson content, NO steps, NO code and NO solutions. If a line tells the trainee what
to choose or why, it belongs in the trainee's write-up, not here. Check every scope item, constraint
and definition-of-done line against the open design questions: none of them may answer a question.
-->

| | |
| --- | --- |
| Stage | <n> of <total> |
| Cloud | <which clouds the stage touches, and what is already provided> |
| Builds on | <earlier stages that must be accepted first, or "Nothing"> |
| Cost | <what the stage may bill, and what to look up before applying; or "None"> |
| Leaves behind | <what survives the stage, or "Nothing"> |

## Objective

<One paragraph. What the trainee will be able to do or explain at the end, in terms they can observe.>

## Scope

### In scope (in the order to tackle)

<!-- Topics, not steps. Each item is something to learn or build, phrased as a noun phrase. -->

1. <topic>
2. <topic>
3. <topic>

### Out of scope

- <thing the trainee should not do here, and the stage that owns it if there is one>

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- <constraint specific to this stage: versions, tools, regions, sizes, names>
- <constraint specific to this stage>

## Deliverable

**<One named deliverable>** — <its components, split at "and", "plus" or ", with">, and your written guide to building it (the write-up).

## Open design questions

<!--
Questions the trainee must reason out and record in "Why it's built this way". Each one asks for a
choice and its cost. Never answer one anywhere else in the brief.
-->

1. <question: which option would you choose, and what does it cost or give up?>
2. <question>
3. <question>

## Definition of done

<!--
Centre it on the trainee's training module: the build plus the write-up that teaches it. Write every item in
one pattern: <the artifact> + <a specific, observable result>, not <the weaker thing people settle for>, with
real evidence from the trainee's own environment (output, a screenshot, a listing). Examples of the pattern:
  - Your notes name your system's actual kernel version and distribution, not generic facts copied from documentation.
  - Every claim in your notes is backed by real output from your own terminal, not paraphrased from memory.
  - You can answer, unprompted, "<a question from this stage>" using the concepts from this stage.
Use "Every ..." for a rule that holds throughout, and add a self-check question where a stage ends in one.
Keep the item "A learner following your training module ends with ..." and keep to eight items or fewer.
Each item is observable: someone else can verify it from evidence. IDs are stable.
-->

Your training module — the build plus the write-up that teaches it — is done when each of these is true.

- [ ] **DoD-1** Your write-up shows <a specific observable result>, as real output from your own <machine or account>, not <the weaker substitute> (<evidence: output pasted, screenshot, plan summary>).
- [ ] **DoD-2** Every <claim or step> in your write-up is backed by <real evidence>, not <paraphrased from memory>.
- [ ] **DoD-3** A learner following your training module ends with <observable end state>, confirmed from <where>, not only from <the weaker check>.
- [ ] **DoD-4** You can answer, unprompted, “<a question from this stage>” using the concepts from this stage, and your write-up gives the same answer.

## Best practices this stage demonstrates

- <practice> (<where in this stage it shows up>)
