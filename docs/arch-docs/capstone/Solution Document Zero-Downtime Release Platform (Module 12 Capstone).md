# Solution Document: Zero-Downtime Release Platform (Module 12 Capstone)

This document specifies the reference solution for the Terraform Shop capstone: two Terraform stacks that release three App versions to AWS with zero failed checkouts, roll back a bad release by changing one variable, and keep an off-site copy of the item inventory in GCP with no stored keys.

## Solution at a glance

Shoppers reach the Web tier through a public load balancer, the Web tier calls one of two App colours through an internal load balancer, and both colours share one private database.

&#91;embedded content: request path and storage links · AWS, GCP, Azure\]

In the diagram, `w` is `green_weight`. The highlighted internal ALB is the only place a stage 2, 3, 4 or 6 change lands. The dashed line is the browser loading theme and images from Azure; the solid line from the S3 exports bucket to GCP is the Storage Transfer job, and the release manifest is also published to both GCP and Azure at every stage.

## Design decisions

Every release is a change to variable values on one stack, and the design is chosen so that each change touches as few resources as possible.

| PRD requirement | Design decision | Why it works |
| --- | --- | --- |
| Zero downtime | One internal ALB listener with a single `forward` action over the `blue` and `green` target groups; weights come from `green_weight` and `100 - green_weight` | Stages 2–4 and 6 change one listener, so no instance is created, replaced or drained |
| One-step rollback | Blue keeps running after cutover; rollback sets `green_weight = 100` | Traffic moves back to a healthy colour in seconds, with no instance replacement |
| One colour replaced at a time | Each colour has its own launch template, Auto Scaling Group (ASG) and target group, built by `app_color` called with `for_each` | A version change alters one launch template's user data, so only that colour refreshes |
| Web tier never changes in a release | `web_tier` takes no App version input; its only link to the App tier is the internal ALB DNS name | An App release cannot reach the Web launch template, so every release plan shows zero Web changes |
| No gap during replacement | `create_before_destroy` on launch templates and target groups; ASG `instance_refresh` with `min_healthy_percentage = 100` and `max_healthy_percentage = 200` | New instances pass health checks before old ones leave |
| Shared database across colours | One RDS instance in `foundation`; v2 adds a nullable column behind an existence check and a named lock | Two colours starting together cannot race, and v1, v2 and v3 all read the same schema |
| Bad release that health checks miss | A CloudWatch 5xx alarm per colour, plus the probe's per-version failure count | v3 returns 200 on `/health` but 500 on orders, so only the 5xx signal catches it |
| Releases never touch network, roles or database | Two stacks, joined by `terraform_remote_state` | The rarely changing layer cannot be hit by a release plan |
| No stored keys | Instance profiles for AWS access; a web-identity role for Google's transfer service | Nothing in code, state or boot scripts grants access except the database password |
| Reproducible stages | Each stage is one `-var` or tfvars change, saved as a plan file | The evidence file can show the exact plan that produced each result |

Two choices need explaining. First, instance refresh is limited to one ASG, so a v3 push to blue cannot disturb green. Second, the only `depends_on` in the code is on the GCP transfer job, which must wait for its AWS role policy and its bucket permission, because neither dependency appears as a reference.

## Repository and state layout

The repository holds two stacks and seven local modules; the `foundation` stack changes rarely and the `release` stack changes at every stage.

```text
shop/
├── README.md
├── evidence.md  design-note.md  ai-review-log.md
├── data/                      # supplied: templates, seed.sql, assets, probe.sh, bad.tfvars, check.sh
├── stages/                    # 0-baseline.tfvars ... 6-rollback.tfvars (release variables only)
├── evidence/                  # saved plans, probe logs, command output
├── envs/
│   ├── dev.tfvars  prod.tfvars
│   ├── dev-foundation.s3.tfbackend  dev-release.s3.tfbackend
│   └── prod-foundation.s3.tfbackend prod-release.s3.tfbackend
├── foundation/                # network, iam, database, exports bucket
│   ├── main.tf variables.tf outputs.tf versions.tf .terraform.lock.hcl
├── release/                   # web_tier, app_tier, app_color x2, alarms, cloud_storage, manifest
│   ├── main.tf variables.tf outputs.tf versions.tf .terraform.lock.hcl
│   ├── moved.tf  manifest.json.tftpl
└── modules/
    ├── network/ iam/ database/ web_tier/ app_tier/ app_color/ cloud_storage/
    └── alarms/                # added in day-2 task 3
```

| Stack | Owns | State key | Reads from |
| --- | --- | --- | --- |
| `foundation` | VPC, subnets, NAT gateway, security groups, `web` and `app` roles and profiles, RDS, S3 exports bucket | `shop/<env>/foundation.tfstate` | Nothing |
| `release` | Public ALB, Web ASG, internal ALB, blue and green colours, alarms, GCP bucket and transfer job, AWS transfer role, Azure storage, manifest | `shop/<env>/release.tfstate` | `foundation` outputs |

**Backend files.** Each `*.s3.tfbackend` holds `bucket`, `key`, `region = "ap-southeast-1"` and `use_lockfile = true`. Run `terraform init -backend-config=../envs/dev-release.s3.tfbackend` per stack; the S3 backend then locks with a lock file next to the state object, and no DynamoDB table is involved.

**Foundation outputs the release stack needs:** VPC ID, public, private and database subnet IDs, the four security group IDs (public ALB, Web, internal ALB, App), both instance profile names, the database endpoint, name and user, the generated password (sensitive), and the exports bucket name and ARN.

**Boundary rule.** A resource belongs in `foundation` if a release never needs to change it and its destruction would lose data or break access. This puts the database and IAM roles in the stable layer, and puts the transfer role in `release`, because its trust depends on a Google service account that `release` creates.

