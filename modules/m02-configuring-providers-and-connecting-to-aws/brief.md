# M02 — Configuring Providers and Connecting to AWS Brief

**Stage:** 2 of 11 · **Builds on:** M01 · **Feeds into:** M03, M11

## Objective

By the end of this stage, you can sign in to the AWS sandbox with the access you were given and say, at any moment, which identity and account Terraform will act as — using your own caller-identity output as the evidence, not an assumption. You can pin Terraform and provider versions deliberately and explain how a configuration, the provider plugins it needs and the lock file fit together, well enough to say what a version bump would change and who should review it.

## Scope

You work from your own sandbox session and configuration, not a worked example. Find out, and write down in your own words:

- **Authenticating to AWS (IAM Identity Center) and verifying Terraform identity** — signing in with the access you were given and confirming which identity and account Terraform will act as. Research: how the AWS provider decides which credentials to use, and how you would prove which identity a plan is using.
- **Keeping static access keys off disk and out of the repository** — where keys end up by accident, and how you check that none are there. Research: what a scan for static keys has to look at, and what it can miss.
- **What a provider is and how Terraform finds and installs one** — the plugins a configuration needs, and where they come from. Research: what Terraform downloads when you initialise, and what a version bump would change.
- **Provider concepts, credential configuration, and default tags** — how a provider obtains its credentials, and tags set at the provider. Research: why tags are set at the provider rather than on each resource, and what would make you tag a resource individually anyway.
- **Dependency management: version constraints, lock files, and safe upgrades** — what you declare, what the lock file records, and how to move a pinned version deliberately. Research: the difference between a version constraint you declare and what the lock file records, how loose or tight a provider constraint should be and who carries the risk of each choice, and what a reviewer should look for in a merge request that changes the lock file.
- **Using and inspecting multiple providers in a single configuration** — seeing which providers and versions a configuration actually uses. Research: what the provider listing tells you that the configuration does not.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- You work in the AWS sandbox that was provided before the course.
- Setting up or managing sandbox access, accounts, budgets or guardrails is not part of this stage, and neither are GCP and Azure (M11), writing providers, authoring modules (M09), or HCP Terraform, Terraform Stacks, Packer and Kubernetes providers.
- You sign in to AWS with IAM Identity Center through the AWS CLI, and you use no IAM user access keys and no long-lived credentials of any kind.
- Terraform is 1.11 or later, the exact Terraform and provider versions to pin come from `versions.env`, and your providers are `aws` and `random`, none of them unconstrained or floating.
- This stage is plan only: you use `init` and `plan` but never `apply`, so nothing is created and nothing bills, and applying starts in M03.

## Deliverable

**A signed-in sandbox session and a minimal Terraform configuration that uses the `aws` and `random` providers**, with Terraform and provider versions pinned, the lock file committed, and default tags configured on the AWS provider.

## Lab

**Goal.** Sign in to the AWS sandbox with the access you were given, know which identity Terraform will act as, and pin versions deliberately.

**You do, in the sandbox.** Sign in, confirm the identity, scan for static keys, write a configuration that uses two providers, initialise and plan it without applying, then change a pinned version on purpose and see what moves.

**You build and capture.** The signed-in session and the small configuration are your deliverable. Capture the caller-identity output, the scan, the lock file in your commit, the provider listing, the plan showing default tags, and the lock file before and after the version change.

**Clean-up.** Nothing is created, so confirm from the cloud side that nothing exists.

## Definition of done

- DoD-01: Your notes show a caller-identity query that returns the sandbox identity from your own signed-in session (output pasted, account details redacted as the trainer directs), not the identity you assumed you had.
- DoD-02: Your notes show the scan you ran for static access keys on disk and in your repository, and what it looked for, not a statement that there are none.
- DoD-03: Your configuration declares a required Terraform version and, for every provider it uses, a source and a version constraint, and the provider listing shows both `aws` and `random` (output pasted), not providers left to float.
- DoD-04: The lock file is committed (it appears in your commit), and your notes show one deliberate version change with the lock file before and after, not a description of what a version change would do.
- DoD-05: Formatting and validation pass with no errors, and the plan shows default tags on at least one taggable resource the configuration would create (plan excerpt), not tags you only set in the code.
- DoD-06: Your notes show that no resources exist in the sandbox as a result of this stage, confirmed from the cloud side, not from Terraform's output.
- DoD-07: Your write-up takes a first-time learner to a signed-in sandbox session and a pinned, plan-only configuration unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- No static credentials
- Pinned versions, lock file
- `default_tags`
- fmt and validate

## Still open / ask your trainer

- Which details of the caller-identity output to redact before you paste it.
- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
