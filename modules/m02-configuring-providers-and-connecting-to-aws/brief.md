# M02 — Configuring Providers and Connecting to AWS

| | |
| --- | --- |
| Stage | 2 of 12 |
| Course reference | Module 2 / Activity 2 "Providers" (solution-design §6.2), extended at the trainer's request: sign-in, session expiry and the static-key check move here from Module 1 (ADR-005, ADR-009). See [README](../README.md#open-items-for-the-trainer). |
| Cloud | AWS. Sandbox access is provided before the course; this stage signs in with it and does not set it up. |
| Builds on | M01 |
| Time box | TBC — see [README](../README.md#open-items-for-the-trainer) |
| Leaves behind | Nothing. This stage plans only; it creates no resources. |

## Objective

Sign in to the AWS sandbox with the access you were given, and know at any moment which identity and account Terraform will act as. Then pin Terraform and provider versions deliberately, and explain how a configuration, the provider plugins it needs and the lock file fit together — well enough to say what a version bump would change and who should review it.

## Scope

### In scope (in the order to tackle)

1. Signing in to the AWS sandbox with the access you were given — IAM Identity Center (SSO) through the AWS CLI
2. Confirming which identity and account Terraform will act as
3. Credential lifetime — session expiry, its symptoms, and recovering from it
4. Browser-based sign-in from inside a container or remote workspace
5. Keeping static access keys off disk and out of the repository
6. What a provider is and how Terraform finds and installs one
7. Version constraints — for Terraform itself and for each provider
8. The dependency lock file — what it records and why it is committed
9. Using more than one provider in a single configuration
10. Provider configuration — how a provider obtains its credentials, and provider-level default tags
11. Inspecting which providers and versions a configuration actually uses
12. Upgrading a pinned version deliberately

### Out of scope

- Setting up, creating or managing sandbox access, accounts, budgets or guardrails — provided before the course and owned outside the program (ADR-005)
- GCP and Azure sign-in and providers (M12)
- Writing providers
- Authoring reusable Terraform modules (M10)
- HCP Terraform, Terraform Stacks, Packer, Kubernetes providers (ADR-015)

## Stack constraints

- Everything under [Rules for every stage](../README.md#rules-for-every-stage).
- AWS sign-in is IAM Identity Center through the AWS CLI. No IAM user access keys and no long-lived credentials of any kind (ADR-005).
- Terraform 1.11 or later. The exact Terraform and provider versions to pin to come from `versions.env`, the program's single source of version truth (ADR-010).
- Providers: `aws` and `random`.
- No unconstrained or floating provider versions.
- Plan only: this stage uses `init` and `plan` but never `apply`. Applying is introduced in M03.

## Deliverable

**A signed-in sandbox session and a minimal Terraform configuration that uses the `aws` and `random` providers**, with Terraform and provider versions pinned, the lock file committed, and default tags configured on the AWS provider.

## Open design questions

1. What does a learner see when their session has expired, and how will you help them tell that apart from a genuine permissions problem?
2. What can go wrong when you sign in from inside a container rather than on the host?
3. How does the AWS provider decide which credentials to use, and how would you prove which identity a plan is using?
4. What is the difference between a version constraint you declare and what the lock file records, and why does the course want both?
5. How loose or tight should a provider constraint be, and who carries the risk of each choice?
6. Why set tags at the provider rather than on each resource, and what would make you tag a resource individually anyway?
7. What should a reviewer look for in a merge request that changes the lock file?

## Definition of done

- [ ] **DoD-1** An authenticated AWS sandbox session exists and a caller-identity query returns the sandbox identity (output pasted, account details redacted as the trainer directs).
- [ ] **DoD-2** You have caused a session to fail, captured the symptom, and recovered; the write-up records both.
- [ ] **DoD-3** No static access keys are present in your AWS configuration on disk or in your repository; your evidence shows the scan you ran and what it looked for.
- [ ] **DoD-4** Signing in also works from inside the dev container, or your write-up records exactly what blocked it (output pasted).
- [ ] **DoD-5** The configuration declares a required Terraform version and, for every provider it uses, a source and a version constraint.
- [ ] **DoD-6** The lock file exists and is committed to version control (it appears in your commit).
- [ ] **DoD-7** The provider listing for the configuration shows both `aws` and `random` (output pasted).
- [ ] **DoD-8** Formatting and validation checks pass with no errors (output pasted).
- [ ] **DoD-9** Default tags are configured on the AWS provider and the plan shows them on at least one taggable resource the configuration would create (plan excerpt).
- [ ] **DoD-10** One deliberate version change is shown with its effect on the lock file (before and after).
- [ ] **DoD-11** No resources exist in the sandbox as a result of this stage, confirmed from the cloud side.

## Best practices this stage demonstrates

- No static credentials (Activity 1 check, moved here)
- Pinned versions, lock file (Activity 2 check)
- `default_tags` (Activity 2 check)
- fmt and validate
