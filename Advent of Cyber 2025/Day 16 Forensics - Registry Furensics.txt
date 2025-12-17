# Forensics - Registry Furensics

## Scenario Overview
- TBFC system **dispatch-srv01** compromised by *King Malhare’s bandits*.
- System coordinates drone-based gift delivery for **SOCMAS**.
- Objective: Perform **registry forensics** as part of a broader incident investigation.

---

## Windows Registry Basics
- The **Windows Registry** is a centralized configuration database for the OS.
- Stores system, hardware, software, and user configuration.
- Data is stored in **binary files** called **Registry Hives**.

---

## Registry Hives

| Hive | Contains | Disk Location |
|-----|---------|---------------|
| SYSTEM | Services, drivers, hardware, boot config | `C:\Windows\System32\config\SYSTEM` |
| SECURITY | Local security & audit policies | `C:\Windows\System32\config\SECURITY` |
| SOFTWARE | Installed programs, OS info, autostarts | `C:\Windows\System32\config\SOFTWARE` |
| SAM | User accounts, password hashes, groups | `C:\Windows\System32\config\SAM` |
| NTUSER.DAT | User prefs, recent files, Run history | `C:\Users\<user>\NTUSER.DAT` |
| USRCLASS.DAT | Shellbags, Jump Lists | `C:\Users\<user>\AppData\Local\Microsoft\Windows\USRCLASS.DAT` |

---

## Registry Root Keys Mapping

| Hive on Disk | Registry Editor Path |
|-------------|---------------------|
| SYSTEM | `HKLM\SYSTEM` |
| SECURITY | `HKLM\SECURITY` |
| SOFTWARE | `HKLM\SOFTWARE` |
| SAM | `HKLM\SAM` |
| NTUSER.DAT | `HKU\<SID>` and `HKCU` |
| USRCLASS.DAT | `HKU\<SID>\Software\Classes` |

> Notes:
> - `HKCR` and `HKCC` are **not standalone hives**; they are dynamically populated.

---

## Why Registry Forensics Matters
- Registry provides evidence of:
  - User activity
  - Installed & executed programs
  - Persistence mechanisms
  - System configuration changes
- Registry analysis is performed **offline** to avoid contamination.

---

## Important Registry Keys for Forensics

| Registry Key | Evidence |
|-------------|----------|
| `HKCU\...\UserAssist` | GUI-launched applications |
| `HKCU\...\TypedPaths` | Explorer address bar paths |
| `HKCU\...\WordWheelQuery` | Explorer search terms |
| `HKCU\...\RecentDocs` | Recently accessed files |
| `HKLM\...\Run` | Startup persistence |
| `HKLM\...\App Paths` | Application install paths |
| `HKLM\SYSTEM\...\ComputerName` | Hostname |
| `HKLM\SOFTWARE\...\Uninstall` | Installed programs |

---

## Example Registry Artefacts

### USB Device History
**Path:**
```
HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR
```
**Contains:**
- USB make & model
- Device IDs
- Unique device instances

---

### Run Dialog History
**Path:**
```
HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU
```
**Contains:**
- Commands executed via `Win + R`

---

## Registry Explorer (Forensic Tool)
- Open-source registry forensic tool
- Parses binary registry data
- Allows **offline hive analysis**
- Prevents modification of original evidence

---

## Practical Workflow (dispatch-srv01)

### 1. Launch Tool
- Open **Registry Explorer** from taskbar

### 2. Load Offline Hives
- `File → Load Hive`
- Location:
  ```
  C:\Users\Administrator\Desktop\Registry Hives
  ```

### 3. Handle Dirty Hives
- Hold **SHIFT + Open**
- Replays transaction logs (`.LOG1`, `.LOG2`)
- Ensures consistent hive state

### 4. Example Investigation: Computer Name
**Path:**
```
ROOT\ControlSet001\Control\ComputerName\ComputerName
```
**Result:**
- Hostname = **DISPATCH-SRV01**

(Searchable via Registry Explorer search bar or bookmarks)

---

## Key Takeaways
- Registry = critical forensic artefact
- Hives must be analyzed **offline**
- Registry Explorer is preferred over Registry Editor
- Valuable timeline and persistence evidence exists in registry keys