## Module specifications

Each module has typed, validated inputs, documented outputs and a README listing both; the table fixes what each module owns and what it hands on.

| Module | Stack | Key inputs | Key outputs | Notable resources |
| --- | --- | --- | --- | --- |
| `network` | foundation | `vpc_cidr`, `azs`, `name_prefix` | VPC and subnet IDs by tier, security group IDs | VPC, subnets via `for_each` over a map of AZ and tier, one NAT gateway, route tables, tier-to-tier security groups |
| `iam` | foundation | `name_prefix`, `exports_bucket_arn` | Instance profile names for `web` and `app` | Two roles, `AmazonSSMManagedInstanceCore` attachments, one `aws_iam_policy_document` for `s3:PutObject` on `exports/*`, two instance profiles |
| `database` | foundation | `db_instance_class`, `db_subnet_ids`, `db_sg_id` | Endpoint, name, user, password (sensitive) | `random_password`, subnet group, RDS MySQL 8.4, `publicly_accessible = false` |
| `web_tier` | release | `web_count`, `instance_type`, subnets, `app_backend_url`, `asset_base_url` | Public ALB DNS name, ASG name | Public ALB, Web target group, launch template from `web.sh.tftpl`, Web ASG |
| `app_tier` | release | Map of colour to target group ARN, map of colour to weight, subnets, internal ALB security group | Internal ALB DNS name, listener ARN | Internal ALB, one listener with a weighted `forward` action |
| `app_color` | release | `color`, `app_version`, `desired_count`, `instance_type`, profile, database and bucket values, `asset_base_url` | ASG name, target group ARN | Target group, launch template from `app.sh.tftpl`, ASG with instance refresh; called with `for_each` over `blue` and `green` |
| `cloud_storage` | release | `exports_bucket`, `backup_interval_hours`, `public_alb_dns`, `assets_path`, manifest content | GCP bucket name, Azure asset base URL | GCP bucket and transfer job, AWS transfer role, Azure Storage Account, container, blobs, CORS rule |
| `alarms` | release | Target group and load balancer ARN suffixes | Alarm ARNs | Unhealthy-host alarms for Web, blue and green; 5xx alarms for both colours |

**Where the public ALB lives.** The PRD names the Web tier and the public ALB together; the public ALB is built inside `web_tier`, so one module owns the front door and its target group.

**Where the transfer role lives.** The PRD requires the transfer role in the `release` stack, and it is built inside `cloud_storage` because its trust policy needs Google's service account subject ID and its ARN feeds the transfer job in the same module.

## Variables and guardrails

Bad input fails at plan time with a message that states the problem and the allowed values; cross-variable rules sit in the root module of the `release` stack.

```hcl
variable "env" {
  type = string
  validation {
    condition     = contains(["dev", "prod"], var.env)
    error_message = "env must be \"dev\" or \"prod\"; got \"${var.env}\"."
  }
}

variable "green_weight" {
  type = number
  validation {
    condition     = contains([0, 10, 50, 100], var.green_weight)
    error_message = "green_weight must be 0, 10, 50 or 100; got ${var.green_weight}."
  }
}

variable "instance_types" {
  type = map(string)
  validation {
    condition     = toset(keys(var.instance_types)) == toset(["web", "blue", "green"])
    error_message = "instance_types must have exactly the keys web, blue and green."
  }
  validation {
    condition     = alltrue([for v in values(var.instance_types) : contains(["t3.micro", "t3.small"], v)])
    error_message = "Each instance_types value must be t3.micro or t3.small."
  }
}

variable "vpc_cidr" {
  type = string
  validation {
    condition     = can(cidrhost(var.vpc_cidr, 0)) && endswith(var.vpc_cidr, "/16")
    error_message = "vpc_cidr must be a valid CIDR block of size /16, such as 10.20.0.0/16; got \"${var.vpc_cidr}\"."
  }
}
```

The remaining variables follow the same pattern:

| Variable | Condition |
| --- | --- |
| `web_count` | `var.web_count >= 2 && var.web_count <= 4 && floor(var.web_count) == var.web_count` |
| `blue_version`, `green_version` | `contains(["v1", "v2", "v3"], var.blue_version)` |
| `blue_count`, `green_count` | Whole number from 0 to 4 each; `green_count` also checks `var.blue_count + var.green_count >= 2`, which needs Terraform 1.9 or later (the pinned minimum is 1.11) |
| `db_instance_class` | `contains(["db.t4g.micro", "db.t4g.small"], var.db_instance_class)` |
| `export_interval_minutes` | Whole number from 5 to 60 |
| `backup_interval_hours` | Whole number from 1 to 24 |

**Plan-level guardrails.** Rules about the plan as a whole use a `precondition`, so a failing plan stops before any change and reports every broken rule together:

```hcl
locals {
  weights = { blue = 100 - var.green_weight, green = var.green_weight }
  counts  = { blue = var.blue_count, green = var.green_count }
}

resource "terraform_data" "guardrails" {
  lifecycle {
    precondition {
      condition     = alltrue([for c in keys(local.weights) : local.weights[c] == 0 || local.counts[c] > 0])
      error_message = "A colour with a non-zero weight needs at least one instance. Raise blue_count or green_count, or set that colour's weight to 0."
    }
    precondition {
      condition     = var.blue_count + var.green_count >= 2
      error_message = "blue_count and green_count must total at least 2 so the footer can show which App server answered."
    }
  }
}
```

The first `precondition` is the distinction proof: `green_weight = 50` with `green_count = 0` stops the plan. Because a `check` block only warns, both rules are preconditions.

## Release mechanics

