# M07 — Remote State and State Management Practices

| | |
| --- | --- |
| Stage | 7 of 12 |
| Course reference | Module 7 / Activity 7 "Remote state" (solution-design §6.2, §6.4) |
| Cloud | AWS |
| Builds on | M06 |
| Time box | TBC — see [README](../README.md#open-items-for-the-trainer) |
| Leaves behind | **The state bucket** — the only thing kept. Everything else is destroyed. |

## Objective

Move state off your laptop into a remote backend that is versioned, encrypted, locked and access-controlled, and prove that locking works. The bucket you create here is reused by M08 to M11, so build it as something you would trust to hold every later stage's state.

## Scope

### In scope (in the order to tackle)

1. Why state moves to a remote backend, and what locking prevents
2. The bootstrapping problem — where the state bucket itself comes from
3. Protecting the bucket — versioning, encryption at rest, blocked public access, restricted access
4. Configuring the backend and migrating existing local state into it
5. Native S3 state locking, and why DynamoDB-based locking is no longer taught
6. Proving that locking works
7. A bucket that outlives its stage — lifecycle and eventual retirement

### Out of scope

- DynamoDB-based locking, except to explain why it is deprecated (ADR-006)
- HCP Terraform and any backend other than S3 (ADR-006)
- GitLab-managed Terraform state — mention only, as something you may meet (ADR-016)
- The `gcs` and `azurerm` backends (reference only, M12)
- Per-environment state layout (M08)

## Stack constraints

- Everything under [Rules for every stage](../README.md#rules-for-every-stage).
- S3 backend with Terraform's native state locking (ADR-006). No DynamoDB table.
- Terraform 1.11 or later — native locking is generally available from 1.11. Verify every locking claim in your write-up against the release notes of the pinned version before you write it down.
- The bucket is bootstrapped from a local-state configuration, then retained. It is the one exception to the destroy-at-the-end rule.
- Existing local state is migrated into the backend, not recreated.
- Your sandbox role must be able to create and delete the lock object. If it cannot, tell the trainer — it is a sandbox-contract gap (ADR-005), not something to work around.

## Deliverable

**A protected S3 state bucket and a configuration that uses it as its remote backend**, with locking demonstrated.

## Open design questions

1. Who and what needs access to the state bucket, and how narrow can you make that without breaking Terraform?
2. How did you solve the problem of creating the thing that stores your state, and what would you do differently on a team?
3. What happens if a lock is left behind, and what must you check before overriding one?
4. Why is this bucket kept when everything else is destroyed, and what risk does that carry?

## Definition of done

- [ ] **DoD-1** A state object for your configuration exists in the bucket (listing pasted).
- [ ] **DoD-2** Versioning is enabled on the bucket (shown from the cloud side).
- [ ] **DoD-3** Encryption at rest is enabled and public access is fully blocked (shown from the cloud side).
- [ ] **DoD-4** The backend configuration enables native locking and no DynamoDB table is used or created.
- [ ] **DoD-5** A plan after migrating local state shows no changes — nothing was recreated.
- [ ] **DoD-6** With one operation in progress, a second is refused with a lock error (the error output pasted).
- [ ] **DoD-7** The bucket is retained and everything else is destroyed, confirmed from the cloud side.
- [ ] **DoD-8** No static keys and no state file contents are committed to version control.

## Best practices this stage demonstrates

- State hygiene (Activity 7 bucket checks)
- Remote state with locking (Activity 7 check)
- fmt and validate
