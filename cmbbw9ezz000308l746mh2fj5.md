---
title: "OWASP : Application Security Verification Standard"
seoTitle: "OWASP ASVS v5.0: Overview & Key Updates"
seoDescription: "Explore OWASP ASVS v5.0—its scope, structure, assurance levels, and key changes from v4.0. Learn how to apply security requirements effectively for modern w"
datePublished: Sat May 31 2025 07:12:10 GMT+0000 (Coordinated Universal Time)
cuid: cmbbw9ezz000308l746mh2fj5
slug: owasp-application-security-verification-standard
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1748674990339/cc1a21b1-2eff-47e8-932f-2b501b6c12f8.png

---

Link to the latest revision *( May , 2025 )* : [click to download](https://github.com/OWASP/ASVS/raw/v5.0.0/5.0/OWASP_Application_Security_Verification_Standard_5.0.0_en.pdf)

---

### **OWASP:** The Open Worldwide Application Security Project (formerly Open Web Application Security Project )

> *“ It is an open-source organisation that provides global guidelines, tools, and best practices to help improve application security and reduce software vulnerabilities.”*

---

## What is OWASP ASVS?

The **OWASP Application Security Verification Standard (ASVS)** is a comprehensive framework that defines **security requirements for web applications and services**.

It serves as an essential resource for developers, architects, and security professionals looking to design, develop, test, and maintain secure software.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1751918049592/3d4534a7-4673-4e20-80dc-c86d5ff49525.png align="center")

---

## Scope of the ASVS

ASVS gets its name from its four foundational pillars:

| Term | Meaning |
| --- | --- |
| **Application** | The software product being developed; security controls must be integrated into it. |
| **Security** | Each requirement must contribute to reducing the likelihood or impact of a security risk. |
| **Verification** | All requirements must be **verifiable**, resulting in a clear **pass/fail** outcome. |
| **Standard** | Only **requirements** ("must") are defined — **no recommendations** ("should"). |

> Requirement: The word requirement is used specifically in the ASVS as it describes what must be achieved to satisfy it. The ASVS only contains requirements (must) and does not contain recommendations (should) as the main condition.

---

## ASVS Levels of Assurance

ASVS uses a **three-level model** to provide varying degrees of assurance depending on risk and use case.

| **Level** | **Description** | **Real-World Use Case** |
| --- | --- | --- |
| **Level 1** | Minimal assurance for low-risk public apps | Marketing sites, blogs, personal portfolios |
| **Level 2** | Recommended default for most business apps | SaaS platforms, dashboards, HRMS, CRMs |
| **Level 3** | High assurance for safety-critical systems | Fintech APIs, healthcare, defense/military apps |

* **Level 1**: ~20% of requirements. Easy adoption, first layer of defense.
    
* **Level 2**: ~70% of total requirements (includes all of Level 1 + Level 2).
    
* **Level 3**: Final ~30%. Suitable for high-security, regulated environmen.
    
    `Note: Select your level based on your application's sensitivity and threat model. A startup may start with Level 1, while a bank must aim for Level 3.`
    

---

## How to Use ASVS

* **ASVS v5.0.0** contains approximately **350 requirements**.
    
* Divided into **17 chapters**, each split into **sections** for easier filtering.
    

> Example: If your app doesn’t use OAuth, you can ignore that chapter altogether.

---

## ASVS Requirement Format

Each requirement follows this format:  
`<chapter>.<section>.<requirement>` — e.g., `6.2.4`

* **Chapter**: Topic (e.g., Chapter 6 = Authentication)
    
* **Section**: Subtopic (e.g., 6.2 = Password Security)
    
* **Requirement**: Specific control (e.g., 6.2.4 = password blacklist check)
    

### Examples

#### Chapter 5: File Handling →

#### Section 2: File Upload →

* `5.2.1`: Verify that the application will only accept files of a size which it can process without causing a loss of performance or a denial of service attack. ( Level 1 )
    
* `5.2.6`: Verify that the application rejects uploaded images with a pixel size larger than the maximum allowed, to prevent pixel flood attacks. ( Level 3 )
    

#### Chapter 6: Authentication →

#### Section 2: Password Security →

* `6.2.1`: Verify that user set passwords are at least 8 characters in length although a minimum of 15 characters is strongly recommended. ( Level 1)
    
* `6.2.4`: Check passwords against top 3000 common passwords. *(Level 1)*
    
* `6.2.12`: Check passwords against a breached password list. *(Level 2)*
    
* `6.6.4`: Use rate limiting for MFA push to prevent bombing. *(Level 3)*
    

#### Chapter 13: Configuration →

#### Section 3: Secret Management →

* `13.3.2`: Verify that access to secret assets adheres to the principle of least privilege. 2 ( Level 2 )
    
* `13.3.4`: Verify that secrets are configured to expire and be rotated based on the application’s documentation. ( Level 3 )
    

> **Referencing tip**: Use versioned IDs like `v5.0.0-6.2.4` to avoid confusion between ASVS versions.

---

## OWASP ASVS v4.0.3 vs v5.0.0 – Summary of Changes

| Area | v4.x | v5.0 |
| --- | --- | --- |
| **Business Logic** | Part of Access Control / General | Split into **V2** with validation |
| **API Security** | Spread across categories | Now has dedicated **V4** |
| **OAuth/OIDC** | Was in Authentication | Now has dedicated **V10** |
| **JWT** | Was in Cryptography or Auth | Now under **V9** (Self-contained Tokens) |
| **Secure Frontend** | Minimal coverage | Now a full chapter **V3** |
| **WebRTC** | Not covered | New in **V17** |

---

### OWASP ASVS v5.0 Chapter List

| # | **Chapter** | **Focus Area** |
| --- | --- | --- |
| **V1** | **Encoding and Sanitization** | Output encoding, sanitization of untrusted data (XSS, injection prevention). |
| **V2** | **Validation and Business Logic** | Input validation and enforcing business logic rules. |
| **V3** | **Web Frontend Security** | Secure JavaScript, DOM-based security, CSP, client-side controls. |
| **V4** | **API and Web Service** | REST, GraphQL, SOAP, versioning, throttling, schema validation. |
| **V5** | **File Handling** | Uploads, downloads, media types, file type validation. |
| **V6** | **Authentication** | Login, MFA, password policies, account management. |
| **V7** | **Session Management** | Cookie flags, session ID protection, timeouts, logout behavior. |
| **V8** | **Authorization** | RBAC, ABAC, vertical/horizontal access control, enforcement. |
| **V9** | **Self-contained Tokens** | JWT, token integrity, expiry, audience, signing. |
| **V10** | **OAuth and OIDC** | Authorization flows, token management, consent, scopes. |
| **V11** | **Cryptography** | Storage, transmission, algorithms, keys, hashing. |
| **V12** | **Secure Communication** | HTTPS, TLS, HSTS, certificate pinning, secure headers. |
| **V13** | **Configuration** | Secure defaults, environment hardening, secrets, patching. |
| **V14** | **Data Protection** | Data classification, retention, minimization, masking. |
| **V15** | **Secure Coding and Architecture** | Design principles, threat modeling, secure SDLC, code practices. |
| **V16** | **Security Logging and Error Handling** | Auditable logs, tamper detection, error response hygiene. |
| **V17** | **WebRTC** | (New) Real-time communication security, media access, signaling. |

`Note:You can refer to the asvs v5 for a detailed read of chapters, sections and requirements, link is shared on the top!`

---