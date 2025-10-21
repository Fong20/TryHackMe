# Core Windows Processes 

## 🪟 Purpose of This Room
- Understand **normal Windows process behavior** to identify malicious activity.
- Foundational for defenders (SOC Analysts, Detection Engineers, Threat Hunters).
- Antivirus alone is no longer sufficient — layered defense is key (AV + EDR + analyst knowledge).

---

## ⚙️ Task Manager Overview
- Access via **Right-click Taskbar → Task Manager**.
- Use “**More details**” for full view.
- Tabs: *Processes, Performance, App history, Startup, Users, Details, Services*.
- Add columns like:
  - **Type**, **Publisher**, **PID**, **Command line**, **CPU**, **Memory**.
- Useful for spotting **outlier processes** by comparing:
  - Image path name
  - Command line arguments
- **Limitations:** Task Manager does *not* show parent-child process relationships.

**Alternatives:**  
- **Process Hacker**
- **Process Explorer**  
→ Both show parent-child hierarchies, verified signatures, and more details.

---

## ⚙️ Command-Line Equivalents
- `tasklist`
- PowerShell: `Get-Process` or `ps`
- `wmic process list full`

---

## 🧩 Core Windows Processes

### 1. System (PID 4)
**Function:** Kernel-mode system threads.  
**Normal:**
- PID = 4 (always)
- Image Path: `C:\Windows\system32\ntoskrnl.exe`
- Parent: `System Idle Process (0)`
- User: `Local System`
- Start: At boot time  
**Abnormal:**
- Parent process other than Idle (0)
- PID ≠ 4
- Multiple instances
- Not running in Session 0

---

### 2. smss.exe (Session Manager Subsystem)
**Function:** Creates user sessions, starts csrss.exe and wininit.exe.  
**Normal:**
- Image Path: `%SystemRoot%\System32\smss.exe`
- Parent: System
- Instances: 1 master + temporary child per session (self-terminating)
- User: Local System
- Start: Seconds after boot  
**Abnormal:**
- Different parent
- Image path ≠ System32
- Multiple persistent instances
- Non-SYSTEM user
- Unexpected Subsystem registry entries

---

### 3. csrss.exe (Client Server Runtime Process)
**Function:** Handles Win32 subsystem, console windows, process/thread creation.  
**Normal:**
- Path: `%SystemRoot%\System32\csrss.exe`
- Parent: smss.exe (which exits)
- Instances: 2+ (Session 0 & 1)
- User: Local System
- Start: Seconds after boot  
**Abnormal:**
- Active parent process (should terminate)
- Path ≠ System32
- Misspelling (e.g., *crss.exe*)
- Non-SYSTEM user

---

### 4. wininit.exe (Windows Initialization Process)
**Function:** Starts services.exe, lsass.exe, lsaiso.exe.  
**Normal:**
- Path: `%SystemRoot%\System32\wininit.exe`
- Parent: smss.exe (self-terminates)
- Instances: 1
- User: Local System
- Start: Boot time  
**Abnormal:**
- Active parent
- Path ≠ System32
- Misspellings
- Multiple instances
- Not SYSTEM user

---

### 5. services.exe (Service Control Manager)
**Function:** Manages system services, device drivers, and LastKnownGood config.  
**Normal:**
- Path: `%SystemRoot%\System32\services.exe`
- Parent: wininit.exe
- Instances: 1
- User: Local System
- Start: Boot time  
**Abnormal:**
- Parent ≠ wininit.exe
- Path ≠ System32
- Misspelling (e.g., *servics.exe*)
- Multiple instances
- Not SYSTEM user

---

### 6. svchost.exe (Service Host)
**Function:** Hosts Windows services (DLL-based).  
**Registry path:** `HKLM\SYSTEM\CurrentControlSet\Services\<ServiceName>\Parameters\ServiceDLL`  
**Normal:**
- Path: `%SystemRoot%\System32\svchost.exe`
- Parent: services.exe
- Instances: Multiple
- User: SYSTEM / Network Service / Local Service
- Start: Boot or later
- Binary Path includes “-k” parameter (service group)
**Abnormal:**
- Parent ≠ services.exe
- Path ≠ System32
- Misspelling (*scvhost.exe*)
- Missing “-k” parameter

---

### 7. lsass.exe (Local Security Authority Subsystem Service)
**Function:** Enforces system security, manages authentication and tokens.  
**Normal:**
- Path: `%SystemRoot%\System32\lsass.exe`
- Parent: wininit.exe
- Instances: 1
- User: Local System
- Start: Boot time  
**Abnormal:**
- Parent ≠ wininit.exe
- Path ≠ System32
- Misspelling (*lsaas.exe*, *1sass.exe*)
- Multiple instances
- Not SYSTEM user

---

### 8. winlogon.exe (Windows Logon)
**Function:** Handles logon (Ctrl+Alt+Del), loads user profile and shell.  
**Normal:**
- Path: `%SystemRoot%\System32\winlogon.exe`
- Parent: smss.exe (self-terminates)
- Instances: 1+ (per logon session)
- User: Local System
- Start: Boot time  
**Abnormal:**
- Active parent process
- Path ≠ System32
- Misspellings
- Not SYSTEM user
- Shell registry value ≠ `explorer.exe`

---

### 9. explorer.exe (Windows Explorer)
**Function:** User interface (taskbar, file explorer, start menu).  
**Normal:**
- Path: `%SystemRoot%\explorer.exe`
- Parent: userinit.exe (exits)
- Instances: One per logged-in user
- User: Logged-in user
- Start: User logon  
**Abnormal:**
- Active parent
- Path ≠ `C:\Windows`
- Running as unknown user
- Misspellings (*explorrer.exe*)
- Outbound TCP/IP connections

---

## 🧱 Additional Windows 10+ Core Processes
- **lsaiso.exe** — works with lsass.exe (Credential Guard)
- **RuntimeBroker.exe** — manages app permissions for UWP apps
- **taskhostw.exe** — hosts background Windows tasks

---

## 🔍 Key Takeaways
- Know **normal process behavior** (path, parent, privileges, timing, count).
- Watch for **misspellings**, **wrong paths**, **unexpected parents**, or **extra instances**.
- **Task Manager** = basic view  
  **Process Hacker / Explorer** = deeper analysis (tree view, signatures, network activity).
- Understanding this baseline is critical for detecting process-based attacks.

---