A release is a set of variable values; the code below turns those values into weights, launch templates and rolling refreshes.

**1. The weighted listener** lives in `app_tier`. It takes a map of colour to target group ARN and a map of colour to weight, so a stage needs no new code.

```hcl
resource "aws_lb_listener" "app" {
  load_balancer_arn = aws_lb.internal.arn
  port              = 80
  protocol          = "HTTP"

  default_action {
    type = "forward"
    forward {
      dynamic "target_group" {
        for_each = var.target_group_arns   # { blue = "...", green = "..." }
        content {
          arn    = target_group.value
          weight = var.weights[target_group.key]   # blue = 100 - green_weight
        }
      }
    }
  }
}
```

**2. One colour per module call.** The root of `release` calls `app_color` once with `for_each` over the colours, so blue and green run identical code:

```hcl
locals {
  colors = {
    blue  = { version = var.blue_version,  count = var.blue_count }
    green = { version = var.green_version, count = var.green_count }
  }
}

module "app_color" {
  source   = "../modules/app_color"
  for_each = local.colors

  color         = each.key
  app_version   = each.value.version
  desired_count = each.value.count
  instance_type = var.instance_types[each.key]
  # profile, subnets, security group, database, bucket, asset URL come from remote state
}
```

**3. Inside `app_color`**, the launch template carries the version in its user data, and the ASG replaces instances when that template changes:

```hcl
resource "aws_launch_template" "this" {
  name_prefix            = "${var.name_prefix}-${var.color}-"
  image_id               = data.aws_ssm_parameter.ami.value
  instance_type          = var.instance_type
  vpc_security_group_ids = [var.app_sg_id]
  iam_instance_profile { name = var.instance_profile }
  metadata_options { http_tokens = "required" }
  user_data = base64encode(templatefile(var.template_path, {
    app_version = var.app_version, color = var.color,
    db_host = var.db_host, db_name = var.db_name, db_user = var.db_user, db_password = var.db_password,
    asset_base_url = var.asset_base_url, exports_bucket = var.exports_bucket,
    export_interval_minutes = var.export_interval_minutes
  }))
  lifecycle { create_before_destroy = true }
}

resource "aws_autoscaling_group" "this" {
  name_prefix               = "${var.name_prefix}-${var.color}-"
  min_size                  = var.desired_count
  max_size                  = var.desired_count + 2
  desired_capacity          = var.desired_count
  vpc_zone_identifier       = var.private_subnet_ids
  target_group_arns         = [aws_lb_target_group.this.arn]
  health_check_type         = "ELB"
  health_check_grace_period = 300

  launch_template {
    id      = aws_launch_template.this.id
    version = aws_launch_template.this.latest_version
  }

  instance_refresh {
    strategy = "Rolling"
    preferences {
      min_healthy_percentage = 100
      max_healthy_percentage = 200
      instance_warmup        = 120
    }
  }
  lifecycle { create_before_destroy = true }
}
```

The target group sits in the same module, with `name_prefix` and `create_before_destroy`; AWS limits a target group name prefix to six characters, so use a short one such as `blu-` and carry the full name in tags.

**4. Manifest stamp.** `timestamp()` in a template would make every plan show a change. Instead a `terraform_data.stage_stamp` records the time only when the release inputs change:

```hcl
resource "terraform_data" "stage_stamp" {
  triggers_replace = [var.release_stage, var.blue_version, var.green_version, var.green_weight, var.blue_count, var.green_count]
  input            = timestamp()
  lifecycle { ignore_changes = [input] }
}
```

The manifest template reads `terraform_data.stage_stamp.output`, so each stage writes a new object version and the plan after it is clean. This adds one variable, `release_stage`, with an allowlist of stage names, which the PRD's table does not list but the manifest needs.

**What this guarantees**

- A stage that changes only `green_weight` edits one listener and nothing else.
- A version change replaces instances of one colour, because the other colour's launch template is a different resource with different inputs.
- Scaling a colour changes `desired_capacity` and does not start a refresh, because the launch template is unchanged.
- The provider starts an instance refresh and may return before it finishes, so each runbook step confirms the refresh with `aws autoscaling describe-instance-refreshes` before the next variable change.

## IAM and security design

Access is granted by role and by security group reference, never by key or by address range, and each tier can reach only the next one.

**Security groups.** Every ingress rule names a source security group, except the public ALB's rule from the internet. Rules are separate `aws_vpc_security_group_ingress_rule` resources so each can be read and checked on its own.

| Group | Ingress | Egress |
| --- | --- | --- |
| Public ALB | 80 from `0.0.0.0/0` | 80 to the Web group |
| Web | 80 from the public ALB group | 80 to the internal ALB group; 443 to the internet for Session Manager and packages |
| Internal ALB | 80 from the Web group | 8080 to the App group |
| App | 8080 from the internal ALB group | 3306 to the database group; 443 to the internet for Session Manager, packages and S3 |
| Database | 3306 from the App group | None |

The database subnets have a route table with the local route only, so they have no path to the NAT gateway. Port 22 appears nowhere, and no key pair resource exists.

**Instance roles.** Both roles trust `ec2.amazonaws.com` and attach `AmazonSSMManagedInstanceCore`. Only `app` gets a customer-managed policy:

```hcl
data "aws_iam_policy_document" "app_exports" {
  statement {
    sid       = "PutExports"
    actions   = ["s3:PutObject"]
    resources = ["${var.exports_bucket_arn}/exports/*"]
  }
}
```

The exports bucket uses default S3-managed encryption, so the role needs no KMS permissions. The Web role has no custom policy, so proof C fails with AccessDenied by construction.

**Transfer role.** Created in `cloud_storage`, trusted only by Google's transfer service account through web identity:

