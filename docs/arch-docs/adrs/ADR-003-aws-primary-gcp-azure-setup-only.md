# ADR-003: AWS as primary cloud; GCP and Azure setup-only plus one storage resource

- **Status:** Accepted
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.2, s.4, s.9, s.15

## Context

Learners need depth in the core workflow before breadth. Teaching three clouds in depth would exceed the 37-42 hour budget and distract from Terraform concepts. At the same time, many teams use more than one cloud and the PRD wants learners to see that the workflow is the same while provider setup differs.

## Decision

- **AWS** carries Modules 1-9 and the AWS portion of the capstone.
- **GCP and Azure** appear in **Module 10 as setup-only tracks**: authentication, explicit project or subscription, provider configuration and a read-only data-source check. The `gcs` and `azurerm` state backends are reference-only.
- The **capstone adds exactly one storage resource per extension cloud**: a Cloud Storage bucket (DB backup) and an Azure Storage Account with a Blob container (static assets).
- No deeper GCP or Azure follow-on is planned.
- Provider differences are shown explicitly; **no generic abstraction layer** hides them.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| AWS only | Misses the multi-cloud setup skills many teams need |
| Equal depth on all three clouds | Not feasible in the time budget; would dilute core concepts |
| Cloud-agnostic abstraction (wrapper modules) | Out of scope (reusable modules are excluded) and teaches a harmful pattern of hiding real differences |
| Separate cloud-specific tracks learners choose | Splits cohorts and triples content maintenance |

## Consequences

**Positive**
- Keeps Weeks 1-3 focused; Week 4 demonstrates transferability.
- Maintenance burden on GCP and Azure content is small.

**Negative / trade-offs**
- Learners finish without real GCP or Azure network or compute experience.
- GCP and Azure account friction can delay Week 4; mitigated by an early-access checklist at the start of Week 3 and an AWS-only capstone path (PRD s.14).
- Week 4 is the heaviest week (11-13 hours). See solution design A7.
