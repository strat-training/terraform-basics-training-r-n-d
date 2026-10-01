# 2026-10-02 — Brief lines that answer their own open questions

Found while running `/trainee-task-planner` for all twelve module stages. The planner restates brief text verbatim, so each line below appears unchanged in that stage's `tasks.md`. Nothing in any brief was edited.

**Pattern.** A definition-of-done line, scope item or stack constraint states the outcome that an open design question asks the trainee to reason their way to. Ten of the twelve stages do it, usually by a DoD line that has to be observable. M03, M05 and M09 are the cleanest; M05's only soft spot is that its constraint prescribes how to run the precedence experiments, by design.

**Where the line also reaches the trainee.** "Task" means the line is restated in `tasks.md`. "Brief only" means it sits in an objective or constraint, which the planner does not copy into tasks.

| Stage | Question | Line that resolves it (where it appears) |
| --- | --- | --- |
| M01 | Q2 which parts must be identical | Constraint: Terraform "at the exact version in `versions.env`" (brief only) |
| M01 | Q3 what fails differently on Windows | Scope 7, "A shell that can run the labs' shell scripts on Windows" (task B7) |
| M01 | Q5 local install vs container | Scope 9, "as an alternative to installing locally" (B9); constraint "not a replacement for the local install" (brief only) |
| M02 | Q2 container sign-in | Scope 4 narrows it to "Browser-based sign-in" (B4) |
| M02 | Q4 constraint vs lock file | Scope 8 "why it is committed" (B8); DoD-6 (V6) |
| M04 | Q2 which repetition mechanism, and why | DoD-3 names the keyed collection and rules out `count` (V3); scope 3 "the course's preference" (B3) |
| M05 | Q6 how a sensitive value reaches Terraform | Scope 7 and DoD-9, "without appearing in any committed file" (B7, V9) |
| M06 | Q1 what leaks into state, Q4 why state is sensitive | DoD-4, "a sensitive value can be read from state" (V4) |
| M07 | Q2 bootstrapping, Q4 why the bucket is kept | Objective "reused by M08 to M11" and constraint "bootstrapped from a local-state configuration, then retained" (brief only); B2, B7 and V7 restate the topic |
| M08 | Q6 how one account misrepresents practice | Constraint "real teams usually separate accounts" (brief only) |
| M09 | Q5–Q7 when to apply dependencies, lifecycle and conditions | Scope 7–9 name `depends_on`, the `lifecycle` block and preconditions (B7–B9) — topics, not answers |
| M10 | Q1 module vs root | DoD-7, "configures no provider itself" (V7) |
| M10 | Q4 file layout | Scope 4 and DoD-3 list inputs, outputs, resources and version requirements (B4, V3) |
| M10 | Q5 what deserves a comment | DoD-5, "explain why rather than restate what" (V5) |
| M10 | Q7 trusting a module | Constraint "you read its source before using it" (brief only) |
| M10 | Q8 when a module is wrong | Scope 12 lists thin wrappers, over-parameterisation and cloud-hiding abstractions (B12) |
| M11 | Q1 knowing nothing real is touched | Scope 6, DoD-1 and DoD-2 name the zero-destroy plan check (B6, V1, V2) |
| M11 | Q3 who owns an unmanaged resource | DoD-9, "including anything Terraform no longer manages" (V9) |
| M11 | Q4 why plan-visible changes | DoD-7 (V7); constraint "declarative … reviewable as code" (brief only) |
| M12 | Q1 ambient-login mismatch | Scope 2 and 3 "explicit project", "explicit subscription", DoD-3 (B2, B3, V3); constraint (brief only) |
| M12 | Q3 why no common wrapper | Scope 6, "— no abstraction layer" (B6) |

**Possible remedies (the trainer's call).** Keep the observable DoD wording but move the explanatory part, such as "why", "rather than" or "not just", out of the DoD and into the reviewer's notes; or restate the DoD as the evidence to capture without saying what it shows. Re-run `/trainee-task-planner re-plan <stage>` after any brief change, since each `tasks.md` is generated from its brief.