```hcl
data "google_storage_transfer_project_service_account" "this" {}

data "aws_iam_policy_document" "transfer_trust" {
  statement {
    actions = ["sts:AssumeRoleWithWebIdentity"]
    principals {
      type        = "Federated"
      identifiers = ["accounts.google.com"]
    }
    condition {
      test     = "StringEquals"
      variable = "accounts.google.com:sub"
      values   = [data.google_storage_transfer_project_service_account.this.subject_id]
    }
  }
}

data "aws_iam_policy_document" "transfer_read" {
  statement {
    sid       = "ListExports"
    actions   = ["s3:ListBucket"]
    resources = [var.exports_bucket_arn]
  }
  statement {
    sid       = "ReadExports"
    actions   = ["s3:GetObject"]
    resources = ["${var.exports_bucket_arn}/exports/*"]
  }
}
```

The PRD asks for list and read on the bucket only; scoping `GetObject` to the `exports/` prefix is tighter and still satisfies it. Google's documentation also lists `s3:GetBucketLocation` for AWS sources; add it only if the pilot transfer fails for that reason, and update proof E to match.

**Rules enforced by `check.sh`.** No `*` in a customer-managed policy's actions or resources, no `AdministratorAccess`, no `aws_iam_user`, `aws_iam_access_key` or `aws_key_pair`, and no `access_key` block on the transfer job. The `0.0.0.0/0` rule applies to ingress only, because Web and App need outbound HTTPS through the NAT gateway.

**Fallback.** If the sandbox forbids creating roles, `foundation` takes `web_instance_profile` and `app_instance_profile` as inputs, calls `iam` with `for_each` over an empty map, and passes the supplied names on as outputs. The transfer role cannot be created either, so the GCP backup path is dropped, proofs D and E are waived, and proofs A–C cover only what the supplied profiles allow.

## Cross-cloud wiring

Three dependency chains cross cloud or tier boundaries, and each is solved with a resource reference so a single `terraform apply` of the `release` stack resolves it.

&#91;embedded content: cross-cloud dependency chains · 3 chains\]

The transfer job is the one box that needs two inputs: the role it assumes and write access to the GCP bucket.

| Chain | How Terraform wires it | Why there is no cycle |
| --- | --- | --- |
| Assets | The Azure Storage Account's blob CORS rule uses `"http://${aws_lb.public.dns_name}"` as its allowed origin; the Web and App launch templates take the account's primary blob endpoint plus the container name as `asset_base_url` | The public ALB depends on no launch template, so it exists before the storage account, which exists before the templates |
| Front door to App tier | `app_backend_url = "http://${module.app_tier.internal_dns_name}"` goes to the Web launch template | The internal ALB depends only on subnets, a security group and target groups |
| Backup | The `google_storage_transfer_project_service_account` data source gives the subject ID; the AWS role trusts it; `role_arn` feeds `aws_s3_data_source` in the transfer job; a bucket IAM member gives the Google service account write access | The job lists the role policy and the bucket permission in `depends_on`, the only `depends_on` in the code, because neither shows up as a reference |

The three chains span module boundaries, which Terraform allows because it orders resources, not modules: `web_tier` outputs the public ALB name that `cloud_storage` needs, and `cloud_storage` outputs the asset URL that `web_tier` needs, and no single resource depends on itself. A learner who copies any of these values by hand has broken the PRD rule, and the second apply would show it.

## Off-site inventory backup

The GCP bucket holds a versioned, off-site copy of the shop's item inventory, and no static credential exists on AWS, Google or in the repository.

**What is backed up.** Each App instance exposes `/inventory/export`, which writes the items the shop sells (what `/products` returns) as one JSON file named `exports/inventory-<UTC timestamp>-<instance ID>.json`, using the `app` instance role. The endpoint replaces `/orders/export` in the PRD's endpoint list, and the same timer runs it every `export_interval_minutes`. The instance ID in the name keeps instances from overwriting each other. Order data is no longer exported; `/orders/stats` still serves the stage 3 proof.

**Credentials by hop**

| Hop | Identity | Credential |
| --- | --- | --- |
| App instance to S3 | `app` instance role | Temporary credentials from the instance metadata service, which requires a session token |
| Google Storage Transfer to S3 | AWS role `shop-<env>-gcs-transfer` | A short-lived Google identity token exchanged through `AssumeRoleWithWebIdentity`; the role trusts one Google service account subject |
| Google Storage Transfer to the bucket | Google's transfer service agent | An IAM binding on the bucket; no key |
| Terraform to GCP | The learner's application default credentials | Never a JSON key file |
| Learner reads the backup (proof D) | The learner's own `gcloud` login | Nothing stored in the repository |

**Transfer job.** It pulls from S3, so the App tier needs no Google client, no Google identity and no outbound path to GCP:

```hcl
resource "google_storage_transfer_job" "inventory_backup" {
  description = "shop-${var.env} inventory backup"
  project     = var.gcp_project

  transfer_spec {
    aws_s3_data_source {
      bucket_name = var.exports_bucket
      role_arn    = aws_iam_role.transfer.arn     # no aws_access_key block
    }
    gcs_data_sink {
      bucket_name = google_storage_bucket.backup.name
      path        = "backups/"
    }
    object_conditions { include_prefixes = ["exports/inventory-"] }
    transfer_options {
      delete_objects_from_source_after_transfer = false
      overwrite_when                            = "DIFFERENT"
    }
  }

  schedule {
    # schedule_start_date comes from plantimestamp(); ignore_changes below keeps plans clean
    repeat_interval = "${var.backup_interval_hours * 3600}s"
  }

  depends_on = [aws_iam_role_policy.transfer_read, google_storage_bucket_iam_member.transfer_writer]
  lifecycle { ignore_changes = [schedule] }
}
```

