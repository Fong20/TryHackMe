
# Notes: Hashing Basics  

## **What is a Hash?**
- **Definition**: A hash value is a fixed-size string of characters computed by a hash function, which takes an arbitrary input size and produces a fixed-length output.  
- **Key Characteristics**:
  - No encryption key is involved.
  - It's computationally impractical to reverse the process (input cannot be derived from the output).  
  - A small change in input causes a significant change in output.  

## **Hash Function Examples**
- **ASCII Example**:
  - Input: Letter "T" → Hex: 54 (Binary: 01010100).  
  - Input: Letter "U" → Hex: 55 (Binary: 01010101).  
  - Despite differing by one bit, their hash outputs (MD5, SHA1, SHA256) differ significantly.

### **Terminal Example**:
```bash
md5sum *.txt
# Outputs:
b9ece18c950afbfa6b0fdbfa4ff731d3 file1.txt
4c614360da93c0a041b22e537de151eb file2.txt
```

---

## **Why is Hashing Important?**
1. **Data Integrity**: Ensures data hasn't been altered.  
2. **Password Security**: Protects stored passwords by hashing them instead of storing in plaintext.  

### **Password Security**
- Servers store hashed passwords, not plaintext passwords.  
- When logging in, the hash of the entered password is compared to the stored hash.  

---

## **Hash Collisions**
- Occurs when two different inputs produce the same hash output.
- **Cause**: The pigeonhole effect (limited output values, unlimited input).  
- **Mitigation**: Use strong hashing algorithms.  

**Examples of Broken Algorithms**:
- MD5 and SHA1 are considered insecure due to engineered hash collisions.

---

## **Insecure Password Storage Practices**
1. **Storing Passwords in Plaintext**:
   - Example: RockYou breach exposed 14M plaintext passwords.  
   ```bash
   wc -l rockyou.txt  # 14,344,392 passwords
   ```

2. **Using Deprecated Encryption**:
   - Example: Adobe breach used outdated encryption methods, exposing plaintext passwords.  

3. **Using Weak Hashing Algorithms**:
   - Example: LinkedIn (2012) used SHA1 without salting, making passwords easier to crack.  

---

## **Improving Password Storage**
- **Process**:
  1. Select a secure hashing algorithm (e.g., Argon2, Bcrypt, Scrypt).  
  2. Add a unique salt to the password.  
  3. Concatenate password and salt, hash the result.  
  4. Store the hash and salt.  

- **Why Not Encrypt Passwords?**
  - Encryption requires storing a key; if the key is compromised, all passwords are exposed.

---

## **Hash Cracking**
- **Tools**:  
  - **Hashcat**: GPU-based hash cracking.  
  - **John the Ripper**: CPU-based hash cracking.

- **Hashcat Syntax**:
  ```bash
  hashcat -m <hash_type> -a <attack_mode> hashfile wordlist
  ```
  Example:
  ```bash
  hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
  ```

---

## **Salting**
- **Definition**: Adding a random value (salt) to the password before hashing to prevent rainbow table attacks.  
- **Salt Characteristics**:
  - Unique per user.  
  - Stored alongside the hash.  

---

## **Hashing on Linux**
- Passwords are stored in `/etc/shadow` in the format:
  ```
  $prefix$options$salt$hash
  ```
  - Example: `$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4`
    - `$y$` → Algorithm: yescrypt.
    - `j9T` → Parameters.
    - `76UzfgEM5PnymhQ7TlJey1` → Salt.
    - `/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4` → Hash value.

---

## **Other Uses of Hashing**
1. **Integrity Checking**: Verify file integrity using hash values (e.g., `sha256sum`).
2. **Finding Duplicates**: Compare file hashes to detect duplicate files.
3. **HMAC (Keyed-Hash Message Authentication Code)**:
   - Ensures both authenticity (via secret key) and integrity (via hashing).

---

## **Encoding vs. Encryption vs. Hashing**
- **Encoding**: Converts data to a compatible format (e.g., Base64). Reversible.  
- **Encryption**: Protects confidentiality using a cipher and key. Reversible with key.  
- **Hashing**: One-way process to generate a fixed-size digest. Irreversible.  

---
