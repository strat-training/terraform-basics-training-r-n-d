# ADR-009: Local check scripts built on native Terraform commands

- **Status:** Proposed
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee) to confirm
- **PRD references:** s.2 ("auto-checked activities"), s.5, s.12, s.13 (FR-4), s.14, s.15

## Context

The PRD requires auto-checked activities, no instructor, no LMS and no external grader (ADR-001). Checks run on the learner's machine against the learner's sandbox. The PRD lists the kinds of checks: `terraform fmt -check`, `terraform validate` and plan checks.

## Decision

Each activity ships a **`check` script** (POSIX shell calling shared helpers, with `jq` for JSON) that:

1. Runs `fmt -check -recursive` and `validate`.
2. Generates a plan with `terraform plan -out` and asserts on `terraform show -json` (resource addresses, change `actions`, variable validation failures, tags). JSON assertions are preferred over text matching.
3. Queries the sandbox for state-dependent assertions (for example, S3 versioning on, state object present, resources destroyed) using the learner's own credentials.
4. Scans the repo and home directory for static keys and secret patterns.
5. Prints pass or fail per item with a **one-line hint** on failure.
6. Never needs network access beyond the learner's cloud account and the provider registry.

Written-answer items (notes in Activities 3, 4, 6, 8, 10) are **self-checked against a model answer** supplied in the activity folder, not machine-graded.

The scripts are validated in CI against both the **solution** (must pass) and the **starter** (must fail with named items), so a check cannot be vacuous.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Hosted auto-grader | Needs learner credentials or uploaded state; conflicts with ADR-001 and ADR-005 |
| `terraform test` based checks | Automated Terraform testing is out of scope for learners, but check authors could use it internally; deferred |
| Policy-as-code (OPA, Sentinel) | Excluded by PRD (ADR-015) |
| Honour-system checklist only | No feedback loop; hurts completion |

## Consequences

**Positive**
- Immediate feedback with hints reduces stalls.
- Scripts are plain files, versioned with the content.
- Teaches `plan -json` inspection, a transferable skill.

**Negative / trade-offs**
- **Results are self-reported**: a learner can edit the script or copy a solution. This is acceptable because certification is not a goal (PRD s.15); the capstone rubric review is the only externally verified element.
- No central pass data. If the pilot shows poor survey response, add an **opt-in signed pass receipt** the learner submits (solution design section 9).
- Shell plus `jq` assertions on plan JSON need maintenance when Terraform changes the plan JSON format; CI catches this.
