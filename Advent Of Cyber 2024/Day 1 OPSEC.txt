
### AOC Day 1: OPSEC
---

#### **Investigation of Malicious Link Files**
1. **Scenario Setup:**
   - Investigating a **YouTube to MP3 converter website** linked to suspicious activity.
   - Downloaded a ZIP file containing:
     - `song.mp3` (legit MP3 file)
     - `somg.mp3` (malicious shortcut file).

2. **Inspection of Files:**
   - **File Analysis:**
     - `song.mp3`: Standard audio file.
     - `somg.mp3`: Windows shortcut file (.lnk) with embedded commands.
   - **Tools Used:**
     - `file` command: Revealed file types.
     - `ExifTool`: Extracted embedded PowerShell command from `somg.mp3`.

3. **Malicious PowerShell Command:**
   - **Command Functionality:**
     - Bypasses execution policies and disables user profile restrictions.
     - Downloads a script (`IS.ps1`) from a remote server.
     - Executes the script on the victim machine.
   - **Downloaded Script Analysis:**
     - Collects sensitive data (crypto wallets, saved browser credentials).
     - Sends data to the attacker's server.

---

#### **Tracking Digital Identities**
1. **GitHub Search:**
   - Searched for unique code signature: `"Created by the one and only M.M."`
   - Found a **GitHub Issues page** where the malicious actor (MM) discussed their code.

2. **OPSEC Failures Identified:**
   - Reuse of identifiable metadata (signature in code).
   - Posting publicly in forums and on GitHub without proper anonymity.

---

#### **Introduction to OPSEC**
1. **Definition:**
   - OPSEC (Operational Security): Process of protecting sensitive information and activities.

2. **Common OPSEC Mistakes:**
   - Reusing usernames or emails across platforms.
   - Embedding identifiable metadata in files.
   - Posting publicly with traceable information.
   - Failing to use VPNs or proxies.

3. **Real-World Examples of OPSEC Failures:**
   - **AlphaBay Admin:**
     - Reused identifiable email and usernames.
     - Linked Bitcoin account to real identity.
   - **APT1 (Chinese Military Group):**
     - Predictable naming conventions.
     - Aligning activity with local business hours.
     - Linking nicknames in malware to personal accounts.

---

#### **Uncovering the Malicious Actor**
1. **Key Clues:**
   - Signature `"Created by the one and only M.M."`.
   - GitHub Issues discussion with timestamps and usernames.

2. **Attribution:**
   - Evidence tied activities to **MM** through poor OPSEC practices.
   - Enabled tracking of MM’s digital footprint, leading to identification.

---
