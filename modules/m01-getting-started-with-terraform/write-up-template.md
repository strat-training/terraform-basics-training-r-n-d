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

One entry per research prompt in the brief's scope, then one for where you spent the most time. Say what you considered, what you chose, why, and what you gave up.

- What problem Terraform solves that a script or the cloud console does not, and where you would not use it.
- Which install method fits each tool on each operating system, and what each choice costs in maintenance and support.
- Which parts of the toolchain must be identical for every learner, which can vary, and what each choice costs in support.
- What the extension adds to the editor, and how you can tell it is doing its job rather than merely installed.
- What fails differently on Windows than on macOS, and how a learner can tell a broken install from a misconfigured one.
- How a learner will know the toolchain is correct, rather than merely present.
- Where OpenTofu and Terraform differ, if you choose to cover it.
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

- What Terraform is
- The core toolchain
- Installing Terraform (macOS/Windows) and managing versions
- Configuring Visual Studio Code for Terraform work
- A shell that can run the labs' shell scripts on Windows
- Verifying the toolchain end to end
- OpenTofu differences

## What tripped me up

The real obstacles — errors, wrong assumptions, anything that cost you real time. Keep the exact error text; these become the course's common-errors list.

## Checkpoint evidence

Show the evidence for every item in the definition of done in `brief.md`, one by one. Paste real output trimmed to the relevant lines, or link a screenshot, and redact anything sensitive.

- DoD-01: Your notes name the actual Terraform version on macOS and on Windows, at the pinned version (1.11 or later), and show the real version output of the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` on each system, not the versions you expected to have installed.
- DoD-02: Visual Studio Code with the Terraform extension is installed on both systems, and a screenshot from each shows the editor flagging an error you introduced on purpose, not the extension's install page.
- DoD-03: A version manager switches between two Terraform versions on each system where one works, with the output of the switch pasted; where none works, your notes say so, not that it was skipped.
- DoD-04: Formatting and validation pass on a configuration that creates nothing, on both systems, with the output pasted, not described from memory.
- DoD-05: Every step for an operating system you do not own is verified on a second machine or by a second person, or is marked unverified, not assumed to work.
- DoD-06: Your write-up takes a first-time learner on either operating system to a working toolchain unaided — verified by you following it end to end from a clean state.
- DoD-07: You can answer, unprompted, “what is infrastructure as code, and what does Terraform add to it?” in your own words, not with a definition copied from documentation.

## Definition-of-done self-assessment

Score yourself honestly against every item in the definition of done in `brief.md` before your trainer reviews it: met, partly met or not met, and why. Then rate yourself against each criterion of the stage rubric in the README. Name any part of your own work you would struggle to explain cold, without re-reading it first.

## What I'd do differently

If you started this stage over today, what would you change?
