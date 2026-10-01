# ADR-002: Teach the Terraform CLI; OpenTofu as a sidebar only

- **Status:** Accepted
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.4 (OpenTofu note), s.13 (CR-6), s.15

## Context

OpenTofu is an open-source fork with a largely compatible CLI. Teaching both doubles testing and confuses beginners. Most employers and documentation still reference Terraform.

## Decision

All activities, check scripts, CI and the dev container use the **Terraform CLI** (1.11 or later, pinned). A short **OpenTofu differences sidebar** explains where behaviour differs. It is **not graded** and not tested as an alternate path in CI.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| OpenTofu as primary | Smaller share of existing team usage and documentation; PRD owner chose Terraform |
| Support both with a CI matrix | Doubles CI time and cost; features such as native S3 locking and `-generate-config-out` may differ by release |
| No mention of OpenTofu | Learners will meet it; a short note prevents confusion |

## Consequences

**Positive**
- One toolchain, one set of expected outputs, simpler check scripts.

**Negative / trade-offs**
- Learners who use OpenTofu may hit differences; the sidebar is best-effort and its accuracy is not CI-verified.
- If licensing or ecosystem changes materially, this ADR should be revisited.
