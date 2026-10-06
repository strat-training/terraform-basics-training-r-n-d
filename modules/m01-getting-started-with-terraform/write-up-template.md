# M01 — Getting Started with Terraform — Write-up

> This write-up is meant to become part of the content library: write it so the next cohort could learn from it, not just as a record of what you did. Copy this file to `write-up.md` in this folder and fill in the copy; leave this template untouched. Write each section as you build, not after it works. Never paste credentials, tokens or key material anywhere in this file.

| | |
| --- | --- |
| Trainee | |
| Status | Draft <!-- Draft → In review → Revising → Accepted --> |
| Build location | <!-- your GitLab repository and branch or merge request holding your Terraform code --> |
| Hours spent | <!-- an honest total --> |

## What I built

Describe the deliverable named in the brief: what it is, what it does, how it is laid out. A diagram is welcome.

## Why it's built this way (key decisions)

One entry per open design question in the brief, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.

- Which install method would you choose for each tool on each operating system, and what does each choice cost in maintenance and support?
- Which parts of the toolchain must be identical for every learner, which can vary, and what does each choice cost in support?
- What fails differently on Windows than on macOS, and how will a learner tell a broken install from a misconfigured one?
- How will a learner know the toolchain is correct, rather than merely present?
- What problem does Terraform solve that a script or the cloud console does not, and where would you not use it?
- Where did you spend the most time, and why?

## AI collaboration log

If you used AI tools, be specific, not a vague "I used AI to help write some code". If you used none, say so in one line.

- Which AI tool(s) did you use, and for roughly what portion of the work?
- Give 2–3 concrete examples of what you asked for.
- At least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design — what was wrong with it, how you noticed, and what you did instead.
- What did you accept largely as-is, and what did you rewrite or redesign yourself?

## How to build it (teach it to the next engineer)

Write this as a guide someone could actually follow to build this stage from scratch — the order you tackled things in, and why that order made sense. Assume the reader is new to Terraform and to this course.

## Concepts worth explaining

Pick 2–3 ideas from this stage and explain each one in your own words, as if teaching it for the first time. The scope in the brief lists the candidates.

- What Terraform is — infrastructure as code, and the problem Terraform solves
- The core toolchain — AWS/GCP/Azure CLIs, Git, jq, curl, and their purposes
- Installing Terraform (macOS/Windows) and managing versions
- Configuring Visual Studio Code for Terraform work
- A shell that can run the labs' shell scripts on Windows
- Verifying the toolchain end to end — versions, and formatting and validation of a configuration that creates nothing
- OpenTofu differences — optional; you decide whether to include it

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-1: Your write-up shows the actual Terraform version on macOS and on Windows, taken from the version output of each machine at the pinned version (1.11 or later), not the version you expected to have installed.
- DoD-2: Your write-up includes a screenshot from each system of Visual Studio Code with the Terraform extension flagging an error you introduced on purpose, not a screenshot of the extension's install page.
- DoD-3: Every tool in your write-up — the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` — is backed by its real version output from each system, not by a list copied from installation instructions.
- DoD-4: Your write-up shows a version manager switching between two Terraform versions on each system where one works, with the output of the switch; where none works, it says so and says what you tried.
- DoD-5: Your write-up shows formatting and validation passing on a configuration that creates nothing, on both systems, as pasted output, not as a description from memory.
- DoD-6: Every step for an operating system you do not own is verified on a second machine or by a second person, or is marked unverified in your write-up, not assumed to work.
- DoD-7: A learner following your training module on either operating system reaches a working, verified toolchain without asking you anything, because you followed it yourself from a clean state.
- DoD-8: You can answer, unprompted, “what is infrastructure as code, and what does Terraform add to it?” in your own words, and your write-up gives the same answer, not a definition copied from documentation — this doubles as your self-check before M02.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
