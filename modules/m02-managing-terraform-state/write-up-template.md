# M02 Write-Up — Managing Terraform State

> **Instructions for the Trainee:** 
> Copy this file to `write-up.md` in this folder and fill it in as you go, not at the end. Write it so a trainee starting this stage next cohort could follow your path. Delete all blockquotes (like this one) before submitting. **Never paste credentials, tokens, or key material.**

## 1. Deliverable & Evidence
> Link your code and provide the exact output proving it works based on the Definition of Done (DoD). Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. 

**Repository:** [Link here]
**Deliverable:** The protected S3 state bucket and the small configuration whose local state you inspected and then migrated into it.

*   **DoD-01 and DoD-02:** Your read-only local state output for one of your own resources, including what it holds for a sensitive value. 
    *   *Output/Evidence:* 
*   **DoD-03 and DoD-04:** The bucket listing showing your migrated state, and the bucket's versioning, encryption and public-access settings from the cloud side.
    *   *Output/Evidence:* 
*   **DoD-05:** The lock error you got when a second operation ran while the first was in progress.
    *   *Output/Evidence:* 

## 2. How to build it (teach it to the next trainee)
> Write a quick guide from local state to a protected remote backend with locking demonstrated. Use your own output/logs to show your reasoning, not just a list of commands. Assume the reader is a peer who hasn't started this stage yet.

## 3. Decisions & Core Concepts
> This section covers the *why* behind your build and the theory you applied. 

**Key Decisions**
*   **What can leak a secret into state, and why is a state file sensitive even when the configuration has no secrets?** 
*   **Who and what needs access to the state bucket, how narrow can you make it, and why is the bucket kept when everything else is destroyed?** 
*   **What does locking prevent, and what does it not?** 

**Concepts Applied**
> Pick 2–3 ideas from this list: what state records and where it lives, why a team needs a remote backend, or migrating local state without recreating anything. Explain each in your own words based on how you actually used it in this stage. 

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
