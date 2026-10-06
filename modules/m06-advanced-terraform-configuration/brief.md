# M06 — Advanced Terraform Configuration Brief

**Stage:** 6 of 9 · **Builds on:** M02, M03, M04 · **Feeds into:** M07

## Objective

By the end of this stage, you can describe infrastructure from data instead of by copy-paste — repeating resources and nested blocks from structured input, deriving and reshaping values, branching on conditions, looking up what already exists, and controlling dependency and lifecycle behaviour — using your own plans as the evidence for what each change does to real infrastructure, not what you expect it to do.

## Scope

You build on your own structured input, not a worked example. Find out, and write down in your own words:

- **Composing Values with Built-in Functions** — deriving a value with functions instead of repeating it. Research: which values should be derived inside the configuration and which the caller should supply.
- **Making Configuration Conditional** — creating or setting something only when a condition holds. Research: when a condition in the configuration is the wrong tool.
- **Reshaping Data with `for` and Splat Expressions** — turning one collection into another, in your own plan output. Research: how a collection looks before and after you reshape it.
- **Going Deeper with `for_each`** — repeating resources from a map or a set, and what makes a key stable. Research: what the keys of a repeated resource should be, and what happens to the real infrastructure when a key changes.
- **Generating Nested Configuration with Dynamic Blocks** — generating repeated nested blocks from data. Research: when a dynamic block makes a configuration clearer, and when it makes it harder to review than the repetition it replaced.
- **Discovering Existing Infrastructure with Data Sources** — looking up what already exists instead of hard-coding it. Research: what a data source supplies that you would otherwise hard-code.
- **Controlling Dependencies and Resource Lifecycle** — ordering that a reference cannot express, and controlling replacement, destruction and ignored changes. Research: where you had to state a dependency explicitly and how you decided that was needed, and which resources should be protected from replacement or destruction, which changes Terraform should ignore, and what each costs the next person who has to change them.
- **Validating Infrastructure with Preconditions and Postconditions** — checking assumptions about real infrastructure. Research: what assumption about real infrastructure is worth checking in your configuration, where the check belongs, and what should happen when it fails.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- You use AWS only, with resources that are free or near-free to run and no NAT gateway.
- Look up what each one bills before you apply, and destroy everything except the M02 bucket at the end.
- Terraform is 1.11 or later, with provider versions pinned from `versions.env`, and state lives in the M02 bucket under its own key.
- Data sources read what already exists.
- They do not create anything.
- Check the behaviour of every feature you write up against the documentation for the pinned Terraform version.
- The basics of repeating a resource (M03) and typed, validated variables (M04), authoring modules (M07), policy-as-code engines and `terraform test` are out of scope.

## Deliverable

**A data-driven AWS configuration** in which resources and nested blocks are generated from structured input instead of repeated by hand, with derived values, a conditional, a data-source lookup, dependency and lifecycle controls, and checks on its own assumptions.

## Lab

**Goal.** Describe infrastructure from data and see exactly what each change does to the real resources.

**You do, in the sandbox.**

1. Define one structured input in `variables.tf`: a map of rules, each with a port and a description.
2. Create an `aws_vpc` and an `aws_security_group` whose ingress rules come from a `dynamic "ingress"` block over the map, and build the names with `locals` and built-in functions.
3. Create one `aws_ssm_parameter` per map entry with `for_each`, and use a `for` expression to turn the map into an output list.
4. Add a conditional so the parameters are created only when a flag is true, and run `terraform plan` with the flag on and off.
5. Look up your account with a `data "aws_caller_identity"` data source and use it in a name, then add one `depends_on` and one `lifecycle` setting and read what each does in the plan.
6. Add a `precondition` or `postcondition` and trigger it on purpose; then add an entry to the map, remove one and change a key, running `terraform plan` each time, and destroy.

**You build and capture.** The data-driven configuration is your deliverable. Capture the plan for each input change, the plan for both outcomes of the conditional, the effect of each lifecycle setting, and the failure message you triggered.

**Clean-up.** Destroy everything except the M02 bucket.

## Definition of done

- DoD-01: Formatting and validation pass with no errors, and derived values are defined once and used in more than one place, with no expression duplicated across files (a reviewer reads the configuration).
- DoD-02: At least one resource is repeated from a structured input — a map, or a collection derived from one — and your notes justify the keys you chose; at least one resource has repeated nested blocks generated from the same structured input, and the plan shows the expected number of them (plan excerpt); adding an entry, removing an entry and changing a key each produce a plan you captured, and your notes say exactly what each plan would do to the real infrastructure, not what you expect it to do.
- DoD-03: At least one conditional changes what the configuration creates or sets, and the plan is shown for both outcomes (two plan excerpts), not only the outcome you expected; a data source supplies a value the configuration uses, and no equivalent value is hard-coded (a reviewer reads the configuration).
- DoD-04: Every explicit dependency and every lifecycle setting in your configuration is justified in your notes (or they say why a reference was always enough), and each lifecycle setting's effect is shown from a plan or a deliberate attempt that it affects (output pasted), not assumed from its name.
- DoD-05: At least one precondition or postcondition is in place and you deliberately triggered it, with the real failure message captured (output pasted).
- DoD-06: Everything is destroyed except the M02 bucket, confirmed from the cloud side.
- DoD-07: Your write-up takes a first-time learner to a data-driven configuration like yours unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- `for_each` over `count`
- Typed, validated inputs (the shape of the structured input)
- Plan review (the key-change plans)
- fmt and validate
- Conditions that check assumptions (preconditions and postconditions)

## Still open / ask your trainer

- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
