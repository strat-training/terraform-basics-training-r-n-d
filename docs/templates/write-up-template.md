<!-- 
INSTRUCTOR SETUP: Copy this file to `modules/<stage-folder>/write-up-template.md`. 
Replace the bracketed placeholders below with the specific details from the stage's brief. 
Delete this comment block before publishing.

VARIABLES TO REPLACE:
- [STAGE_ID] and [STAGE_TITLE]
- [DELIVERABLE_DESCRIPTION] (One line naming the deliverable and its companion pieces)
- [DESIGN_QUESTION_1/2/3] (Up to 3 specific prompts tied to Objective claims)
- [GUIDE_SCOPE] (e.g., "from an empty AWS account to a running auto-scaling group")
- [SCOPE_TOPIC_1/2/3] (3+ candidates for concepts worth explaining)
- [DOD_ID_1/2/3] and [DOD_EVIDENCE_REQ_1/2/3] (Specific output requests hardest to fake)

RULES FOR FILLING THEM (generate from the stage's brief, and keep it short):
- Key decisions: up to three of the brief's research prompts, each cut down to one or two short
  questions. Pick the prompts that tie to a claim in the brief's Objective (something the trainee
  is meant to be able to explain), and check that every Objective claim has a question or a
  "Concepts Applied" candidate. Merge only prompts that are close; drop the rest. Do not add a
  "where did you spend the most time" question: the Friction Log already asks it.
- Guide scope: one line saying what the guide takes a learner from and to.
- Concepts: 3 or more candidates, inline, taken from the scope topic titles. Use only scope topics
  that no key-decision question already covers, so the two sections never ask about the same thing.
- Evidence: up to three items, each one piece of real output (or a note, where the brief asks for
  one) that shows a central claim of the brief's Objective was actually done, naming the DoD id it
  backs. Pick the outputs that are hardest to fake; do not restate every definition-of-done bullet.
Everything else is the same in every stage.
-->

# [STAGE_ID] Write-Up — [STAGE_TITLE]

> **Instructions for the Trainee:** 
> Copy this file to `write-up.md` in this folder and fill it in as you go, not at the end. Write it so a trainee starting this stage next cohort could follow your path. Delete all blockquotes (like this one) before submitting. **Never paste credentials, tokens, or key material.**

## 1. Deliverable & Evidence
> Link your code and provide the exact output proving it works based on the Definition of Done (DoD). Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. 

**Repository:** [Link here]
**Deliverable:** [DELIVERABLE_DESCRIPTION]

*   **DoD-[DOD_ID_1]:** [DOD_EVIDENCE_REQ_1] 
    *   *Output/Evidence:* 
*   **DoD-[DOD_ID_2]:** [DOD_EVIDENCE_REQ_2]
    *   *Output/Evidence:* 
*   **DoD-[DOD_ID_3]:** [DOD_EVIDENCE_REQ_3]
    *   *Output/Evidence:* 

## 2. How to build it (teach it to the next trainee)
> Write a quick guide covering the scope below. Use your own output/logs to show your reasoning, not just a list of commands. Assume the reader is a peer who hasn't started this stage yet.

**Guide scope:** [GUIDE_SCOPE]

## 3. Decisions & Core Concepts
> This section covers the *why* behind your build and the theory you applied. 

**Key Decisions**
*   **[DESIGN_QUESTION_1]:** 
*   **[DESIGN_QUESTION_2]:** 
*   **[DESIGN_QUESTION_3]:** 

**Concepts Applied**
> Pick 2–3 of the ideas below. Explain each in your own words based on how you actually used it in this stage. 

**Ideas this stage covers:** [SCOPE_TOPIC_1], [SCOPE_TOPIC_2], or [SCOPE_TOPIC_3].

## 4. AI Collaboration Log
> Be specific, and answer each prompt below in as many lines as it needs. Only if you used no AI at all, say so in one line and skip the rest.

*   **Tools & Scope:** Which AI tool(s) did you use, and for roughly what portion of the work?
*   **Prompt Examples:** Give 2–3 concrete examples of what you asked for.
*   **Course Correction:** Describe at least one moment the tool's first suggestion was wrong, inefficient, or didn't fit your design. What was wrong, how did you notice, and what did you do instead?
*   **Human Intervention:** What did you accept largely as-is, and what did you rewrite or redesign yourself?

## 5. Retrospective & Self-Assessment
> Reflect on the friction you faced, how you grade your own work, and what you would change. 

*   **Friction Log (What tripped me up):** Where did you spend the most time, and why? What didn't behave the way you expected the first time? (Keep the exact error texts and how you resolved them).
*   **What I'd do differently:** If you started this stage over today, what is the single biggest change you'd make to your approach?
*   **DoD Self-Assessment:** Rate yourself honestly against every item in the DoD (Met, Partly Met, Not Met) and the stage rubric.
*   **Blind Spots:** Name any part of your own work you would struggle to explain cold right now, without re-reading it first.