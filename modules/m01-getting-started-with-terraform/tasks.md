# M01 — Getting Started with Terraform — Tasks

**Objective:** By the end of this stage, you can explain what Terraform is and the problem it solves, and show a working, pinned toolchain for the labs on your own machine, on macOS or Windows — using your own terminal output as the evidence, not an installation page. You can tell a newcomer what each tool is for, and how to tell that it is installed correctly rather than merely present.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its stack constraints, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Check its “Still open / ask your trainer” list, and ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that you have the access and tools the brief's stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: What Terraform is
- [ ] Work on: The core toolchain
- [ ] Work on: Installing Terraform (macOS/Windows) and managing versions
- [ ] Work on: Configuring Visual Studio Code for Terraform work
- [ ] Work on: A shell that can run the labs' shell scripts on Windows
- [ ] Work on: Verifying the toolchain end to end
- [ ] Work on: OpenTofu differences
- [ ] Have ready: A verified lab toolchain for macOS and Windows — Terraform, Visual Studio Code with its Terraform extension, and the cloud and shell tools the labs use
- [ ] Have ready: your written installation guide for both systems (the write-up)

## Verify

- [ ] Confirm DoD-01: Your notes name the actual Terraform version on macOS and on Windows, at the pinned version (1.11 or later), and show the real version output of the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` on each system, not the versions you expected to have installed. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-02: Visual Studio Code with the Terraform extension is installed on both systems, and a screenshot from each shows the editor flagging an error you introduced on purpose, not the extension's install page. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-03: A version manager switches between two Terraform versions on each system where one works, with the output of the switch pasted; where none works, your notes say so, not that it was skipped. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-04: Formatting and validation pass on a configuration that creates nothing, on both systems, with the output pasted, not described from memory. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-05: Every step for an operating system you do not own is verified on a second machine or by a second person, or is marked unverified, not assumed to work. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-06: Your write-up takes a first-time learner on either operating system to a working toolchain unaided — verified by you following it end to end from a clean state. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-07: You can answer, unprompted, “what is infrastructure as code, and what does Terraform add to it?” in your own words, not with a definition copied from documentation. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] Under “Why it's built this way (key decisions)”: One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader is new to Terraform and to this course.
- [ ] Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
