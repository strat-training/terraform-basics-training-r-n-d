# M03 Write-Up — Managing Resources with Network Provisioning

> **Instructions for the Trainee:** 
> Copy this file to `write-up.md` in this folder and fill it in as you go, not at the end. Write it so a trainee starting this stage next cohort could follow your path. Delete all blockquotes (like this one) before submitting. **Never paste credentials, tokens, or key material.**

## 1. Deliverable & Evidence
> Link your code and provide the exact output proving it works based on the Definition of Done (DoD). Paste real output, trimmed to the relevant lines and redacted, or link a screenshot. 

**Repository:** [Link here]
**Deliverable:** The small AWS network — a VPC, subnets in more than one availability zone, the routing the public tier needs and no NAT gateway.

*   **DoD-01 and DoD-04:** Your plan showing the VPC, subnets in two or more zones and the public routing, with no NAT gateway. 
    *   *Output/Evidence:* 
*   **DoD-05:** Your note naming the implicit dependencies in your configuration and where each one comes from.
    *   *Output/Evidence:* 
*   **DoD-02 and DoD-03:** Your plan or state listing showing the subnets created from one repeated block, and the value your data source read.
    *   *Output/Evidence:* 

## 2. How to build it (teach it to the next trainee)
> Write a quick guide from an empty configuration to a small multi-zone AWS network. Use your own output/logs to show your reasoning, not just a list of commands. Assume the reader is a peer who hasn't started this stage yet.

## 3. Decisions & Core Concepts
> This section covers the *why* behind your build and the theory you applied. 

**Key Decisions**
*   **Where did you rely on Terraform to infer ordering, and where did you have to state it explicitly?** 
*   **What are the trade-offs between the two ways of repeating a resource, and what happens to existing subnets if you add or remove one?** 
*   **How does a resource differ from a data source, and what happens to each on destroy?** 

**Concepts Applied**
> Pick 2–3 ideas from this list: the VPC and subnets across availability zones, the routing a public tier needs, or why there is no NAT gateway. Explain each in your own words based on how you actually used it in this stage. 

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
