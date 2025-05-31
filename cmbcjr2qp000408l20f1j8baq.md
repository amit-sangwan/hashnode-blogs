---
title: "Authentication & Authorization"
seoTitle: "Authentication vs. Authorization: Key Differences"
seoDescription: "Explore designing strong, scalable authentication and authorization systems with OAuth2, OIDC, RBAC, ABAC, and OWASP ASVS to prevent security flaws"
datePublished: Sat May 31 2025 18:09:45 GMT+0000 (Coordinated Universal Time)
cuid: cmbcjr2qp000408l20f1j8baq
slug: authentication-and-authorization
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1748714828649/75de7fa8-0169-4ab5-967e-d159e9ef1a95.jpeg
tags: owasp, software-development, authentication, technology, security, cybersecurity-1, appsecdev

---

---

In this blog, we’ll unpack how to design strong, scalable authentication & authorization systems using **OAuth2, OIDC, RBAC, and ABAC**, while aligning with the **OWASP ASVS** to prevent common security flaws.

## Authentication vs Authorization: Know the Difference

| Term | Purpose | Example |
| --- | --- | --- |
| **Authentication** | Verifies identity | "This is User x" |
| **Authorization** | Controls access | "User x can delete invoices" |

While authentication confirms *who* a user is, authorization defines *what* they're allowed to do.

Get this wrong, and attackers might act as admins—or regular users may see sensitive data.

---

## Secure Identity Patterns: OAuth2, OIDC, RBAC, ABAC

### **OAuth 2.0** – Delegated Authorization

OAuth2 allows applications to access APIs on a user’s behalf **without storing passwords**.

**Typical Flow**:

1. User authenticates via an **Identity Provider (IdP)**
    
2. The IdP returns an **access token**
    
3. The client app uses the token to call protected APIs
    

**Example:** A user logs into a photo editing application (client app) and grants it permission to access their photos stored on Google Photos (resource server) through Google (IdP). The photo editing app receives an access token and uses it to retrieve photos without ever seeing the user's Google password.

> Use **short-lived access tokens** and **refresh tokens** to maintain security and user experience.

---

### **OpenID Connect (OIDC)** – Add Authentication on Top

OIDC extends OAuth2 with **identity** features:

* Issues an **ID token** (JWT) containing claims like `sub`, `email`, `name`
    
* Perfect for Single Sign-On (SSO)
    

Use OIDC when your app needs to **know who the user is** and validate sessions.

**Example:** A user signs into a new e-commerce website using their existing Google account. OIDC allows the e-commerce site to verify the user's identity (e.g., their name and email) from Google, enabling a seamless sign-up and login experience

---

### **RBAC** – Role-Based Access Control

The simplest and most common authorization model:

* Users get **roles** (e.g., admin, editor, viewer)
    
* Roles define access to resources and actions
    

```plaintext
jsonCopyEdit{
  "user": "alice",
  "roles": ["admin"]
}
```

**Pros**: Easy to implement  
**Cons**: Lacks flexibility—permissions are fixed

**Example:** In a content management system, users can be assigned "Editor" or "Viewer" roles. An "Editor" can create, edit, and publish articles, while a "Viewer" can only read published articles.

---

### **ABAC** – Attribute-Based Access Control

ABAC uses dynamic rules based on **user**, **resource**, and **contextual attributes**.

**Example Policy**:

> *Allow access if* `user.department == resource.department` and `user.level >= 3`

**Pros**: Granular, flexible  
**Cons**: Needs a policy engine (e.g., OPA, Cedar)

**Example:** An ABAC policy in a healthcare system might state: "A doctor (user role) can view patient records (resource) if the patient is assigned to their department (resource attribute) and the doctor has a valid medical license (user attribute) and the access request is made during business hours (contextual attribute)."

---

## Common ASVS Flaws in Authentication & Authorization

The OWASP Application Security Verification Standard (ASVS) defines security requirements for software.

Here’s how to mitigate auth-related flaws across key ASVS sections:

---

### ASVS **V2 – Authentication Controls**

| Flaw | Fix |
| --- | --- |
| Weak password hashing | Use Argon2id, bcrypt, or PBKDF2 **Example:** Instead of storing passwords as plain text or using outdated hashing like MD5, use Argon2id to securely hash and store user passwords, making them resistant to rainbow table attacks. |
| No brute-force defense | Apply rate-limiting & CAPTCHA **Example:** After 5 failed login attempts from a single IP address, implement a 60-second lockout or present a CAPTCHA to prevent automated brute-force attacks. |
| No MFA | Enable for high-risk roles **Example:** For administrators or users accessing sensitive financial data, require Multi-Factor Authentication (MFA) where they need to provide a code from a mobile authenticator app in addition to their password. |
| Insecure reset flows | Avoid security questions, use expiring reset tokens Avoid security questions, use expiring reset tokens **Example:** Instead of asking "What was your mother's maiden name?", send a unique, time-limited password reset link to the user's verified email address. |

---

### ASVS **V3 – Session Management**

| Flaw | Fix |
| --- | --- |
| Long-lived sessions | Use short JWT `exp` + refresh tokens **Example:** Instead of a single session token valid for days, issue an access token valid for 15 minutes and a refresh token valid for 7 days. The client can use the refresh token to get new access tokens. |
| No revocation on logout | Invalidate sessions and refresh tokens **Example:** When a user logs out, immediately invalidate their session token and refresh token on the server-side, preventing their reuse even if stolen. |
| Shared sessions | Prevent session fixation attacks with rotation on auth **Example:** After a user successfully logs in, regenerate their session ID and issue a new one, preventing an attacker from using a previously established session ID. |

---

### ASVS **V4 – Access Control**

| Flaw | Fix |
| --- | --- |
| Missing checks (IDOR) | Verify resource ownership (`user.id == resource.owner_id`) |
| Over-permissive roles | Enforce least privilege |
| Business logic abuse | Validate action intent with contextual checks |

---

## How to Enforce Auth Across the SDLC

| SDLC Phase | Best Practice |
| --- | --- |
| **Design** | Use STRIDE + threat modeling for login, session, and role logic |
| **Dev** | Implement token-based auth, RBAC/ABAC layers, centralized policy logic **Example:** Developers integrate a JWT (JSON Web Token) library for authentication |
| **Test** | Add tests for broken access control, token validation, expired sessions |
| **Deploy** | Use WAFs and API gateways for token validation and header enforcement |
| **Operate** | Log all login, access, and privilege elevation events; monitor anomalies |

---

## Secure Implementation Patterns

* **Store tokens securely** (e.g., HTTP-only cookies)
    
* **Validate JWT claims**: `iss`, `aud`, `exp`, `scope`
    
* **Centralize policy checks** (middleware or gateways)
    
* **Use libraries**: `passport.js`, Spring Security, Auth0 SDKs, OPA
    

---

## Tools of the Trade

| Purpose | Tool |
| --- | --- |
| Identity Provider | Auth0, Keycloak, Azure AD, Okta |
| Policy Enforcement | Open Policy Agent (OPA), Cedar |
| API Gateways | Kong, NGINX, Envoy with JWT plugin |
| Logging & SIEM | ELK, Datadog, Sumo Logic |

---

## Final Takeaways

* Use **OIDC for identity**, **OAuth2 for delegation**
    
* Start with **RBAC**, scale to **ABAC** for fine-grained control
    
* Map authentication and access logic to **ASVS requirements**
    
* **Treat tokens like passwords**: secure them, rotate them, expire them
    
* Use **threat modeling + automation** to catch logic flaws before attackers do
    

---