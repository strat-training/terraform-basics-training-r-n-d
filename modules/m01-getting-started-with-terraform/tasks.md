# M01 — Getting Started with Terraform — Tasks

**Objective:** Understand what Terraform is and the problem it solves, then install and verify everything needed to perform the labs on your own machine, on macOS or Windows, so that every later stage starts from a working, pinned toolchain. Be able to explain to a newcomer what each tool is for and how to tell that it is installed correctly rather than merely present.

> There is no solutions file for this stage. This checklist guides the work — it doesn't contain it. See `brief.md` for the full requirements, the stack constraints and the definition of done, and fill in `write-up.md` — your copy of `write-up-template.md` — as you go, not after.

## Setup

- [ ] Read `brief.md` from top to bottom, including its cost, stack constraints and out-of-scope list, and the rules for every stage in the [README](../../README.md#rules-for-every-stage). Ask the trainer about anything unclear before you build.
- [ ] Copy `write-up-template.md` to `write-up.md` in this folder and fill in the header table. Leave the template itself untouched.
- [ ] Confirm that you have the access and tools the brief's stack constraints require. Raise anything missing with the trainer before you build.

## Build

- [ ] Work on: What Terraform is — infrastructure as code, and the problem Terraform solves
- [ ] Work on: The core toolchain — AWS/GCP/Azure CLIs, Git, jq, curl, and their purposes
- [ ] Work on: Installing Terraform (macOS/Windows) and managing versions
- [ ] Work on: Configuring Visual Studio Code for Terraform work
- [ ] Work on: A shell that can run the labs' shell scripts on Windows
- [ ] Work on: Verifying the toolchain end to end — versions, and formatting and validation of a configuration that creates nothing
- [ ] Work on: OpenTofu differences — optional; you decide whether to include it
- [ ] Have ready: A verified lab toolchain for macOS and Windows — Terraform, Visual Studio Code with its Terraform extension, and the cloud and shell tools the labs use
- [ ] Have ready: your written installation guide for both systems (the write-up)

## Verify

- [ ] Confirm DoD-1: Your write-up shows the actual Terraform version on macOS and on Windows, taken from the version output of each machine at the pinned version (1.11 or later), not the version you expected to have installed. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-2: Your write-up includes a screenshot from each system of Visual Studio Code with the Terraform extension flagging an error you introduced on purpose, not a screenshot of the extension's install page. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-3: Every tool in your write-up — the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` — is backed by its real version output from each system, not by a list copied from installation instructions. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-4: Your write-up shows a version manager switching between two Terraform versions on each system where one works, with the output of the switch; where none works, it says so and says what you tried. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-5: Your write-up shows formatting and validation passing on a configuration that creates nothing, on both systems, as pasted output, not as a description from memory. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-6: Every step for an operating system you do not own is verified on a second machine or by a second person, or is marked unverified in your write-up, not assumed to work. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-7: A learner following your training module on either operating system reaches a working, verified toolchain without asking you anything, because you followed it yourself from a clean state. Capture the evidence under “Checkpoint evidence”.
- [ ] Confirm DoD-8: You can answer, unprompted, “what is infrastructure as code, and what does Terraform add to it?” in your own words, and your write-up gives the same answer, not a definition copied from documentation — this doubles as your self-check before M02. Capture the evidence under “Checkpoint evidence”.

## Write-up

- [ ] Under “What I built”: Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.
- [ ] Under “Why it's built this way (key decisions)”: One entry per open design question in the brief, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.
- [ ] Under “AI collaboration log”: If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.
- [ ] Under “How to build it (teach it to the next engineer)”: Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader is new to Terraform and to this course.
- [ ] Under “Concepts worth explaining”: Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.
- [ ] Under “What tripped me up”: The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.
- [ ] Under “Checkpoint evidence”: Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.
- [ ] Under “Definition-of-done self-assessment”: Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README.
- [ ] Under “What I'd do differently”: If you started this stage over today, what would you change?
- [ ] Final self-review: go back through this list, the brief's definition of done and your write-up. Every item is ticked, or you have written down why not and told the trainer. Then set Status in `write-up.md` to “In review” and tell the trainer the stage is ready for review.
