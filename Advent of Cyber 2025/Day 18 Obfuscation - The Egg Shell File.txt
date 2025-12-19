# Obfuscation - The Egg Shell File

## Scenario Context
- Suspicious email posing as **northpole-hr** (fake; HR is at the South Pole).
- Email contained a tiny PowerShell file with unreadable, random-looking strings.
- Indicates **obfuscation**, a common attacker technique.

## What is Obfuscation?
- Practice of making data/code hard to read or analyze.
- Used to evade detection and slow down investigations.
- Does NOT necessarily secure data; it hides intent.

## Obfuscation vs Encoding vs Encryption
- **Encoding**: Changes format for compatibility (e.g., Base64). Easily reversible.
- **Encryption**: Protects confidentiality using a key; intended to be secure.
- **Obfuscation**: Hides meaning to avoid detection; not meant to be cryptographically secure.

## Simple Obfuscation Techniques

### ROT Ciphers
- **ROT1**: Shifts letters forward by 1.
  - Example: `carrot coins go brr` → `dbsspu dpjot hp css`
  - Spaces remain unchanged.
- **ROT13**: Shifts letters forward by 13.
  - Example: `the` → `gur`, `and` → `naq`

### XOR Obfuscation
- Each byte is XORed with a key.
- Output often contains strange or unreadable characters.
- Length stays the same as the original text.
- Not practical to reverse manually.

#### XOR Example (CyberChef)
Input:
```
carrot supremacy
```
Operation:
- XOR
- Key: `a` (HEX)

Output:
```
ikxxe~*yzxogkis!
```

## Detecting Obfuscation Patterns
- **ROT1**: Words look one letter off, spaces intact.
- **ROT13**: Common words transformed predictably (`the` → `gur`).
- **Base64**:
  - Mostly A–Z, a–z, 0–9
  - May include `+`, `/`
  - Often ends in `=` or `==`
- **XOR**:
  - Random symbols
  - Same length as input
  - Repeating patterns if key reused

## CyberChef for Deobfuscation
- Widely used tool for safe analysis.
- Apply the **reverse operation** to recover plaintext.
  - Example: `From Base64` instead of `To Base64`.

### Magic Operation
- Automatically attempts common decoders.
- Can enable **Intensive Mode** for more coverage.
- Useful for hints, not guaranteed to solve everything.

## Layered Obfuscation
- Attackers often stack multiple techniques.
- Example process:
  1. Compress with gzip
  2. XOR with key `x`
  3. Base64 encode

### Deobfuscation Order
- Always reverse the steps:
  1. Base64 decode
  2. XOR with key
  3. Decompress gzip

## Key Takeaways
- Obfuscation hides intent, not data securely.
- Pattern recognition helps identify techniques.
- CyberChef is essential for safe and effective analysis.
- Layered obfuscation requires step-by-step reversal.
