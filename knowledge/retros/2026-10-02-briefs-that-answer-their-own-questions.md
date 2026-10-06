# 2026-10-02 — Brief lines that answer their own open questions

Found while running `/trainee-task-planner` for all twelve module stages. The planner restates brief text verbatim, so each line below appeared unchanged in that stage's `tasks.md`.

**Resolved the same day.** The trainer chose to reword the worst five stages (M03, M02, M07, M08 and M09) and removed the dev container from the course, which removed M01's question 5 and M02's question 2 along with the container topics. The Status column says what happened to each row. The other stages were left as they are.

**Pattern.** A definition-of-done line, scope item or stack constraint states the outcome that an open design question asks the trainee to reason their way to. Ten of the twelve stages did it, usually by a DoD line that has to be observable. M03, M05 and M09 are the cleanest; M05's only soft spot is that its constraint prescribes how to run the precedence experiments, by design.

**Where the line also reaches the trainee.** "Task" means the line is restated in `tasks.md`. "Brief only" means it sits in an objective or constraint, which the planner does not copy into tasks.

| Stage | Question | Line that resolved it (where it appears) | Status |
| --- | --- | --- | --- |
| M01 | Q2 which parts must be identical | Constraint: Terraform "at the exact version in `versions.env`" (brief only) | Kept |
| M01 | Q3 what fails differently on Windows | Scope 7, "A shell that can run the labs' shell scripts on Windows" (task B7) | Kept |
| M01 | Q5 local install vs container | Scope 9 and a constraint on the dev container | Removed with the dev container |
| M01 | Q2 container sign-in | Scope 4 narrowed it to "Browser-based sign-in" (B4) | Removed with the dev container |
| M01 | Q4 constraint vs lock file | Scope 8 "why it is committed" (B8); DoD-6 (V6) | Kept |
| M03 | Q2 which repetition mechanism, and why | DoD-3 named the keyed collection and ruled out `count`; scope 3 "the course's preference"; a constraint pointing at the preferred mechanism | Reworded |
| M04 | Q6 how a sensitive value reaches Terraform | Scope 7 and DoD-9, "without appearing in any committed file" (B7, V9) | Kept |
| M02 | Q1 what leaks into state, Q4 why state is sensitive | DoD-4, "a sensitive value can be read from state" | Reworded |
| M02 | Q2 bootstrapping, Q4 why the bucket is kept | Objective "reused by M08 to M11" and constraint "bootstrapped from a local-state configuration, then retained" (brief only) | Kept |
| M05 | Q6 how one account misrepresents practice | Constraint "real teams usually separate accounts" (brief only) | Kept |
| M06 | Q5–Q7 when to apply dependencies, lifecycle and conditions | Scope 7–9 name `depends_on`, the `lifecycle` block and preconditions (B7–B9) — topics, not answers | Kept |
| M07 | Q1 module vs root | DoD-7, "configures no provider itself" | Reworded |
| M07 | Q4 file layout | Scope 4 and DoD-3 listed inputs, outputs, resources and version requirements | Reworded |
| M07 | Q5 what deserves a comment | DoD-5, "explain why rather than restate what" | Reworded |
| M07 | Q7 trusting a module | Constraint "you read its source before using it" (brief only) | Reworded |
| M07 | Q8 when a module is wrong | Scope 12 listed thin wrappers, over-parameterisation and cloud-hiding abstractions | Reworded |
| M08 | Q1 knowing nothing real is touched | Scope 6 named the zero-destroy check; DoD-1 and DoD-2 still do, because the objective names that outcome | Scope 6 reworded; DoD-1 and DoD-2 kept |
| M08 | Q3 who owns an unmanaged resource | DoD-9, "including anything Terraform no longer manages" | Reworded |
| M08 | Q4 why plan-visible changes | DoD-7; constraint "declarative … reviewable as code" (brief only) | Reworded |
| M09 | Q1 ambient-login mismatch | Scope 2 and 3 "explicit project" and "explicit subscription", DoD-3, and the constraint | Reworded |
| M09 | Q3 why no common wrapper | Scope 6, "— no abstraction layer" | Reworded |

**What rewording did.** It kept each observable outcome and removed the explanatory half: "why", "rather than", "not just", the name of the mechanism, or the reason. Each stage's `tasks.md` was regenerated from the reworded brief and validated.

**Still open.** The two outcomes the objectives themselves name in M11 (zero destroys, zero replacements) and the "Best practices this stage demonstrates" lists, which name the preferred answers such as `for_each` over `count`. Both are brief-only or intrinsic to the stage.
