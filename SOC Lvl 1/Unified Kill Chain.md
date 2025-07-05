
# Unified Kill Chain (UKC) 

## Objectives of UKC Framework
- Understand attacker behaviours, objectives, and methodologies.
- Help improve cybersecurity posture and threat modelling.
- Complements existing frameworks like MITRE ATT&CK and Lockheed Martin’s Kill Chain.

## Importance of Threat Modelling
- Identify and secure critical systems and applications.
- Assess vulnerabilities and potential exploits.
- Develop plans and policies to mitigate risks.
- Use tools like STRIDE, DREAD, CVSS.

## Benefits of UKC Over Other Frameworks
| UKC Framework | Other Frameworks |
|---------------|-------------------|
| Released in 2017, updated in 2022 | Older (e.g., MITRE ATTACK - 2013) |
| 18 detailed phases | Limited phases |
| Covers full attack lifecycle | Often limited scope |
| Allows phase recurrence | Linear phase structure |

---

## UKC Phases Overview

### Reconnaissance (MITRE TA0043)
- Info gathering (systems, services, employees, credentials).
- Both passive and active methods.

### Weaponization (MITRE TA0001)
- Set up C2 infrastructure and payloads.

### Social Engineering (MITRE TA0001)
- Techniques: malicious attachments, phishing, impersonation.

### Exploitation (MITRE TA0002)
- Gain code execution using vulnerabilities (e.g., reverse shells).

### Persistence (MITRE TA0003)
- Maintain access via services, C2 linkage, backdoors.

### Defence Evasion (MITRE TA0005)
- Bypass WAFs, firewalls, antivirus, IDS.

### Command & Control (MITRE TA0011)
- Establish link with compromised systems to:
  - Execute commands
  - Steal data
  - Pivot in network

### Pivoting (MITRE TA0008)
- Access internal systems using compromised public-facing systems.

### Discovery (MITRE TA0007)
- Learn about systems, users, permissions, software.

### Privilege Escalation (MITRE TA0004)
- Gain higher privileges (root, admin).

### Execution (MITRE TA0002)
- Deploy malware, C2 scripts, persistence mechanisms.

### Credential Access (MITRE TA0006)
- Steal credentials (keylogging, dumping).

### Lateral Movement (MITRE TA0008)
- Move across the network using acquired credentials.

### Collection (MITRE TA0009)
- Gather target data (files, emails, media).

### Exfiltration (MITRE TA0010)
- Extract and transfer data using secure channels.

### Impact (MITRE TA0040)
- Disrupt operations (DoS, ransomware, defacement).

### Objectives
- Financial: Ransomware and extortion.
- Reputational: Leak confidential data.
