
## AOC Day 23: Hash cracking

## Learning Objectives
- Understanding hash functions and hash values.
- Techniques for saving hashed passwords.
- Methods for cracking hashes.
- Approaches for accessing password-protected documents.


---

### **Hashed Passwords**
1. **Password Storage History**: 
   - Initially stored in plaintext (e.g., "ASDF1234").
   - This is insecure as databases can be stolen or leaked.

2. **Modern Practices**:
   - **Hash Functions**: Converts passwords to a fixed-size value. Example: `SHA-256`.
     - Example command: `sha256sum FILE_NAME`.
   - **Salting**: Adding a random string to passwords before hashing:
     - Example: `hash(password + salt)`.
   - Protects against database breaches and common attack vectors.

3. **Issues**:
   - Outdated or weak hash algorithms (e.g., MD5).
   - Poor implementation or lack of security practices.

---

### **Password-Protected Files**
1. **Importance**: Protecting data at rest (e.g., encrypted disks/files).
2. **Use Case**: Investigators (like Glitch) may need to bypass encryption for forensic purposes.

---

### **Cracking Hashed Passwords**
#### **Step 1: Identify the Hash Type**
- Use tools like `hash-id.py`.
  - Example: `python hash-id.py` outputs potential hash types.

#### **Step 2: Attempt to Crack the Hash**
- **Tools**: Use `john` (John the Ripper).
- **Commands**:
  - Simple attempt:  
    ```bash
    john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt
    ```
  - Enhanced with rules:  
    ```bash
    john --format=raw-sha256 --rules=wordlist --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt
    ```
  - Show cracked passwords:  
    ```bash
    john --format=raw-sha256 --show hash1.txt
    ```

---

### **Cracking Password-Protected PDF**
#### **Step 1: Generate PDF Hash**
- Use `pdf2john` to extract the hash from a PDF file:
  ```bash
  pdf2john.pl private.pdf > pdf.hash
  ```

#### **Step 2: Custom Wordlist**
- Personalized wordlists can improve success rates.
  - Example custom wordlist (`wordlist.txt`):
    ```
    Fluffy
    FluffyCat
    Mayor
    Malware
    MayorMalware
    ```

#### **Step 3: Crack with John**
- Command with custom wordlist and rules:
  ```bash
  john --rules=single --wordlist=wordlist.txt pdf.hash
  ```

---

### **Common Passwords**
- **Top Choices**: "123456", "password", "12345678", "qwerty", etc.
- **Tips**: Users often modify common passwords slightly (e.g., adding numbers/symbols).

---

### **Practical Example Summary**
1. Identify the hash type of a given password.
2. Use wordlists and rules with `john` to crack hashes.
3. For password-protected files, generate a hash and use targeted wordlists to find the password.

---

### Saved Code and Steps:
1. **Identify Hash Type**:
   ```bash
   python hash-id.py
   ```

2. **Crack with RockYou Wordlist**:
   ```bash
   john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash1.txt
   ```

3. **Create and Use Custom Wordlist**:
   Save the following as `wordlist.txt`:
   ```
   Fluffy
   FluffyCat
   Mayor
   Malware
   MayorMalware
   ```
   Use with `john`:
   ```bash
   john --rules=single --wordlist=wordlist.txt pdf.hash
   ```
