# M09 — Advanced Terraform Configuration

| | |
| --- | --- |
| Stage | 9 of 12 |
| Course reference | None — added at the trainer's request. The solution design names `for_each` over `count` (§7, Activity 4) and, in ADR-015, preconditions and postconditions, but gives neither a stage of its own. |
| Cloud | AWS |
| Builds on | M04, M05, M06 |
| Time box | TBC — see [README](../README.md#open-items-for-the-trainer) |
| Leaves behind | Nothing except the M07 state bucket. Destroy everything else. |

## Objective

Use Terraform's more advanced language features to describe infrastructure from data instead of by copy-paste: repeat resources and nested blocks from structured input, derive and reshape values, branch on conditions, look up what already exists, and control dependency and lifecycle behaviour. Be able to say when a feature makes a configuration harder to read than the repetition it replaced.

## Scope

### In scope (in the order to tackle)

1. Composing built-in functions to derive values
2. Conditional expressions — and when a condition belongs in configuration at all
3. `for` expressions and splat expressions — reshaping collections
4. `for_each` in depth — maps, sets and derived collections, and what makes a key stable
5. Dynamic blocks — generating repeated nested blocks from data
6. Data sources in depth — beyond the basic lookup introduced in M04
7. Explicit dependencies with `depends_on` — when a reference cannot express the ordering
8. The `lifecycle` block — controlling replacement, destruction and ignored changes
9. Preconditions and postconditions — checking assumptions about real infrastructure
10. When a feature costs more readability than it saves

### Out of scope

- The basics of repeating a resource (M04) and typed, validated variables (M05)
- Authoring reusable modules (M10)
- Ephemeral values and write-only arguments — not covered until checked against the pinned version (see README, proposed additions)
- Policy-as-code engines — preconditions and postconditions are the course's native route (ADR-015)
- `terraform test` (ADR-015)

## Stack constraints

- Everything under [Rules for every stage](../README.md#rules-for-every-stage).
- AWS only. Choose resources that are free or near-free to run. No NAT gateway (ADR-011).
- Terraform 1.11 or later, provider versions pinned from `versions.env`.
- State lives in the M07 bucket under its own key.
- Data sources are used for reading what already exists; they do not create anything.
- Verify the behaviour of every feature you write up against the documentation for the pinned Terraform version.

## Deliverable

**A data-driven AWS configuration** in which resources and nested blocks are generated from structured input instead of repeated by hand, with derived values, a conditional, a data-source lookup, dependency and lifecycle controls, and checks on its own assumptions, plus a readability note on where each feature helped and where it hurt.

## Open design questions

1. What should the keys of a repeated resource be, and what happens to the real infrastructure when a key changes?
2. When does a dynamic block make a configuration clearer, and when does it make it harder to review than the repetition it replaced?
3. Which values should be derived inside the configuration, and which should the caller supply?
4. When is a condition in the configuration the wrong tool?
5. Where did you have to state a dependency explicitly rather than rely on a reference, and how did you decide that was genuinely needed?
6. Which resources, if any, should be protected from replacement or destruction, which changes should Terraform ignore, and what does each cost the next person who has to change them?
7. What assumption about real infrastructure is worth checking in your configuration, where does the check belong, and what should happen when it fails?

## Definition of done

- [ ] **DoD-1** Formatting and validation checks pass with no errors.
- [ ] **DoD-2** At least one resource is repeated from a structured input — a map, or a collection derived from one — and your write-up justifies the keys you chose.
- [ ] **DoD-3** At least one resource has repeated nested blocks generated from the same structured input, and the plan shows the expected number of them (plan excerpt).
- [ ] **DoD-4** Adding an entry, removing an entry and changing a key in the input each produce a plan you have captured, and your write-up says exactly what each plan would do to the real infrastructure.
- [ ] **DoD-5** Derived values are defined once and used in more than one place, and no expression is duplicated across files (a reviewer reads the configuration).
- [ ] **DoD-6** At least one conditional changes what the configuration creates or sets, and the plan is shown for both outcomes of the condition (two plan excerpts).
- [ ] **DoD-7** A data source supplies a value the configuration uses, and no equivalent value is hard-coded (a reviewer reads the configuration).
- [ ] **DoD-8** Every explicit dependency in the configuration is justified in the write-up; if there are none, the write-up says why a reference was always enough.
- [ ] **DoD-9** Every lifecycle setting you used is justified in the write-up, and its effect is shown from a plan or a deliberate attempt that it affects (output pasted).
- [ ] **DoD-10** At least one precondition or postcondition is in place, and you have deliberately triggered it and captured the failure message (output pasted).
- [ ] **DoD-11** Your readability note says, for each advanced feature you used, where it helped and where it made the configuration harder to follow.
- [ ] **DoD-12** Everything is destroyed except the M07 bucket, confirmed from the cloud side.

## Best practices this stage demonstrates

- `for_each` over `count` (extends the Activity 4 check)
- Typed, validated inputs (the shape of the structured input)
- Plan review (the key-change plans)
- fmt and validate
- Not in the current 14-practice list: conditions that check assumptions (named in ADR-015, not mapped in the coverage matrix)
