# Architecture Decision Records

Decisions for the **Terraform Concepts & Best Practices Training (4-Week Self-Paced)** program. See the [solution design](../solution-design.md) for the full context.

**Status key**
- **Accepted**: stated as a decision in the PRD, or confirmed by the program stakeholders since (ADR-016).
- **Proposed**: proposed by the solution design to implement the PRD; needs sign-off from the program owner (@Lee).

| ADR | Title | Status |
| --- | --- | --- |
| [001](ADR-001-delivery-as-markdown-in-starter-repo.md) | Deliver the program as Markdown modules in a starter repository | Accepted (hosting amended by 016) |
| [002](ADR-002-terraform-cli-with-opentofu-sidebar.md) | Teach the Terraform CLI; OpenTofu as a sidebar only | Accepted |
| [003](ADR-003-aws-primary-gcp-azure-setup-only.md) | AWS as primary cloud; GCP and Azure setup-only plus one storage resource | Accepted |
| [004](ADR-004-pinned-dev-container.md) | Pinned dev container, run locally; GitLab Workspaces optional | Accepted (amended by 016) |
| [005](ADR-005-sandbox-accounts-and-short-lived-credentials.md) | Pre-made sandbox accounts and short-lived credentials | Accepted |
| [006](ADR-006-s3-remote-state-native-locking.md) | S3 remote state with native locking (`use_lockfile`) | Accepted |
| [007](ADR-007-environments-via-tfvars-and-backend-config.md) | Environments via per-environment `.tfvars` and backend config files | Proposed |
| [008](ADR-008-declarative-refactoring-blocks.md) | Teach declarative refactoring blocks over state commands | Proposed |
| [009](ADR-009-local-check-scripts.md) | Local check scripts built on native Terraform commands | Proposed |
| [010](ADR-010-content-ci-and-version-pinning.md) | Content CI with a single pinned-version source and scheduled canary runs | Proposed |
| [011](ADR-011-cost-and-destroy-controls.md) | Cost controls: destroy at the end of each activity, NAT only in the capstone | Accepted |
| [012](ADR-012-capstone-single-root-multi-cloud.md) | Capstone as one root module, one apply, three clouds, one state | Proposed |
| [013](ADR-013-capstone-app-delivery-and-secrets.md) | Capstone app delivered via EC2 user-data templates; RDS-managed secret | Proposed |
| [014](ADR-014-offsite-backup-without-static-keys.md) | Off-site backup to GCS without static keys | Proposed (needs spike) |
| [015](ADR-015-sandbox-compatible-tooling-only.md) | Sandbox-compatible tooling only | Accepted |
| [016](ADR-016-gitlab-for-hosting-and-ci.md) | Host the starter repository and content CI on GitLab | Accepted (changes PRD wording) |

## Format

Each ADR has: Status, Date, Context, Decision, Alternatives considered, Consequences, and References to PRD sections. Use the next free number for new decisions; do not edit an accepted ADR's decision, supersede it with a new one and link both ways.