**Bucket settings.** Versioning on, a lifecycle rule that deletes non-current versions after 30 days, `uniform_bucket_level_access = true`, `public_access_prevention = "enforced"` and `force_destroy = true` for teardown. Only the transfer service agent and the learner can write.

**Guardrails.** `check.sh` fails the submission on any `google_service_account_key`, any `aws_access_key` block on the transfer job and any `aws_iam_access_key`. If the GCP project enforces the organisation policy that blocks service account key creation, the design still works, because it never creates one.

**Alternative not chosen.** The App tier could push to GCS directly through workload identity federation from its AWS role. That is also keyless, but it adds an identity pool and provider, a Google client in the boot script and an outbound path from the App tier to GCP, so the pull model is simpler to build and to prove.

**Stock levels.** The inventory includes a stock quantity per item, so each snapshot records what was on hand at that moment and the versioned GCP bucket keeps the history. This changes four course assets:

| Asset | Change |
| --- | --- |
| `seed.sql` | `products` gains `stock INT NOT NULL` with a high starting value for each of the 12 items. Seeding uses `INSERT IGNORE`, so a second run never resets stock |
| `app.sh.tftpl`, all versions | `/products` returns `stock`. Placing an order inserts the order and decrements stock in one transaction, using `UPDATE products SET stock = stock - ? WHERE id = ? AND stock >= ?`, and answers 409 when stock is short. `/inventory/export` writes `stock` with each item |
| Frontend build | Shows the stock on each product card and disables the add button at zero (optional for the proof) |
| `probe.sh` | No change, but the starting stock must be large enough that the probe cannot exhaust it during an attempt; a sold-out item would look like a failed checkout |

**Why stock is safe across versions.** The column exists from v1, so v2 and v3 add nothing to it and rollback needs no schema step. The decrement is one atomic statement, so blue and green can sell the same item at once without overselling. v3's order failure happens before any write, so a failed order never changes stock.

**Stock checks**

- At the end of stage 3, the stock removed from all items equals the units in the orders placed by v1 and v2 together.
- After a stage 5 failure run, stock has not moved for the failed orders.
- The latest GCP snapshot shows stock values that match `/products` at the time of the export.

The starting stock is a course-team decision: 100,000 per item is far above any probe run in this capstone, and still a plain `INT`.

## Release runbook

Each stage is one small tfvars overlay applied on top of the environment file, so the evidence file can name the exact input that produced each result.

```bash
cd release
terraform plan -var-file=../envs/dev.tfvars -var-file=../stages/2-canary.tfvars -out=stage2.tfplan
terraform show -no-color stage2.tfplan > evidence/stage2.plan.txt   # keep the "Plan: x to add, y to change, z to destroy" line
terraform apply stage2.tfplan                                       # probe.sh keeps running in a second terminal
```

Stage overlays live in `stages/` and hold only release variables (`release_stage`, versions, counts, `green_weight`); environment differences stay in `envs/dev.tfvars` and `envs/prod.tfvars`.

| Stage | Overlay values (change from the previous stage) | Resources that change besides the manifest and its stamp | Confirm before moving on |
| --- | --- | --- | --- |
| 0. Baseline | `web_count = 2`, `blue_version = v1`, `blue_count = 2`, `green_count = 0`, `green_weight = 0` | Everything is created; green exists with zero instances | All Web, blue and green targets report healthy; shop loads in a browser; probe shows 0 failures |
| 1. Warm green | `green_version = v2`, `green_count = 2` | Green launch template (in place) and green ASG | Green targets healthy; probe shows only v1 |
| 2. Canary | `green_weight = 10` | Internal ALB listener | Probe shows v1 and v2, about 1 in 10 on v2, 0 failures |
| 3. Half and half | `green_weight = 50` | Internal ALB listener | About half on each version; `/orders/stats` shows orders from both versions |
| 4. Cutover | `green_weight = 100` | Internal ALB listener | Every probe response is v2; blue still running |
| 5. Bad release | `blue_version = v3`, `green_weight = 90` | Blue launch template and blue ASG (instance refresh), listener | Refresh status is `Successful`; probe failures appear on v3 only; 5xx alarm is in ALARM |
| 6. Rollback | `green_weight = 100` | Internal ALB listener | Failures stop within one probe cycle; no instance was replaced |

**What "manifest and its stamp" means.** The PRD describes stages 2–4 and 6 as "listener weights only". The reference plan also shows the `terraform_data.stage_stamp` replacement and the manifest objects on GCP and Azure, because the PRD requires a new manifest version at every stage. Assessors should read the rule as: no compute, network or Web-tier change.

**Commands for the checks**

```bash
# Target health for a colour
aws elbv2 describe-target-health --target-group-arn "$(terraform output -raw green_target_group_arn)"

# Instance refresh finished (run after any stage that changes a version)
aws autoscaling describe-instance-refreshes --auto-scaling-group-name "$ASG" --query 'InstanceRefreshes[0].Status'

# Manifest versions on GCP, as evidence that every stage published
gcloud storage ls --all-versions "gs://$GCP_BUCKET/release-manifest.json"
```

**Alarm behaviour for stage 5.** Each colour has a 5xx alarm on `HTTPCode_Target_5XX_Count` for its target group, with a one-minute period, one evaluation period, a threshold of 1 and `treat_missing_data = "notBreaching"`. At 10 percent of probe traffic, v3 produces enough failed orders for the alarm to fire within a few minutes. Save the alarm state with the stage 5 evidence.

## Day-2 changes

Each task starts from the end of stage 6, where green runs v2 at 100 percent of traffic and blue runs v3 idle at weight 0.

