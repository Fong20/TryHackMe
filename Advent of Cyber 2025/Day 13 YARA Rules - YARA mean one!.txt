# YARA Rules - YARA mean one!

## Scenario Overview
- McSkidy disappeared but sent help via **images with hidden messages**.
- Blue team must:
  - Create a **YARA rule**.
  - Run it on a directory of images.
  - Detect a **keyword followed by a code word**.
  - Extract all code words in **ascending order** to decode the message.

---

## Learning Objectives
- Understand what YARA is and why it’s used.
- Learn different YARA rule types.
- Write YARA rules.
- Detect malicious indicators practically with YARA.

---

## What is YARA?
- A pattern-matching tool used to **identify and classify malware**.
- Searches files, memory, or data for:
  - Text strings
  - Byte patterns
  - Regular expressions
- Often described as a **signature-based hunting tool**.

---

## Why YARA Matters
Use cases:
- Post-incident analysis
- Threat hunting
- Intelligence-based scans
- Memory analysis

Key advantages:
- Speed
- Flexibility
- Analyst control
- Shareable rules
- Better visibility into attacks

---

## YARA Rule Structure

```yara
rule RULE_NAME
{
    meta:
        author = ""
        description = ""
        date = ""

    strings:
        $s1 = "example"
        $s2 = { 4D 5A }

    condition:
        any of them
}
```

### Sections
- **meta**: Documentation (optional but recommended)
- **strings**: Indicators to search for
- **condition**: Logic that triggers the rule

---

## String Types

### 1. Text Strings
```yara
$xmas = "Christmas"
```

Common modifiers:
- `nocase` – case-insensitive
- `wide` / `ascii` – Unicode vs ASCII
- `xor` – XOR-obfuscated strings
- `base64` / `base64wide` – encoded strings

Examples:
```yara
$hidden = "Malhare" xor
$b64 = "SOC-mas" base64
```

---

### 2. Hexadecimal Strings
Used for binary patterns.

```yara
$mz = { 4D 5A }   // PE header
```

Supports wildcards:
- `??` – any byte

---

### 3. Regular Expressions
Used for variable patterns.

```yara
$url = /http:\/\/.*malhare.*/ nocase
```

Useful for:
- URLs
- Encoded commands
- Changing filenames

---

## Conditions

Common conditions:
```yara
$xmas
any of them
all of them
```

Logical operators:
```yara
($s1 or $s2) and not $benign
```

File property checks:
```yara
any of them and filesize < 700KB
```

---

## Practical Example – IcedID Detection

```yara
rule TBFC_Simple_MZ_Detect
{
    meta:
        author = "TBFC SOC L2"
        description = "IcedID Rule"
        date = "2025-10-10"
        confidence = "low"

    strings:
        $mz   = { 4D 5A }
        $hex1 = { 48 8B ?? ?? 48 89 }
        $s1   = "malhare" nocase

    condition:
        all of them and filesize < 10485760
}
```

---

## Running YARA

Command:
```bash
yara -r icedid_starter.yar C:\
```

Useful flags:
- `-r` : recursive directory scan
- `-s` : show matched strings

---

## Key Takeaway
YARA empowers defenders to:
- Proactively hunt threats
- Detect obfuscated malware
- Define their own detection logic
- Respond faster during incidents
