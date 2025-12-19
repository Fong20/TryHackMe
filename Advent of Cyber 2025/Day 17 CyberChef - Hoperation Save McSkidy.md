# CyberChef - Hoperation Save McSkidy

## Story Context
- McSkidy is imprisoned in **King Malhare's Quantum Warren**
- **Sir BreachBlocker III** implemented 5 locks
- Locks are broken via:
  - Base64-encoded chat (“Bunnygram”)
  - Guard interaction
  - HTTP headers
  - Login logic (Debugger tab)
  - CyberChef recipes

---

## Core Concepts

### Encoding vs Encryption
| Encoding | Encryption |
|--------|------------|
| Compatibility | Security |
| Standardized | Algorithm + Key |
| No confidentiality | Confidential |
| Fast | Slower |
| Example: Base64 | Example: TLS |

### Decoding
- Reverses encoding back to original data

---

## CyberChef Basics
- **Operations**: Tools (Base64, XOR, ROT, etc.)
- **Recipe**: Chained operations
- **Input / Output**: Data in → result out

Example:
- Input: `IamRoot`
- To Base64 → From Base64 → original string

---

## Web Inspection Tips
- **Elements**: Guard name hints
- **Network tab**: HTTP headers (magic question, recipe ID)
- **Debugger tab**: Login logic & comments

---

## Lock Breakdown

### 🔐 Lock 1 – Outer Gate
**Logic**
- Username: Base64(Guard Name)
- Password: Base64

**Steps**
1. Find guard name → Base64 encode → username
2. Magic Question (header):
   - "What is the password for this level?" → Base64
3. Send encoded question in chat
4. Guard replies with Base64(password)
5. Decode once → plaintext password

**CyberChef**
```
From Base64
```

---

### 🔐 Lock 2 – Double Encoding
**Logic**
- Password encoded twice in Base64

**Steps**
1. Guard name → Base64 → username
2. Magic Question:
   - "Did you change the password?" → Base64
3. Guard reply → decode Base64 twice

**CyberChef**
```
From Base64
From Base64
```

---

### 🔐 Lock 3 – XOR + Base64
**Logic**
- Password XORed with key, then Base64 encoded
- XOR Key: `cyberchef`

**Steps**
1. Ask guard for password (short message)
2. Reverse process

**CyberChef**
```
From Base64
XOR (key: cyberchef)
```

**XOR Property**
- XOR(data, key) XOR key = original data

---

### 🔐 Lock 4 – MD5 Hash
**Logic**
- Password hashed with MD5

**Steps**
1. Decode guard message → MD5 hash
2. Use **CrackStation**
3. Retrieve plaintext password

---

### 🔐 Lock 5 – Dynamic Recipe
**Logic**
- Determined by Recipe ID in HTTP header

| Recipe ID | Reverse Logic |
|---------|----------------|
| 1 | From Base64 → Reverse → ROT13 |
| 2 | From Base64 → From Hex → Reverse |
| 3 | ROT13 → From Base64 → XOR(key) |
| 4 | ROT13 → From Base64 → ROT47 |

**Steps**
1. Get guard name → Base64
2. Get recipe ID from headers
3. Build matching CyberChef recipe
4. Decode password

---

## Key Takeaways
- Base64 is reversible and not secure
- XOR is reversible with the same key
- Hashes (MD5) require cracking, not decoding
- HTTP headers often leak critical info
- CyberChef chaining is essential

---

## Outcome
✅ All 5 locks breached  
🎉 McSkidy escapes safely
