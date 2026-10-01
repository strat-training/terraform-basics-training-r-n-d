# ADR-007: Environments via per-environment `.tfvars` and backend config files

- **Status:** Proposed
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee) to confirm
- **PRD references:** s.8 (Module 8, Activity 8), s.10 ("Separate state per environment; keep the blast radius small")

## Context

The PRD requires learners to deploy `dev` and `prod` from one configuration with separate state, and to write a decision note on when workspaces would fit instead. It names the mechanism (a `.tfvars` file and a backend config file per environment) but does not record why that was preferred.

## Decision

Teach **one configuration, many environments** through:

- `dev.tfvars` and `prod.tfvars` for inputs (CIDRs, instance sizes, names)
- `dev.backend.hcl` and `prod.backend.hcl` passed with `terraform init -backend-config=...`, each with its own **state key** in the shared bucket
- A naming pattern `<app>-<env>-<resource>` and `default_tags` including `Environment`

Workspaces are **explained, not used**. Activity 8 requires a short decision note on when workspaces would fit (for example, short-lived identical copies in the same account with the same permissions).

## Alternatives considered

| Option | Pros | Cons / why not chosen |
| --- | --- | --- |
| Workspaces | Built in, little code | Same backend and credentials for all environments; easy to apply to the wrong one; weak isolation for prod |
| Directory per environment (copy of code) | Strong isolation, explicit | Duplication and drift; not a "same configuration" lesson; module reuse is out of scope |
| Separate repositories per environment | Strongest isolation | Heavy for a training exercise |
| Terragrunt or wrapper tools | Reduces boilerplate | Extra tool; out of scope |

## Consequences

**Positive**
- Teaches the idea that code is shared and **state is separate**, which is what limits blast radius.
- Works with a single sandbox account.

**Negative / trade-offs**
- Learners must remember to `init -reconfigure` when switching environments; the check script and cheat sheet must call this out.
- Both environments live in one sandbox account in the course; real teams usually separate accounts. The module should say so explicitly.
- Risk of applying `dev.tfvars` against `prod` state. Mitigation: a small wrapper `Makefile` or script in the starter repo that pairs the right files, shown as a good habit.
