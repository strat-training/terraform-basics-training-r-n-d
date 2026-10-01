# ADR-010: Content CI with a single pinned-version source and scheduled canary runs

- **Status:** Proposed
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee) to confirm
- **PRD references:** s.13 (CR-1, CR-4, CR-8, content maintenance), s.14 (risk: releases break activities), s.15 verification note

## Context

Providers release frequently and a broken activity in a self-paced course has no instructor to absorb the confusion. The PRD requires that all activity code is tested in CI against the pinned Terraform version and fails the content build when a provider upgrade breaks it, with review after each Terraform minor release or provider major release.

## Decision

1. **One source of truth** for versions: `versions.env` (Terraform version and provider constraints). The dev container, activity starters, solutions and CI all read from it.
2. **Per-merge-request CI** (GitLab merge request pipelines), for every activity:
   - `fmt`, `validate` on starter and solution
   - the check script passes on the solution and fails with the expected items on the starter
   - activities that need real cloud run in a **dedicated CI sandbox** with a nightly sweeper and budget alarm; S3-only activities may use LocalStack
   - markdown link check and a **coverage matrix check** that every best practice in PRD s.10 maps to at least one activity check and one quiz question (CR-4)
3. **Scheduled weekly CI** (a GitLab scheduled pipeline) re-runs everything on pinned versions, plus a **canary** run on the latest provider versions (non-blocking) to see breakage early.
4. **Capstone `data/` tests (CR-8)**: render templates, shellcheck, boot the API against MySQL 8.4 locally, hit all six endpoints, validate `seed.sql`, confirm `bad.tfvars` fails validation with the expected message.
5. **Triggered review** after each Terraform minor release and AWS, Google or AzureRM provider major release; full **six-monthly** review.
6. Version bumps are deliberate merge requests that update `versions.env`, the lock files and any affected content together.
7. Pipelines are defined in `.gitlab-ci.yml`, with `rules:` on `$CI_PIPELINE_SOURCE` separating merge request, scheduled and tag pipelines. Cloud jobs authenticate with GitLab CI/CD ID tokens (see ADR-016).

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Manual testing before each cohort | Does not scale; misses silent breakage |
| CI against latest versions only | Learners get unpredictable content; PRD requires pinning |
| Floating provider constraints in activities | Violates the pinning practice the course teaches |

## Consequences

**Positive**
- Learners and CI run the same versions; breakage shows before learners see it.
- Teaches by example: the course repo follows its own best practices.

**Negative / trade-offs**
- A real-cloud CI sandbox has running cost and needs credentials management (federated OIDC from GitLab CI/CD ID tokens to each cloud, no stored keys). On a self-managed GitLab, the clouds must be able to reach its OIDC issuer URL [TBD: SaaS or self-managed].
- Weekly canary runs generate maintenance work; someone must own triage.
- CI sandbox is a fourth set of cloud accounts that this program must request from the sandbox owner (ADR-005 follow-up).
