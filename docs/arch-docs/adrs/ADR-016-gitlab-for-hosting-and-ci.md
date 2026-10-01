# ADR-016: Host the starter repository and content CI on GitLab

- **Status:** Accepted (stakeholder direction, 2026-10-01; changes PRD wording)
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee) to record in the PRD
- **PRD references:** s.11 (starter repository, dev container), s.13 (FR-1, FR-3, FR-7, CR-1, CR-8), s.14 (dependencies: "A GitHub organization ... plus Codespaces and Actions")
- **Amends:** ADR-001 (hosting), ADR-004 (dev environment), ADR-010 (CI mechanics)

## Context

The PRD names GitHub, Codespaces and GitHub Actions. The teams that will run and take the program keep their code in **GitLab**. [ASSUMPTION: this applies both to the program's starter repository and to the learners' own repositories; the instance type (gitlab.com or self-managed), the tier and the runner setup are not yet known.]

The platform change touches three areas: where content lives and how learners copy it, how CI runs, and how learners get the pinned toolchain.

## Decision

1. **Hosting.** The starter repository is a project in a **GitLab group**. Learners fork it, or use it as a template, into their own namespace or a cohort subgroup. Their "what broke and what I learned" notes and capstone repositories live there too.
2. **CI/CD.** Content CI is defined in **`.gitlab-ci.yml`**, using `rules:` on `$CI_PIPELINE_SOURCE` to separate three pipeline types: **merge request pipelines** (per-change tests), **scheduled pipelines** (weekly pinned run and non-blocking latest-provider canary), and **tag pipelines** (version bumps and releases). Everything in ADR-010 is unchanged in substance.
3. **Cloud authentication in CI.** Real-cloud CI jobs authenticate with **GitLab CI/CD ID tokens (OIDC)** federated to AWS (IAM role with web identity), GCP (workload identity federation) and Azure (federated credential). **No cloud keys are stored in CI variables.**
4. **Review.** Capstone peer review (FR-7) uses **merge requests** in a shared group, with the rubric supplied as a **merge request template** under `.gitlab/merge_request_templates/`.
5. **Dev environment.** The dev container image is built in CI and stored in the project's **Container Registry** (ADR-004).
6. **Terraform state is not hosted in GitLab.** GitLab offers its own managed Terraform state, but the program teaches the **S3 backend with native locking** (ADR-006), so GitLab-managed state is not used and is mentioned only as an option learners may meet.
7. **Documentation.** The Markdown modules render in GitLab, including tables and Mermaid diagrams. A published docs site (for example with GitLab Pages) remains optional and does not change ADR-001.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| GitHub, as written in the PRD | The teams' code lives in GitLab; learners and reviewers would need a second platform and account |
| GitLab as the home, mirrored to GitHub for Codespaces and Actions | Two platforms to keep in sync, double the access control, split issue and review history, and mirroring only to get a cloud IDE is not worth it |
| Another CI tool (Jenkins, others) | GitLab CI/CD is already part of the chosen platform; a second CI adds cost and ownership without benefit |
| Keep GitHub only for the public course content | Reasonable only if the program is meant to be public; the PRD does not say so |

## Consequences

**Positive**
- Learners and reviewers work in the platform they already use, so the Git prerequisites in the PRD (clone, branch, commit, pull or merge request) apply directly.
- CI, container registry, merge requests and review live in one product.
- No stored cloud keys in CI, consistent with the program's own best practice.

**Negative / trade-offs**
- **PRD changes are needed**: s.13 FR-3 ("dev container or Codespace"), s.3 prerequisite ("or a browser"), s.14 dependencies ("GitHub organization ... Codespaces and Actions") and "pull request" wording in s.3 and FR-7 must be updated. The PRD still says GitHub.
- There is **no Codespaces equivalent by default** (see ADR-004). Zero-install browser access depends on GitLab Workspaces being enabled.
- GitLab runners must be able to **build the dev container image** (for example with rootless builders such as Kaniko or Buildah, or Docker-in-Docker) and run Terraform plus the cloud CLIs. [TBD: runner type and permitted build method, from the GitLab owner.]
- If the instance is **self-managed**, AWS, GCP and Azure must be able to reach its OIDC issuer URL to trust the ID tokens, which may need network or DNS changes. gitlab.com has no such issue. [TBD: SaaS or self-managed.]
- Pipeline minutes or runner capacity for real-cloud CI are a cost the program must budget (ADR-010).
- Some GitLab features used here (Workspaces, certain review and security features) depend on the **tier**; ADR-015's rule against paid tools means none of them may become a hard requirement for learners.

**Follow-ups**
- Update the PRD wording listed above.
- Confirm tier, SaaS or self-managed, runner setup, and Workspaces availability with the GitLab owner (solution design A11).
- Convert the CI design in ADR-010 into a `.gitlab-ci.yml` skeleton in weeks 1-2 of the launch plan.
