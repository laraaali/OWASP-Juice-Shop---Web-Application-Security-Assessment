# OWASP Juice Shop - Web Application Security Assessment

**Course/Phase:** CYS423 Final | Phase 4
**Student Identifier:** 20220001588-lara
**Environment:** Kali Linux
**Target:** Local OWASP Juice Shop (`localhost:3000`)

---

## Overview

This repository documents the deployment, testing, and verification of multiple security challenges performed against a locally hosted **OWASP Juice Shop** instance.

The assessment focuses on common web application security vulnerabilities, including:

* SQL Injection
* Broken Access Control
* Cross-Site Scripting (XSS)
* CAPTCHA Bypass
* Sensitive Data Exposure
* Authentication Vulnerabilities
* Improper Input Validation

The assessment was conducted using **Kali Linux, Docker, Burp Suite, and Firefox**.

---

## Environment Setup

OWASP Juice Shop was deployed locally using Docker on Kali Linux.

```bash
# Update package repositories
sudo apt update

# Install Docker
sudo apt install docker.io -y

# Verify Docker installation
docker --version

# Start Docker
sudo systemctl start docker
sudo systemctl enable docker

# Test Docker installation
sudo docker run hello-world
```

The Juice Shop application was then accessed locally through:

```text
http://localhost:3000
```

---

## Testing Methodology

The assessment followed a controlled web application security testing process:

1. Deployed the intentionally vulnerable OWASP Juice Shop application locally.
2. Identified and analyzed application functionality and available attack surfaces.
3. Tested authentication and authorization mechanisms.
4. Intercepted and analyzed HTTP requests using Burp Suite.
5. Modified selected requests to evaluate input validation and access-control weaknesses.
6. Tested client-side injection vulnerabilities.
7. Verified successful exploitation through application responses and challenge completion.
8. Documented the techniques, vulnerabilities, and security impact.

---

## Solved Security Challenges

### 1. Login as Admin - SQL Injection

* **Category:** Injection
* **Technique:** SQL Injection authentication bypass
* **Impact:** Unauthorized access to the administrator account.

The login functionality was tested for SQL injection vulnerabilities that could alter the application's authentication query and bypass normal credential validation.

---

### 2. Access Administration Section - Broken Access Control

* **Category:** Broken Access Control
* **Technique:** Direct access to a restricted application route
* **Impact:** Unauthorized access to administrative functionality and user information.

The application was tested to determine whether restricted administrative functionality could be accessed without appropriate authorization.

---

### 3. Access a Confidential Document - Sensitive Data Exposure

* **Category:** Sensitive Data Exposure / Information Disclosure
* **Technique:** Directory enumeration through the `/ftp` endpoint
* **Impact:** Unauthorized access to confidential internal documents.

The application's accessible file resources were examined to identify files that should not have been publicly accessible.

---

### 4. DOM-Based XSS

* **Category:** Cross-Site Scripting
* **Technique:** Client-side injection through the application search functionality
* **Impact:** Execution of attacker-controlled JavaScript within the application's browser context.

The search functionality was tested for DOM-based XSS by supplying a JavaScript-based iframe payload:

```html
<iframe src="javascript:alert('XSS')">
```

A secondary iframe payload was also tested to demonstrate client-side content injection.

---

### 5. Login as Bender - Authentication Bypass

* **Category:** Injection
* **Tool:** Burp Suite
* **Technique:** Intercepted and modified the login request sent to `/rest/user/login`
* **Impact:** Authentication bypass and unauthorized account access.

Burp Suite Proxy was used to intercept the authentication request. The request was modified and replayed to evaluate whether the application's authentication mechanism could be bypassed.

---

### 6. CAPTCHA Bypass

* **Category:** Broken Anti-Automation
* **Tool:** Burp Suite
* **Technique:** Replayed application requests to bypass CAPTCHA-based submission restrictions
* **Impact:** Multiple feedback submissions could be generated within a short period.

The feedback submission process was analyzed using Burp Suite to determine whether CAPTCHA validation was properly enforced on the server side.

---

### 7. Change Bender's Password

* **Category:** Broken Authentication
* **Tool:** Burp Suite Repeater
* **Technique:** Modified the password-change request sent to `/rest/user/change-password`
* **Impact:** Password modification without knowledge of the existing password.

The password-change functionality was tested by intercepting and modifying the associated HTTP request. This demonstrated insufficient server-side validation of the password-change process.

---

### 8. Forgotten Developer Backup

* **Category:** Sensitive Data Exposure / Improper Input Validation
* **Technique:** URL encoding and null-byte manipulation to access a backup configuration file
* **Impact:** Unauthorized access to sensitive developer configuration data.

The application's file-handling functionality was tested using URL encoding and null-byte manipulation to determine whether restricted backup files could be accessed.

---

## Scoreboard Progress

| Challenge Type          | Progress |
| ----------------------- | -------: |
| Hacking Challenges      |      11% |
| Coding Challenges       |      23% |
| Total Challenges Solved | 26 / 173 |

### Challenges by Difficulty

| Difficulty | Completed | Total |
| ---------- | --------: | ----: |
| ⭐ 1        |        13 |    28 |
| ⭐ 2        |         6 |    24 |
| ⭐ 3        |         4 |    44 |
| ⭐ 4        |         2 |    37 |
| ⭐ 5        |         1 |    26 |

---

## Tools Used

* **Kali Linux** — Security testing environment
* **Docker** — Local application deployment
* **Burp Suite Community Edition** — HTTP interception, request analysis, and request manipulation
* **Firefox** — Web application testing
* **OWASP Juice Shop** — Intentionally vulnerable target application

---

## Skills Demonstrated

* Web application security testing
* SQL Injection
* Authentication bypass
* Broken Access Control
* Cross-Site Scripting (XSS)
* CAPTCHA bypass testing
* HTTP request interception and analysis
* Burp Suite Proxy and Repeater
* Input validation testing
* Sensitive data exposure analysis
* Authentication security testing
* HTTP request manipulation
* Docker-based security lab deployment
* Vulnerability identification and documentation

---

## Security Impact

The completed challenges demonstrate how weaknesses in authentication, authorization, input validation, client-side processing, and anti-automation controls can lead to unauthorized access or manipulation of application functionality.

The assessment provided practical experience in identifying vulnerabilities, reproducing security issues, analyzing HTTP requests, and documenting their potential impact.

---

## Disclaimer

This assessment was conducted exclusively against a **locally hosted OWASP Juice Shop instance**, an intentionally vulnerable application designed for security education and testing.

No unauthorized systems, networks, or applications were targeted. All testing was performed within a controlled educational environment.
