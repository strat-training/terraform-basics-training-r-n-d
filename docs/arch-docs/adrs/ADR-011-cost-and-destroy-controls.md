# ADR-011: Cost controls: destroy at the end of each activity, no NAT gateways

- **Status:** Accepted (NAT gateways are not used at all, see [ADR-017](ADR-017-aws-only-no-capstone.md))
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.5, s.11, s.14 (risk: surprise cloud bills), s.15

## Context

Learners create real infrastructure in pre-made sandboxes. Budgets and guardrails are owned outside the program, so the program must still prevent learners from leaving billable resources running.

## Decision

- **Every activity ends with `terraform destroy`**, except Activity 7, which keeps the S3 state bucket. The check script **confirms the stack is gone**.
- Activities use **small instance types** and **never create NAT gateways** (hourly billing). Activity 4 explicitly uses no NAT.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Rely on sandbox budgets only | Not owned by this program; does not teach the habit |
| Auto-destroy via scheduled cloud job | Needs extra permissions; outside program scope (sandbox management) |

## Consequences

**Positive**
- Cost-awareness is part of every activity; supports the "no surprise bills" risk mitigation.

**Negative / trade-offs**
- Destroy checks rely on learners running them; this is self-reported. Sandbox-level budget alerts remain the backstop.
- The retained state bucket is a small ongoing cost until removed; the clean-up step at the end of the last module covers it.
