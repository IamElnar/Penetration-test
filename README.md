# BOZP Portal Penetration Test Report

This repository contains the penetration testing report for the **BOZP Portal**, conducted as part of a semester project by **Elnar Yantay** and **Yaroslav Bakhirkin**. The goal of the test was to identify security vulnerabilities within the BOZP Portal, evaluate its resilience against cyber threats, and suggest remediation steps for the discovered vulnerabilities.

## Project Overview

The BOZP Portal is used by students and staff to access occupational safety and health materials, participate in online assessments, and register for events. Our penetration testing focused on a non-production environment, testing its security defenses.

## Testing Methodology

We used the **OWASP Web Security Testing Guide** as our primary methodology. The testing was conducted on a virtual machine with static IP `10.0.0.10`, containing anonymized student data and two user roles:
- **Student** (regular user)
- **Admin** (administrator)

### Tools Used
- Nmap
- Nikto
- OWASP ZAP

## Key Findings

### 1. Unencrypted Transfer of Credentials (Critical)
- **Description**: Credentials were being transmitted over HTTP without encryption, making them vulnerable to interception.
- **Recommendation**: Implement HTTPS for all sensitive operations and enable HSTS headers.

### 2. Outdated Server Version (High)
- **Description**: The Apache web server was running version 2.4.38, which has several known vulnerabilities.
- **Recommendation**: Update Apache to the latest stable version.

### 3. CSRF Vulnerability on Homepage (High)
- **Description**: The admin's homepage allowed sensitive operations (e.g., article deletion) via GET requests, vulnerable to CSRF.
- **Recommendation**: Use POST requests with CSRF protection tokens.

### 4. Improper Access Control (Medium)
- **Description**: Regular users could modify other users' (including admin’s) email and phone number.
- **Recommendation**: Enforce strict authorization checks on the server side.

### 5. Presence of Default Files (Low)
- **Description**: Default files such as `/icons/README` and `.gitignore` were accessible.
- **Recommendation**: Remove or restrict access to default and unnecessary files.

### 6. Server Shutdown via Input Injection (Note)
- **Description**: The server could be shut down temporarily through input injection in the admin's "Filter" form.
- **Recommendation**: Sanitize input and implement proper input validation.

## Conclusion

The BOZP Portal exhibited several critical vulnerabilities, most notably the unencrypted transfer of credentials and use of outdated software. By addressing these issues, the overall security of the portal can be significantly improved. The report also highlights the importance of proper access control, input validation, and server updates.

## Authors
- **Elnar Yantay** (yantaeln@fit.cvut.cz)
- **Yaroslav Bakhirkin** (bakhiyar@fit.cvut.cz)
