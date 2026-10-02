# M05 — Defining Variables, Inputs and Outputs in Terraform

| | |
| --- | --- |
| Stage | 5 of 12 |
| Cloud | AWS |
| Builds on | M04 (you may reuse that work) |
| Cost | Small, cheap resources only. Look up what each resource in your plan bills before you apply, and destroy everything at the end of the stage. |
| Leaves behind | Nothing. Destroy everything. |

## Objective

Turn a hard-wired configuration into a parameterised one with typed, described and validated inputs. Use local values to derive a value once. Work out by experiment which source of a variable's value wins when several are present. Handle sensitive inputs and outputs so that secrets reach Terraform and leave it without being committed or casually displayed.

## Scope

### In scope (in the order to tackle)

1. Input variables — type, description and default
2. Validation rules enforced at plan time
3. Supplying values — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables
4. Variable value precedence — which source wins when several supply the same variable, found by hands-on experiment
5. Keeping environment-specific values out of the main configuration
6. Local values — naming and reusing derived values within a configuration
7. Sensitive input variables — marking them and getting their values into Terraform without committing them
8. Output values — what to expose and how to mark an output sensitive
9. What marking a value sensitive does and does not protect

### Out of scope

- Per-environment backends and state (M08)
- Sensitive values in state — how they get there and who can read them (M06)
- Secrets managers and credential stores — not covered in these stages
- Policy-as-code engines
- Reusable Terraform modules (M10)

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- AWS only. The AWS region, the network address ranges and the resource name prefix must all be inputs.
- Validation uses only what Terraform provides natively; no external policy tooling.
- **Precedence experiments are mutually exclusive.** Each experiment lets exactly one source supply the variable, so every result can be attributed to that source. Only after every source has been tried alone may you combine sources to establish which wins.
- Use throwaway placeholder values for every sensitive input. Never use a real credential.
- State is local in this stage and is never committed.

## Deliverable

**A parameterised AWS configuration** in which region, network address ranges and the resource name prefix are inputs, with two different sets of values that both plan cleanly, plus a record of your precedence experiments and a configuration that handles a sensitive input and a sensitive output.

## Open design questions

1. Which rules deserve plan-time validation, and which are better left for AWS to reject at apply time?
2. Which inputs should have defaults and which should be required — what is the risk of each?
3. Where does a typed variable stop being enough?
4. If several sources can supply the same variable, why might a team still allow only one source per variable, and how would you enforce that?
5. How should a sensitive value reach Terraform, and what are the risks of each way you tried?
6. What does marking a value sensitive hide, and where can it still be seen?
7. Which outputs are worth exposing at all, and who is the audience for each?
8. When is a local value clearer than repeating an expression, and when does it hide too much?

## Definition of done

- [ ] **DoD-1** Formatting and validation checks pass with no errors.
- [ ] **DoD-2** An invalid network address range is rejected at plan time with your validation message and nothing is planned for creation (output pasted).
- [ ] **DoD-3** Both sets of values produce clean, error-free plans (output for each).
- [ ] **DoD-4** The main configuration file contains no hard-coded region, network address range or name prefix.
- [ ] **DoD-5** Every variable has a type and a description.
- [ ] **DoD-6** At least one value is derived once as a local value and used in more than one place (a reviewer reads the configuration).
- [ ] **DoD-7** Your precedence record has one isolated experiment for each source — defaults, `terraform.tfvars`, `*.auto.tfvars`, `-var`, `-var-file` and environment variables — and each shows the single source supplying the variable and the value Terraform used (plan output per experiment).
- [ ] **DoD-8** After the isolated experiments you combined sources deliberately, and your record states the order in which sources win, supported by your combined-run evidence.
- [ ] **DoD-9** At least one sensitive input is marked sensitive, its value reaches Terraform without appearing in any committed file, and the plan output does not display it (output pasted).
- [ ] **DoD-10** At least one output is marked sensitive, and your evidence shows what is displayed for it.
- [ ] **DoD-11** Your write-up states what marking a value sensitive does and does not protect, supported by what you observed using placeholder values only.
- [ ] **DoD-12** Everything created is destroyed, confirmed from the cloud side.

## Best practices this stage demonstrates

- Typed, validated inputs
- fmt and validate
- Value precedence, and handling sensitive inputs and outputs
