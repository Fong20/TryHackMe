
# SSRF (Server-Side Request Forgery) Notes

## What is SSRF?
- SSRF allows an attacker to make the web server send a crafted HTTP request to a resource of the attacker's choice.
- Two types:
  - Regular SSRF: Response returned to attacker.
  - Blind SSRF: No response shown to attacker.

## Impact of SSRF:
- Unauthorized area access.
- Data exposure (customer/org).
- Internal network reachability.
- Exposure of tokens/credentials.

## Common SSRF Vectors:
- Full URL in a URL parameter.
- Hidden form fields.
- Hostname-only input.
- Path-only input.

## Blind SSRF Detection:
- Use logging tools like requestbin.com, custom HTTP server, or Burp Collaborator.

## SSRF Protections:
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

