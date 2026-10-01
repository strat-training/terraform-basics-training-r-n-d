# M08 — Terraform for Multi-Environment Deployments

| | |
| --- | --- |
| Stage | 8 of 12 |
| Course reference | Module 8 / Activity 8 "Environments" (solution-design §6.2) |
| Cloud | AWS |
| Builds on | M05, M07 |
| Time box | TBC — see [README](../README.md#open-items-for-the-trainer) |
| Leaves behind | Nothing except the M07 state bucket. Destroy both environments. |

## Objective

Deploy two environments — dev and prod — from one configuration with separate state, laid out, named and tagged so consistently that anyone can tell which environment a resource belongs to at a glance. Be able to say when you would use workspaces or a directory per environment instead.

## Scope

### In scope (in the order to tackle)

1. One configuration, many environments — what is shared and what must be separate
2. Per-environment input values
3. Per-environment backend settings and separate state keys in the shared bucket
4. Blast radius — what separate state does and does not protect
5. The standard file layout for a root configuration
6. A naming convention and required tags applied through provider defaults
7. Switching between environments safely
8. Other ways to separate environments — a directory per environment, and workspaces — and when each fits (explained, not used)

### Out of scope

- Using workspaces for the environments (explain only, ADR-007)
- Building the environments with a directory or repository per environment (explained in the comparison note, not built)
- Terragrunt or other wrapper tools (ADR-007)
- Separate accounts per environment — explain why real teams do it, but do not build it
- Reusable Terraform modules (M10)

## Stack constraints

- Everything under [Rules for every stage](../README.md#rules-for-every-stage).
- One configuration, with a variable-definition file and a backend-configuration file per environment (ADR-007, which is still Proposed).
- State lives in the bucket from M07, under a distinct key per environment.
- Resource names follow `<app>-<env>-<resource>`. Provider-level default tags include `Environment`.
- Both environments live in the same sandbox account. Your write-up must say that real teams usually separate accounts.
- Keep resources small and cheap; destroy both environments at the end (ADR-011).

## Deliverable

**One configuration deployed as both dev and prod with separate state**, plus a note comparing three ways to separate environments.

## Open design questions

1. What makes it easy to apply one environment's values to the other's state, and what will you do to make that harder?
2. Which tags would a clean-up or cost report need beyond `Environment`, and why?
3. How should the files be laid out so a newcomer finds each concern without being told?
4. When would workspaces be the right tool, and what do you give up by not using them here?
5. When would a directory per environment be the right tool, and what do you give up by not using it here?
6. In what ways does keeping both environments in one account misrepresent real practice?

## Definition of done

- [ ] **DoD-1** Two state objects exist in the bucket under different keys (listing pasted).
- [ ] **DoD-2** Both environments produce clean plans (output for each).
- [ ] **DoD-3** Environment-specific inputs differ between the two environments and live outside the main configuration files.
- [ ] **DoD-4** Every resource follows the naming convention and carries the required tags (shown from the plan, state or cloud side).
- [ ] **DoD-5** The file layout follows the standard root-configuration layout; a reviewer can find each concern from file names alone.
- [ ] **DoD-6** The comparison note is present and covers a directory per environment, workspaces, and the per-environment files you used, saying when each fits.
- [ ] **DoD-7** Both environments are destroyed and the bucket is retained, confirmed from the cloud side.

## Best practices this stage demonstrates

- Separate state per environment (Activity 8 check)
- Layout and naming (Activity 8 check)
- `default_tags` (Activity 8 check)
- fmt and validate
