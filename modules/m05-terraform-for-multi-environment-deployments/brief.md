# M05 — Terraform for Multi-Environment Deployments Brief

**Stage:** 5 of 11 · **Builds on:** M04 · **Feeds into:** M09

## Objective

By the end of this stage, you can deploy dev and prod from one configuration with separate state, named and tagged so consistently that anyone can tell which environment a resource belongs to at a glance — using your own two environments as the evidence, not a diagram. You can say when you would use workspaces or a directory per environment instead.

## Scope

You work from your own two environments, not a worked example. Find out, and write down in your own words:

- **One configuration, many environments** — what is shared and what must be separate. Research: what makes it easy to apply one environment's values to the other's state, and what you will do to make that harder.
- **Per-environment input values** — which values differ between dev and prod, and where they live. Research: which inputs are the same in both environments and which must differ.
- **Per-environment backend settings and separate state keys in the shared bucket** — how the state key keeps one environment's state apart from the other's. Research: how you would notice if both environments ended up in the same state.
- **Managing blast radius through state separation** — what separate state protects, and what it does not. Research: what separate state does and does not protect.
- **Enforcing naming conventions and default provider tags** — a convention for names, and tags applied through the provider. Research: which tags a clean-up or cost report would need beyond `Environment`, and why.
- **Switching between environments safely** — what you check before every apply so you are in the environment you meant. Research: how you would notice that you are in the wrong environment.
- **Alternative isolation methods: directories vs workspaces (theory)** — explained in your comparison note, not built. Research: when workspaces would be the right tool and what you give up by not using them here, when a directory per environment would be the right tool and what you give up by not using it, and in what ways keeping both environments in one account misrepresents real practice.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- You use one configuration, with a variable-definition file and a backend-configuration file per environment, and state lives in the bucket from M04 under a distinct key per environment.
- Resource names follow `<app>-<env>-<resource>`, and provider-level default tags include `Environment`.
- Both environments live in the same sandbox account, and your notes must say that real teams usually separate accounts.
- Two environments mean twice the resources, so keep them small and cheap, look up what each resource bills before you apply, and destroy both environments at the end.
- Workspaces and a directory per environment are explained in your comparison note, not built.
- Separate accounts, Terragrunt and other wrapper tools, and reusable modules (M09) are out of scope.

## Deliverable

**One configuration deployed as both dev and prod with separate state**, plus a note comparing three ways to separate environments.

## Lab

**Goal.** Deploy dev and prod from one configuration with separate state, named and tagged consistently.

**You do, in the sandbox.** Set per-environment inputs and backend settings, apply each environment, name and tag everything through the convention, switch between environments carefully, and write up how other ways of separating environments compare.

**You build and capture.** The one configuration deployed twice is your deliverable. Capture two state objects, a clean plan for each environment, the names and tags, and your comparison note.

**Clean-up.** Destroy both environments and keep the bucket.

## Definition of done

- DoD-01: Two state objects exist in the bucket under different keys (listing pasted).
- DoD-02: Both environments produce clean plans, with the output for each, not one plan reported as covering both.
- DoD-03: Environment-specific inputs differ between your two environments and live outside the main configuration files.
- DoD-04: Every resource follows the naming convention and carries the required tags, shown from the plan, the state or the cloud side, not from your code.
- DoD-05: Your comparison note covers a directory per environment, workspaces and the per-environment files you used, and says when each fits.
- DoD-06: Both environments are destroyed and the bucket is retained, confirmed from the cloud side.
- DoD-07: Your write-up takes a first-time learner to one configuration deployed as dev and prod with separate state unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- Separate state per environment
- Naming
- `default_tags`
- fmt and validate

## Still open / ask your trainer

- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
