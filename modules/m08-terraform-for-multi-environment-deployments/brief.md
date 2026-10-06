# M08 — Terraform for Multi-Environment Deployments

| | |
| --- | --- |
| Stage | 8 of 12 |
| Cloud | AWS |
| Builds on | M05, M07 |
| Cost | Two environments mean twice the resources. Look up what each resource in your plan bills before you apply, and destroy both environments at the end of the stage. |
| Leaves behind | Nothing except the M07 state bucket. Destroy both environments. |

## Objective

Deploy two environments — dev and prod — from one configuration with separate state, named and tagged so consistently that anyone can tell which environment a resource belongs to at a glance. Be able to say when you would use workspaces or a directory per environment instead.

## Scope

### In scope (in the order to tackle)

1. One configuration, many environments — what is shared and what must be separate
2. Per-environment input values
3. Per-environment backend settings and separate state keys in the shared bucket
4. Managing blast radius through state separation
5. Enforcing naming conventions and default provider tags
6. Switching between environments safely
7. Alternative isolation methods: directories vs workspaces (theory)

### Out of scope

- Using workspaces for the environments (explain only)
- Building the environments with a directory or repository per environment (explained in the comparison note, not built)
- Terragrunt or other wrapper tools
- Separate accounts per environment — explain why real teams do it, but do not build it
- Reusable Terraform modules (M10)

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- One configuration, with a variable-definition file and a backend-configuration file per environment.
- State lives in the bucket from M07, under a distinct key per environment.
- Resource names follow `<app>-<env>-<resource>`. Provider-level default tags include `Environment`.
- Both environments live in the same sandbox account. Your write-up must say that real teams usually separate accounts.
- Keep resources small and cheap; destroy both environments at the end.

## Deliverable

**One configuration deployed as both dev and prod with separate state**, plus a note comparing three ways to separate environments.

## Open design questions

1. What makes it easy to apply one environment's values to the other's state, and what will you do to make that harder?
2. Which tags would a clean-up or cost report need beyond `Environment`, and why?
3. When would workspaces be the right tool, and what do you give up by not using them here?
4. When would a directory per environment be the right tool, and what do you give up by not using it here?
5. In what ways does keeping both environments in one account misrepresent real practice?

## Definition of done

- [ ] **DoD-1** Two state objects exist in the bucket under different keys (listing pasted).
- [ ] **DoD-2** Both environments produce clean plans (output for each).
- [ ] **DoD-3** Environment-specific inputs differ between the two environments and live outside the main configuration files.
- [ ] **DoD-4** Every resource follows the naming convention and carries the required tags (shown from the plan, state or cloud side).
- [ ] **DoD-5** The comparison note is present and covers a directory per environment, workspaces, and the per-environment files you used, saying when each fits.
- [ ] **DoD-6** Both environments are destroyed and the bucket is retained, confirmed from the cloud side.
- [ ] **DoD-7** Your write-up takes a first-time learner to one configuration deployed as dev and prod with separate state unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- Separate state per environment
- Naming
- `default_tags`
- fmt and validate
