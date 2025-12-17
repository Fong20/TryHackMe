
# Web Attack Forensics - Drone Alone

## Overview
Splunk alerts indicated unusual Apache behavior: long HTTP requests containing Base64 payloads that triggered suspicious process creation. Investigation focused on correlating Apache web logs with Sysmon host telemetry to identify command injection, payload execution, and attacker activity.

---

## Step 1: Detect Suspicious Web Commands (Apache Access Logs)

**Splunk Query**
```
index=windows_apache_access (cmd.exe OR powershell OR "powershell.exe" OR "Invoke-Expression")
| table _time host clientip uri_path uri_query status
```

**Purpose**
Identify possible command injection attempts via HTTP parameters (e.g., vulnerable CGI script `hello.bat`).

**Key Finding**
- HTTP requests contained long Base64-encoded PowerShell strings.
- Example encoded string:
```
VABoAGkAcwAgAGkAcwAgAG4AbwB3ACAATQBpAG4AZQAhACAATQBVAEEASABBAEEASABBAEEA
```

**Decoded Payload**
Using base64 decoding:
```
This is now Mine! MUAHHAHAHA
```

**Assessment**
Confirms attacker testing code execution via encoded PowerShell commands.

---

## Step 2: Apache Error Logs – Execution Evidence

**Splunk Query**
```
index=windows_apache_error ("cmd.exe" OR "powershell" OR "Internal Server Error")
```

**Purpose**
Detect backend execution failures or errors caused by malicious input.

**Key Finding**
- Requests like `/cgi-bin/hello.bat?cmd=powershell` triggered HTTP 500 errors.

**Assessment**
Indicates attacker input reached server-side execution logic, suggesting partial or failed exploitation attempts.

---

## Step 3: Trace Suspicious Process Creation (Sysmon)

**Splunk Query**
```
index=windows_sysmon ParentImage="*httpd.exe"
```

**Purpose**
Identify processes spawned by Apache (httpd.exe).

**Key Finding**
```
ParentImage: C:\Apache24\bin\httpd.exe
Image:       C:\Windows\System32\cmd.exe
```

**Assessment**
Apache should not spawn system shells. This confirms successful command injection and OS-level compromise.

---

## Step 4: Confirm Attacker Enumeration

**Splunk Query**
```
index=windows_sysmon *cmd.exe* *whoami*
```

**Purpose**
Detect post-exploitation reconnaissance.

**Key Finding**
- Execution of `whoami` via cmd.exe.

**Assessment**
Attacker confirmed execution context and privileges, validating interactive command execution on the host.

---

## Step 5: Identify Encoded PowerShell Payloads

**Splunk Query**
```
index=windows_sysmon Image="*powershell.exe"
(CommandLine="*enc*" OR CommandLine="*-EncodedCommand*" OR CommandLine="*Base64*")
```

**Purpose**
Detect obfuscated PowerShell execution.

**Key Finding**
- No successful encoded PowerShell execution observed.

**Assessment**
Payloads were likely tested but not fully executed, limiting attacker impact.

---

## Final Assessment – Scope & Impact

- **Attack Vector:** Web-based command injection via Apache CGI.
- **Evidence of Compromise:** Apache spawning `cmd.exe`, execution of `whoami`.
- **Payload Analysis:** Base64-encoded PowerShell used for obfuscation.
- **Impact Scope:** Single web server host compromised at OS level.
- **Attacker Intent:** Reconnaissance and proof-of-access rather than full malware deployment.

---

## Recommendations
- Patch or disable vulnerable CGI scripts.
- Implement strict input validation.
- Restrict Apache from spawning system shells.
- Enhance detection for encoded PowerShell and unusual parent-child process relationships.