| Task | Change | Plan shows | Proof |
| --- | --- | --- | --- |
| 1. Scale out | `green_count = 3` | One in-place change: green ASG `desired_capacity` 2 to 3 (`min_size` follows) | Footer shows a third App server; probe shows 0 failures |
| 2. Resize without downtime (distinction) | Five plans, below | Each plan touches one idle colour | Probe shows 0 failures throughout |
| 3. Move and rename safely | `moved` blocks | 0 to add, 0 to change, 0 to destroy | Plan output with the move lines |
| 4. Adopt a hand-made alarm | `import` block and `-generate-config-out` | One import, then a clean plan | Second plan reports no changes |
| 5. Catch drift | Console edit, then `-refresh-only` | Listener weights differ from the variables | Final plan is clean |

**Task 1.** The instance is not a Terraform resource, so the plan cannot "add one App instance". It shows the ASG change; the third instance is visible in the footer and in `aws autoscaling describe-auto-scaling-groups`. The PRD wording should say this.

**Task 2.** Blue still runs v3, so the sequence starts by repairing it while it is idle:

1. `blue_version = v2`. Blue refreshes with no traffic on it.
2. `instance_types.blue = "t3.small"` with `green_weight = 100`. The plan replaces blue instances only; wait for the refresh to finish.
3. `green_weight = 0`. All traffic moves to blue, which now runs v2 on the new size.
4. `instance_types.green = "t3.small"`. The plan replaces green instances only; wait for the refresh and healthy targets.
5. `green_weight = 100`.

Change one key of `instance_types` per apply. A plan that changes both keys would refresh both colours together, which is the failure this task is meant to catch.

**Task 3.** Moved blocks keep the addresses in state and so avoid replacement:

```hcl
# release/moved.tf: alarms leave the root and enter the alarms module
moved {
  from = aws_cloudwatch_metric_alarm.app_5xx
  to   = module.alarms.aws_cloudwatch_metric_alarm.app_5xx
}
moved {
  from = aws_cloudwatch_metric_alarm.unhealthy
  to   = module.alarms.aws_cloudwatch_metric_alarm.unhealthy
}

# modules/app_color/moved.tf: rename inside the module; applies to both colours
moved {
  from = aws_launch_template.this
  to   = aws_launch_template.app
}
```

For resources created with `for_each`, the `from` and `to` addresses without an index move every instance at once.

**Task 4.** Create an alarm named `shop-dev-web-5xx` in the console, then:

```hcl
import {
  to = aws_cloudwatch_metric_alarm.web_5xx
  id = "shop-dev-web-5xx"
}
```

```bash
terraform plan -generate-config-out=generated_web_5xx.tf
```

Tidy the generated file: replace literal ARNs and names with references and variables, and delete computed-only arguments. Config generation works for resources in the root module, so the adopted alarm stays in the root of `release`. The first apply imports it and adds the default tags; the plan after that must be clean. The PRD's "plan after the import is clean" therefore means after that apply.

**Task 5.** Edit the internal listener's weights in the console, then run `terraform plan -refresh-only` to see the drift. The variables describe the intended release, so the console was wrong: a normal `terraform apply` puts the weights back (one in-place change). Accepting the drift with `apply -refresh-only` would instead record the wrong weights in state, which is the answer to give if the console change had been the intended one.

## Proofs

Each proof is saved in `evidence.md` as the command run and its output; the failure proofs run before the first apply of the environment.

**Failure proofs (plan time, nothing created)**

| Proof | Command and input | Expected result |
| --- | --- | --- |
| 1. Supplied file | `terraform plan -var-file=../data/bad.tfvars` in `release` | Exit code 1 with at least three `Invalid value for variable` errors (for example `green_weight = 150`, `blue_version = "v9"`), each stating the allowed values; no plan file written |
| 2. Invalid network | `vpc_cidr = "10.0.0.0/24"` in a learner file, run in `foundation` | The `/16` rule rejects it; repeat with `"10.0.0.0/33"` to show the `can(cidrhost())` branch |
| 3. Disallowed size | `instance_types = { web = "t3.micro", blue = "m5.large", green = "t3.micro" }`, and separately `db_instance_class = "db.r6g.large"` | Both rejected with the allowlist in the message |
| Distinction | `-var green_weight=50 -var green_count=0` | The `precondition` stops the plan and says which colour has weight but no instances |

**Identity and backup proofs.** Open sessions with `aws ssm start-session --target <instance-id>`; there is no SSH.

| Proof | Where | Command | Expected result |
| --- | --- | --- | --- |
| A. App role works | App instance | `aws sts get-caller-identity`, then `echo ok \| aws s3 cp - s3://shop-dev-exports/exports/proof-a.txt` | ARN contains `assumed-role/shop-dev-app`; object appears under `exports/` |
| B. App role is limited | App instance | The same copy to `s3://shop-dev-exports/other/x.txt`, and to the state bucket | `AccessDenied` for both |
| C. Web role has no S3 | Web instance | The proof A copy | `AccessDenied` |
| D. Backup lands in GCP | Workstation | `gcloud storage ls --recursive gs://$GCP_BUCKET/backups/` | At least one inventory snapshot object; its name and size match the S3 object, and its item count equals what the shop's product list returns |
| E. Transfer role is limited | Workstation, read-only | `aws iam get-role --role-name shop-dev-gcs-transfer --query Role.AssumeRolePolicyDocument`, then `aws iam get-role-policy` for its policy | Only Google's service account subject can assume it; only `s3:ListBucket` and `s3:GetObject` on the exports bucket |

