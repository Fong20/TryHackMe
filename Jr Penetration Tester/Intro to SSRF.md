
# Intro to SSRF

## What is SSRF?
- SSRF (Server-Side Request Forgery) allows an attacker to make the web server send a crafted HTTP request to a resource of the attacker's choice.
- Two types:
  - Regular SSRF: Response returned to attacker.
  - Blind SSRF: No response shown to attacker.

## Impact of SSRF:
- Unauthorized area access.
- Data exposure (customer/org).
- Internal network reachability.
- Exposure of tokens/credentials.

## Common SSRF Vulnerabilities:
Potential SSRF vulnerabilities can be spotted in web applications in many different ways. Here is an example of four common places:

### 1. Full URL in a URL parameter.
![image](https://github.com/user-attachments/assets/73622e2c-61d7-4e31-9b75-778b4865ed2a)

### 2. Hidden field in a form.
![image](https://github.com/user-attachments/assets/00df005d-fe24-4927-8a55-b9f4168579f7)

### 3. Hostname-only input.
![image](https://github.com/user-attachments/assets/5628ca7f-4eec-483e-af7f-ecea2674a4d2)

### 4. Path-only input.
![image](https://github.com/user-attachments/assets/0cef85af-6d9b-490d-8d5d-743923a34a5d)

## Blind SSRF Detection:
If we are working with blind SSRF where there is no output is reflected back, we will need to use logging tools like requestbin.com, custom HTTP server, or Burp Collaborator to monitor requests.

## Identifying and breaking through SSRF Defenses:
More security-savvy developers aware of the risks of SSRF vulnerabilities may implement checks in their applications to make sure the requested resource meets specific rules. There are usually two approaches to this, either a deny list or an allow list.

### Deny List:
- Blocks certain resources (e.g., localhost, 127.0.0.1).
- Bypass techniques:
  - Use alternate localhost representations: 0, 0.0.0.0, 127.1, 127.*.*.*, 2130706433, etc.
  - DNS-resolved subdomains: 127.0.0.1.nip.io.
  - Cloud metadata IP: 169.254.169.254 → map a subdomain to this IP.

### Allow List:
- Only allows specified domains/patterns (e.g., must start with `https://website.thm`).
- Bypass technique:
  - Use subdomain trick: `https://website.thm.attacker-domain.thm`.

### Open Redirect:
- Redirects internal request using a legitimate domain redirection mechanism.
- Example:
  - Endpoint: `https://website.thm/link?url=https://tryhackme.com`
  - If SSRF restriction only allows `https://website.thm/`, attacker uses redirection to control request destination.

## Practical Lab Walkthrough:
1. Start machine and access the lab URL.
2. Create and sign into an account.
3. Navigate to `/customers/new-account-page`.
4. View avatar form → inspect avatar value (URL/path).
5. Choose an avatar and update – see base64-encoded image using data URI.
6. Try modifying avatar value to `/private` (fails due to deny list).
7. Bypass deny list with:
   ```
   x/../private
   ```
   - Directory traversal bypasses path restriction.
8. Avatar now displays base64-encoded contents of `/private`.
9. Decode to get the flag.

## Example Payloads:
- Basic SSRF: `http://127.0.0.1:80/admin`
- Deny list bypass: `http://2130706433/`
- Allow list bypass: `https://website.thm.attacker.com`
- Open redirect SSRF: `https://website.thm/link?url=http://attacker.com`

