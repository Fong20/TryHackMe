# Phishing Emails in Action

## Overview
This document summarizes multiple real-world phishing email samples and the techniques attackers use to make them appear legitimate. The goal is to recognize red flags and understand attacker objectives.

---

## Sample 1: PayPal Purchase / Cancel Order

### Techniques Used
- Spoofed email address
- URL shortening service
- HTML impersonation of PayPal

### Key Indicators
- Recipient email does not match the actual PayPal account
- Sender display name: `service@paypal.com`
- Actual sender email: `gibberish@sultanbogor.com`
- Subject line suggests an unfamiliar transaction to create urgency
- Only interactive element is a **Cancel the order** button

### Link Analysis
- Uses a URL shortener
- Shortened URL redirects to `google.com`
- Demonstrates how shortened URLs hide the true destination

---

## Sample 2: Package / Tracking Notification

### Techniques Used
- Spoofed email address
- Pixel tracking
- Link manipulation

### Key Indicators
- Appears to come from a mail distribution center
- Subject includes a tracking number
- Email body link matches subject line
- Images blocked automatically by Yahoo

### Technical Findings
- Embedded image named `Tracking.png`
- Tracking pixel sends data back to attacker server
- Yahoo blocks images to prevent tracking
- Hyperlink points to a suspicious domain, not a legitimate courier

---

## Sample 3: Expiring Fax Document (OneDrive / Adobe)

### Techniques Used
- Urgency
- HTML impersonation (OneDrive, Adobe)
- Link manipulation
- Credential harvesting
- Poor grammar and typos

### Attack Flow
1. Email claims fax document expires same day
2. Victim clicks download button
3. Redirected to fake OneDrive page (non-Microsoft URL)
4. Redirected again to fake Adobe login page
5. Page title says “Share Point Online” (inconsistent branding)
6. Victim prompted to log in with email credentials

### Outcome
- Credentials sent directly to attacker server
- Error message shown regardless of credentials entered
- Multiple grammar and spelling errors present

---

## Sample 4: Netflix Billing Suspension

### Techniques Used
- Spoofed email address
- Urgency
- HTML impersonation
- Poor grammar and typos
- Malicious attachments

### Key Indicators
- Sender: `z99@musacombi.online`
- Claims Netflix account is suspended
- Multiple misspellings of “Netflix”
- Attachment (PDF) required to update account
- Unusual phone number for a US-based service

### Attachment Behavior
- Embedded link: **Update Payment Account**
- Leads victim to phishing infrastructure

---

## Sample 5: DHL Shipment (Excel Attachment)

### Techniques Used
- Spoofed email address
- HTML impersonation
- Malicious attachments

### Key Indicators
- Sender email does not belong to DHL
- Subject implies a pending shipment
- Email body mimics DHL branding
- “View as web page” link has no real destination

### Attachment Analysis
- Excel document is the only interactive element
- File executes a payload
- Payload results in an error after execution

---

## Sample 6: Apple Support (DOT Attachment)

### Techniques Used
- Spoofed email address
- BCC abuse
- Urgency
- Poor grammar and typos
- Malicious attachments

### Key Indicators
- Sender: `gibberish@sumpremed.com`
- Victim placed in BCC field
- Spoofed recipient address to resemble Apple
- Typos: `donoreply`, `payament`
- No email body, only an attachment

### Attachment Details
- File type: `.DOT` (Microsoft Word template)
- Large image resembling App Store receipt
- Embedded link with Apple-related keywords (`apps`, `ios`)

---

## Key Takeaways
- Always verify sender and recipient addresses
- Be suspicious of urgency and expiring links
- Hovering over links is not always reliable
- Shortened URLs hide real destinations
- Attachments are a common malware delivery method
- Grammar and spelling mistakes remain common phishing indicators

Understanding phishing requires continuous awareness and practice.
