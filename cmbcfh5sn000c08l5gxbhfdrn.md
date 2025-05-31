---
title: "Building Sustainable Security Requirements with OWASP ASVS"
seoTitle: "Sustainable Security with OWASP ASVS"
seoDescription: "Learn how to make OWASP ASVS practical and sustainable for secure software development without overwhelming developers"
datePublished: Sat May 31 2025 16:10:04 GMT+0000 (Coordinated Universal Time)
cuid: cmbcfh5sn000c08l5gxbhfdrn
slug: building-sustainable-security-requirements-with-owasp-asvs
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/wMRIcT86SWU/upload/7edc203e4cfe53de62952b918cc33029.jpeg
tags: owasp, technology, security, asvs, cybersecurity-1, ndc

---

---

> *"Start securely—without upsetting people."*  
> That’s the essence of Josh Grossman's talk at NDC Security, where he outlined how to turn the massive OWASP Application Security Verification Standard (ASVS) into a practical, repeatable, and developer-friendly security requirements engine.

In a world where "shift left" and "secure by design" are buzzwords, Grossman’s session brought something developers and AppSec teams actually need: **a way to operationalise ASVS in the earliest phases of software development without overwhelming everyone involved.**

---

## **Drive Enforcement Throughout the SDLC**

Here’s how to integrate your custom ASVS into the dev lifecycle:

| SDLC Phase | ASVS Mapping Strategy |
| --- | --- |
| **Requirements** | Feature-level mapping to ASVS controls via questionnaire |
| **Design** | Run contextual threat modeling against mapped controls |
| **Development** | Provide “how to” guidance for each ASVS requirement (e.g., password hashing libraries, header settings) |
| **Testing** | Use ASVS numbers to build checklists, static/dynamic test cases |
| **Deployment** | Add final checks for deferred items in the Security Backlog |
| **Post-release** | Track compliance and improvement using the ASVS mapping as baselineThe Problem: Checklists, Chaos, and Burnout |

A large organization attempted to roll out a 50-page secure development lifecycle (SDLC) policy—complete with a monstrous checklist—for every product team.

Predictably, no one used it.

The effort failed not because developers didn’t care about security, but because:

* The security requirements were not contextual to their features.
    
* Too much was expected too early, and
    
* There was no sustainable process for updating or maintaining the effort.
    

---

## Solution: Four Key Strategies to Make ASVS Work

---

### 1\. **Information Overload**: *Customise the ASVS*

ASVS has around 300 requirements. Expecting teams to apply all of them to every feature is unrealistic.

**Instead**:

* Fork the ASVS and tailor it to your organisation.
    
* Remove irrelevant sections (e.g., skip GraphQL items if you're not using it).
    
* Build a lightweight questionnaire: Developers answer a few yes/no questions about a new feature, and the system returns only the applicable ASVS requirements.
    

> Tip: Always document **why** a requirement is dropped—don’t silently trim.

---

### 2\. **Security as an External Force** → *Contextualise Security*

Security is often seen as a team that “drops in,” runs some scans, throws out some advice, and disappears.

Treat security as a quality attribute, just like functionality, performance, reliability, or usability.

Use threat modelling to ask:

* “What could go wrong here?”
    
* “What would make our business sad?”
    

It is a structured process to identify, assess, and address potential security threats to a system before they become real issues. It helps you understand:

* What could go wrong (threats)
    
* Where it could happen (attack surfaces)
    
* How an attacker might exploit vulnerabilities
    
* What to do to mitigate or prevent those risks
    

This aligns security with business risk, not just compliance.

---

### 3\. **If Everything Is Important, Nothing Is Important** → *Prioritise Thoughtfully*

Once you know which ASVS controls are relevant, you still need to prioritize.

Use these filters:

* **Business impact**: What risk does this feature introduce?
    
* **Effort vs. value**: Is this a quick win or a long-term investment?
    
* **Developer fatigue**: Balance tougher controls with easier ones to maintain morale.
    

> Maintain a **Security Backlog** to track deferred items—set timelines (e.g., "next release" or "in 6 months") to avoid “infinite backlog syndrome.”

---

### 4\. **Point-in-Time Solutions Don't Scale** → *Operationalise and Reuse*

The final pillar: make security requirements and solutions reusable.

Create a centralised repository where developers can:

* Look up how your org stores passwords
    
* Find the right output encoding for HTML/JS
    
* Know what HTTP headers to include
    
* Understand how to securely use an external auth provider (e.g., Auth0)
    

Each requirement from ASVS should link to how your team solves it in your environment. Think: curated playbooks, not just static policies.

> Developers vastly outnumber AppSec pros. **Scaling knowledge means documenting solutions.**

---

## Summary: Make ASVS Actionable, Contextual, and Sustainable

| Problem | Solution |
| --- | --- |
| ASVS is too big | Customize and reduce scope |
| Security feels like a burden | Integrate it as a quality attribute |
| Too many priorities | Use threat modeling to focus |
| Inconsistent fixes | Centralize and reuse implementation guidance |

---

## Final Thoughts

The OWASP ASVS is a **powerful tool**—but only if used strategically. Josh Grossman’s approach turns it from an academic list into a **living system for secure development**.

Start small. Ask the right questions. Link requirements to business risk. And above all, give developers what they need to build secure systems **without friction**.

> *Security should not be the enemy of velocity. With the right system, it can be a multiplier.*