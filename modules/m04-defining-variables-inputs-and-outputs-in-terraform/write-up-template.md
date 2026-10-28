# M04 Write-Up — Defining Variables, Inputs and Outputs in Terraform

> **Instructions for the Trainee:** 
> Copy this file to `write-up.md` in this folder and fill it in as you go, not at the end. Write it so a trainee starting this stage next cohort could follow your path. Delete all blockquotes (like this one) before submitting. **Never paste credentials, tokens, or key material.**

## 1. Deliverable & Evidence
> Link your code and provide the exact output proving it works based on the Definition of Done (DoD). Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. 

**Repository:** [Link here]
**Deliverable:** The parameterised AWS configuration with two sets of values that both plan cleanly, your precedence record, and the configuration's sensitive input and output.

*   **DoD-01 and DoD-02:** A clean plan for each of your two sets of values, and the plan rejecting an invalid network address range with your validation message. 
    *   *Output/Evidence:* 
*   **DoD-04:** Your precedence record — one plan output per value source, then your combined run.
    *   *Output/Evidence:* 
*   **DoD-05:** Your plan output with a sensitive input, and the output showing what is displayed for your sensitive output.
    *   *Output/Evidence:* 

## 2. How to build it (teach it to the next trainee)
> Write a guide covering the scope below. Use your own output/logs to show your reasoning, not just a list of commands. Assume the reader is a peer who hasn't started this stage yet.

**Guide scope:** from a hard-coded configuration to one that plans cleanly with two sets of values

## 3. Decisions & Core Concepts
> This section covers the *why* behind your build and the theory you applied. 

**Key Decisions**
*   **Which inputs should have defaults and which should be required, and what is the risk of each?** 
*   **How does each way of supplying a value show up in a plan?** 
*   **What does marking a value sensitive hide, and where can it still be seen?** 

**Concepts Applied**
> Pick 2–3 of the ideas below. Explain each in your own words based on how you actually used it in this stage. 

**Ideas this stage covers:** validation rules, local values, or output values.

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
