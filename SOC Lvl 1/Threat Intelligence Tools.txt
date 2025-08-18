# Threat Intelligence Tools

## Learning Objectives
- Basics of threat intelligence & its classifications  
- Using **UrlScan.io** for malicious URL scanning  
- Using **Abuse.ch** for tracking malware and botnet indicators  
- Investigating phishing emails using **PhishTool**  
- Using **Cisco Talos Intelligence** for intel gathering  

---

## Threat Intelligence Overview
- Definition: Analysis of data to generate meaningful patterns for mitigating risks from threats targeting organizations, industries, or governments.  

**Key Questions:**  
- Who’s attacking you?  
- What’s their motivation?  
- What are their capabilities?  
- What indicators of compromise (IoCs) should you watch for?  

---

## Threat Intelligence Classifications
1. **Strategic Intel**: High-level, trends, business risk mapping.  
2. **Technical Intel**: Evidence & artifacts of attack. Used by IR teams.  
3. **Tactical Intel**: TTPs (tactics, techniques, procedures). Strengthens security controls.  
4. **Operational Intel**: Adversary motives, intent, targeted assets.  

---

## UrlScan.io
- Free tool for scanning & analyzing websites.  
- Records: domains, IPs, requests, snapshots, technologies, metadata.  

**Key Scan Results Sections:**  
- **Summary**: General info (IP, domain, history, screenshot).  
- **HTTP**: Connections, file types fetched.  
- **Redirects**: HTTP & client-side redirects.  
- **Links**: Outgoing links.  
- **Behaviour**: Variables, cookies, frameworks.  
- **Indicators**: IPs, domains, hashes.  

---

## Abuse.ch Platforms
Hosted by Bern University of Applied Sciences (Switzerland).  

### Tools:
- **MalwareBazaar**  
  - Upload & share malware samples.  
  - Malware hunting (tags, signatures, YARA, ClamAV, vendor detection).  

- **Feodo Tracker**  
  - Botnet C2 tracking: Dridex, Emotet, TrickBot, QakBot, BazarLoader.  
  - Provides IP/IOC blocklists & mitigation info.  

- **SSL Blacklist**  
  - Detects malicious SSL certs.  
  - Provides denylist & JA3/JA3s fingerprints.  

- **URLHaus**  
  - Shares malware distribution sites (URLs, domains, hashes).  
  - Provides feeds by country, AS number, TLD.  

- **ThreatFox**  
  - Search/share/export IoCs (MISP, Suricata rules, Host files, DNS RPZ, JSON, CSV).  

---

## PhishTool (Phishing Email Analysis)
- Helps investigate & mitigate phishing campaigns.  
- Versions: **Community** (free), **Enterprise** (advanced features).  

**Community Features:**  
- Email analysis (metadata, attachments, URLs).  
- Heuristic intelligence (OSINT integration).  
- Classification & forensic reporting.  

**Enterprise Features:**  
- User-reported phishing management.  
- Email stack integration (Microsoft 365, Google Workspace).  

**Analysis Tabs:**  
- Headers, Received Lines, X-headers.  
- Security (SPF, DKIM, DMARC).  
- Attachments, Message URLs.  
- Plaintext & source details.  
- Resolution: classify emails, flag artifacts, assign classification codes.  

---

## Cisco Talos Intelligence
- Security research & intel team at Cisco.  

**Key Teams:**  
1. Threat Intelligence & Interdiction  
2. Detection Research  
3. Engineering & Development  
4. Vulnerability Research & Discovery  
5. Communities  
6. Global Outreach  

**Platform Features:**  
- **Reputation Lookup**: Email traffic overview (legitimate, spam, malware).  
- **Vulnerability Info**: CVEs, CVSS, advisories, timelines, Snort rules.  
- **Reputation Center**: Threat data lookup (IPs, SHA256 hashes, spam data).  

---

✅ These notes are condensed for study or quick reference.
