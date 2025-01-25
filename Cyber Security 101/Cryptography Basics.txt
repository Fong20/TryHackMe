
# Cryptography Basics

## **Purpose of Cryptography**
- Ensures **secure communication** in the presence of adversaries by protecting:
  - **Confidentiality**: Preventing unauthorized disclosure.
  - **Integrity**: Ensuring the data is not altered.
  - **Authenticity**: Verifying the identity of communicators.

---

## **Applications of Cryptography**
- **Encrypted logins**: Protect credentials during transmission.
- **SSH connections**: Create encrypted tunnels.
- **Online banking**: Verify server authenticity using certificates.
- **File verification**: Use hash functions to ensure file integrity.
- **Compliance Standards**:
  - PCI DSS (for payment data): Encryption in storage and transmission.
  - Medical records: Standards like HIPAA (USA), GDPR (EU), DPA (UK).

---

## **Key Terms**
- **Plaintext**: Readable data before encryption.
- **Ciphertext**: Scrambled data after encryption.
- **Cipher**: Algorithm for encrypting and decrypting data.
- **Key**: Secret string used in the encryption/decryption process.
- **Encryption**: Converting plaintext into ciphertext.
- **Decryption**: Converting ciphertext back into plaintext.

---

## **Caesar Cipher**
- **Algorithm**: Shifts each letter by a fixed number (e.g., Key = 3).
  - Example: Plaintext = "TRYHACKME", Ciphertext = "WUBKDFNPH".
  - **Insecurity**: Only 25 possible keys → vulnerable to brute force.

---

## **Types of Encryption**
1. **Symmetric Encryption**:
   - Uses **one shared key** for encryption and decryption.
   - Challenges: Secure key sharing.
   - Examples:
     - **DES** (56-bit, insecure since 1999).
     - **3DES** (168-bit, deprecated in 2019).
     - **AES** (128, 192, or 256-bit, standard since 2001).

2. **Asymmetric Encryption**:
   - Uses **two keys**:
     - Public key: For encryption (shared with others).
     - Private key: For decryption (kept secret).
   - Examples:
     - **RSA** (2048-4096-bit keys).
     - **Diffie-Hellman** (2048+ bits).
     - **Elliptic Curve Cryptography (ECC)**: Shorter keys (e.g., 256-bit ≈ 3072-bit RSA).

---

## **Mathematical Operations in Cryptography**
1. **XOR Operation**:
   - Logical operation: 1 if bits differ, 0 if they match.
   - Useful properties:
     - \( A \oplus A = 0 \), \( A \oplus 0 = A \).
     - Commutative: \( A \oplus B = B \oplus A \).
     - Associative: \( (A \oplus B) \oplus C = A \oplus (B \oplus C) \).
   - Example:
     - Plaintext (P) = 1010, Key (K) = 1100.
     - Ciphertext \( C = P \oplus K \) = 0110.

2. **Modulo Operation**:
   - Remainder after division: \( X \% Y = R \).
   - Properties:
     - Result is always non-negative: \( 0 \leq R < Y \).
   - Examples:
     - \( 25 \% 5 = 0 \), \( 23 \% 6 = 5 \).

---

## **Summary**
- **Symmetric Encryption**: Single shared key; efficient but challenging for key distribution.
- **Asymmetric Encryption**: Public/private key pair; more secure but slower.
- Cryptography relies heavily on mathematical principles, such as XOR and modulo operations.
