# Pyramid of Pain
- Is a well-renowned concept which is used to improve the effectiveness of CTI (Cyber Threat Intelligence), threat hunting, and incident response exercises.

## Hash Values (Trivial)
- Unique numeric value from hashing algorithm to identify data.
- Common algorithms:
  - **MD5**: 128-bit, insecure (RFC 6151 highlights collisions).
  - **SHA-1**: 160-bit, deprecated (susceptible to brute-force, replaced by SHA-2/SHA-3).
  - **SHA-2 (SHA-256)**: 256-bit, secure.
- Security usage: uniquely identify malicious files (malware samples, suspicious files).
- Online tools: VirusTotal, Metadefender Cloud (OPSWAT).
- Weakness: easy for attackers to modify files → new hash → evade detection.

## IP Addresses (Easy)
- Identifies devices in a network.
- Defense: blocking IPs on firewall.
- Weakness: attackers can easily change IPs (Fast Flux techniques).
- **Fast Flux**: rapidly changing DNS records to obscure C2 infrastructure (per Akamai).

## Domain Names (Simple)
- Maps IP to text string (e.g., evilcorp.com, tryhackme.evilcorp.com).
- Harder to change than IPs (requires domain registration/DNS changes).
- Weaknesses in some DNS providers (loose standards, easy APIs).
- **Punycode attacks**: deceptive domains (e.g., adıdas.de → xn--addas-o4a.de).
- Detection: Proxy or web server logs.
- Common URL shorteners used in attacks: bit.ly, goo.gl, ow.ly, s.id, smarturl.it, tiny.pl, tinyurl.com, x.co.

### Viewing Connections in Any.run
- **Networking Tab**: shows HTTP, DNS requests, and process communications.
- **HTTP Requests**: resources retrieved (droppers, callbacks).
- **Connections Tab**: all communications (C2 traffic, FTP uploads/downloads).
- **DNS Requests Tab**: domain lookups (connectivity checks).

## Host & Network Artifacts (Annoying)
- Examples: registry values, process execution, IOCs, dropped files, user-agent strings, C2 info, URI patterns.
- Detection makes attack more costly for adversaries.
- Tools: Wireshark PCAPs, TShark, IDS logs (e.g., Snort).
- Example TShark command to extract User-Agent strings:
  ```bash
  tshark --Y http.request -T fields -e http.host -e http.user_agent -r analysis_file.pcap
  ```
- Example threat: Emotet Downloader Trojan custom User-Agent strings.

## Tools (Challenging)
- E.g., "Stealer.exe" dropped in Temp folder.
- Tools for detection:
  - Antivirus signatures
  - Detection/YARA rules
  - Sources: MalwareBazaar, Malshare.
  - Detection rule marketplace: SOC Prime Threat Detection Marketplace.
  - **Fuzzy hashing** (e.g., SSDeep) for similarity analysis.

## Tactics, Techniques & Procedures (TTPs) (Tough)
- Covers entire adversary kill chain (MITRE ATT&CK matrix).
- If defenders detect TTPs early, attackers face high cost to adapt:
  - Example: detect Pass-the-Hash via Windows Event Log Monitoring.
- Forces attackers to:
  1. Rebuild or retrain tools (expensive).
  2. Abandon target (low effort).
