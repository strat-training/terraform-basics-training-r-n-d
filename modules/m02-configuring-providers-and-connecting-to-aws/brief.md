# M02 — Configuring Providers and Connecting to AWS

| | |
| --- | --- |
| Stage | 2 of 12 |
| Cloud | AWS. Sandbox access is provided before the course; this stage signs in with it and does not set it up. |
| Builds on | M01 |
| Cost | None. This stage plans only, so nothing bills. |
| Leaves behind | Nothing. This stage plans only; it creates no resources. |

## Objective

Sign in to the AWS sandbox with the access you were given, and know at any moment which identity and account Terraform will act as. Then pin Terraform and provider versions deliberately, and explain how a configuration, the provider plugins it needs and the lock file fit together — well enough to say what a version bump would change and who should review it.

## Scope

### In scope (in the order to tackle)

1. Authenticating to AWS (IAM Identity Center) and verifying Terraform identity
2. Keeping static access keys off disk and out of the repository
3. What a provider is and how Terraform finds and installs one
4. Provider concepts, credential configuration, and default tags
5. Dependency management: version constraints, lock files, and safe upgrades
6. Using and inspecting multiple providers in a single configuration

### Out of scope

- Setting up, creating or managing sandbox access, accounts, budgets or guardrails — provided before the course and owned outside this course
- GCP and Azure sign-in and providers (M12)
- Writing providers
- Authoring reusable Terraform modules (M10)
- HCP Terraform, Terraform Stacks, Packer, Kubernetes providers

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- AWS sign-in is IAM Identity Center through the AWS CLI. No IAM user access keys and no long-lived credentials of any kind.
- Terraform 1.11 or later. The exact Terraform and provider versions to pin to come from `versions.env`, the course's single source of version truth.
- Providers: `aws` and `random`.
- No unconstrained or floating provider versions.
- Plan only: this stage uses `init` and `plan` but never `apply`. Applying is introduced in M03.

## Deliverable

**A signed-in sandbox session and a minimal Terraform configuration that uses the `aws` and `random` providers**, with Terraform and provider versions pinned, the lock file committed, and default tags configured on the AWS provider.

## Open design questions

1. How does the AWS provider decide which credentials to use, and how would you prove which identity a plan is using?
2. What is the difference between a version constraint you declare and what the lock file records, and why does the course want both?
3. How loose or tight should a provider constraint be, and who carries the risk of each choice?
4. Why set tags at the provider rather than on each resource, and what would make you tag a resource individually anyway?
5. What should a reviewer look for in a merge request that changes the lock file?

## Definition of done

Your training module — the build plus the write-up that teaches it — is done when each of these is true.

- [ ] **DoD-1** Your write-up shows a caller-identity query that returns the sandbox identity from your own signed-in session (output pasted, account details redacted as the trainer directs), not the identity you assumed you had.
- [ ] **DoD-2** Your write-up shows the scan you ran for static access keys on disk and in your repository, and what it looked for, not a statement that there are none.
- [ ] **DoD-3** Your configuration declares a required Terraform version and, for every provider it uses, a source and a version constraint, not a provider left unconstrained.
- [ ] **DoD-4** Your write-up shows the lock file committed (it appears in your commit) and one deliberate version change with the lock file before and after, not a description of what a version change would do.
- [ ] **DoD-5** Your write-up shows the provider listing for your configuration with both `aws` and `random`, as real output.
- [ ] **DoD-6** Your write-up shows formatting and validation passing with no errors, as pasted output.
- [ ] **DoD-7** Your write-up shows default tags configured on the AWS provider and appearing in the plan on at least one taggable resource the configuration would create (plan excerpt), not tags you only set in the code.
- [ ] **DoD-8** A learner following your training module ends with no resources in the sandbox as a result of this stage, confirmed from the cloud side, not only from Terraform's output.

## Best practices this stage demonstrates

- No static credentials
- Pinned versions, lock file
- `default_tags`
- fmt and validate
