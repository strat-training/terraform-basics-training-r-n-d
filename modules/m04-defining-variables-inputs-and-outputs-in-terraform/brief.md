# M04 — Defining Variables, Inputs and Outputs in Terraform Brief

**Stage:** 4 of 9 · **Builds on:** M03 (you may reuse that work) · **Feeds into:** M05, M06, M07

## Objective

By the end of this stage, you can turn a hard-wired configuration into a parameterised one, work out by experiment which source of a variable's value wins, and handle a sensitive input and a sensitive output so that secrets reach Terraform and leave it without being committed or casually displayed — using your own plans as the evidence, not the documentation's description. You use local values to derive a value once.

## Scope

You experiment on your own configuration, not a worked example. Find out, and write down in your own words:

- **Input variables** — what a variable declares, and the defaults you give it. Research: which inputs should have defaults and which should be required, and the risk of each.
- **Validation rules enforced at plan time** — rules that reject a bad value before anything is planned. Research: which rules deserve plan-time validation and which are better left for AWS to reject at apply time, and where a typed variable stops being enough.
- **Supplying values** — the ways to give a variable a value. Research: how each way of supplying a value shows up in a plan.
- **Variable value precedence** — which source wins when several supply the same variable, found by hands-on experiment. Research: why a team might still allow only one source per variable, and how you would enforce that.
- **Keeping environment-specific values out of the main configuration** — what belongs in the main configuration and what does not. Research: which values differ between environments and where they live.
- **Local values** — naming and reusing derived values within a configuration. Research: when a local value is clearer than repeating an expression, and when it hides too much.
- **Sensitive input variables** — marking them and getting their values into Terraform without committing them. Research: how a sensitive value should reach Terraform, and the risks of each way you tried.
- **Output values** — what to expose and how to mark an output sensitive. Research: which outputs are worth exposing at all, and who the audience is for each.
- **What marking a value sensitive does and does not protect** — what the marking does and does not protect, shown with placeholder values. Research: what marking a value sensitive hides, and where it can still be seen.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- You use AWS only, with small, cheap resources.
- Look up what each resource in your plan bills before you apply, and destroy everything at the end of the stage.
- The AWS region, the network address ranges and the resource name prefix must all be inputs, and state is local in this stage and is never committed.
- Validation uses only what Terraform provides natively, with no external policy tooling.
- **Your precedence experiments are mutually exclusive.** Each lets exactly one source supply the variable, so every result can be attributed to that source.
- Only after every source has been tried alone may you combine sources to establish which wins.
- Use throwaway placeholder values for every sensitive input, and never use a real credential.
- Per-environment backends and state (M05), sensitive values in state (M02), secrets managers and credential stores, policy-as-code engines and reusable modules (M07) are not part of this stage.

## Deliverable

**A parameterised AWS configuration** in which region, network address ranges and the resource name prefix are inputs, with two different sets of values that both plan cleanly, plus a record of your precedence experiments and a configuration that handles a sensitive input and a sensitive output.

## Lab

**Goal.** Turn a hard-wired configuration into a parameterised one, and find out by experiment which source of a value wins.

**You do, in the sandbox.**

1. Take the network from M03 and replace the hard-coded region, address range and name prefix with `variable` blocks, each with a type, a description and a default.
2. Add a `validation` block that rejects a bad address range, and test it with `terraform plan -var vpc_cidr=10.0.0.0/33`.
3. Add a `locals` block for a name you use in more than one place.
4. Run the precedence experiments: supply one variable from one source at a time — its default, `terraform.tfvars`, a `*.auto.tfvars` file, `-var`, `-var-file` and a `TF_VAR_` environment variable — run `terraform plan` for each, then combine sources and see which one wins.
5. Add a variable marked `sensitive = true` with a placeholder value and a sensitive output, and run `terraform plan` and `terraform output` to see what is hidden.
6. Plan with two different `.tfvars` files, then destroy anything you applied.

**You build and capture.** The parameterised configuration is your deliverable. Capture an invalid range rejected at plan time, clean plans for both sets of values, one plan per experiment and one for the combined run, and what is displayed for the sensitive input and output.

**Clean-up.** Destroy everything you created.

## Definition of done

- DoD-01: Formatting and validation pass with no errors, and both sets of values produce clean, error-free plans (output for each), not one run reported as covering both.
- DoD-02: Every variable has a type and a description, and an invalid network address range is rejected at plan time with your validation message and nothing planned for creation (output pasted), not a rule you wrote but never triggered.
- DoD-03: The main configuration file contains no hard-coded region, network address range or name prefix, and at least one value is derived once as a local value and used in more than one place (a reviewer reads the configuration).
- DoD-04: Your precedence record has one isolated experiment for each source — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables — each showing the single source supplying the variable and the value Terraform used (plan output per experiment); after them you combined sources deliberately, and your record states the order in which sources win, backed by your combined-run evidence, not by the documentation.
- DoD-05: At least one sensitive input is marked sensitive, its value reaches Terraform without appearing in any committed file, and the plan output does not display it; at least one output is marked sensitive, and your evidence shows what is displayed for it. Your notes state what marking a value sensitive does and does not protect, backed by what you observed with placeholder values only.
- DoD-06: Everything you created is destroyed, confirmed from the cloud side, not only from Terraform's output.
- DoD-07: Your write-up takes a first-time learner to a parameterised configuration that plans cleanly with two sets of values unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- Typed, validated inputs
- fmt and validate
- Value precedence, and handling sensitive inputs and outputs

## Still open / ask your trainer

- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
