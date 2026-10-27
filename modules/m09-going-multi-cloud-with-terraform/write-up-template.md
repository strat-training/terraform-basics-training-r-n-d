# M09 Write-Up — Going Multi-Cloud with Terraform

> **Instructions for the Trainee:** 
> Copy this file to `write-up.md` in this folder and fill it in as you go, not at the end. Write it so a trainee starting this stage next cohort could follow your path. Delete all blockquotes (like this one) before submitting. **Never paste credentials, tokens, or key material.**

## 1. Deliverable & Evidence
> Link your code and provide the exact output proving it works based on the Definition of Done (DoD). Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. 

**Repository:** [Link here]
**Deliverable:** The two small configurations, one for GCP and one for Azure, each signing in with a short-lived login and outputting the identity it runs as.

*   **DoD-02:** Each cloud's plan output with its identity output and nothing to add. 
    *   *Output/Evidence:* 
*   **DoD-03:** The output showing each configuration targets the intended project or subscription while the active login points elsewhere.
    *   *Output/Evidence:* 
*   **DoD-04:** The output of your scan for secrets and keys.
    *   *Output/Evidence:* 

## 2. How to build it (teach it to the next trainee)
> Write a quick guide from installing the two CLIs to a successful plan on GCP and on Azure. Use your own output/logs to show your reasoning, not just a list of commands. Assume the reader is a peer who hasn't started this stage yet.

## 3. Decisions & Core Concepts
> This section covers the *why* behind your build and the theory you applied. 

**Key Decisions**
*   **How do you confirm which project and subscription you are signed in to?** 
*   **What goes wrong if the ambient login points at a different project than you intended, and what in your configuration prevents it?** 
*   **What goes wrong if it points at a different subscription, and what in your configuration prevents it?** 

**Concepts Applied**
> Pick 2–3 ideas from this list: state across clouds, where this course stops, or what carries over from the AWS workflow and what does not. Explain each in your own words based on how you actually used it in this stage. 

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
