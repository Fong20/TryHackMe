# Phishing Analysis Fundamentals

## Social Engineering Overview
- **Spam & Phishing** are common social engineering attacks.
- Phishing attack vectors include:
  - Email (primary focus)
  - Phone calls (vishing)
  - Text messages (smishing)
- Even with layered defenses, **one user interaction** (clicking a link or attachment) can lead to compromise.

## Historical Context
- First spam email: **1978**
- Email invented in the **1970s (ARPANET)** by **Ray Tomlinson**
- Introduced the use of the **@ symbol** in email addresses.

## Email Address Structure
An email address consists of:
- **User Mailbox (Username)**
- **@**
- **Domain**

Example: `billy@johndoe.com`
- User mailbox: `billy`
- Domain: `johndoe.com`

Analogy:
- Domain = street name
- Mailbox/user = house number + resident name

## Email Protocols
### SMTP (Simple Mail Transfer Protocol)
- Handles **sending** emails
- Default port: **25**

### POP3 (Post Office Protocol)
- Emails downloaded to **one device**
- Sent mail stored locally
- Emails typically deleted from server unless configured otherwise

### IMAP (Internet Message Access Protocol)
- Emails stored on **server**
- Accessible and synced across **multiple devices**
- Sent mail stored on server

## How Email Travels (High-Level Flow)
1. Sender composes email and clicks send.
2. SMTP server queries DNS for recipient domain.
3. DNS returns mail server info.
4. Email travels across the internet via multiple SMTP servers.
5. Destination SMTP server receives email.
6. Email stored on recipient’s POP3/IMAP server.
7. Recipient’s email client checks for new mail.
8. Email is downloaded (POP3) or synced (IMAP).

## Email Message Structure
Emails consist of two main parts:
- **Header** – metadata and routing information
- **Body** – content (text or HTML)

Email format standard: **Internet Message Format (IMF)**

## Key Email Header Fields
Common visible fields:
- **From** – sender address
- **To** – recipient address
- **Subject**
- **Date**

Important headers when analyzing raw emails:
- **X-Originating-IP** – sender’s IP address
- **Authentication-Results**
  - `smtp.mailfrom`
  - `header.from`
- **Reply-To** – address replies are sent to (may differ from From)

⚠️ Mismatch between **From** and **Reply-To** can indicate phishing.

## Email Body Types
### Plain Text
- Simple text, no formatting

### HTML
- Can include:
  - Images
  - Hyperlinks
  - Styling
- Often used in phishing to impersonate brands

You can view:
- Rendered HTML
- Raw HTML source code (client-dependent)

## Attachments
Attachments are visible in:
- Email UI
- Raw source code

Important attachment headers:
- **Content-Type** (e.g., application/pdf)
- **Content-Disposition** (attachment)
- **Content-Transfer-Encoding** (e.g., base64)

Base64-encoded attachments can be decoded and saved.

⚠️ Never double-click unknown attachments.

## Malicious Email Categories
- **Spam** – unsolicited bulk emails
  - **MalSpam** – malicious spam
- **Phishing** – impersonates trusted entities
- **Spear Phishing** – targeted individuals/orgs
- **Whaling** – targets executives (CEO, CFO)
- **Smishing** – phishing via SMS
- **Vishing** – phishing via voice calls

## Common Phishing Characteristics
- Spoofed sender address/name
- Urgent or alarming language (Invoice, Suspended, Action Required)
- Brand impersonation (Amazon, Netflix, etc.)
- Poor grammar or formatting
- Generic greetings (Dear Sir/Madam)
- Shortened or hidden URLs
- Malicious attachments disguised as documents

## Defanging
- Makes URLs/emails non-clickable to prevent accidental execution
- Example:
  - `http://www.badsite.com`
  - `hxxp[://]www[.]badsite[.]com`
- Tools: **CyberChef**

## Business Email Compromise (BEC)
- Attacker compromises a **legitimate internal email account**
- Uses it to trick employees into:
  - Fraudulent payments
  - Unauthorized actions
- Common real-world attack and interview topic

## Key Takeaways
- Understand email structure and delivery flow
- Know how to view raw headers and HTML
- Identify suspicious indicators in headers, body, and attachments
- Apply safe handling techniques (defanging, no-click policy)
