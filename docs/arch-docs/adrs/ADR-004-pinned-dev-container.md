# ADR-004: Pinned dev container, run locally; GitLab Workspaces optional

- **Status:** Accepted (amended by [ADR-016](ADR-016-gitlab-for-hosting-and-ci.md): the PRD named GitHub Codespaces, but the code is hosted on GitLab)
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.3, s.11, s.13 (FR-3, CR-1)

## Context

Terraform activities are sensitive to tool versions (for example, native S3 locking needs Terraform 1.11 or later). Learners use varied laptops. Environment problems are a leading cause of early drop-off in self-paced technical courses.

The PRD assumed GitHub Codespaces as the browser-based option. The code will be hosted on GitLab (ADR-016), which has no Codespaces equivalent that works everywhere: GitLab Workspaces exist but depend on the GitLab tier and on a Kubernetes agent set up by the GitLab administrators. [TBD: confirm with the GitLab owner whether Workspaces are available and for which groups.]

## Decision

Ship a **dev container** definition in the starter repository, built as a single image and **run locally** with VS Code Dev Containers or any dev-container tool on Docker or Podman. The image is built by GitLab CI and pushed to the project's **GitLab Container Registry**; CI jobs use the same image. It pins:

- Terraform 1.11 or later (exact version from `versions.env`)
- AWS CLI, `gcloud`, Azure CLI
- Terraform language server, plus the shell tools the check scripts need (`jq`, `curl`, and similar)

**GitLab Workspaces are an optional, second path** for learners without a container-capable laptop, offered only if the GitLab owner enables them for the group. The same dev container definition (or an equivalent devfile derived from it) is used so there is one source of tool versions.

Module 1 also teaches a **local install path** using a version manager (`tfenv` or `mise`) for learners who prefer it, but the dev container is the supported path.

**LocalStack** is optional, for S3-only offline practice. Anything involving VPC or EC2 behaviour runs against real AWS.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Local install only | Version drift, support burden |
| GitHub Codespaces (as in the PRD) | Needs the code on GitHub; mirroring a GitLab repo to GitHub only for Codespaces adds a second platform, sync and sign-in |
| Third-party cloud IDE that opens GitLab repositories | Extra vendor, contract and cost; not chosen unless GitLab Workspaces are unavailable and a browser path proves essential |
| GitLab Web IDE alone | Edits files but does not run the Terraform and cloud CLIs the activities need |
| LocalStack for everything | VPC/EC2 emulation differs from real AWS; teaches wrong behaviours |

## Consequences

**Positive**
- Reproducible environment; CI uses the same image, so what passes in CI passes for learners.
- No per-hour cloud IDE cost for the default path.
- Works with the GitLab Container Registry the team already has, with nothing new to procure.

**Negative / trade-offs**
- **Prerequisite change:** the PRD says learners need a laptop that can install CLI tools "or a browser for the provided dev container". Without Workspaces, every learner needs Docker or Podman on their machine, which some corporate laptops restrict. The pre-assessment (PRD s.3) should check for this, and the PRD wording should be updated (see ADR-016 and solution design A11).
- If Workspaces are enabled, they need administrator setup and compute capacity that this program does not own, and learners' cloud logins must work in them.
- Authentication flows needing a browser (`aws sso login`, `gcloud auth ... login`, `az login`) must use device-code or port-forward modes inside remote workspaces and containers; Module 1 and 10 must document this.
