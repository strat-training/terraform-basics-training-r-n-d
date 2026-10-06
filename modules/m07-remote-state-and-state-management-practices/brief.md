# M07 — Remote State and State Management Practices

| | |
| --- | --- |
| Stage | 7 of 12 |
| Cloud | AWS |
| Builds on | M06 |
| Cost | The bucket you keep bills for as long as it exists, so look up what it bills before you create it. Destroy everything else at the end of the stage. |
| Leaves behind | **The state bucket** — the only thing kept. Everything else is destroyed. |

## Objective

Move state off your laptop into a remote backend that is versioned, encrypted, locked and access-controlled, and prove that locking works. The bucket you create here is reused by M08 to M11, so build it as something you would trust to hold every later stage's state.

## Scope

### In scope (in the order to tackle)

1. Why state moves to a remote backend, and what locking prevents
2. Bootstrapping, securing, and managing the lifecycle of the state bucket
3. Configuring the backend and migrating existing local state into it
4. Proving that native locking works and recovering abandoned locks

### Out of scope

- DynamoDB-based locking
- HCP Terraform and any backend other than S3
- GitLab-managed Terraform state — mention only, as something you may meet
- The `gcs` and `azurerm` backends (reference only, M12)
- Per-environment state layout (M08)

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- S3 backend with Terraform's native state locking. No DynamoDB table.
- Terraform 1.11 or later — native locking is generally available from 1.11. Verify every locking claim in your write-up against the release notes of the pinned version before you write it down.
- The bucket is bootstrapped from a local-state configuration, then retained. It is the one exception to the destroy-at-the-end rule.
- Existing local state is migrated into the backend, not recreated.
- Your sandbox role must be able to create and delete the lock object. If it cannot, tell the trainer — it is a gap in your sandbox access, not something to work around.

## Deliverable

**A protected S3 state bucket and a configuration that uses it as its remote backend**, with locking demonstrated.

## Open design questions

1. Who and what needs access to the state bucket, and how narrow can you make that without breaking Terraform?
2. How did you solve the problem of creating the thing that stores your state, and what would you do differently on a team?
3. What happens if a lock is left behind, and what must you check before overriding one?
4. Why is this bucket kept when everything else is destroyed, and what risk does that carry?

## Definition of done

Your training module — the build plus the write-up that teaches it — is done when each of these is true.

- [ ] **DoD-1** Your write-up shows a state object for your own configuration in the bucket (listing pasted).
- [ ] **DoD-2** Your write-up shows versioning and encryption at rest enabled and public access fully blocked on the bucket, shown from the cloud side, not from your configuration.
- [ ] **DoD-3** Your write-up shows a backend configuration that enables native locking, with no DynamoDB table used or created.
- [ ] **DoD-4** Your write-up shows a plan after migrating local state with no changes, so nothing was recreated.
- [ ] **DoD-5** Your write-up shows a second operation refused with a lock error while one is in progress (the error output pasted), not a description of what locking should do.
- [ ] **DoD-6** Your write-up shows a lock you left behind deliberately and your recovery without losing or corrupting state (the error and the recovery output pasted).
- [ ] **DoD-7** A learner following your training module ends with the bucket retained and everything else destroyed, confirmed from the cloud side, not only from Terraform's output.
- [ ] **DoD-8** No static keys and no state file contents are committed to version control, shown by your commit history, not assumed.

## Best practices this stage demonstrates

- State hygiene
- Remote state with locking
- fmt and validate
