# M04 — Managing Resources with Network Provisioning

| | |
| --- | --- |
| Stage | 4 of 12 |
| Cloud | AWS |
| Builds on | M03 |
| Cost | Some networking resources bill by the hour (see scope 7). Look up what each resource in your plan bills before you apply, and destroy everything at the end of the stage. |
| Leaves behind | Nothing. Destroy everything. |

## Objective

Provision a small AWS network and use it to understand how Terraform works out what depends on what, and how to create several similar resources without writing each one out by hand, and to read information that already exists instead of hard-coding it.

## Scope

### In scope (in the order to tackle)

1. Resource references and the dependency graph Terraform builds from them
2. Implicit versus explicit dependencies
3. Repeating a resource — the two mechanisms Terraform offers
4. Data sources — reading information that already exists, and how it differs from a resource
5. A VPC, subnets in more than one availability zone, and the routing a public tier needs
6. Public versus private subnets — what makes a subnet public
7. Cost awareness — why some networking resources bill by the hour

### Out of scope

- NAT gateways — hourly billing, so not used in these stages
- Compute instances, security groups and IAM roles — not covered in these stages
- Variables and validation (M05)
- Advanced repetition, dynamic blocks and in-depth data sources (M09)
- Reusable Terraform modules (M10)

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- AWS only. No NAT gateway anywhere in this stage.
- State is local in this stage.
- Anything repeated across availability zones is repeated by one of the mechanisms in scope, and your write-up says which.

## Deliverable

**A small AWS network configuration** — one VPC with public and private subnets across more than one availability zone and the routing the public tier needs — with no NAT gateway.

## Open design questions

1. Where in your configuration did you rely on Terraform to infer ordering, and was there anywhere you felt you had to state it explicitly? Why?
2. What are the trade-offs between the two ways of repeating a resource, and why does the course want one preferred?
3. What happens to your existing subnets if you later add or remove one from the set you are repeating over?
4. What distinguishes a public subnet from a private one in AWS, and how would you prove which is which?
5. What is the difference between a resource and a data source in what Terraform manages, and what happens to each when you destroy?

## Definition of done

- [ ] **DoD-1** Formatting and validation checks pass with no errors.
- [ ] **DoD-2** The plan contains the VPC, subnets in at least two availability zones, and the routing for the public tier (resource addresses shown from the plan output or its JSON form).
- [ ] **DoD-3** Subnets in more than one availability zone are created by repeating one resource block rather than writing each one out (a reviewer reads the configuration).
- [ ] **DoD-4** At least one value the configuration needs about the account or region is read with a data source rather than hard-coded (a reviewer reads the configuration).
- [ ] **DoD-5** No NAT gateway appears in the plan or in state.
- [ ] **DoD-6** Your note names the implicit dependencies in your configuration and where each one comes from.
- [ ] **DoD-7** Everything is destroyed, confirmed from the cloud side.

## Best practices this stage demonstrates

- Implicit dependencies
- `for_each` over `count`
- fmt and validate
