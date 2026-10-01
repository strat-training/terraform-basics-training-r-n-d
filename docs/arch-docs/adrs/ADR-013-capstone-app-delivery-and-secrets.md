# ADR-013: Capstone app delivered via EC2 user-data templates; RDS-managed secret

- **Status:** Proposed
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee) to confirm
- **PRD references:** s.9 (provided application), s.12 (Security and cost: "password not hard-coded"), s.13 (CR-8)

## Context

The PRD fixes the delivery mechanism of the provided app: EC2 boot scripts as templates (`data/templates/web.sh.tftpl`, `app.sh.tftpl`), a React frontend served by Nginx on the Web tier, a Node.js API on the App tier (port 8080), and MySQL 8.4 on RDS. It also requires that the database is not public and its password is not hard-coded. It does not say how the App tier receives the password.

Marking a password via `random_password` writes it to Terraform state in plain text, which Activity 6 teaches learners to treat as a problem.

## Decision

1. **App delivery:** keep the PRD's design. Boot scripts are rendered with `templatefile()` and passed as `user_data`. No container registry, no AMI pipeline.
2. **Secrets:** create the RDS instance with **`manage_master_user_password = true`**, so RDS and AWS Secrets Manager generate and rotate the master password. The password never appears in Terraform code or in state.
3. The **App tier instance role** is allowed `secretsmanager:GetSecretValue` on that one secret; the boot script fetches it at start and passes it to the API process through the environment of the service, not through the repository or the template.
4. **Network:** Web tier in public subnets, App tier and RDS in private subnets. Security groups chain internet to Web to App to RDS and nothing else. No SSH ingress; shell access if needed is through SSM Session Manager.
5. Boot scripts are **idempotent** and use **bounded retries** to wait for RDS, so a re-run does not cause plan diffs and no `time_sleep` workaround is required.
6. Content CI tests the templates (CR-8) by rendering, linting, and running the API against a local MySQL 8.4 container.

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| `random_password` passed into RDS and user data | Password in state and in instance metadata (user data); contradicts Module 6 |
| Password as a `sensitive` variable supplied by the learner | Moves the problem to the learner's shell history or `.tfvars`; still ends up in state |
| SSM Parameter Store SecureString created by Terraform | Value still originates in Terraform state |
| Containers on ECS/EKS | Out of scope; adds large concepts and cost |
| Pre-baked AMIs | Needs an image pipeline; PRD chose boot scripts |

## Consequences

**Positive**
- Secure by default; reinforces the "no secrets in code or state" message.
- Rubric line "password not hard-coded" is satisfied structurally.

**Negative / trade-offs**
- Slightly more IAM (instance role, policy) than a simple variable; useful teaching content but more for learners to read.
- Sandbox must permit Secrets Manager and RDS-managed secrets and KMS use for it.
- Boot-time dependency on internet access (via NAT) for package install; see ADR-011.
- Destroy must remove the managed secret; secrets can have a recovery window, so the clean-up check should tolerate "scheduled for deletion" status or the RDS instance should be destroyed with the secret force-deleted by RDS. To be verified in the build spike.
- User data is visible in instance metadata; it contains no secrets under this design.
