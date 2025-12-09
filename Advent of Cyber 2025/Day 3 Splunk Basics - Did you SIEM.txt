# Splunk Basics - Did you SIEM?
**Date:** (from provided scenario)
**Context:** The Best Festival Company (TBFC) SOC investigates a ransomware incident (King Malhare / Bandit Bunnies) using Splunk. Data already ingested (web_traffic, firewall_logs). Compromised webserver local IP: **10.10.1.15** (note: firewall pivot used 10.10.1.5 in scenario — keep both when correlating).

---
## Learning objectives
- Ingest & interpret custom log data in Splunk
- Create/apply custom field extractions
- Use SPL to filter & refine searches
- Conduct an investigation to uncover key insights

---
## Datasets (sourcetypes)
- **web_traffic** — web server connection logs (fields: user_agent, path, client_ip, status, host, source, _time, etc.)
- **firewall_logs** — firewall events (fields: src_ip, dest_ip, dest_port, action, bytes_transferred, protocol, reason, _time, etc.)

---
## Initial triage
Base query to show all ingested logs:
```spl
index=main
```

Search for web traffic sourcetype (All time timeframe initially):
```spl
index=main sourcetype=web_traffic
```

Visualize event counts per day (timeline / identify traffic spike):
```spl
index=main sourcetype=web_traffic | timechart span=1d count
```

Reverse-sort to show highest-count day first:
```spl
index=main sourcetype=web_traffic | timechart span=1d count | sort by count | reverse
```

---
## Anomaly detection / fields examined
- **user_agent** — many suspicious non-browser user agents (curl, wget, sqlmap, Havij, zgrab, bunnylock)
- **client_ip** — a single external IP dominates suspicious agents (replace `<REDACTED>` with that IP)
- **path** — suspicious URIs like `/.env`, `/*phpinfo*`, `/.git*`, `*..*` (path traversal), `*redirect*`, `*backup.zip*`, `*logs.tar.gz*`, `*bunnylock.bin*`, `*shell.php?cmd=*`

Filter out common/benign browsers to focus on scripted/tools traffic:
```spl
index=main sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox*
```

Get top suspicious client IPs (after excluding common browsers):
```spl
sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox* 
| stats count by client_ip | sort -count | head 5
```

---
## Tracing the attack chain (pivot on attacker IP = `<REDACTED>`)
### Reconnaissance (probing for exposed config / files)
```spl
sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("/.env", "/*phpinfo*", "/.git*") 
| table _time, path, user_agent, status
```

Observed 404/403/401 responses to cURL/wget probes.

### Enumeration (path traversal, open redirect)
Basic search for path traversal / redirect attempts:
```spl
sourcetype=web_traffic client_ip="<REDACTED>" AND (path="*..*" OR path="*redirect*")
```
Escaped path-traversal pattern and get counts:
```spl
sourcetype=web_traffic client_ip="<REDACTED>" AND (path="*..\/..\/*" OR path="*redirect*") 
| stats count by path
```

Findings: Attempts to read `../../*`, indicating path-traversal exploitation attempts.

### SQL Injection (automated tools)
Detect sqlmap / Havij user agents & payload effects:
```spl
sourcetype=web_traffic client_ip="<REDACTED>" AND user_agent IN ("*sqlmap*", "*Havij*")
| table _time, path, status
```
Notes: Payloads like `SLEEP(5)` and 504 timeouts indicate time-based SQLi success.

### Exfiltration attempts (downloads of archives / logs)
```spl
sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("*backup.zip*", "*logs.tar.gz*")
| table _time, path, user_agent
```

Observed tools: curl, zgrab, custom scripts — large archive downloads requested.

### Ransomware staging & remote code execution (RCE)
Look for webshells & payload exec:
```spl
sourcetype=web_traffic client_ip="<REDACTED>" AND path IN ("*bunnylock.bin*", "*shell.php?cmd=*")
| table _time, path, user_agent, status
```
Evidence: `GET /shell.php?cmd=./bunnylock.bin` — indicates shell executed a binary (ransomware) on server.

---
## Firewall correlation (pivot from compromised server -> attacker C2)
Compromised server internal IP noted in scenario: **10.10.1.5** (firewall pivot uses this as src_ip). Confirm outbound allowed C2 connections:
```spl
sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="<REDACTED>" AND action="ALLOWED"
| table _time, action, protocol, src_ip, dest_ip, dest_port, reason
```

