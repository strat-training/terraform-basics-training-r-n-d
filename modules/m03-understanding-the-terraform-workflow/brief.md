# M03 — Understanding the Terraform Workflow Brief

**Stage:** 3 of 11 · **Builds on:** M02 · **Feeds into:** M04, M06, M10

## Objective

By the end of this stage, you can explain why Terraform describes the desired state of infrastructure instead of scripting steps, and predict from a plan whether a change updates a resource in place or replaces it — using your own plans as the evidence, not a diagram from a slide. You run the core workflow end to end on a real EC2 t3.micro instance and read the plan before every apply.

## Scope

You work on your own EC2 instance and your own plans, not the textbook ones. Find out, and write down in your own words:

- **Declarative versus imperative infrastructure** — what it means that Terraform describes desired state. Research: how describing the desired state differs from scripting the steps, and what that changes about running the same configuration twice.
- **Anatomy of a resource** — type, name, arguments and attributes. Research: which parts of a resource you set and which Terraform reports back, found in your own resource.
- **The core workflow** — initialise, plan, apply, destroy. Research: what each of the four commands changes, and what it leaves alone.
- **What a plan shows** — reading the action for each resource, and the difference between in-place updates and replacement. Research: how you can tell from the plan alone that a change will destroy something, which changes to your resource are made in place and which force replacement and how sure you are, and what a replacement costs when the resource holds data or other resources depend on it.
- **Plan review as a habit** — what to check before approving. Research: what you would do if a plan showed a destroy you did not expect.
- **Destroying what you created** — removing what you built, and proving it is gone. Research: how you confirm from the cloud side that the instance is gone.

## Stack constraints

- Everything under [Rules for every stage](../../README.md#rules-for-every-stage) applies.
- You use AWS only, with one EC2 instance of type t3.micro.
- Look up what it bills before you apply, and destroy it at the end of the stage, because the stage's check confirms that the instance is gone.
- State is local in this stage, and you read the plan before every apply.
- Variables and validation (M07), state and remote state (M04), lifecycle controls that change replacement behaviour (M08) and refactoring without replacement (M10) belong to later stages.

## Deliverable

**A configuration managing one EC2 t3.micro instance, taken through create, in-place change, forced replacement and destroy**, with a written plan-review note.

## Lab

**Goal.** Run the core Terraform workflow on one EC2 t3.micro instance and make reading the plan before applying a habit.

**You do, in the sandbox.** Launch an EC2 t3.micro instance, apply the same configuration twice, make an in-place change, force a replacement, read each plan before you approve it, then destroy the instance.

**You build and capture.** The configuration managing that one instance is your deliverable. Capture both apply outputs, the plan for each change before it was applied, your classification of each change, and the destroy confirmed from the cloud side.

**Clean-up.** Destroy the instance and confirm from the cloud side that it is gone.

## Definition of done

- DoD-01: Formatting and validation pass with no errors, shown as pasted output.
- DoD-02: Your notes show the same apply run twice on an unchanged configuration, with both outputs pasted, and explain the difference in terms of desired state, not as “it did nothing the second time”.
- DoD-03: Your notes identify the type, name, arguments and attributes of your own resource and show an attribute whose value you did not set, from real output.
- DoD-04: You made at least one in-place change and at least one forced replacement, and the plan output for each was captured before it was applied, not afterwards.
- DoD-05: Your plan-review note classifies every change you made as in-place or replacement, and your trainer confirms each classification on review.
- DoD-06: After destroy the instance is gone (shown as terminated), confirmed from the cloud side, not only from Terraform's output.
- DoD-07: Your write-up takes a first-time learner to an EC2 t3.micro instance taken through create, in-place change, forced replacement and destroy unaided — verified by you following it end to end from a clean state.

## Best practices this stage demonstrates

- Plan review
- fmt and validate

## Still open / ask your trainer

- Whether your sandbox lets you launch a t3.micro EC2 instance, and which image and network it expects you to use.
- How much detail your notes need — confirm the expected length and depth with your trainer before you invest significant time.
