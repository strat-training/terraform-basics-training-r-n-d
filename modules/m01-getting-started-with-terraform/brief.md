# M01 — Getting Started with Terraform

| | |
| --- | --- |
| Stage | 1 of 12 |
| Course reference | Module 1 / Activity 1 "Toolchain" (solution-design §6.2), reworked at the trainer's request: sandbox access is provided before the course, so this stage installs and verifies tools only; sign-in moves to M02. See [README](../README.md#open-items-for-the-trainer). |
| Cloud | None are used here. The AWS, Google Cloud and Azure tools are installed, and sandbox access is already provided, so nothing is set up or signed in. |
| Builds on | Nothing |
| Time box | TBC — see [README](../README.md#open-items-for-the-trainer) |
| Leaves behind | A working toolchain on your machine. No cloud resources. |

## Objective

Understand what Terraform is and the problem it solves, then install and verify everything needed to perform the labs on your own machine, on macOS or Windows, so that every later stage starts from a working, pinned toolchain. Be able to explain to a newcomer what each tool is for and how to tell that it is installed correctly rather than merely present.

## Scope

### In scope (in the order to tackle)

1. What Terraform is — infrastructure as code, and the problem Terraform solves
2. The tools the labs need, and what each one is for
3. Installing Terraform at the pinned version on macOS
4. Installing Terraform at the pinned version on Windows
5. Visual Studio Code for Terraform work — installation and the Terraform extension
6. The AWS, Google Cloud and Azure command-line tools, plus Git, `jq` and `curl`
7. A shell that can run the labs' shell scripts on Windows
8. Switching between Terraform versions with a version manager
9. The pinned dev container as an alternative to installing locally
10. Verifying the toolchain end to end — versions, and formatting and validation of a configuration that creates nothing
11. OpenTofu differences — an ungraded sidebar

### Out of scope

- Sandbox access — provided before the course — and signing in to it (M02)
- Creating or managing sandbox accounts, budgets or guardrails — owned outside the program (ADR-005)
- Using the Google Cloud and Azure tools (M12)
- Authoring the dev container image or its CI build
- Any cloud resource, and any Terraform configuration other than one that creates nothing (from M02 on)

## Stack constraints

- Everything under [Rules for every stage](../README.md#rules-for-every-stage).
- Operating systems: macOS and Windows. Your write-up must serve a learner on either one.
- Terraform 1.11 or later at the exact version in `versions.env`. Terraform CLI, not OpenTofu (ADR-002).
- Editor: Visual Studio Code with the HashiCorp Terraform extension.
- Other tools the labs use: the AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl`; the labs' scripts are POSIX shell (ADR-004, ADR-009).
- Version manager: `tfenv` or `mise`, on the platforms where it works. Say in the write-up where it does not.
- Dev container: Docker or Podman. It is an alternative path, not a replacement for the local install. If your laptop cannot run containers, tell the trainer (ADR-004).
- LocalStack is optional and S3-only. It is not needed for this stage.
- If you own only one of the two operating systems, agree with the trainer how the other will be verified.

## Deliverable

**A verified lab toolchain for macOS and Windows** — Terraform, Visual Studio Code with its Terraform extension, and the cloud and shell tools the labs use — and your written installation guide for both systems (the write-up).

## Open design questions

1. Which install method would you choose for each tool on each operating system, and what does each choice cost in maintenance and support?
2. Which parts of the toolchain must be identical for every learner, which can vary, and what does each choice cost in support?
3. What fails differently on Windows than on macOS, and how will a learner tell a broken install from a misconfigured one?
4. How will a learner know the toolchain is correct, rather than merely present?
5. Why might a team prefer the local install over the dev container, or the reverse, and what does each give up?
6. What problem does Terraform solve that a script or the cloud console does not, and where would you not use it?

## Definition of done

- [ ] **DoD-1** Terraform at the pinned version (1.11 or later) runs on macOS and on Windows (version output pasted for each).
- [ ] **DoD-2** Visual Studio Code with the Terraform extension is installed on both systems, and the editor flags a deliberately introduced error in a configuration (screenshot for each).
- [ ] **DoD-3** The AWS, Google Cloud and Azure command-line tools, Git, `jq` and `curl` run on both systems (version output pasted for each).
- [ ] **DoD-4** A version manager switches between two Terraform versions on each system where one works; where none does, the write-up says so (output pasted).
- [ ] **DoD-5** The pinned dev container starts and runs the same Terraform version (version output pasted).
- [ ] **DoD-6** Formatting and validation checks pass on a configuration that creates nothing, on both systems (output pasted).
- [ ] **DoD-7** The steps for any operating system you do not own are verified on a second machine or by a second person, or are marked unverified in the write-up.
- [ ] **DoD-8** Your write-up takes a first-time learner on either operating system to DoD-1 through DoD-3 unaided — verified by you following it end to end from a clean state.
- [ ] **DoD-9** Your write-up explains, in your own words, what infrastructure as code is and what Terraform adds to it.

## Best practices this stage demonstrates

- Pinned versions (the toolchain's pinned Terraform version)
- fmt and validate (the verification configuration)
