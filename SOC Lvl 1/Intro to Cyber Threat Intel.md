# Intro to Cyber Threat Intel (CTI)

## Role of CTI in SOC
- SOC L1 analysts are the **first human touchpoint** for alerts.
- CTI helps enrich indicators, triage alerts, and transform data into actionable stories.
- Goals:
  - Understand threat intelligence (TI) & its relevance.
  - Learn TI lifecycle & key indicators.
  - Use feeds & platforms for intelligence sharing.

### CTI Helps Answer:
1. Who/what is behind an alert?
2. What was their past behaviour?
3. How should the organisation respond now?

---

## From Data → Information → Intelligence
| Layer       | Definition                          | Example                        | SOC L1 Action         |
|-------------|--------------------------------------|--------------------------------|------------------------|
| Data        | Raw observable                       | `45.155.205.3 :443`            | Capture artefact       |
| Information | Data + annotation                    | IP registered to Hetzner       | Record attributes      |
| Intelligence| Analysed info → action               | BumbleBee C2 → block           | Escalate/suppress      |

- **IOC** = Evidence of breach (e.g., C2 IP).
- **IOA** = Malicious action (e.g., suspicious PowerShell).
- **TTPs** = Adversary methodologies (MITRE ATT&CK IDs).

---

## Indicator Types & Resources
| Indicator   | Example                           | Look-up Sources                                | IOA/TTP Examples                     |
|-------------|-----------------------------------|------------------------------------------------|--------------------------------------|
| IPv4/6      | `45.155.205.3`                   | WHOIS, VirusTotal, Shodan                      | T1110.003 Password Guessing           |
| Domain/FQDN | `malicious-updates[.]net`        | WHOIS, RiskIQ, urlscan.io                      | DNS queries to new domain             |
| URL         | `hxxp://malicious-updates[.]net` | URLhaus, urlscan.io, Any.Run                   | Browser POST to `/gateway.php`        |
| File Hash   | `e99a18c428cb38d5…`              | VirusTotal, Hybrid-Analysis, MalShare          | T1055 Process Injection               |
| Email       | `billing@evil-corp.com`          | MXToolbox, Have I Been Pwned                   | SPF failure + new domain              |
| Local Art.  | `HKCU\Software\Run\updater.exe`  | Sigma rules, EDR query, vendor KB              | T1060.001 Registry Run Keys           |

*Tip: Maintain bookmarks or SIEM launchers for quick look-ups.*

---

## Feeds vs. Platforms
- **Feed**: Stream of indicators (CSV, JSON, STIX, TAXII).
- **Platform**: Repository that stores, enriches & shares indicators (e.g., MISP, OpenCTI).
- Best practice: Ingest feeds cautiously → validate → promote to platform.

---

## CTI Sources
1. **Internal telemetry**: SIEM, EDR, phishing submissions.
2. **Commercial services**: Premium feeds, paid sandboxes.
3. **OSINT**: AbuseIPDB, URLhaus, blogs.
4. **Communities/ISACs**: Sector-specific lists.

---

## Threat Intelligence Classifications
- **Strategic**: Trends/patterns (e.g., ransomware forecast).
- **Tactical**: TTPs (e.g., ATT&CK notes).
- **Operational**: Campaign-specific motives/targets.
- **Technical**: IOCs (IPs, hashes).

---

## Traffic Light Protocol (TLP)
| TLP  | Sharing Scope                     | SOC L1 Use                                   |
|------|-----------------------------------|----------------------------------------------|
| CLEAR| No restriction                    | Post internally                              |
| GREEN| Share with trusted community      | Upload to MISP, Slack                        |
| AMBER| Org-only, limited client sharing  | Keep in platform; reference in tickets        |
| RED  | Named recipients only             | Store encrypted, do not ticket without clearance |

---

## CTI Lifecycle (Scenario: Protecting TryHatMe DB)
**Step 1 – Direction**
- Asset: PostgreSQL DB.
- Risk: GDPR fines, customer trust loss.
- Controls: NGFW, EDR.
- Questions:
  - Q1: Which IPs/domains target PostgreSQL?
  - Q2: Which malware families/hashes are active?

**Step 2 – Collection**
- Sources: Vendor feeds, AbuseIPDB, MISP, reports.
- Store raw intel in S3.

**Step 3 – Processing**
- Normalise & deduplicate.
- Tag with source, date, TLP.
- Create action files:
  - `firewall_blocklist.csv`
  - `edr_hash_rules.yar`

**Step 4 – Analysis**
- Grade indicators:
  - **High**: ≥2 sources + local hits → block
  - **Medium**: 1 source, no hits → alert
  - **Low**: OSINT only → monitor

**Step 5 – Dissemination**
- Firewall team → CSV + ticket
- EDR team → YARA rules
- CTI platform → full objects
- Management → summary memo

**Step 6 – Feedback**
- Metrics after 2 weeks:
  - Median dwell time: 48h → 0h
  - FP rate: 0%
- Next cycle: add DNS tunneling IOCs.

---

## Standards & Frameworks
- **MITRE ATT&CK**: Maps adversary TTPs.
- **MITRE D3FEND**: Defensive countermeasures.
- **Cyber Kill Chain** (Lockheed Martin):
  1. Recon
  2. Weaponisation
  3. Delivery
  4. Exploitation
  5. Installation
  6. C2
  7. Actions on objectives
- **CVE / CVSS / NVD**:
  - CVE = vulnerability ID.
  - CVSS = severity scoring (0–10).
  - NVD = canonical vulnerability database.

---

## Sharing & Processing Standards
- **STIX**: Structured JSON schema for threat intel.
- **TAXII**: Secure API for intel exchange.
  - Supports *Collections* (hosted by producer) & *Channels* (published streams).
- Benefits: Faster collective defense, reciprocal trust.
- Caution: Don’t share IOCs restricted by privacy laws/NDAs.

---

✅ **Key Takeaway:**  
L1 analysts use CTI not just to identify artefacts, but to **enrich, contextualise, classify, and share** them, ensuring triage decisions are data-driven and actionable.
