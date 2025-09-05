# Traffic Analysis Essentials

## Network Security Overview
- **Definition**: Protects data, applications, devices, and systems connected to a network.  
- **Focus**:  
  - Authentication & Authorisation  
  - System design, operation, and management  
  - Ensures accessibility, integrity, continuity, and reliability  

---

## Base Security Control Levels
1. **Physical** – Prevents unauthorised physical access (devices, cables, locks).  
2. **Technical** – Prevents unauthorised access to data (tunnels, security layers).  
3. **Administrative** – Policies, access levels, and authentication processes.  

---

## Main Approaches
- **Access Control** → Authentication & authorisation  
- **Threat Control** → Detecting & preventing anomalies/malicious activities  

---

## Access Control Elements
- **Firewall Protection** – Filters traffic, blocks suspicious traffic.  
- **Network Access Control (NAC)** – Checks device compliance before access.  
- **Identity & Access Management (IAM)** – Manages user/asset identities.  
- **Load Balancing** – Distributes tasks to optimize resources.  
- **Network Segmentation** – Isolates groups/assets to improve protection.  
- **VPN (Virtual Private Network)** – Encrypted communication, often for remote access.  
- **Zero Trust Model** – “Never trust, always verify”; minimum required access.  

---

## Threat Control Elements
- **IDS/IPS** – Detects (IDS) or blocks (IPS) anomalous traffic.  
- **DLP (Data Loss Prevention)** – Inspects traffic to prevent sensitive data leaks.  
- **Endpoint Protection** – Secures devices (antivirus, encryption, IDS/IPS).  
- **Cloud Security** – Protects cloud resources with VPNs, encryption, etc.  
- **SIEM** – Threat detection & compliance via log/event analysis.  
- **SOAR** – Automates and coordinates security tasks.  
- **Network Traffic Analysis (NTA) / NDR** – Identifies anomalies through traffic inspection.  

---

## Typical Network Security Management
- **Deployment**: Device/software installation  
- **Configuration**: Policies, NAT, VPN, automation  
- **Management**: Threat mitigation, access config  
- **Monitoring**: System, user activity, logs, threats  
- **Maintenance**: Updates, rule adjustments, licenses  

---

## Managed Security Services (MSS)
- **Reason**: Cost, skillset, organisation size → outsourcing  
- **Providers**: MSSPs (Managed Security Service Providers)  
- **Common MSS Elements**:  
  - Network Penetration Testing  
  - Vulnerability Assessment  
  - Incident Response  
  - Behavioural Analysis (baseline traffic, detect anomalies)  

---

## Traffic Analysis (Network Traffic Analysis)
- **Definition**: Intercepting, monitoring, and analysing network data to detect anomalies, threats, and performance issues.  
- **Applications**: Security + operational (availability, performance).  

### Disciplines Involving Traffic Analysis
- Network Sniffing & Packet Analysis (Wireshark)  
- Network Monitoring (Zeek)  
- IDS/IPS (Snort)  
- Network Forensics (NetworkMiner)  
- Threat Hunting (Brim)  

---

## Techniques in Traffic Analysis
1. **Flow Analysis**  
   - Summary-level data from devices  
   - ✔️ Easy to collect & analyse  
   - ❌ Lacks full packet details  

2. **Packet Analysis**  
   - In-depth, full packet capture (Deep Packet Inspection - DPI)  
   - ✔️ Root cause analysis possible  
   - ❌ Requires time & expertise  

---

## Benefits of Traffic Analysis
- Full network visibility  
- Helps with asset tracking & baselining  
- Supports anomaly & threat detection  

---

## Importance Today
- Attackers evolve to bypass modern tools/cloud defenses  
- Network data remains valuable even when encrypted  
- **Still essential for security analysts**
