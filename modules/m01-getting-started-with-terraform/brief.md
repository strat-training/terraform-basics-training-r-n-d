# M01 — Getting Started with Terraform

| | |
| --- | --- |
| Stage | 1 of 12 |
| Cloud | None are used here. The AWS, Google Cloud and Azure tools are installed, and sandbox access is already provided, so nothing is set up or signed in. |
| Builds on | Nothing |
| Cost | None. No cloud resource is created, so nothing bills. |
| Leaves behind | A working toolchain on your machine. No cloud resources. |

## Objective

Understand what Terraform is and the problem it solves, then install and verify everything needed to perform the labs on your own machine, on macOS or Windows, so that every later stage starts from a working, pinned toolchain. Be able to explain to a newcomer what each tool is for and how to tell that it is installed correctly rather than merely present.

## Scope

### In scope (in the order to tackle)

1. What Terraform is — infrastructure as code, and the problem Terraform solves
2. The core toolchain — AWS/GCP/Azure CLIs, Git, jq, curl, and their purposes
3. Installing Terraform (macOS/Windows) and managing versions
4. Configuring Visual Studio Code for Terraform work
5. A shell that can run the labs' shell scripts on Windows
6. Verifying the toolchain end to end — versions, and formatting and validation of a configuration that creates nothing
7. OpenTofu differences — optional; you decide whether to include it

### Out of scope

- Sandbox access — provided before the course — and signing in to it (M02)
- Creating or managing sandbox accounts, budgets or guardrails — owned outside this course
- Using the Google Cloud and Azure tools (M12)
- Any cloud resource, and any Terraform configuration other than one that creates nothing (from M02 on)

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- Operating systems: macOS and Windows. Your write-up must serve a learner on either one.
- Terraform 1.11 or later at the exact version in `versions.env`. Terraform CLI, not OpenTofu.
- Editor: Visual Studio Code with the HashiCorp Terraform extension.
- Other tools the labs use: the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl`; the labs' scripts are POSIX shell.
- Version manager: `tfenv` or `mise`, on the platforms where it works. Say in the write-up where it does not.
- LocalStack is optional and S3-only. It is not needed for this stage.
- If you own only one of the two operating systems, agree with the trainer how the other will be verified.

## Deliverable

**A verified lab toolchain for macOS and Windows** — Terraform, Visual Studio Code with its Terraform extension, and the cloud and shell tools the labs use — and your written installation guide for both systems (the write-up).

## Open design questions

1. Which install method would you choose for each tool on each operating system, and what does each choice cost in maintenance and support?
2. Which parts of the toolchain must be identical for every learner, which can vary, and what does each choice cost in support?
3. What fails differently on Windows than on macOS, and how will a learner tell a broken install from a misconfigured one?
4. How will a learner know the toolchain is correct, rather than merely present?
5. What problem does Terraform solve that a script or the cloud console does not, and where would you not use it?

## Definition of done

- [ ] **DoD-1** Terraform at the pinned version (1.11 or later), the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` run on macOS and on Windows (version output pasted for each).
- [ ] **DoD-2** Visual Studio Code with the Terraform extension is installed on both systems, and the editor flags a deliberately introduced error in a configuration (screenshot for each).
- [ ] **DoD-3** A version manager switches between two Terraform versions on each system where one works; where none does, the write-up says so (output pasted).
- [ ] **DoD-4** Formatting and validation checks pass on a configuration that creates nothing, on both systems (output pasted).
- [ ] **DoD-5** The steps for any operating system you do not own are verified on a second machine or by a second person, or are marked unverified in the write-up.
- [ ] **DoD-6** Your write-up takes a first-time learner on either operating system to DoD-1 and DoD-2 unaided — verified by you following it end to end from a clean state.
- [ ] **DoD-7** Your write-up explains, in your own words, what infrastructure as code is and what Terraform adds to it.

## Best practices this stage demonstrates

- Pinned versions (the toolchain's pinned Terraform version)
- fmt and validate (the verification configuration)
