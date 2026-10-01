# ADR-015: Sandbox-compatible tooling only

- **Status:** Accepted
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.4 (out of scope, sandbox environment exclusions), s.11, s.13

## Context

All activities run in restricted sandbox accounts on AWS, GCP and Azure, without organization-level or billing-level privileges and without paid external services. The PRD lists six exclusions.

## Decision

Design every activity, check script and CI job to run **without**:

1. AWS Organizations and Service Control Policies.
2. Account-level billing APIs (raw Cost Explorer, Billing Conductor).
3. Tag-filtered budgets and cost allocation tags (budgets, where mentioned, are account-wide).
4. Paid third-party SaaS tools and API keys (for example, Infracost SaaS).
5. Policy-as-code engines (OPA/Rego, Sentinel); validation is native HCL only (variable validation, `precondition` and `postcondition`, plan JSON assertions).
6. Complex multi-cloud global traffic routing (for example, Azure Front Door in front of AWS ALBs); multi-cloud examples use storage and static-asset patterns.

Also in line with the PRD scope, the program does not use HCP Terraform, Terraform Stacks, Packer, Kubernetes providers, authoring of reusable modules, `terraform test`, or CI/CD pipelines as learner content.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Request elevated sandbox permissions | Conflicts with the sandbox model owned outside the program |
| Add third-party linters and cost tools as optional extras | Fragmentation and, for some, paid tiers; may be added later as non-graded sidebars (open-source linters only) |

## Consequences

**Positive**
- Every learner can complete every activity with the permissions they have; fewer support cases.
- Clear scope boundary for content authors and reviewers.

**Negative / trade-offs**
- Learners do not see policy-as-code or cost estimation tooling that many teams use; the course should name these in "next steps" without teaching them.
- Reviewers should reject activity ideas that quietly need excluded capabilities. The CI sandbox should be configured with equivalent restrictions so such activities fail in CI, not in front of learners.
