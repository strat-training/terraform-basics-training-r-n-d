# M08 Write-Up — Change with Confidence: Safe Terraform Refactoring

Fill this in as you go, not after the fact. Write it so a trainee starting this stage next cohort could follow your path on their own. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Never paste credentials, tokens or key material.

## What I built

The small configuration after its three refactors — a rename, an adoption and a stop-managing — with the saved plans that show no destroys, and your note on legacy state commands (link your repository).

## Why it's built this way (key decisions)

- How can you tell before applying that a refactor won't touch real infrastructure, and how do you avoid orphaned cost when you stop managing a resource?
- What did the generated configuration get wrong or leave out, and how did you decide what to keep?
- Why prefer changes that appear in a plan over commands that edit state, and when might you still meet those commands?
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write a guide to a rename, an adoption and a stop-managing with no destroys, using your own plans to show the reasoning, not just the blocks and commands.

## Concepts worth explaining

Pick 2–3 ideas — reading plans as JSON with `jq`, recovering from a partial apply or a failed destroy, or targeted operations — and explain each in your own words.

## What tripped me up

Anything that didn't behave the way you expected the first time. Keep the exact error text.

## Checkpoint evidence

Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. The definition of done in `brief.md` still applies in full.

- DoD-01: the saved-plan summary after each of the three refactors showing no destroys or replacements, and your `jq` output listing the action on every resource.
- DoD-02: the output showing the renamed resource kept its identity, the adopted resource plans clean, and the stopped resource still exists in AWS.
- DoD-03: the diff for each refactor, and your list of every command you ran against state.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over, what would you do differently?
