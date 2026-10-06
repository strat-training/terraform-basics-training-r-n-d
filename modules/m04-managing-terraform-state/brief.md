# M04 — Managing Terraform State Brief

**Stage:** 4 of 11 · **Builds on:** M03 · **Feeds into:** M05, M08, M09, M10

## Objective

By the end of this stage, you can explain what Terraform's local state records and why it must be treated as sensitive, and move that state into a protected remote backend that you can show is versioned, encrypted and locked — using your own state, your own bucket and your own lock error as the evidence, not a description from the documentation. The bucket you create here is reused by the later stages that keep state, so build it as something you would trust to hold their state.

## Scope

You inspect your own state and build your own bucket, not a worked example. Find out, and write down in your own words:

- **Understanding and inspecting local state (read-only)** — what state records, where it lives and what Terraform uses it for, looked at without changing anything. Research: what you would check before trusting a state file you did not create, and what goes wrong when state is edited by hand.
- **Secrets and state** — what lands in state and who can read it. Research: what can leak a secret into state and how you would demonstrate that safely without a real credential, and why the course treats a state file as sensitive even when the configuration contains no secrets.
- **Why state moves to a remote backend** — what a team loses when state stays on one machine. Research: what a remote backend gives a team that local state cannot.
- **Bootstrapping and securing the state bucket** — where the bucket itself comes from, how it is protected, and why it outlives the stage. Research: how you solved the problem of creating the thing that stores your state and what you would do differently on a team, who and what needs access to the bucket and how narrow you can make that without breaking Terraform, and why the bucket is kept when everything else is destroyed and what risk that carries.
- **Configuring the backend and migrating existing local state into it** — moving the state you already have, without recreating anything. Research: how you know that nothing was recreated.
- **Native state locking** — holding one operation while a second tries to run. Research: what locking prevents, and what it does not.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies, with one exception: the bucket you create is kept when everything else is destroyed.
- You use AWS only, and a few small, cheap resources are enough for the local-state part.
- The bucket bills for as long as it exists, so look up what each resource bills before you create it, and destroy everything else at the end of the stage.
- State is local until you migrate it, and state files never go into version control.
- State subcommands are for read-only inspection only, and you change nothing about state outside the plan and apply cycle.
- You use the S3 backend with Terraform's native state locking and no DynamoDB table, and Terraform is 1.11 or later.
- Native locking is generally available from 1.11, so check every locking claim in your notes against the release notes of the pinned version before you write it down.
- You bootstrap the bucket from a local-state configuration and then keep it, and you migrate your existing local state into the backend rather than recreating it.
- Your sandbox role must be able to create and delete the lock object.
- If it cannot, tell your trainer — it is a gap in your sandbox access, not something to work around.
- Drift and reconciliation, ephemeral values and write-only arguments, recovering a lock left behind, HCP Terraform and any backend other than S3 (GitLab-managed Terraform state is mention-only), per-environment state layout (M05), marking inputs and outputs sensitive (M07) and moving, importing or removing resources from state (M10) are not part of this stage.

## Deliverable

**A protected S3 state bucket and a small configuration whose local state you inspected and then migrated into it as its remote backend**, with locking demonstrated.

## Lab

**Goal.** See what local state records, then move it into a protected S3 backend and prove that locking works.

**You do, in the sandbox.** Create a few small resources, inspect their local state read-only, create the bucket from a local-state configuration and protect it, migrate your local state into it, then hold one operation while a second tries to run.

**You build and capture.** The bucket and the configuration that now uses it as its backend are your deliverable. Capture the read-only inspection, what state holds for a sensitive value (a placeholder only), the state object in the bucket, the protections shown from the cloud side, the plan after migration, and the lock error.

**Clean-up.** Keep the bucket and destroy everything else.

## Definition of done

- DoD-01: Your notes show where your local state lives and what it records for one of your own resources, captured read-only from your own state (output pasted), not described from the documentation.
- DoD-02: Your notes show what state holds for a sensitive value, captured from your own state without exposing a real credential, not a claim taken from the documentation.
- DoD-03: A state object for your configuration exists in the bucket (listing pasted), and a plan after migrating local state shows no changes — nothing was recreated.
- DoD-04: Versioning is enabled on the bucket, encryption at rest is enabled and public access is fully blocked, shown from the cloud side, not from your configuration.
- DoD-05: The backend configuration enables native locking and no DynamoDB table is used or created, and with one operation in progress a second is refused with a lock error (the error output pasted), not described from what locking should do.
- DoD-06: The bucket is retained and everything else is destroyed, confirmed from the cloud side, and no static keys, state files or state file contents are committed to version control, shown by the ignore rule and a clean commit history.
- DoD-07: Your write-up takes a first-time learner from local state to a protected remote backend, with locking demonstrated, unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- State hygiene
- Remote state with locking
- fmt and validate

## Still open / ask your trainer

- Whether your sandbox role can create and delete the lock object — tell your trainer if it cannot.
- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
