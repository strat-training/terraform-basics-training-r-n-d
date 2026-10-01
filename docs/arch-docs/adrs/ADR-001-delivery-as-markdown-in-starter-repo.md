# ADR-001: Deliver the program as Markdown modules in a starter repository

- **Status:** Accepted (hosting platform amended by [ADR-016](ADR-016-gitlab-for-hosting-and-ci.md))
- **Date:** 2026-10-01
- **Deciders:** Program owner (@Lee)
- **PRD references:** s.1, s.5, s.13 (FR-1, FR-2), s.14, s.15

## Context

The program is self-paced and asynchronous with no instructor. Learners are working engineers who already use Git. The PRD must choose a delivery vehicle for reading, activities, quizzes and progress tracking.

## Decision

Deliver everything as **11 Markdown module files plus activity folders in a GitLab starter repository**, inside a GitLab group. Progress is a Markdown checklist learners tick off. Quizzes live in the module files with answer keys. **No LMS and no external auto-grader.**

## Alternatives considered

| Option | Why not chosen |
| --- | --- |
| Hosted LMS (Moodle, Thinkific, internal LMS) | Extra procurement and integration, content split from the code, poor fit for Git-based activities |
| External auto-grading platform | Needs cloud credentials from learners, extra cost, conflicts with sandbox constraints |
| Documentation site (MkDocs, Docusaurus) over the same Markdown | Nicer reading experience, but adds a build and hosting step; can be layered later (for example with GitLab Pages) without changing this decision |
| Video-first course | Costly to maintain as providers change; poor fit for copy-paste-able code |

## Consequences

**Positive**
- Content, starter code, solutions and CI live together and are versioned together.
- Works on any device that can open a repository; a zero-install browser path exists only if GitLab Workspaces are enabled (see ADR-004, ADR-016).
- Low operating cost and nothing to procure.

**Negative / trade-offs**
- No central telemetry; completion and pass rates come from surveys and capstone submissions (see ADR-009).
- Gating between weeks is by convention, not enforced.
- Reading experience is plain Markdown unless a docs site is added later.

**Follow-ups**
- Decide whether to rename the `modules/` reading folder (to avoid confusion with Terraform modules). See solution design 4.1.