Compute volume exfiltrated (bytes transferred):
```spl
sourcetype=firewall_logs src_ip="10.10.1.5" AND dest_ip="<REDACTED>" AND action="ALLOWED"
| stats sum(bytes_transferred) by src_ip
```

Findings: Large data transfers to attacker's dest_ip on suspicious dest_port; reason field indicates `C2_CONTACT` and action ALLOWED.

---
## Key conclusions (from scenario)
- **Attacker identity**: External IP with highest volume of malicious web traffic.
- **Intrusion vector**: Web application exploitation observed in web_traffic sourcetype.
- **Reconnaissance**: cURL/wget probes for `/.env`, `phpinfo`, `.git` etc.
- **Exploitation**: SQL injection using tools (sqlmap/Havij), evidenced by SLEEP(5) and 504 responses.
- **Payload delivery**: Webshell (`/shell.php`) used to execute `./bunnylock.bin` (ransomware).
- **Post-exploitation**: Outbound C2 from compromised server (10.10.1.5) to attacker's IP confirmed in firewall_logs; significant bytes transferred (data exfiltration).

---
## Actions / remediation (recommended, from typical SOC playbook)
- Immediately isolate compromised host (10.10.1.5 / 10.10.1.15 as noted) from network.
- Block attacker IP at perimeter and firewall (dest_ip / client_ip `<REDACTED>`).
- Revoke or rotate any credentials possibly exposed in exfiltrated `.env` or config files.
- Preserve logs, create forensics image of compromised host for offline analysis.
- Sweep other hosts for presence of `bunnylock.bin`, webshells (`shell.php`) and Indicators of Compromise (IoCs).
- Patch vulnerable web application components; perform code review for SQL injection and file inclusion vulnerabilities.
- Review firewall rules to prevent unauthorized outbound C2 communications; implement egress filtering and strict allowlists.
- Update detection rules (Splunk) to alert on: non-browser user_agent spikes, SQLMAP / Havij signatures, `*/shell.php?cmd=*`, large archive downloads, and outbound connections to flagged IPs/ports.

---
## Quick-reference PoC SPL queries (copy/paste)
**Base web logs:** `index=main sourcetype=web_traffic`
**Exclude browsers:** `index=main sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox*`
**Top suspicious IPs:** `sourcetype=web_traffic user_agent!=*Mozilla* user_agent!=*Chrome* user_agent!=*Safari* user_agent!=*Firefox* | stats count by client_ip | sort -count | head 5`
**Recon (.env/.git/phpinfo):** `sourcetype=web_traffic client_ip=\"<REDACTED>\" AND path IN (\"/.env\", \"/*phpinfo*\", \"/.git*\") | table _time, path, user_agent, status`
**Path traversal counts:** `sourcetype=web_traffic client_ip=\"<REDACTED>\" AND (path=\"*..\/..\/*\" OR path=\"*redirect*\") | stats count by path`
**SQLi tools detection:** `sourcetype=web_traffic client_ip=\"<REDACTED>\" AND user_agent IN (\"*sqlmap*\", \"*Havij*\") | table _time, path, status`
**RCE/webshell:** `sourcetype=web_traffic client_ip=\"<REDACTED>\" AND path IN (\"*bunnylock.bin*\", \"*shell.php?cmd=*\") | table _time, path, user_agent, status`
**Firewall C2 pivot:** `sourcetype=firewall_logs src_ip=\"10.10.1.5\" AND dest_ip=\"<REDACTED>\" AND action=\"ALLOWED\" | table _time, action, protocol, src_ip, dest_ip, dest_port, reason`
**Bytes exfiltrated:** `sourcetype=firewall_logs src_ip=\"10.10.1.5\" AND dest_ip=\"<REDACTED>\" AND action=\"ALLOWED\" | stats sum(bytes_transferred) by src_ip`

---
## Notes / discrepancies to confirm in real environment
- The scenario references both **10.10.1.15** (web server local IP) and **10.10.1.5** (firewall pivot compromised server). When investigating, confirm the true internal host IP mapping (hostnames/asset inventory) to avoid mis-isolation.
- Replace `<REDACTED>` with the actual attacker/client IP observed in the Splunk fields (client_ip/dest_ip).
- Confirm timezone on `_time` fields when building a timeline.
- Preserve raw event examples (copy a few event `_raw` examples with timestamps) to include in IOC reports.

---
## End of notes
