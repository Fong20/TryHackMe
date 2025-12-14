# Phishing - Phishmas Greetings

## Scenario Context
- TBFC Email Protection Platform is down.
- SOC team must manually triage suspicious emails.
- Attackers: *Malhare’s Eggsploit Bunnies*.
- Goal: identify **legitimate vs phishing emails**, noting that some phishing is cleverly disguised as normal TBFC operations.

---

## Learning Objectives
- Spot phishing emails
- Learn trending phishing techniques
- Understand differences between spam and phishing

---

## Phishing Overview
Phishing is a targeted attack focused on **deception and persuasion**, not volume.

### Common Phishing Goals
- **Credential theft** (passwords, VPN access)
- **Malware delivery** (malicious attachments)
- **Data exfiltration**
- **Financial fraud** (fake payroll changes, invoices)

### Key Insight
Phishing targets **people**, the weakest link, rather than technology.

---

## Spam vs Phishing

### Spam
- High-volume, low-precision
- Usually harmless
- Focuses on marketing or promotion

**Spam Intentions**
- Promotion / advertising
- Clickbait traffic generation
- Email address harvesting

### Phishing
- Low-volume, high-precision
- Designed to deceive
- Targets specific users or roles

**Key Difference**
➡️ Look at the **intention** behind the message, not just whether it’s unwanted.

---

## Common Phishing Techniques

### 1. Impersonation
- Attacker pretends to be:
  - Manager
  - IT department
  - Internal service
- Red flag: sender uses **free or external domain** (e.g., Gmail instead of TBFC domain)

**Example**
- Subject: *“URGENT: McSkidy VPN access for incident response”*
- Sender impersonates McSkidy using Gmail

---

### 2. Social Engineering
Manipulating emotions instead of exploiting software.

**Techniques Observed**
- Urgency (“urgent”, “immediately”)
- Authority (pretending to be McSkidy)
- Isolation (discouraging verification via normal channels)
- Malicious request (VPN credentials, approvals)

---

### 3. Typosquatting & Punycode

#### Typosquatting
- Misspelled domains
- Example: `glthub.com` instead of `github.com`

#### Punycode
- Uses Unicode characters that visually resemble Latin letters
- Example:
  - Cyrillic or Greek letters replacing Latin ones
  - Domain looks legit but is encoded

**Detection Tip**
- Check **Return-Path** in headers
- Look for `xn--` ACE encoding

---

### 4. Spoofing
- Email appears to come from a trusted internal domain
- Headers reveal fraud

**Key Header Checks**
- Authentication-Results
  - SPF: ❌
  - DKIM: ❌
  - DMARC: ❌
- Return-Path shows external attacker domain

➡️ If SPF & DMARC fail → **Strong spoofing indicator**

---

### 5. Malicious Attachments
- Attachments disguised as:
  - Voice messages
  - Invoices
  - Agreements

**Dangerous Formats**
- `.html` / `.hta`
  - Run scripts without browser sandboxing
  - Can steal credentials or install malware

---

## Trending Phishing Techniques

### Modern Shift
- Less malware attachments
- More **credential harvesting**
- Focus on moving users outside secure environments

### Typical Flow
1. Phishing email
2. Link to legitimate-looking service
3. Redirect to:
   - Fake login page
   - Malicious download
   - Fake invoice

---

## Abuse of Legitimate Applications
Attackers hide behind trusted platforms:
- OneDrive
- Google Docs
- Dropbox

**Common Lures**
- Laptop upgrade
- Salary raise
- HR documents

**Example**
- Fake TBFC IT email
- Punycode domain
- OneDrive document with attractive offer

---

## Fake Login Pages
- Primary goal: **credential theft**
- Commonly mimicked services:
  - Microsoft 365
  - Google

**Red Flag**
- Login domain does not match official service
- Example:
  - `microsoftonline.login444123.com`

---

## Side-Channel Communication
- Attacker moves conversation off email to:
  - SMS
  - WhatsApp / Telegram
  - Phone or video calls
  - Shared document platforms

**Why**
- Avoids company email controls
- Increases social engineering success

---

## Key Takeaways
- Not all unwanted emails are phishing → check intent
- Always verify:
  - Sender domain
  - Email headers
  - Attachments and links
- Phishing today is about **trust abuse**, not malware delivery
