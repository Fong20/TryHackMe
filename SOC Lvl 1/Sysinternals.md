# Sysinternals

## Overview
- **Sysinternals Suite:** 70+ Windows tools categorized into:
  - File and Disk Utilities  
  - Networking Utilities  
  - Process Utilities  
  - Security Utilities  
  - System Information  
  - Miscellaneous
- **Creators:** Mark Russinovich & Bryce Cogswell (Wininternals Software, 1990s)  
- **Acquired by Microsoft:** 2006  
- **Mark Russinovich:** CTO of Microsoft Azure  
  - Discovered Sony rootkit (2005) and Symantec rootkit-like behavior (2006)

---

## 📦 Installation & Usage
- Download individual tools or full suite:  
  👉 [Sysinternals Utilities Index](https://docs.microsoft.com/en-us/sysinternals/downloads/)
- Run from web via **Sysinternals Live**:  
  ```
  \\live.sysinternals.com\tools\<toolname>
  ```
- Requires:
  - **WebDAV client** (running service `webclient`)
  - **Network Discovery** enabled
- Example command:
  ```
  \\live.sysinternals.com\tools\procmon.exe
  ```
- Optional setup:
  - Add Sysinternals path to `Environment Variables` for quick CLI use
  - PowerShell install:
    ```
    Download-SysInternalsTools C:\Tools\Sysint
    ```

---

## 🔍 File & Disk Utilities

### **Sigcheck**
- Checks file versions, timestamps, and digital signatures
- VirusTotal integration
- **Use Case:** Identify unsigned executables  
  ```
  sigcheck -u -e C:\Windows\System32
  ```
  - `-u`: show unsigned/unknown files  
  - `-e`: scan executable images only  

---

### **Streams**
- Views **Alternate Data Streams (ADS)** in NTFS
- Syntax: `file:stream`
- Used to detect hidden/malicious data or downloaded-from-Internet markers
- Example:
  ```
  streams SysinternalsSuite.zip
  ```

---

### **SDelete**
- Secure file deletion utility implementing **DOD 5220.22-M** wipe method
- Associated with MITRE:
  - **T1485** – Data Destruction  
  - **T1070.004** – Indicator Removal on Host  
- Example:
  ```
  sdelete -p 3 -s C:\sensitive_folder
  ```

---

## 🌐 Networking Utilities

### **TCPView**
- Displays TCP/UDP connections with owning processes (GUI)
- Command-line version: `tcpvcon`
- Similar built-in tool: **Resource Monitor (`resmon`)**
- Filtering options:
  - Toggle protocols (TCPv4/v6, UDPv4/v6)
  - Filter by connection state (e.g., exclude “Listen”)
- Example:
  ```
  tcpview
  ```

---

## ⚙️ Process Utilities

### **Autoruns**
- Lists all auto-start locations:
  - Startup folders, Run keys, Winlogon, Explorer extensions, etc.
- Useful for detecting **persistence mechanisms**
- Example:
  ```
  autoruns
  ```

---

### **ProcDump**
- Generates process dumps for analysis
- Useful for diagnosing CPU spikes or application crashes  
- Example:
  ```
  procdump -ma notepad.exe C:\Dumps\
  ```
- Alternative: right-click in **Process Explorer** → *Create Dump*

---

### **Process Explorer (ProcExp)**
- Visual replacement for Task Manager
- Shows processes, threads, DLLs, and handles
- Features:
  - Verify digital signatures
  - Replace Task Manager
  - Run at logon
- Color codes represent process types
- Example:
  ```
  procexp
  ```

---

### **Process Monitor (ProcMon)**
- Monitors real-time **file, registry, and process/thread** activity
- Combines features of Filemon + Regmon
- Capture filters essential for usability  
  - Example: monitor specific process
    ```
    Process Name = notepad.exe
    ```
- Example:
  ```
  procmon
  ```

---

### **PsExec**
- Execute commands on remote systems (no agent needed)
- Adversary tool (MITRE):
  - **T1570** – Lateral Tool Transfer  
  - **T1021.002** – Remote Services: SMB/Windows Admin Shares  
  - **T1569.002** – Service Execution  
- Example:
  ```
  psexec \\RemoteHost cmd
  ```

---

## 🔐 Security Utilities

### **Sysmon**
- Monitors and logs process creations, network connections, file time changes
- Logs to Windows Event Log
- Used for **threat detection and forensic analysis**
- Example:
  ```
  sysmon -i sysmonconfig.xml
  ```

---

## 🧩 System Information

### **WinObj**
- Views the **NT Object Manager** namespace
- Demonstrates session-level differences (Session 0 vs Session 1)
- Example:
  ```
  winobj
  ```

---

## 🧮 Miscellaneous Utilities

### **BgInfo**
- Displays system info (hostname, IP, etc.) on desktop background
- Handy for managing multiple servers
  ```
  bginfo
  ```

---

### **RegJump**
- Opens Registry Editor directly at specified key
  ```
  regjump HKLM\Software\Microsoft\Windows\CurrentVersion\Run
  ```

---

### **Strings**
- Extracts readable strings from binaries (ASCII/Unicode)
- Example:
  ```
  strings zoomit.exe | findstr zoom
  ```

---

## 💡 Real-World Usage (Security Engineer)
| Scenario | Tool Used | Purpose |
|-----------|------------|---------|
| Agent not responding | ProcExp | Inspect process & threads |
| Agent malfunction | ProcMon | Analyze registry/filesystem activity |
| Vendor debugging | ProcDump | Capture dump for analysis |

---

## 🔗 Additional Resources
- [Mark’s Blog](https://docs.microsoft.com/en-us/archive/blogs/markrussinovich/)
- [Windows Blog Archive](https://techcommunity.microsoft.com/t5/windows-blog-archive/bg-p/Windows-Blog-Archive/)
- 🎥 [License to Kill: Malware Hunting with Sysinternals Tools](https://www.youtube.com/watch?v=A_TPZxuTzBU)
- 🎥 [Malware Hunting with Mark Russinovich](https://www.youtube.com/watch?v=vW8eAqZyWeo)

---

✅ **Summary:**  
Sysinternals tools are essential for system administrators, analysts, and security engineers alike. They provide low-level visibility into processes, registry, network connections, and file operations—valuable for both troubleshooting and threat analysis.
