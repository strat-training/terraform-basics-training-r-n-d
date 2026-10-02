# M08 — Terraform for Multi-Environment Deployments — Tasks

**Objective:** Deploy two environments — dev and prod — from one configuration with separate state, laid out, named and tagged so consistently that anyone can tell which environment a resource belongs to at a glance. Be able to say when you would use workspaces or a directory per environment instead.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that each stage named under "Builds on" in the brief (M05, M07) has been accepted, and that you have the access and tools its stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: One configuration, many environments — what is shared and what must be separate
- [ ] Work on: Per-environment input values
- [ ] Work on: Per-environment backend settings and separate state keys in the shared bucket
- [ ] Work on: Blast radius — what separate state does and does not protect
- [ ] Work on: The standard file layout for a root configuration
- [ ] Work on: A naming convention and required tags applied through provider defaults
- [ ] Work on: Switching between environments safely
- [ ] Work on: Other ways to separate environments — a directory per environment, and workspaces — and when each fits (explained, not used)
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: What makes it easy to apply one environment's values to the other's state, and what will you do to make that harder?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: Which tags would a clean-up or cost report need beyond `Environment`, and why?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: How should the files be laid out so a newcomer finds each concern without being told?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: When would workspaces be the right tool, and what do you give up by not using them here?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: When would a directory per environment be the right tool, and what do you give up by not using it here?
- [ ] Decide, and record your reasons under “Why it's built this way (key decisions)”: In what ways does keeping both environments in one account misrepresent real practice?
- [ ] Have ready: One configuration deployed as both dev and prod with separate state
- [ ] Have ready: a note comparing three ways to separate environments

## Verify

- [ ] Confirm DoD-1: Two state objects exist in the bucket under different keys (listing pasted). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: Both environments produce clean plans (output for each). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Environment-specific inputs differ between the two environments and live outside the main configuration files. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: Every resource follows the naming convention and carries the required tags (shown from the plan, state or cloud side). Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: The file layout follows the standard root-configuration layout; a reviewer can find each concern from file names alone. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: The comparison note is present and covers a directory per environment, workspaces, and the per-environment files you used, saying when each fits. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: Both environments are destroyed and the bucket is retained, confirmed from the cloud side. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] Under “Why it's built this way (key decisions)”: One entry per open design question in the brief, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader has completed the earlier stages this one builds on but hasn't built this stage before.
- [ ] Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
