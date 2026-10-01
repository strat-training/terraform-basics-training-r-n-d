# ADR-006: S3 remote state with native locking (`use_lockfile`)

- **Status:** Accepted
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.8 (Module 7, Activities 7-8), s.10, s.11, s.12

## Context

Remote state with locking is a headline best practice. Terraform's S3 backend previously needed a DynamoDB table for locking. Native S3 locking (`use_lockfile`) was experimental in Terraform 1.10 and generally available in 1.11, and DynamoDB-based locking is now deprecated (PRD checked October 2026).

## Decision

- Teach and require the **S3 backend with `use_lockfile = true`**. Do **not** teach DynamoDB locking, except to explain why it is deprecated.
- The state bucket has **versioning, server-side encryption and a public-access block**, and access restricted to the learner's role.
- The bucket is **bootstrapped once** with a local-state configuration in Activity 7, then **kept** across later activities (and reused by the capstone with a different state key).
- Existing local state is moved with `terraform init -migrate-state`.
- Locking is **proven** by starting two simultaneous applies and reading the lock error.
- Terraform **1.11 or later** is the minimum pinned version everywhere.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| S3 + DynamoDB locking | Deprecated; extra resource and cost; two things to bootstrap |
| HCP Terraform remote state | Out of scope (HCP administration excluded); needs external accounts |
| Local state shared by hand | The anti-pattern the program exists to eliminate |
| `gcs` or `azurerm` backend as primary | AWS is the primary cloud (ADR-003); other backends shown for reference only |

## Consequences

**Positive**
- One bucket, no extra table; simplest correct setup.
- Matches current best practice.

**Negative / trade-offs**
- Locks are lock objects in the bucket; learners need `s3:PutObject` and `s3:DeleteObject` on the lock key, which the sandbox role must allow.
- Content must be re-verified against release notes for the exact pinned version (PRD verification note).
- The state bucket outlives activities; learners must remember to remove it at the end (capstone clean-up step, solution design A5).
