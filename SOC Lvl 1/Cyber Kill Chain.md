# Cyber Kill Chain

## Overview
- Cyber Kill Chain is a cybersecurity framework developed by Lockheed Martin in 2011 based on a military attack model.
- It is used to understand adversary behavior and defend against cyberattacks, including APTs, ransomware, and breaches.

---

## Attack Phases of the Cyber Kill Chain

### 1. Reconnaissance
- **Goal**: Gather intelligence on the target.
- **Techniques**:
  - OSINT (Open-Source Intelligence)
  - Email harvesting
  - Tools: 
    - `theHarvester`: Collects emails, names, IPs, URLs.
    - `Hunter.io`: Domain-associated contact info.
    - `OSINT Framework`: Category-based OSINT tools.
  - Social media analysis (LinkedIn, Facebook, etc.)

### 2. Weaponization
- **Goal**: Create a weaponized payload.
- **Components**:
  - **Malware**: Software designed to harm or exploit.
  - **Exploit**: Code exploiting vulnerabilities.
  - **Payload**: Malicious code executed on the target.
- **Examples**:
  - Malicious Office docs with macros/VBA.
  - USB-based malware delivery.
  - Custom or DarkWeb-purchased malware.

### 3. Delivery
- **Goal**: Transmit the weaponized payload to the target.
- **Methods**:
  - **Phishing (spearphishing)**: Social engineering via emails.
  - **Infected USBs**: Planted in public or mailed.
  - **Watering Hole Attack**: Compromise popular websites.
  - **Drive-by Downloads**: Malware downloaded through browsing.

### 4. Exploitation
- **Goal**: Exploit vulnerabilities for code execution.
- **Examples**:
  - User action (opening file/clicking link).
  - Zero-day exploits.
  - Server/software/human vulnerabilities.

### 5. Installation
- **Goal**: Establish persistence on the system.
- **Techniques**:
  - Web shells (`.php`, `.asp`, etc.).
  - Meterpreter backdoor (Metasploit).
  - Modify Windows services (`T1543.003`).
  - Add payloads to registry or startup folders.
  - **Timestomping**: Alter file timestamps.

### 6. Command & Control (C2)
- **Goal**: Maintain remote control of the compromised system.
- **Channels**:
  - HTTP/HTTPS (ports 80/443)
  - DNS Tunneling
  - Previously used: IRC (now outdated)

### 7. Actions on Objectives
- **Goal**: Achieve the attacker’s goals (data theft, damage, etc.)
- **Actions**:
  - Credential harvesting
  - Privilege escalation
  - Lateral movement
  - Data exfiltration
  - Deleting backups (e.g., shadow copies)
  - Data corruption or deletion

---

## Limitations of the Traditional Kill Chain

- Created in 2011, lacks updates.
- Focused primarily on perimeter defenses and malware.
- Ineffective against:
  - Insider threats
  - Modern multi-TTP attacks

---

## Recommendations

- Use Cyber Kill Chain alongside:
  - **MITRE ATT&CK**: Real-world adversary behavior mapping.
  - **Unified Kill Chain**: Combines multiple frameworks.
