
# Content Discovery

## What is "Content"?
- Can include: files, videos, pictures, backups, and website features.
- Hidden/unintended public content includes:
  - Admin/staff portals
  - Old site versions
  - Backup/configuration files

## Content Discovery Methods
1. **Manual**
2. **Automated**
3. **OSINT (Open-Source Intelligence)**

---

## Manual Discovery Techniques

### 1. `robots.txt`
- Used to restrict search engine indexing.
- May contain paths to sensitive/admin areas.

### 2. Favicon Clues
- Default icons from frameworks can reveal tech stack.
- Reference: [OWASP Favicon DB](https://wiki.owasp.org/index.php/OWASP_favicon_database)

### 3. `sitemap.xml`
- Lists URLs intended for indexing.
- May contain hidden/old web pages.

### 4. HTTP Headers
- Reveal software & versions (e.g., NGINX, PHP).
- Use `curl` to inspect headers:
  ```bash
  curl http://MACHINE_IP -v
  ```

---

## Framework Stack Discovery
- Sources: favicon, page source comments, copyrights.
- Learn tech stack, find vulnerabilities, discover content.

---

## OSINT Tools and Techniques

### 1. Google Hacking / Dorking
- Advanced search filters:
  - `site:tryhackme.com admin`
  - `inurl:admin`
  - `filetype:pdf`
  - `intitle:admin`
- More: [Google Hacking Wikipedia](https://en.wikipedia.org/wiki/Google_hacking)

### 2. Wappalyzer
- Tech stack analysis: [Wappalyzer](https://www.wappalyzer.com/)

### 3. Wayback Machine
- View archived pages: [archive.org/web](https://archive.org/web/)

### 4. GitHub
- Search for repos containing secrets/code related to target.

### 5. AWS S3 Buckets
- Public buckets may leak files.
- Format: `http(s)://{name}.s3.amazonaws.com`
- Brute-force common naming conventions.

---

## Automated Discovery

### Wordlists
- Prebuilt lists of filenames/dirs for brute-forcing.
- Resource: [SecLists GitHub](https://github.com/danielmiessler/SecLists)

### Tools

#### FFUF
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://MACHINE_IP/FUZZ
```

#### Dirb
```bash
dirb http://MACHINE_IP/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

#### Gobuster
```bash
gobuster dir --url http://MACHINE_IP/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

---
