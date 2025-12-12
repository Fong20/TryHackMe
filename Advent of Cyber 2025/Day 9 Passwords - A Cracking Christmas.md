# Day 9 Passwords - A Cracking Christmas

# Key Concepts
-   Encryption strength depends heavily on password complexity.
-   Weak or common passwords can be recovered via offline guessing.
-   PDF and ZIP use different encryption/key derivation mechanisms; some
    legacy modes are weak.
-   Encryption protects confidentiality but does not prevent
    password‑guessing attempts.

## How Attackers Recover Weak Passwords

### Dictionary Attacks
-   Attackers test passwords from wordlists (e.g., rockyou.txt).
-   Very effective due to common password reuse.

### Brute‑Force / Mask Attacks
-   Try every possible combination.
-   Mask attacks reduce search space (e.g., ?l?l?l?d?d → 3 lowercase
    letters + 2 digits).

### Practical Attacker Workflow
1.  Start with general wordlists.
2.  Move to targeted wordlists.
3.  Apply mask/incremental strategies for short passwords.
4.  Use GPU acceleration when possible.

### Tools

### PDF
-   pdfcrack
-   john using pdf2john

### ZIP
-   fcrackzip
-   john using zip2john

### General
-   john, hashcat

### Sample Commands

1. Identify File Type

    file flag.pdf
    file flag.zip

2. PDF Dictionary Attack

    pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt

3. ZIP (John)

    zip2john flag.zip > ziphash.txt
    john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt

## Detection & Telemetry
-   Process creation signals: john, hashcat, pdfcrack, fcrackzip,
    zip2john, pdf2john.
-   High GPU utilisation for GPU cracking.
-   Wordlist and encrypted file read patterns.
-   Network activity: downloading wordlists/tools.

### Detection Examples

### 1. Sysmon

    (ProcessName="C:\Program Files\john\john.exe" OR
     ProcessName="C:\Tools\hashcat\hashcat.exe" OR
     CommandLine="*pdf2john.pl*" OR
     CommandLine="*zip2john*")

### 2. Linux Audit

    auditctl -w /usr/share/wordlists/rockyou.txt -p r -k wordlists_read
    auditctl -a always,exit -F arch=b64 -S execve -F exe=/usr/bin/john -k crack_exec

### 3. Sigma Rule (Windows)

    title: Password Cracking Tools Execution
    id: 9f2f4d3e-4c16-4b0a-bb3a-7b1c6c001234
    status: experimental
    ...

### Response Playbook
-   Isolate affected host.
-   Capture triage data (process list, GPU status, dumps).
-   Preserve working dir, wordlists, hashes, shell history.
-   Check decrypted files, investigate follow‑on activity.
-   Determine authorisation; escalate if needed.
-   Rotate credentials, enforce MFA.
