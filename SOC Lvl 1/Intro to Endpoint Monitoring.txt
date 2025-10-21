# Intro to Endpoint Monitoring 

## Overview
**Goal:** Understand endpoint security monitoring fundamentals, tools, and methodology to identify and remediate malicious activity on endpoints.

---

## 1. Endpoint Security Fundamentals

### Core Windows Processes
**Purpose:** Understand how Windows operates to identify outliers.

**Tool:** **Task Manager**
- GUI utility to view running processes and resource usage.
- Can terminate unresponsive processes.

**Normal Process Hierarchy:**
```
System
System > smss.exe
csrss.exe
wininit.exe
wininit.exe > services.exe
wininit.exe > services.exe > svchost.exe
lsass.exe
winlogon.exe
explorer.exe
```
> Note: Only “System” should have “System Idle Process (0)” as parent.

---

## 2. Sysinternals Suite
A collection of **70+ Windows-based tools** for system investigation.

### Categories:
- File & Disk Utilities  
- Networking Utilities  
- Process Utilities  
- Security Utilities  
- System Information  
- Miscellaneous  

### Key Tools:
#### a. **TCPView** (Networking Utility)
- Displays TCP/UDP endpoints, local/remote addresses, and connection states.
- Lists processes owning each endpoint.
- Command-line version: **Tcpvcon**.

#### b. **Process Explorer** (Process Utility)
- Two-pane display:
  - **Top:** Active processes & owning accounts.
  - **Bottom:** Handles or DLLs (depending on mode).
- Shows:
  - Associated services
  - Network traffic invoked
  - Open handles
  - Loaded DLLs and memory-mapped files

---

## 3. Endpoint Logging and Monitoring

### Windows Event Logs
- Stored as `.evt` / `.evtx` in `C:\Windows\System32\winevt\Logs`
- Access methods:
  - **Event Viewer** (GUI)
  - **wevtutil.exe** (CLI)
  - **Get-WinEvent** (PowerShell cmdlet)
- Binary format; can be parsed via XML using Windows API.

---

### Sysmon (System Monitor)
- Part of Sysinternals suite.
- Provides **detailed, granular** event logging.
- Captures **27 event types** (e.g., process creation, network connections).
- Works with SIEMs for correlation and visualization.
- Configurable via XML (e.g., SwiftOnSecurity config).

---

### Osquery
- **Open-source** endpoint querying tool (by Facebook).
- Uses **SQL syntax** to query system data.
- Works on Windows, Linux, macOS, FreeBSD.
- **Interactive shell:** `osqueryi`

**Example:**
```sql
osquery> select pid,name,path from processes where name='lsass.exe';
+-----+-----------+-------------------------------+
| pid | name      | path                          |
+-----+-----------+-------------------------------+
| 748 | lsass.exe | C:\Windows\System32\lsass.exe |
+-----+-----------+-------------------------------+
```

**Fleet Management:**  
- **Kolide Fleet** enables querying multiple endpoints via web UI.

---

### Wazuh
- **Open-source EDR** (Endpoint Detection & Response).
- Operates via **manager-agent** architecture.
- Functions:
  - Vulnerability auditing
  - Suspicious activity monitoring
  - Data visualization
  - Behavioral baselining
- Suitable for all scales of deployment.

---

## 4. Endpoint Log Analysis

### Event Correlation
- Connects artefacts from multiple log sources (e.g., Sysmon, Firewall).
- Example attributes:
  - Source/Destination IP & Port
  - Protocol
  - Action Taken
  - Process Name
  - User Account
  - Machine Name

**Purpose:** Build a full picture of an incident by correlating multiple artefacts.

---

### Baselining
- Defines **normal behavior** to detect anomalies.
- Requires data on:
  - User activity
  - Network traffic
  - Running processes

**Examples:**

| Baseline | Unusual Activity |
|-----------|------------------|
| Employees in London (9 AM–6 PM) | VPN login from Singapore at 3 AM |
| 1 workstation per employee | User authenticates to multiple devices |
| Access only to approved sites | Upload of 3GB file to Google Drive |
| Only Microsoft apps allowed | `firefox.exe` running on multiple systems |

**Purpose:** Quickly distinguish benign vs. malicious activity.

---

## 5. Key Takeaways
- **Baseline documentation** helps distinguish malicious events.  
- **Event correlation** provides a full investigative context.  
- **Artefact tracking** is critical for remediation.  
- **Cross-asset inspection** ensures complete mitigation.

---

## Summary of Covered Concepts
| Area | Key Topics |
|------|-------------|
| **Endpoint Security Fundamentals** | Core Windows Processes, Sysinternals |
| **Endpoint Logging & Monitoring** | Windows Event Logs, Sysmon, Osquery, Wazuh |
| **Endpoint Log Analysis** | Baselining, Event Correlation |

---

✅ **End of Notes: Endpoint Security Monitoring Fundamentals**
