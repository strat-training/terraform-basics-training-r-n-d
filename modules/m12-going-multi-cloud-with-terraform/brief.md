# M12 — Going Multi-Cloud with Terraform

| | |
| --- | --- |
| Stage | 12 of 12 |
| Cloud | GCP and Azure |
| Builds on | M01, M02 |
| Cost | None. Read-only checks create no resources. |
| Leaves behind | Nothing. No resources are created. |

## Objective

See that the core Terraform workflow carries over to GCP and Azure while provider setup does not: sign in with short-lived logins, make the project or subscription explicit, and prove each provider works with a read-only check.

## Scope

### In scope (in the order to tackle)

1. Confirming access to the GCP and Azure sandboxes
2. GCP — Application Default Credentials sign-in, project selection, provider configuration
3. Azure — CLI sign-in, subscription selection, provider configuration
4. State management across clouds: `gcs` and `azurerm` backends
5. Where this course stops — HCP Terraform and Sentinel, named and not taught

### Out of scope

- Installing the Google Cloud and Azure command-line tools (M01)
- Creating any cloud resource
- Configuring the `gcs` or `azurerm` backends
- Networking or compute on GCP or Azure
- Any wrapper or abstraction that hides cloud differences
- Teaching HCP Terraform or Sentinel — they are named in the next-steps note only

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- GCP uses Application Default Credentials from an interactive login; Azure uses the Azure CLI login. Nothing else.
- No service-account keys, client secrets or any static credential, in the repository or on disk.
- The GCP project and the Azure subscription each configuration uses must not depend on whichever login happens to be active.
- Read-only data sources only. No resources are created.
- One configuration per cloud. Terraform 1.11 or later with provider versions pinned from `versions.env`.
- If either sandbox is not accessible to you, tell the trainer before you start.

## Deliverable

**Two small Terraform configurations, one per cloud, each authenticating with a short-lived login and outputting the identity it runs as**.

## Open design questions

1. What can go wrong if the ambient login points at a different project or subscription than you intended, and what in your configuration prevents it?
2. Where should state live for a configuration that creates nothing, and does your answer change once it does?

## Definition of done

Your training module — the build plus the write-up that teaches it — is done when each of these is true.

- [ ] **DoD-1** Your write-up shows both configurations passing formatting and validation checks, as pasted output.
- [ ] **DoD-2** Your write-up shows both configurations planning successfully, with an identity output for each cloud (output pasted), not the identity you expected.
- [ ] **DoD-3** Each configuration targets the intended GCP project or Azure subscription even when the active login points elsewhere (evidence shown), or your write-up records why that was not possible.
- [ ] **DoD-4** Your write-up shows the scan that found no secrets or keys in your repository or on disk, and what it looked for, not a statement that there are none.
- [ ] **DoD-5** Your write-up shows neither configuration creating a resource: the plan shows nothing to add.
- [ ] **DoD-6** Your write-up closes with a short next-steps note that names HCP Terraform and Sentinel and says in one line what each is for, in your own words.

## Best practices this stage demonstrates

- No static credentials
- Cloud differences explicit
- fmt and validate