**Proof D details.** The transfer copies objects whose names start with `exports/inventory-`, so they arrive under `backups/exports/`; list `backups/` recursively. Each snapshot is a JSON array of the shop's items, so compare its item count with what `/products` returns. For objects uploaded in a single part, the S3 ETag is the MD5 checksum and can be compared with the GCS `md5Hash` after base64 decoding. The first copy needs a snapshot to exist (each App instance writes one every `export_interval_minutes`) and a transfer run to follow, so run this proof after the first hour of the stack's life, or trigger a snapshot early through `/inventory/export`.

**Proof A and B cleanup.** The test object `proof-a.txt` stays in the exports bucket until teardown, where `force_destroy` removes it with the bucket; no manual deletion is needed or allowed.

## Checks and teardown

`check.sh` reads `terraform show -json` output and the AWS CLI; the table fixes what each rule inspects so the script and the reference solution agree.

| Rule | Where it looks |
| --- | --- |
| `required_version` is 1.11 or later; `aws`, `google`, `azurerm`, `random` have version constraints; lock files committed | `configuration.provider_config.*.version_constraint` in the plan JSON; `.terraform.lock.hcl` present in both stacks |
| `default_tags` with `app`, `env`, `owner`, `managed_by` | AWS provider config; every planned AWS resource's `tags_all` |
| Names follow `<app>-<env>-<resource>` | `name` of each planned resource matches `^shop-(dev\|prod)-` |
| No ingress from `0.0.0.0/0` except the public ALB | `aws_vpc_security_group_ingress_rule` with `cidr_ipv4 = "0.0.0.0/0"` whose group is not the public ALB group |
| No port 22; no key pair | Any ingress range that includes 22; any `aws_key_pair` |
| Database private | `publicly_accessible = false`; database route tables have no `0.0.0.0/0` or `nat_gateway_id` route |
| No wildcard IAM | Customer-managed policy JSON: no `*` or `service:*` action, no `Resource = "*"`; no `AdministratorAccess` attachment |
| No static credentials | No `aws_iam_user`, `aws_iam_access_key`; the transfer job uses `role_arn` and has no AWS access key block; no Google service account key exists |
| Colours use `for_each` | `app_color` module call has a `for_each_expression` in the configuration JSON |
| Native state locking | Backend files contain `use_lockfile = true` and no `dynamodb_table` |
| No hard-coded location values | `.tf` files contain no literal region, zone name or CIDR outside tfvars and backend files |

`-target` and console changes leave no trace in the code, so they are caught by the clean plan after every stage and by spot checks of the evidence file.

**Destroy settings that make teardown work in one pass**

- S3 exports bucket and GCP bucket: `force_destroy = true`.
- RDS: `skip_final_snapshot = true` and `deletion_protection = false`, otherwise destroy stops and the database keeps billing.
- Storage Transfer API: `google_project_service` with `disable_on_destroy = false`, because Activity 11 may share the project.
- The transfer job is removed by Terraform destroy, which marks it deleted on the Google side.

**Teardown order.** Stop the probe, run `terraform destroy` in `release`, then in `foundation`, then `check.sh --teardown`. A failure is fixed in Terraform and re-run, never in the console.

**Teardown scan.** Every resource carries `app = shop`, as a tag on AWS and Azure and as a label on the GCP bucket.

| Cloud | Scan (read-only) | Caveat |
| --- | --- | --- |
| AWS | `aws resourcegroupstaggingapi get-resources --tag-filters Key=app,Values=shop --region ap-southeast-1` | The tagging API lags after deletion, so retry for a few minutes before reporting; IAM roles need `aws iam list-roles` plus `list-role-tags`, because the tagging API lists IAM only in `us-east-1` |
| GCP | `gcloud storage buckets list --filter="labels.app=shop"`, and `gcloud transfer jobs list` filtered by a `shop-` description | Transfer jobs cannot carry labels, so the job description holds the prefix |
| Azure | `az resource list --tag app=shop` | The Azure provider has no default tags, so the module sets `tags` on every resource |

The S3 state bucket from Activity 7 is kept and must not carry `app = shop`.

## Cost

The reference stack costs about $0.24 an hour on `t3.micro` and $0.32 on `t3.small`, so a focused 8-hour attempt costs about $2.20 and a stack left up for 24 hours about $5.80.

These are the PRD's planning figures for `ap-southeast-1` (checked Oct 2, 2026 in the PRD); I did not re-verify them, and the Singapore load balancer and database rates are scaled estimates that need a Pricing Calculator check before the Module 12 file is published.

| Line item | Quantity | Rate (USD per hour) | USD per hour |
| --- | --- | --- | --- |
| Application Load Balancers | 2 | 0.0252 each | 0.050 |
| Load balancer capacity units | 2 | About 0.2 LCU each at 0.008 | 0.003 |
| NAT gateway | 1 | 0.059 | 0.059 |
| Public IPv4 addresses | 3 | 0.005 each | 0.015 |
| EC2 `t3.micro` | 6 (2 Web, 2 blue, 2 green) | 0.0132 each | 0.079 |
| RDS `db.t4g.micro` | 1 | 0.021 | 0.021 |
| Storage, alarms, S3 | Small | Not itemised | About 0.01 |
| **Total at peak** |  |  | **About 0.24** |

| Scenario | Hours up | Approximate cost (USD) |
| --- | --- | --- |
| Focused attempt, one working window | 8 | 2.20 (8 × 0.24 plus about 0.30 of NAT data) |
| Two sessions, destroyed in between | 16 | 4.40 |
| Distinction: `prod` applied for one hour | 1 | 0.25 |
| Left running by mistake | 24 | 5.80 (7.60 on `t3.small`) |

**What this design adds.** Instance refresh with `max_healthy_percentage = 200` briefly doubles one colour's instances during a version change, and day-2 task 1 adds a third App instance. Both add a few cents at most. The design note's hand-made estimate should list each billed resource, its rate and its hours, using the Pricing Calculator for `ap-southeast-1`.

