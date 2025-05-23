# SOC Fundamentals

#### 1. Introduction
- Technology improves efficiency but increases security responsibilities.
- Critical data (secrets) are no longer physical but stored in networks.
- Threat actors exploit vulnerabilities daily, making cybersecurity crucial.
- Traditional security methods may not be enough—organizations need a **dedicated SOC team**.

#### 2. What is SOC?
- **Security Operations Center (SOC)** is a **24/7** dedicated facility monitoring an organization’s network for security threats.
- Focus: **Detection & Response**
- SOC integrates company-wide security solutions for centralized monitoring.

---

### 3. Focus Areas of SOC
#### Detection
1. **Detect vulnerabilities**
   - Weaknesses in software (OS, apps, etc.) that attackers exploit.
2. **Detect unauthorized activity**
   - Example: Stolen credentials used to access company systems.
3. **Detect policy violations**
   - Example: Downloading pirated files, insecure file transfers.
4. **Detect intrusions**
   - Unauthorized access via exploited vulnerabilities or malware.

#### Response
- **Incident Response**:
  - Minimize impact, analyze root cause, assist in containment & recovery.

---

### 4. Three Pillars of SOC
1. **People** (SOC team)
2. **Process** (Incident handling, triage, response)
3. **Technology** (Security tools like SIEM, EDR, Firewalls)

---

### 5. SOC Team Roles & Responsibilities
#### Hierarchy of SOC Team
- **SOC Analyst (Level 1)**
  - First responders for alerts, perform basic triage.
- **SOC Analyst (Level 2)**
  - Investigates detections, correlates data for deeper analysis.
- **SOC Analyst (Level 3)**
  - Experienced professionals handling high-severity incidents, proactive threat hunting.
- **Security Engineer**
  - Deploys & configures security solutions.
- **Detection Engineer**
  - Develops security detection rules.
- **SOC Manager**
  - Oversees SOC processes, reports to the CISO.

---

### 6. SOC Processes
#### Alert Triage (The 5 Ws of SOC)
- **What?** Malicious file detected on GEORGE PC.
- **When?** June 5, 2024, 13:20.
- **Where?** Directory on George's PC.
- **Who?** User: George.
- **Why?** File downloaded from pirated software website.

#### Reporting
- Escalate critical alerts to higher-level analysts via tickets.
- Reports must include **5 Ws, analysis, and screenshots as evidence**.

#### Incident Response & Forensics
- **High-severity incidents** require incident response.
- **Forensic analysis** identifies root causes using system/network artifacts.

---

### 7. SOC Technology (Security Solutions)
1. **SIEM (Security Information and Event Management)**
   - Collects logs from devices, applies detection rules, correlates alerts.
   - Provides **user behavior analytics & threat intelligence**.
   - SIEM **focuses on detection only**.
2. **EDR (Endpoint Detection & Response)**
   - Monitors device activities, detects threats, automates responses.
   - Provides both **detection & response**.
3. **Firewall**
   - Filters incoming/outgoing traffic, blocks unauthorized access.
4. **Other Security Tools**
   - **Antivirus, IDS/IPS, XDR, SOAR, EPP**—each plays a unique role.
   - Technology selection depends on threat landscape & available resources.
