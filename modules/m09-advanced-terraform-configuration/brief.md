# M09 — Advanced Terraform Configuration

| | |
| --- | --- |
| Stage | 9 of 12 |
| Cloud | AWS |
| Builds on | M04, M05, M06 |
| Cost | Free or near-free resources only. Look up what each one bills before you apply, and destroy everything except the M07 bucket at the end of the stage. |
| Leaves behind | Nothing except the M07 state bucket. Destroy everything else. |

## Objective

Use Terraform's more advanced language features to describe infrastructure from data instead of by copy-paste: repeat resources and nested blocks from structured input, derive and reshape values, branch on conditions, look up what already exists, and control dependency and lifecycle behaviour.

## Scope

### In scope (in the order to tackle)

1. Composing Values with Built-in Functions
2. Making Configuration Conditional
3. Reshaping Data with `for` and Splat Expressions
4. Going Deeper with `for_each`
5. Generating Nested Configuration with Dynamic Blocks
6. Discovering Existing Infrastructure with Data Sources
7. Controlling Dependencies and Resource Lifecycle
8. Validating Infrastructure with Preconditions and Postconditions

### Out of scope

- The basics of repeating a resource (M04) and typed, validated variables (M05)
- Authoring reusable modules (M10)
- Policy-as-code engines — preconditions and postconditions are the course's native route
- `terraform test`

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage).
- AWS only. Choose resources that are free or near-free to run. No NAT gateway.
- Terraform 1.11 or later, provider versions pinned from `versions.env`.
- State lives in the M07 bucket under its own key.
- Data sources are used for reading what already exists; they do not create anything.
- Verify the behaviour of every feature you write up against the documentation for the pinned Terraform version.

## Deliverable

**A data-driven AWS configuration** in which resources and nested blocks are generated from structured input instead of repeated by hand, with derived values, a conditional, a data-source lookup, dependency and lifecycle controls, and checks on its own assumptions.

## Open design questions

1. What should the keys of a repeated resource be, and what happens to the real infrastructure when a key changes?
2. When does a dynamic block make a configuration clearer, and when does it make it harder to review than the repetition it replaced?
3. Which values should be derived inside the configuration, and which should the caller supply?
4. When is a condition in the configuration the wrong tool?
5. Where did you have to state a dependency explicitly rather than rely on a reference, and how did you decide that was genuinely needed?
6. Which resources, if any, should be protected from replacement or destruction, which changes should Terraform ignore, and what does each cost the next person who has to change them?
7. What assumption about real infrastructure is worth checking in your configuration, where does the check belong, and what should happen when it fails?

## Definition of done

- [ ] **DoD-1** Formatting and validation checks pass with no errors, and derived values are defined once and used in more than one place, with no expression duplicated across files (a reviewer reads the configuration).
- [ ] **DoD-2** At least one resource is repeated from a structured input — a map, or a collection derived from one — and your write-up justifies the keys you chose; at least one resource has repeated nested blocks generated from the same structured input, and the plan shows the expected number of them (plan excerpt); adding an entry, removing an entry and changing a key in the input each produce a plan you have captured, and your write-up says exactly what each plan would do to the real infrastructure.
- [ ] **DoD-3** At least one conditional changes what the configuration creates or sets, and the plan is shown for both outcomes of the condition (two plan excerpts); a data source supplies a value the configuration uses, and no equivalent value is hard-coded (a reviewer reads the configuration).
- [ ] **DoD-4** Every explicit dependency in the configuration is justified in the write-up (if there are none, the write-up says why a reference was always enough), and every lifecycle setting you used is justified, with its effect shown from a plan or a deliberate attempt that it affects (output pasted).
- [ ] **DoD-5** At least one precondition or postcondition is in place, and you have deliberately triggered it and captured the failure message (output pasted).
- [ ] **DoD-6** Everything is destroyed except the M07 bucket, confirmed from the cloud side.
- [ ] **DoD-7** Your write-up takes a first-time learner to a data-driven configuration like yours unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- `for_each` over `count`
- Typed, validated inputs (the shape of the structured input)
- Plan review (the key-change plans)
- fmt and validate
- Conditions that check assumptions (preconditions and postconditions)
