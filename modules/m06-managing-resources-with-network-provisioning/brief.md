# M06 — Managing Resources with Network Provisioning Brief

**Stage:** 6 of 11 · **Builds on:** M03 · **Feeds into:** M07, M08

## Objective

By the end of this stage, you can explain how Terraform works out what depends on what, create several similar resources without writing each one out by hand, and read information that already exists instead of hard-coding it — using the small AWS network you built as the evidence, not a diagram.

## Scope

You build and inspect your own network, not a worked example. Find out, and write down in your own words:

- **Resource references and the dependency graph Terraform builds from them** — where your own configuration refers to one resource from another. Research: where in your configuration you relied on Terraform to infer ordering.
- **Implicit versus explicit dependencies** — which ordering Terraform infers, and which you would have to state. Research: whether there was anywhere you had to state an ordering explicitly, and why.
- **Repeating a resource** — the two mechanisms Terraform offers. Research: the trade-offs between the two ways of repeating a resource and why the course wants one preferred, and what happens to your existing subnets if you later add or remove one from the set you are repeating over.
- **Data sources** — reading information that already exists, and how it differs from a resource. Research: the difference between a resource and a data source in what Terraform manages, and what happens to each when you destroy.
- **A VPC, subnets in more than one availability zone, and the routing a public tier needs** — the small network you build. Research: what the routing for a public tier needs, and how you would see it in the plan.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- You use AWS only, with no NAT gateway anywhere in this stage, and no compute instances, security groups or IAM roles.
- Some networking resources bill by the hour, so look up what each resource in your plan bills before you apply, and destroy everything at the end of the stage.
- State is local in this stage.
- Anything repeated across availability zones is repeated by one of the mechanisms in scope, and your notes say which.
- Variables and validation (M07), advanced repetition, dynamic blocks and in-depth data sources (M08), and reusable modules (M09) belong to later stages.

## Deliverable

**A small AWS network configuration** — one VPC with public and private subnets across more than one availability zone and the routing the public tier needs — with no NAT gateway.

## Lab

**Goal.** Build a small AWS network and watch Terraform work out what depends on what.

**You do, in the sandbox.** Create a VPC, subnets in more than one availability zone and the routing a public tier needs; repeat resources from one definition; read existing information with a data source; read the plan before every apply; then destroy it.

**You build and capture.** The network configuration is your deliverable. Capture the plan showing the VPC, the subnets and the public routing, where your dependencies come from, the data source in use, and the destroy confirmed from the cloud side.

**Clean-up.** Destroy everything; no NAT gateway is created.

## Definition of done

- DoD-01: Formatting and validation pass with no errors, and the plan contains the VPC, subnets in at least two availability zones, and the routing for the public tier, with resource addresses taken from the plan output or its JSON form, not from your code.
- DoD-02: Subnets in more than one availability zone are created by repeating one resource block, not by writing each one out (a reviewer reads the configuration).
- DoD-03: At least one value your configuration needs about the account or region is read with a data source, not hard-coded (a reviewer reads the configuration).
- DoD-04: No NAT gateway appears in the plan or in state, shown from real output, not from the absence of one in your code.
- DoD-05: Your note names the implicit dependencies in your own configuration and where each one comes from, not a general definition of an implicit dependency.
- DoD-06: Everything is destroyed, confirmed from the cloud side, not only from Terraform's output.
- DoD-07: Your write-up takes a first-time learner to the same small AWS network unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- Implicit dependencies
- `for_each` over `count`
- fmt and validate

## Still open / ask your trainer

- Whether your sandbox lets you create a VPC, subnets and routing — tell your trainer before you start if it does not.
- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
