# M11 — Going Multi-Cloud with Terraform Brief

**Stage:** 11 of 11 · **Builds on:** M01, M02 · **Feeds into:** the capstone

## Objective

By the end of this stage, you can sign in to GCP and Azure with short-lived logins, make the project or subscription explicit, and prove each provider works with a read-only check — using your own identity output as the evidence, not the identity you expected. You can see that the core Terraform workflow carries over to GCP and Azure while provider setup does not.

## Scope

You work from your own two sandboxes, not a worked example. Find out, and write down in your own words:

- **Confirming access to the GCP and Azure sandboxes** — checking that you can reach both sandboxes before you write anything. Research: how you confirm which project and which subscription you are signed in to.
- **GCP — Application Default Credentials sign-in, project selection, provider configuration** — signing in with a short-lived login and pointing the configuration at the right project. Research: what can go wrong if the ambient login points at a different project than you intended, and what in your configuration prevents it.
- **Azure — CLI sign-in, subscription selection, provider configuration** — signing in with a short-lived login and pointing the configuration at the right subscription. Research: what can go wrong if the ambient login points at a different subscription than you intended, and what in your configuration prevents it.
- **State management across clouds: `gcs` and `azurerm` backends** — reference only: you do not configure them. Research: where state should live for a configuration that creates nothing, and whether your answer changes once it does.
- **Where this course stops** — HCP Terraform and Sentinel, named and not taught. Research: what each of HCP Terraform and Sentinel is for, in one line.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- GCP uses Application Default Credentials from an interactive login, and Azure uses the Azure CLI login, and nothing else.
- You use no service-account keys, client secrets or any other static credential, in the repository or on disk, and the GCP project and the Azure subscription each configuration uses must not depend on whichever login happens to be active.
- You use read-only data sources only, so no resources are created and nothing bills.
- You write one configuration per cloud, with Terraform 1.11 or later and provider versions pinned from `versions.env`.
- If either sandbox is not accessible to you, tell your trainer before you start.
- Installing the Google Cloud and Azure command-line tools (M01), creating any cloud resource, configuring the `gcs` or `azurerm` backends, networking or compute on GCP or Azure, and any wrapper that hides cloud differences are out of scope, and HCP Terraform and Sentinel are named in your next-steps note only.

## Deliverable

**Two small Terraform configurations, one per cloud, each authenticating with a short-lived login and outputting the identity it runs as**.

## Lab

**Goal.** Sign in to GCP and Azure with short-lived logins and prove each provider works without creating anything.

**You do, in the sandbox.** Confirm access to both sandboxes, sign in to each cloud, point a configuration at the right project or subscription, and plan each configuration.

**You build and capture.** The two configurations are your deliverable. Capture the identity output for each cloud, evidence that the intended project or subscription is used even when the login points elsewhere, the scan for secrets and keys, and a plan with nothing to add.

**Clean-up.** Nothing is created, so there is nothing to destroy.

## Definition of done

- DoD-01: Both configurations pass formatting and validation checks, shown as pasted output.
- DoD-02: Both configurations plan successfully, and the plan output includes an identity output for each cloud (output pasted), not the identity you expected.
- DoD-03: Each configuration targets the intended GCP project or Azure subscription even when the active login points elsewhere (evidence shown), or your notes record why that was not possible.
- DoD-04: No secrets or keys exist in the repository or on disk, and the scan you ran is in your evidence, not a statement that there are none.
- DoD-05: Neither configuration creates a resource: the plan shows nothing to add.
- DoD-06: Your notes close with a short next-steps note that names HCP Terraform and Sentinel and says in one line what each is for.
- DoD-07: Your write-up takes a first-time learner to a working sign-in and a successful plan for GCP and for Azure unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- No static credentials
- Cloud differences explicit
- fmt and validate

## Still open / ask your trainer

- Whether both the GCP and the Azure sandboxes are accessible to you.
- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
