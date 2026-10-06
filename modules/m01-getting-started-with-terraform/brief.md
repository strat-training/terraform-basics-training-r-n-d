# M01 — Getting Started with Terraform Brief

**Stage:** 1 of 11 · **Builds on:** — (course entry point) · **Feeds into:** M02, M11

## Objective

By the end of this stage, you can explain what Terraform is and the problem it solves, and show a working, pinned toolchain for the labs on your own machine, on macOS or Windows — using your own terminal output as the evidence, not an installation page. You can tell a newcomer what each tool is for, and how to tell that it is installed correctly rather than merely present.

## Scope

You set up and inspect your own machine, not a worked example. Find out, and write down in your own words:

- **What Terraform is** — infrastructure as code, and the problem Terraform solves. Research: what problem Terraform solves that a script or the cloud console does not, and where you would not use it.
- **The core toolchain** — AWS/GCP/Azure CLIs, Git, jq, curl, and their purposes. Research: which install method fits each tool on each operating system, and what each choice costs in maintenance and support.
- **Installing Terraform (macOS/Windows) and managing versions** — at the pinned version on each system, and switching between Terraform versions with a version manager. Research: which parts of the toolchain must be identical for every learner, which can vary, and what each choice costs in support.
- **Configuring Visual Studio Code for Terraform work** — installing the editor and the Terraform extension, and an editor that flags your mistakes. Research: what the extension adds to the editor, and how you can tell it is doing its job rather than merely installed.
- **A shell that can run the labs' shell scripts on Windows** — making the labs' shell scripts run on a Windows machine. Research: what fails differently on Windows than on macOS, and how a learner can tell a broken install from a misconfigured one.
- **Verifying the toolchain end to end** — versions, and formatting and validation of a configuration that creates nothing. Research: how a learner will know the toolchain is correct, rather than merely present.
- **OpenTofu differences** — optional; you decide whether to include it. Research: where OpenTofu and Terraform differ, if you choose to cover it.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- You work on macOS or Windows, and your notes must serve a learner on either one.
- If you own only one of the two, agree with your trainer how the other will be verified.
- Terraform is 1.11 or later at the exact version in `versions.env`, and you use the Terraform CLI, not OpenTofu.
- Your editor is Visual Studio Code with the HashiCorp Terraform extension, and the other tools the labs use are the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl`.
- The labs' scripts are POSIX shell.
- For switching versions, use `tfenv` or `mise` on the platforms where one works, and say in your notes where neither does.
- LocalStack is optional and S3-only, and you do not need it for this stage.
- Sandbox access is provided before the course and signing in to it is M02, so no cloud resource is created here and nothing bills.

## Deliverable

**A verified lab toolchain for macOS and Windows** — Terraform, Visual Studio Code with its Terraform extension, and the cloud and shell tools the labs use — and your written installation guide for both systems (the write-up).

## Lab

**Goal.** Get a working, verified toolchain for the labs on your own machine, on macOS or Windows, that every later stage starts from.

**You do, on your own machine.** Install and verify the tools the labs need, set up the editor for Terraform, switch between Terraform versions, and run formatting and validation on a configuration that creates nothing.

**You build and capture.** The toolchain is your deliverable. Capture the version output for each tool on each system, the editor flagging an error you introduced on purpose, and the validation result; each one goes straight into your installation guide.

**Clean-up.** Nothing to destroy: no cloud resource is created.

## Definition of done

- DoD-01: Your notes name the actual Terraform version on macOS and on Windows, at the pinned version (1.11 or later), and show the real version output of the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` on each system, not the versions you expected to have installed.
- DoD-02: Visual Studio Code with the Terraform extension is installed on both systems, and a screenshot from each shows the editor flagging an error you introduced on purpose, not the extension's install page.
- DoD-03: A version manager switches between two Terraform versions on each system where one works, with the output of the switch pasted; where none works, your notes say so, not that it was skipped.
- DoD-04: Formatting and validation pass on a configuration that creates nothing, on both systems, with the output pasted, not described from memory.
- DoD-05: Every step for an operating system you do not own is verified on a second machine or by a second person, or is marked unverified, not assumed to work.
- DoD-06: Your write-up takes a first-time learner on either operating system to a working toolchain unaided — verified by you following it end to end from a clean state.
- DoD-07: You can answer, unprompted, “what is infrastructure as code, and what does Terraform add to it?” in your own words, not with a definition copied from documentation.

## Best practices this stage demonstrates

- Pinned versions (the toolchain's pinned Terraform version)
- fmt and validate (the verification configuration)

## Still open / ask your trainer

- How the operating system you do not own will be verified.
- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
