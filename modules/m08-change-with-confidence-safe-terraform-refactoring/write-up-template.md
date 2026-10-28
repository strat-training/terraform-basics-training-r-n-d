# M08 Write-Up — Change with Confidence: Safe Terraform Refactoring

> **Instructions for the Trainee:** 
> Copy this file to `write-up.md` in this folder and fill it in as you go, not at the end. Write it so a trainee starting this stage next cohort could follow your path. Delete all blockquotes (like this one) before submitting. **Never paste credentials, tokens, or key material.**

## 1. Deliverable & Evidence
> Link your code and provide the exact output proving it works based on the Definition of Done (DoD). Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. 

**Repository:** [Link here]
**Deliverable:** The small configuration after its three refactors — a rename, an adoption and a stop-managing — with the saved plans that show no destroys, and your note on legacy state commands.

*   **DoD-01:** The saved-plan summary after each of the three refactors showing no destroys or replacements, and your `jq` output listing the action on every resource. 
    *   *Output/Evidence:* 
*   **DoD-02:** The output showing the renamed resource kept its identity, the adopted resource plans clean, and the stopped resource still exists in AWS.
    *   *Output/Evidence:* 
*   **DoD-03:** The diff for each refactor, and your list of every command you ran against state.
    *   *Output/Evidence:* 

## 2. How to build it (teach it to the next trainee)
> Write a guide covering the scope below. Use your own output/logs to show your reasoning, not just a list of commands. Assume the reader is a peer who hasn't started this stage yet.

**Guide scope:** from a small configuration to a rename, an adoption and a stop-managing with no destroys

## 3. Decisions & Core Concepts
> This section covers the *why* behind your build and the theory you applied. 

**Key Decisions**
*   **How can you tell before applying that a refactor won't touch real infrastructure, and how do you avoid orphaned cost when you stop managing a resource?** 
*   **What did the generated configuration get wrong or leave out, and how did you decide what to keep?** 
*   **Why prefer changes that appear in a plan over commands that edit state, and when might you still meet those commands?** 

**Concepts Applied**
> Pick 2–3 of the ideas below. Explain each in your own words based on how you actually used it in this stage. 

**Ideas this stage covers:** reading plans as JSON with `jq`, recovering from a partial apply or a failed destroy, or targeted operations.

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
