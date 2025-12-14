# XSS - Merry XSSMas

## Scenario
Santa's workshop portal shows unusual logs with scripts/code. Investigation focuses on Cross-Site Scripting (XSS) vulnerabilities.

## Learning Objectives
- Understand how XSS works
- Learn how to prevent XSS attacks

## XSS Overview
XSS allows attackers to inject malicious JavaScript into web apps when input is not validated or escaped.

### Types Covered
- Reflected XSS
- Stored XSS

## Reflected XSS
- Payload is reflected immediately in HTTP response.
- Often exploited via phishing links.

### Example Payload
<script>alert('Reflected Meow Meow')</script>

### Impact
- Execute actions as victim
- Steal data or modify content

## Stored XSS
- Malicious payload is saved server-side.
- Executes for every user loading the page.

### Example Payload
<script>alert('Stored Meow Meow')</script>

### Impact
- Persistent compromise
- Cookie theft, fake logins, defacement

## Prevention Techniques
- Avoid innerHTML; use textContent
- Set cookies with HttpOnly, Secure, SameSite
- Sanitize and encode all user input/output

## Exploitation Summary
- Search bar vulnerable → Reflected XSS
- Message form vulnerable → Stored XSS
- Confirmed via alert popups and system logs

## Conclusion
Portal is vulnerable to XSS; explains odd logs. Hardening needed to sanitize input and secure rendering.
