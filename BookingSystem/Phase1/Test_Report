# 1️⃣ Introduction

**Tester:**
- Name: Baptiste Rault

**Purpose:**
- To identify security vulnerabilities in the registration module, focusing on input validation, session management, and server configuration.

**Scope:** 
- Tested components: Registration Page (`/register` endpoint).
- Exclusions: Production database, Login page (Phase 2), Payment gateways.
- Test approach: Gray-box (Black-box testing with knowledge of API parameters) and Black-box / Automated Scanning (OWASP ZAP)..

**Test environment & dates:** 
- Start: 2025-11-25
- End: 2025-11-25 
- Test environment details: Localhost:8000, ZAP Scanner.

**Assumptions & constraints:**
- Testing performed in a local development environment.

---

# 2️⃣ Executive Summary

**Short summary (1-2 sentences):** The registration page is critically vulnerable to Privilege Escalation and Input Validation attacks. A malicious user can register as an administrator without authorization and inject malicious scripts or SQL commands into the database.

**Overall risk level:** 🔴 **High**

**Top 5 immediate actions:** 
1.  **Fix SQL Injection:** Implement prepared statements for the username parameter immediately.
2.  **Implement CSRF Protection:** Add unique Anti-CSRF tokens to the registration form.
3.  **Sanitize Inputs:** Address the Format String error by strictly validating user input types.
4.  **Set Security Headers:** Configure Content-Security-Policy and X-Frame-Options to prevent XSS and Clickjacking.
5.  **Custom Error Handling:**Disable verbose 500 Internal Server Error responses to prevent information leakage.

---

# 3️⃣ Severity scale & definitions

|  **Severity Level** | **Description** | **Recommended Action** |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
|      🔴 **High** | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | *Immediate fix required* |
|     🟠 **Medium** | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF).                              | *Fix ASAP* |
|      🟡 **Low** | A minor issue or configuration weakness (e.g., server version disclosure).                                                   | *Fix soon* |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers).                                            | *Monitor and fix in maintenance* |


---

# 4️⃣ Findings

| ID | Severity | Finding | Description | Evidence / Proof |
|------|-----------|----------|--------------|------------------|
| F-01 | 🔴 High | SQL Injection in Registration | The username parameter is vulnerable to SQL injection. Sending a single quote causes a server error. | Payload: ' Result: HTTP/1.1 500 Internal Server Error |
| F-02 | 🟠 Medium | Absence of Anti-CSRF Tokens | The registration form lacks Anti-CSRF tokens, making it possible to forge requests on behalf of users. | Form fields: birthdate, password, username found without tokens. |
| F-03 | 🟠 Medium  | Format String Error | The application evaluates input strings as commands, potentially leading to crashes or execution. | Payload: ZAP%n%s%n%s... |
| F-04 | 🟠 Medium | Missing Security Headers (CSP & Clickjacking) | Content-Security-Policy and X-Frame-Options are missing, exposing the site to XSS and Clickjacking. | Headers missing on /register and / |
| F-06 | 🟡 Low | Application Error Disclosure | The application returns verbose 500 errors that may disclose sensitive file paths or stack traces. | Status: 500 Internal Server Error on /register |
