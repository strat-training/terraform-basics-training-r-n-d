# ADR-017: AWS only: remove the GCP and Azure module and the capstone

- **Status:** Accepted (course maintainer direction, 2026-11-26; changes PRD scope)
- **Date:** 2026-11-26
- **Deciders:** Course maintainer; program owner (@Lee) to record in the PRD
- **PRD references:** s.2, s.4 (clouds), s.9 (capstone), s.10 (best practice 14), s.12 (rubric), s.13 (FR-7, CR-8), s.15
- **Supersedes:** ADR-003, ADR-012, ADR-013, ADR-014
- **Amends:** ADR-001, ADR-004, ADR-005, ADR-006, ADR-009, ADR-010, ADR-011, ADR-015, ADR-016

## Context

The course has been cut to the AWS stages. The GCP and Azure setup stage (Module 10 in this design) and the capstone project (Module 11 in this design, "Terraform Flashcard Quiz", later reshaped as a zero-downtime shop) were removed from the repository on 2026-11-26.

Several decisions existed only to support them: ADR-003 (GCP and Azure as setup-only clouds), ADR-012 (one root module, three clouds, one state), ADR-013 (capstone app delivery and the RDS-managed secret) and ADR-014 (off-site backup to GCS through workload identity federation, which still needed a spike). Other ADRs mention the capstone, GCP or Azure in passing, for example in a cost rule, a CI step or a consequence.

## Decision

1. **The course is AWS only.** It has no GCP or Azure content, sandbox accounts, command-line tools or CI federation.
2. **There is no capstone.** The three-tier app, its `data/` payload, the boot-script templates, the off-site backup, the 100-point rubric and the peer review of the capstone are out of scope.
3. **Superseded:** ADR-003, ADR-012, ADR-013 and ADR-014. They stay in the repository as the record of what was considered, with their status changed to Superseded.
4. **Amended**, with each ADR's text changed only where it referred to the removed content:

| ADR | What changes |
| --- | --- |
| 001 | Completion data comes from surveys only, not capstone submissions |
| 004 | The dev container pins the AWS CLI only (no `gcloud`, no Azure CLI) |
| 005 | Sandboxes are AWS only; the GCP and Azure logins, the Activity 10 key check and the capstone-driven sandbox permissions are dropped |
| 006 | The state bucket is no longer reused by a capstone; it is removed in a clean-up step at the end of the last module |
| 009 | There is no externally verified element: the capstone rubric review was the only one |
| 010 | The capstone `data/` tests are dropped; the triggered review covers AWS provider releases only |
| 011 | No NAT gateway anywhere (it was allowed in the capstone only), and the capstone sizing and cost rules are dropped; title changed to match |
| 015 | The sandbox restriction is AWS only, and exclusion 6 now excludes multi-cloud scenarios entirely |
| 016 | CI federation is to AWS only; peer review of the capstone (FR-7) has no subject |

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Leave ADR-012 to ADR-014 as Proposed for a possible later capstone | Keeps unresolved proposals, one of them blocked on a spike, for content that is not being built. Git history and the Superseded notes keep the reasoning |
| Delete ADR-003 and ADR-012 to ADR-014 | Breaks the numbering and the links from other ADRs; the ADR index says to supersede, not delete |
| Rewrite the four ADRs in place to describe an AWS-only course | Loses the record of why the multi-cloud design was chosen and what its risks were |
| Keep GCP and Azure as setup-only and drop only the capstone | Not what was asked: the multi-cloud stage was removed too |

## Consequences

**Positive**
- Smaller scope: no GCP or Azure sandbox friction, no workload-identity spike (solution design A1), no Secrets Manager or KMS permission needs for the capstone, and no NAT gateway cost.
- Simpler dev container, credentials, CI and sandbox contract.

**Negative / trade-offs**
- Learners finish without GCP or Azure provider setup and without an integrating end-to-end project.
- **Best practice 14, "cloud differences explicit" (PRD s.10), has no activity left.** The coverage matrix in ADR-010 fails CI for a practice with no mapped check, so the practice must be dropped from the matrix or covered another way.
- The PRD still assumes these items: the "AWS first, then GCP and Azure" goal, Week 4 and its hours, the assessment weights (activities 40%, capstone 40%), the 100-point capstone rubric, FR-7 and CR-8. The solution design records this as A13; the program owner needs to update the PRD and decide what, if anything, is the summative assessment.
- Nothing in the program is externally verified (ADR-009); completion is self-reported and measured by survey.
