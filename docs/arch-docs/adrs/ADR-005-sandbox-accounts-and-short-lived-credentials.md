# ADR-005: Pre-made sandbox accounts and short-lived credentials

- **Status:** Accepted
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.3, s.4 (out of scope), s.10, s.11, s.13 (FR-5), s.14, s.15

## Context

Learners run real infrastructure. The program must be safe on cost and security without owning account management. The PRD explicitly excludes creating or managing sandboxes, budgets and guardrails.

## Decision

1. Learners receive **pre-made sandbox accounts** on AWS, GCP and Azure from outside this program. GCP and Azure are needed from Week 4 only.
2. Authentication uses **short-lived, interactive logins**:
   - AWS: IAM Identity Center (`aws sso login`)
   - GCP: Application Default Credentials (`gcloud auth application-default login`)
   - Azure: `az login`
3. **No static access keys** are created, stored on disk or committed. Check scripts verify this (Activities 1 and 10) and scan the learner repo for key patterns.
4. The program assumes sandboxes have **short-lived roles and sandbox-level guardrails**, but does not provide them.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Learners use their own personal accounts | Cost risk, security risk, uneven setup |
| Program provisions per-learner accounts | Out of scope; needs organizations-level permissions that the PRD excludes |
| Long-lived IAM user keys | Contradicts the first best practice the program teaches |

## Consequences

**Positive**
- Teaches the right habit from day one; reduces credential leakage risk.
- Program team avoids account administration.

**Negative / trade-offs**
- **Hard dependency** on the sandbox owner. If sandbox policies are tighter than assumed (for example, no IAM role creation, no workload identity pools, no public blob access), some capstone designs break. See ADR-013 and ADR-014 and solution design A1, A4.
- Interactive logins expire; Module 1 must teach re-login and the symptoms of expired tokens.
- Cost containment relies on the sandbox owner's budgets; the program only controls what learners leave running (ADR-011).

**Follow-ups**
- Write a one-page **sandbox contract** for the sandbox owner listing the permissions the activities need (including capstone IAM, Secrets Manager, GCP IAM and workload identity pools, Azure storage public-access setting).
