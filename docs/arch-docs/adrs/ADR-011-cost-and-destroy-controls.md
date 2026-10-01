# ADR-011: Cost controls: destroy at the end of each activity, NAT only in the capstone

- **Status:** Accepted
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.5, s.9 (capstone), s.11, s.14 (risk: surprise cloud bills), s.15

## Context

Learners create real infrastructure in pre-made sandboxes. Budgets and guardrails are owned outside the program, so the program must still prevent learners from leaving billable resources running.

## Decision

- **Every activity ends with `terraform destroy`**, except Activity 7, which keeps the S3 state bucket. The check script **confirms the stack is gone**.
- Activities use **small instance types** and **avoid NAT gateways** (hourly billing). Activity 4 explicitly uses no NAT.
- The **capstone may create one NAT gateway** so the private App tier can install packages; the capstone includes a destroy and a "nothing left behind" proof.
- Capstone sizing: smallest practical EC2 and RDS classes, single-AZ RDS, minimal storage and backup retention, LRS on Azure, regional GCS bucket.
- The capstone module states an **expected cost per hour** and asks learners to complete the proof phase in a single sitting.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Rely on sandbox budgets only | Not owned by this program; does not teach the habit |
| Auto-destroy via scheduled cloud job | Needs extra permissions; outside program scope (sandbox management) |
| Avoid NAT in capstone (VPC endpoints, public App tier) | VPC endpoints cost similar or more; a public App tier teaches a poor security pattern |
| Pre-baked AMIs to avoid package installs | Adds an image pipeline and content maintenance; the PRD specifies boot-script delivery |

## Consequences

**Positive**
- Cost-awareness is part of every activity; supports the "no surprise bills" risk mitigation.

**Negative / trade-offs**
- NAT gateway is the largest hourly cost in the capstone (plus data processing). Learners who pause overnight pay for it.
- Destroy checks rely on learners running them; this is self-reported. Sandbox-level budget alerts remain the backstop.
- The retained state bucket is a small ongoing cost until removed; the capstone clean-up step covers it.
