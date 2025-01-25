
## Public Key Cryptography Basics

### Key Concepts
- **Asymmetric Cryptography**: Used for secure key exchange but slower than symmetric encryption.
- **Symmetric Cryptography**: Faster, used for ongoing secure communication once a shared key is exchanged.
- **RSA**: A public-key encryption algorithm based on the difficulty of factoring large numbers.

### Key Exchange
- **Box with a Lock Analogy**:
  - **Lock** = Public Key
  - **Key to the Lock** = Private Key
  - **Secret Code** = Symmetric Encryption Cipher + Key
  - Asymmetric cryptography is used only during the key exchange to minimize overhead.

---

### RSA Overview
- Based on the mathematical challenge of factoring the product of two large primes.
- **Key Variables**:
  - `p` & `q`: Large prime numbers.
  - `n = p × q`: Modulus for public/private keys.
  - `e`: Public exponent.
  - `d`: Private exponent (calculated as `e × d ≡ 1 (mod ϕ(n))`).
- **Encryption**: `y = x^e mod n` (ciphertext).
- **Decryption**: `x = y^d mod n` (plaintext).

#### Numerical Example
- **Prime numbers**: `p = 157`, `q = 199`.
- **Public Key**: `(n = 31243, e = 163)`.
- **Private Key**: `(n = 31243, d = 379)`.
- **Encryption**: Encrypt message `x = 13` → `y = 13163 mod 31243 = 16341`.
- **Decryption**: Decrypt `y = 16341` → `x = 16341379 mod 31243 = 13`.

---

### Diffie-Hellman Key Exchange
- Establishes a shared secret over an insecure channel.
- **Process**:
  1. Agree on public variables: prime `p` and generator `g`.
  2. Private keys: `a` (Alice) and `b` (Bob).
  3. Public keys: `A = g^a mod p`, `B = g^b mod p`.
  4. Shared key: `s = g^(ab) mod p`.

---

### Digital Signatures
- Used to verify authenticity and integrity of data.
- **Process**:
  - Sign with private key.
  - Verify with public key.

---

### SSH and Key Authentication
- **Public Key Authentication**: Uses SSH key pairs (`id_rsa`/`id_rsa.pub` or `id_ed25519`).
- **Generating Keys**: `ssh-keygen -t ed25519` or `ssh-keygen -t rsa`.
- **Key Security**:
  - Protect private keys (set correct file permissions, e.g., `chmod 600`).
  - Use a passphrase for additional security.

---

### Certificates and HTTPS
- **TLS Certificates**:
  - Issued by Certificate Authorities (CAs).
  - Verified through a chain of trust.
  - Root CAs are pre-trusted by browsers and operating systems.
- **Tools**:
  - Free certificates: Let’s Encrypt.
  - View CAs: Mozilla Firefox and Google Chrome lists.

---

### Tools for RSA Challenges (CTFs)
- **RsaCtfTool**: Automates attacking RSA-based challenges.
- **rsatool**: Another useful tool for calculating RSA variables.

---

### Practical Tools
- **GPG for Digital Signatures and Encryption**:
  - Generate keys: `gpg --full-gen-key`.
  - Import backup keys: `gpg --import backup.key`.
  - Decrypt messages: `gpg --decrypt <file>`.