**Not itemised.** GCP storage, Azure Blob storage and the S3-to-GCP data transfer hold or move a few megabytes, which the PRD expects to cost well under $0.01 each and did not look up.

## Risks, fallbacks and open questions

The design depends on sandbox permissions that the PRD has not yet confirmed, and writing it down surfaced ten gaps in the PRD that the course team should settle before the reference build.

**Sandbox risks and the design's fallback**

| Risk | Fallback in this design |
| --- | --- |
| Roles or instance profiles blocked | Supplied profile names through `web_instance_profile` and `app_instance_profile`; `iam` and the transfer role are skipped; proofs D and E waived |
| Storage Transfer API or web-identity roles blocked | `cloud_storage` keeps the bucket and manifest and drops the transfer job; proofs D and E waived |
| Load balancers, Auto Scaling or Session Manager through the NAT gateway blocked | Fixed instances behind the load balancers; drop scaling tasks 1 and 2 |
| Boot time makes the probe flaky | Health check grace of 300 seconds, `min_healthy_percentage = 100`, probe warm-up window calibrated in the pilot |
| Anonymous Blob access or a disabled GCP API | The Azure proof becomes a successful upload; the footer check is waived |
| Learner forgets to destroy | Same-day rule, teardown scan, warning in the Module 12 file |

**Gaps and decisions for the course team**

1. **Global names collide.** S3 and GCS bucket names and Azure Storage Account names are global, so `<app>-<env>-exports` will clash between learners, and Azure account names cannot contain hyphens. Proposed: add the AWS account ID (or a `random_id` suffix) to bucket names and use `shop<env>assets<suffix>` on Azure; update `check.sh` and the proof commands to match.
2. **"Listener only" plans.** Every stage also replaces `terraform_data.stage_stamp` and updates the manifest objects. State the rule as "no compute, network or Web-tier change".
3. **Stage name variable.** The manifest records a stage name, so add `release_stage` to the variable table with an allowlist.
4. **Task 1 wording.** The plan shows an ASG capacity change, not an added instance.
5. **Task 2 starting point.** Blue runs v3 after stage 6, so the task must begin by setting `blue_version = v2`.
6. **Provider and instance refresh.** The AWS provider may return before an instance refresh ends; the runbook confirms completion with the CLI. Verify this behaviour against the pinned provider version.
7. **Single apply for the transfer job.** Google checks access to the S3 source when it creates the job, so IAM propagation can make the first apply fail. The job `depends_on` the role policy and the bucket permission, and the pilot should show whether one apply is reliable; if not, allow one re-apply and say so in the Module 12 file.
8. **First transfer timing.** Use `plantimestamp()` for the schedule start date with `ignore_changes` on the schedule so plans stay clean, and confirm in the pilot that the first run starts within the hour.
9. **Transfer permissions.** Confirm whether `s3:GetBucketLocation` is required, and which GCS bucket role the transfer service account needs (a legacy bucket writer role is the usual choice).
10. **Public ALB placement.** This design builds the public ALB inside `web_tier`; confirm that matches the module split the course intends.

## Acceptance test plan and build order

The course team should build the assets first, because the Terraform solution can only be proven against boot scripts that already behave identically on both colours.

**Build order**

1. Boot scripts, `seed.sql`, frontend build and `probe.sh`; test each on a single instance.
2. `foundation` stack and its modules; apply `dev` and run proofs A–C.
3. `release` stack at stage 0, then stages 1–6 with probe output saved.
4. Failure proofs 1–3 and the `precondition` proof.
5. Day-2 tasks 1–5.
6. `check.sh` static mode, then the `prod` plans.
7. Teardown and `check.sh --teardown`; time the whole run.

**Tests before launch**

| Test | Pass condition |
| --- | --- |
| Every version on both colours at once | v1, v2 and v3 each run on blue and green behind both load balancers; every response reports `version`, `color` and `server` |
| Concurrent schema change | Blue and green start v2 together on a fresh database; the `discount_code` column exists once and neither boot fails |
| Zero-failure stages | Stages 0–4 and 6 show 0 failed requests in three repeat runs |
| Contained failure | In stage 5, failures occur on v3 order placement only and `/health` stays 200; the 5xx alarm reaches ALARM |
| One-step rollback | Stage 6 plan changes the listener, the stamp and the manifests; no instance is replaced |
| Backup path | At least one inventory snapshot reaches `backups/` on GCP within an hour of the first snapshot |
| Check script, negative tests | Introducing each common AI mistake (wildcard policy, port 22, `count` on colours, open database group, missing `default_tags`) makes `check.sh` fail |
| Fallbacks | A run with supplied instance profiles, and a run with the transfer path dropped, both complete |
| Environments | `prod` `foundation` plan is clean; a brief `prod` apply and a clean `prod` `release` plan work |
| Timing | One timed run lands inside the 14–18 hour estimate |

**Rubric coverage**

| Criterion (points) | Where the reference solution shows it |
| --- | --- |
| Provision (15) | Both stacks apply with no manual step; plan after each apply is clean |
| Release proofs (25) | Runbook stages 0–6, probe summaries, manifest versions on GCP |
| Structure and quality (20) | Two stacks, seven modules plus `alarms`, `for_each`, validation, pinned versions, `default_tags`, two environments |
| Day-2 round (15) | Saved plans for tasks 1–5 |
| AI review log and design note (15) | Not a solution artefact; assessors use the common-mistake list in the PRD |
| Security, cost, teardown (10) | Isolated database subnets, tier-to-tier groups, proofs A–E, teardown scan |
