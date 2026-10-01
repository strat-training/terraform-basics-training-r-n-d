# ADR-008: Teach declarative refactoring blocks over state commands

- **Status:** Proposed
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee) to confirm
- **PRD references:** s.7 (Module 6: "never edit state by hand"), s.8 (Module 9, Activity 9), s.10

## Context

Learners must be able to rename, adopt and stop managing resources without destroying them. Terraform offers imperative commands (`terraform state mv`, `state rm`, `import`) and declarative configuration blocks (`moved`, `import`, `removed`). The PRD already teaches "treat state as sensitive; never edit it by hand" and "refactor with a plan that shows zero replacements or destroys".

## Decision

Teach **`moved`, `import` and `removed` blocks** (and `-generate-config-out` for adoption) as the standard refactoring tools. Imperative `terraform state` subcommands are introduced in Module 6 for **inspection only** (`list`, `show`). `-target` is taught as an emergency tool, never routine.

Every refactor step is verified by a **plan that shows zero destroys and zero replacements**, which the Activity 9 check asserts after each of its three steps.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| `terraform state mv` / `state rm` / CLI `import` | Imperative, not reviewable in a merge request, easy to mistype, edits state outside the plan/apply cycle |
| Destroy and recreate | Causes outages and data loss; the anti-pattern |
| Hand-editing state JSON | Explicitly discouraged by the program |

## Consequences

**Positive**
- Refactors are code-reviewed, repeatable across environments (the same block applies to dev and prod) and visible in a plan.
- Consistent with the plan-review habit taught in Module 3.

**Negative / trade-offs**
- Requires a Terraform version with `removed` and `import` blocks and config generation (verified against the pinned version per the PRD note).
- Learners will see imperative commands in older blog posts and team habits; Module 9 includes a short "when you will see `state mv`" note so they can read legacy guidance.
- `-generate-config-out` output needs manual tidying; the activity makes that part of the task.
