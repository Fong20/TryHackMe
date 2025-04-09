
# Subdomain Enumeration

## Purpose of Subdomain Enumeration:
- Expands the attack surface.
- Helps in discovering additional vulnerabilities by finding valid subdomains.

## Methods of Subdomain Enumeration
--------------------------------
1. Brute Force Enumeration
   - Tries common subdomain names from a pre-defined wordlist.
   - Automated using tools like dnsrecon.

2. OSINT (Open-Source Intelligence) Enumeration
   - Uses publicly available resources such as:
     - Certificate Transparency logs (e.g., https://crt.sh)
     - Search engines using filters (e.g., site:*.domain.com -site:www.domain.com)
   - Tools like Sublist3r can automate this process.

3. Virtual Host Enumeration
   - Exploits the Host header in HTTP requests.
   - Web servers often host multiple domains on one server using the Host header to distinguish them.

## Certificate Transparency Logs
-----------------------------
- Maintained by Certificate Authorities (CAs).
- Record all SSL/TLS certificates issued.
- Useful for discovering current and historical subdomains.

## Google Dork Example:
--------------------
site:*.domain.com -site:www.domain.com

## Host File Information:
----------------------
- Private DNS records may be stored in:
  - Linux: /etc/hosts
  - Windows: C:\Windows\System32\drivers\etc\hosts

## Virtual Host Discovery using FFUF
---------------------------------

### Initial Command:
----------------
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.website_domain" -u http://MACHINE_IP

- -w: Specifies the wordlist.
- -H: Adds/edits HTTP headers, here manipulating the Host header.
- FUZZ: Placeholder to try each subdomain from the wordlist.

### Filtered Command (Using Page Size):
-----------------------------------
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.website_domain" -u http://MACHINE_IP -fs {size}

- -fs {size}: Filters out responses with a specific size (noise filtering).
