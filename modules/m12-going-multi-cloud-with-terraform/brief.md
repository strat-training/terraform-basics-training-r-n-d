# M12 — Going Multi-Cloud with Terraform

| | |
| --- | --- |
| Stage | 12 of 12 |
| Course reference | Solution-design Module 10 / Activity 10 "GCP/Azure setup" (§6.2); stage 12 here because M09 and M10 are new |
| Cloud | GCP and Azure |
| Builds on | M01, M02 |
| Time box | Week 4; the activity is 45–60 minutes plus reading and checkpoint (solution-design A7) |
| Leaves behind | Nothing. No resources are created. |

## Objective

See that the core Terraform workflow carries over to GCP and Azure while provider setup does not: sign in with short-lived logins, make the project or subscription explicit, and prove each provider works with a read-only check. Be able to say plainly where the clouds differ.

## Scope

### In scope (in the order to tackle)

1. Confirming access to the GCP and Azure sandboxes
2. GCP — Application Default Credentials sign-in, explicit project, provider configuration
3. Azure — CLI sign-in, explicit subscription, provider configuration
4. Read-only data sources as a safe proof of identity
5. Sign-in modes for when no browser is available — inside a container or remote workspace
6. Where the clouds differ, stated explicitly — no abstraction layer
7. The `gcs` and `azurerm` state backends — reference only

### Out of scope

- Installing the Google Cloud and Azure command-line tools (M01)
- Creating any cloud resource
- Configuring the `gcs` or `azurerm` backends (ADR-003, solution-design A10)
- Networking or compute on GCP or Azure
- Any wrapper or abstraction that hides cloud differences (ADR-003)

## Stack constraints

- Everything under [Rules for every stage](../README.md#rules-for-every-stage).
- GCP uses Application Default Credentials from an interactive login; Azure uses the Azure CLI login. Nothing else (ADR-005).
- No service-account keys, client secrets or any static credential, in the repository or on disk.
- The GCP project and the Azure subscription are set explicitly in the configuration, not inferred from whichever login happens to be active (ADR-003).
- Read-only data sources only. No resources are created.
- One configuration per cloud. Terraform 1.11 or later with provider versions pinned from `versions.env`.
- If either sandbox is not accessible to you, tell the trainer before you start.

## Deliverable

**Two small Terraform configurations, one per cloud, each authenticating with a short-lived login and outputting the identity it runs as**, plus a written comparison of how the clouds differ in setup.

## Open design questions

1. What can go wrong if the ambient login points at a different project or subscription than you intended, and what in your configuration prevents it?
2. What stays the same across all three clouds in the Terraform workflow, and what changes?
3. Why does the course refuse to hide cloud differences behind a common wrapper?
4. Where should state live for a configuration that creates nothing, and does your answer change once it does?

## Definition of done

- [ ] **DoD-1** Both configurations pass formatting and validation checks.
- [ ] **DoD-2** Both configurations plan successfully and the plan output includes an identity output for each cloud (output pasted).
- [ ] **DoD-3** The GCP project and the Azure subscription are set explicitly in configuration.
- [ ] **DoD-4** No secrets or keys exist in the repository or on disk (the scan you ran is in your evidence).
- [ ] **DoD-5** Neither configuration creates a resource (the plan shows nothing to add).
- [ ] **DoD-6** Your written comparison of cloud differences agrees with the trainer's model answer on review.

## Best practices this stage demonstrates

- No static credentials (Activity 10 check)
- Cloud differences explicit (Activity 10 note)
- fmt and validate
