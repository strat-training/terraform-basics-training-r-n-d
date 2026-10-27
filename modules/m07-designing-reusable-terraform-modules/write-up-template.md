# M07 Write-Up — Designing Reusable Terraform Modules

> **Instructions for the Trainee:** 
> Copy this file to `write-up.md` in this folder and fill it in as you go, not at the end. Write it so a trainee starting this stage next cohort could follow your path. Delete all blockquotes (like this one) before submitting. **Never paste credentials, tokens, or key material.**

## 1. Deliverable & Evidence
> Link your code and provide the exact output proving it works based on the Definition of Done (DoD). Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. 

**Repository:** [Link here]
**Deliverable:** The reusable AWS module with its documented interface, the root configuration that calls it twice with different inputs, and your decision note.

*   **DoD-01:** Clean plans for both module calls, and the state listing showing distinct module paths. 
    *   *Output/Evidence:* 
*   **DoD-02:** Your module's file listing and its input and output declarations with types and descriptions.
    *   *Output/Evidence:* 
*   **DoD-05:** Your review of one published module and your decision note on what you put in the module, what you left out, and when you would not write a module.
    *   *Output/Evidence:* 

## 2. How to build it (teach it to the next trainee)
> Write a quick guide from repeated configuration to a reusable module called twice from a root configuration. Use your own output/logs to show your reasoning, not just a list of commands. Assume the reader is a peer who hasn't started this stage yet.

## 3. Decisions & Core Concepts
> This section covers the *why* behind your build and the theory you applied. 

**Key Decisions**
*   **What belongs inside the module and what stays in the root, and how did you draw the line?** 
*   **Which inputs did you expose and which did you fix, what does each extra input cost, and what must the outputs tell a caller?** 
*   **How do resource addresses change when something moves into a module, and what would that mean for a configuration that is already deployed?** 

**Concepts Applied**
> Pick 2–3 ideas from this list: file structure and naming conventions, calling a module more than once, module sources and pinning, consuming a published module, or when a module is the wrong answer. Explain each in your own words based on how you actually used it in this stage. 

## 4. AI Collaboration Log
> Be specific. If you used no AI, state that in one line.

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
