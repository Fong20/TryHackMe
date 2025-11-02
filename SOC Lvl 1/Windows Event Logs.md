# Windows Event Logs 

## Definition of Event Logs
- Event logs record system and application events for auditing, troubleshooting, and diagnostics.
- Essential for system administrators, IT technicians, and blue teamers.
- Combine logs from multiple sources → detect correlations using SIEMs (e.g., Splunk, Elastic).

## SIEM Overview
- SIEM (Security Information and Event Management) tools collect, normalize, and analyze logs.
- Key capabilities:
  - Threat detection
  - Investigation
  - Response

## Windows Event Logs
- Stored in binary format (.evt or .evtx).
- Location: C:\Windows\System32\winevt\Logs
- Can be converted to XML via the Windows API.

### Types of Windows Event Logs
| Log Type | Description |
|-----------|--------------|
| System | OS-related events (hardware, drivers, updates). |
| Security | Logon/logoff and audit events. |
| Application | Logs from installed apps. |
| Directory Service | AD changes and activities. |
| File Replication Service | Group Policy and logon script replication. |
| DNS | DNS server-related logs. |
| Custom | Logs from specific apps requiring custom data or ACLs. |

### Windows Event Log Types
- Information
- Warning
- Error
- Success Audit
- Failure Audit

### Accessing Windows Event Logs
1. Event Viewer (GUI-based)
2. Wevtutil.exe (CLI)
3. Get-WinEvent (PowerShell)

---

## Event Viewer

**Launch:**
- GUI: Right-click Start → Event Viewer  
- CLI: `eventvwr.msc`

**Structure:**
- Left pane: Hierarchical tree of log providers.  
- Middle pane: Displays logs for the selected provider.  
- Right pane: Action options.

**Key Functions:**
- View properties (location, size, rotation policy).
- Clear Logs (used by admins or attackers to cover tracks).
- Filter Current Log and Create Custom View.
- Connect to Another Computer to view remote logs.

---

## Command-Line: wevtutil.exe

**Purpose:**
- Retrieve, export, archive, or clear logs.
- Manage publishers and manifests.

**Help Command:**
```powershell
wevtutil.exe /?
```

**Common Commands:**
| Command | Full Name | Description |
|----------|------------|-------------|
| el | enum-logs | List log names. |
| gl | get-log | Get log configuration. |
| sl | set-log | Modify log configuration. |
| ep | enum-publishers | List event publishers. |
| gp | get-publisher | Get publisher info. |
| qe | query-events | Query events. |
| epl | export-log | Export logs. |
| cl | clear-log | Clear logs. |

**Common Options:**
```powershell
/r:REMOTEPC       # Run on remote machine
/u:USERNAME       # Specify user
/p:PASSWORD       # Specify password
/a:AUTHMETHOD     # Auth type (Negotiate, Kerberos, NTLM)
```

**Example Query:**
```powershell
wevtutil qe Application /q:"*/System[EventID=100]" /f:text /c:1
```

---

## PowerShell Cmdlet: Get-WinEvent

**Purpose:**
- Get events from local/remote computers.
- Supports XPath and FilterHashtable for filtering.

**Examples:**

### 1. Get All Logs
```powershell
Get-WinEvent -ListLog *
```

### 2. Get Event Providers
```powershell
Get-WinEvent -ListProvider *
```

### 3. Filter Using Where-Object
```powershell
Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }
```

### 4. Filter Using FilterHashtable
```powershell
Get-WinEvent -FilterHashtable @{
  LogName='Application'
  ProviderName='WLMS'
}
```

**Hash Table Syntax:**
```powershell
@{ <name> = <value>; [<name> = <value> ] ...}
```

---

## Filtering with XPath

**XPath Syntax Example:**
```xpath
*[System[(Level <= 3) and TimeCreated[timediff(@SystemTime) <= 86400000]]]
```

**Event ID Query:**
```powershell
Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=100'
```

**Provider Query:**
```powershell
Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"]'
```

**Combined Query:**
```powershell
Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=101 and */System/Provider[@Name="WLMS"]'
```

**Querying EventData:**
```powershell
Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="System"' -MaxEvents 1
```

---

## Event ID Resources

| Source | Description |
|--------|--------------|
| Windows Logging Cheat Sheet (2016) | Event IDs for Accounts, Processes, etc. |
| NSA: Spotting the Adversary | Concepts and event ID monitoring. |
| MITRE ATT&CK (T1098) | Detection and mitigation examples. |
| Microsoft Docs | "Events to Monitor" and "Security Auditing & Monitoring Reference". |

---

## Additional Logging Features

### Enable PowerShell Logging
Path: `Local Computer Policy > Computer Configuration > Administrative Templates > Windows Components > Windows PowerShell`

### Enable Audit Process Creation
Path: `Local Computer Policy > Computer Configuration > Administrative Templates > System > Audit Process Creation`
- Generates Event ID 4688 (process creation logs).

---

## Further Reading
- EVTX Attack Samples
- PowerShell ❤️ Blue Team
- Tampering with Windows Event Tracing
- Microsoft Docs on:
  - Get-WinEvent
  - Wevtutil
  - XPath Reference
  - PowerShell Logging
  - Process Creation Auditing

---

## Summary
- Event Logs: Vital for incident response and auditing.  
- SIEMs: Aggregate logs for detection & correlation.  
- wevtutil.exe / Get-WinEvent: Core tools for log querying.  
- XPath & FilterHashtable: Advanced filtering for efficient log analysis.  
- Enable extra logging: PowerShell & Process Creation for richer telemetry.
