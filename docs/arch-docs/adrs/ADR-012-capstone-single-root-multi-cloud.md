# ADR-012: Capstone as one root module, one apply, three clouds, one state

- **Status:** Proposed
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee) to confirm
- **PRD references:** s.9 (capstone), s.12 (rubric: Provision 30, Tear down 15), s.10

## Context

The capstone must "provision everything on all three clouds with one `terraform apply`" with a clean plan afterwards, and `terraform destroy` must remove everything. The PRD also asks for remote state in S3 and a standard file layout. Modules 1-10 deliberately do not build the app, so the capstone is a fresh configuration.

## Decision

Use **one root module** with **three provider configurations** (`aws` with `default_tags` and region `ap-southeast-1`, `google` with explicit project, `azurerm` with `features {}` and explicit `subscription_id`), a **single state** stored in the Activity 7 S3 bucket under its own key.

- Standard file layout from Module 8 (`versions.tf`, `providers.tf`, `variables.tf`, `network.tf`, `database.tf`, `compute.tf`, `backup.tf`, `assets.tf`, `outputs.tf`).
- Dependencies are **implicit through references** (for example, the Web tier template receives the App tier address and the Azure asset URL).
- Variables are **typed with validation**; `data/bad.tfvars` deliberately violates a rule to prove failure is safe.
- Resources carry the same tags or labels on every cloud so the clean-up check can find them.
- No child modules (authoring modules is out of scope).

## Alternatives considered

| Option | Pros | Cons / why not chosen |
| --- | --- | --- |
| Separate root module per cloud | Smaller blast radius, independent apply | Fails the "one apply" requirement; learners juggle three states and outputs |
| One root with `-target` staging | Handles ordering problems | Teaches the anti-pattern the course warns against |
| Reusable modules per tier | Cleaner structure | Out of scope; adds a concept learners have not been taught |
| Orchestrator script that runs three applies | Isolation | Not "Terraform alone" and breaks the clean single-plan proof |

## Consequences

**Positive**
- Demonstrates the PRD message: same workflow on every cloud, differences in provider setup.
- One plan shows the entire system; one destroy removes it.

**Negative / trade-offs**
- Blast radius is large for a real team; the capstone README must say that production teams would normally split state by cloud or tier, consistent with the "small blast radius" practice. This is a deliberate teaching compromise for a time-boxed exercise.
- A failure in the GCP or Azure provider setup blocks the whole apply; the AWS-only fallback path (PRD s.14) is a documented reduced-scope variant, scored with reduced Provision and Prove criteria (rubric to define).
- Requires credentials for all three clouds to be live during apply and destroy; expired logins mid-run are a likely support issue (FAQ entry).
