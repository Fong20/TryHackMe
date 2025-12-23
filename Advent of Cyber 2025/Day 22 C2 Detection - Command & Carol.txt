# C2 Detection - Command & Carol

## Scenario Context
- TBFC investigates potential Command & Control (C2) traffic after prior attacks.
- Sir Elfo proposes using **RITA (Real Intelligence Threat Analytics)** to analyze network traffic efficiently.
- Workflow: **PCAP → Zeek logs → RITA analysis**.

---

## Learning Objectives
- Convert a PCAP to Zeek logs
- Use RITA to analyze Zeek logs
- Interpret RITA output for threat hunting

---

## What is RITA?
**Real Intelligence Threat Analytics (RITA)** is an open-source framework by Active Countermeasures.

### Core Capabilities
- C2 beacon detection
- DNS tunneling detection
- Long connection detection
- Data exfiltration detection
- Threat intel feed correlation
- Severity scoring of connections
- Host prevalence analysis
- First-seen timestamps for external hosts

### Analytics Signals Used
- Periodic connection intervals
- Excessive DNS queries
- Long or random FQDNs / subdomains
- Data volume trends (HTTPS, DNS, non-standard ports)
- SSL/TLS anomalies (self-signed, short-lived certs)
- Known malicious IPs/domains

---

## Zeek Overview
- Zeek is an **NSM tool**, not an IDS/IPS.
- It passively analyzes traffic from SPAN ports, taps, or PCAP files.
- Converts traffic into **structured logs**.
- Covers:
  - Transaction data (e.g., HTTP, DNS)
  - Extracted content (files, artifacts)

RITA **only accepts Zeek logs** as input.

---

## Converting PCAP to Zeek Logs

### Directory Structure
- `pcaps/` – example malware PCAPs
- `zeek_logs/` – output Zeek logs

### Command
```bash
zeek readpcap pcaps/AsyncRAT.pcap zeek_logs/asyncrat
```

### Output Logs (Examples)
- conn.log
- dns.log
- http.log
- ssl.log
- files.log
- x509.log
- notice.log

> Logs are self-descriptive and can be inspected with `cat`.

---

## Importing Zeek Logs into RITA

### Command
```bash
rita import --logs ~/zeek_logs/asyncrat/ --database asyncrat
```

### Notes
- RITA parses conn, http, ssl, dns logs.
- Threat intel feeds are updated during import.

---

## Viewing RITA Results

### Command
```bash
rita view asyncrat
```

### Interface Sections
1. **Search Bar**
   - Activate with `/`
   - Use `?` for search field help
2. **Results Pane**
3. **Details Pane**

---

## Results Pane Fields
- Severity score
- Source → Destination IP/FQDN
- Beacon likelihood
- Connection duration
- Subdomain count
- Threat intel hits

### Interesting Findings
- `sunshine-bizrate-inc-software[.]trycloudflare[.]com`
- IP: `91[.]134[.]150[.]150`

---

## Details Pane Breakdown

### Threat Modifiers
- MIME type / URI mismatch
- Rare signature (e.g., unique TLS handshake)
- Low prevalence
- First seen timestamp
- Missing HTTP host header
- Large outbound data
- No direct connections

### Connection Info
- Connection count
- Total bytes sent
- Port / Protocol / Service
- Non-standard ports flagged

---

## Analysis Takeaways
- Long FQDNs and rare TLS signatures strongly indicate C2 activity.
- VirusTotal confirms both highlighted destinations as malicious.
- Small datasets may affect severity scoring (false positives possible).
- Even low-severity entries warrant investigation.

---

## Next Steps (Out of Scope)
- Pivot into Zeek logs for deeper inspection
- Analyze original PCAP for payloads
- Exercise caution: PCAPs may contain active malicious artifacts
