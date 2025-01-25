
# Notes: Hashing Basics  

## **What is a Hash?**
- A hash value is a fixed-size string of characters computed by a hash function, which takes an arbitrary input size and produces a fixed-length output.
- Hash functions are different from encryption. There are no encryption keys involved. Hence, it's computationally impractical to reverse the process (input cannot be derived from the output).
- The output of a hash function is typically raw bytes, which are then encoded using common encodings such as  base64 or hexadecimal. md5sum, sha1sum, sha256sum, and sha512sum produce their outputs in hexadecimal format. Remember that hexadecimal format prints each raw byte as two hexadecimal digits.  

## **Why is Hashing Important?**
1. **Data Integrity**: Ensures data hasn't been altered.  
2. **Password Security**: Server only stores the hash value of the password for verification instead of storing the actual password which increases the risk. When logging in, the hash of the entered password is compared to the stored hash.  

**Example:** 
- Any changes in the input, even a single bit, causes a significant change in output:
  - Input of file1.txt: Letter "T" → Hex: 54 (Binary: 01010100).  
  - Input of file2.txt : Letter "U" → Hex: 55 (Binary: 01010101).  
  - Despite differing by one bit, their hash outputs (MD5, SHA1, SHA256) differ significantly.

![image](https://github.com/user-attachments/assets/afb64f39-2e90-42cd-916a-edfd8eeb6170)

## **Hash Collisions**
- Occurs when two different inputs produce the same hash output.
- **Cause**: The pigeonhole effect as there are unlimited inputs and limited output values.  
- Collisions are unavoidable. However, a good hash function ensures that the probability of a collision is negligible.
- MD5 and SHA1 are considered insecure due to engineered hash collisions. Thus, it is not recommended to trust either algorithm for hashing passwords or data.
  
---

## **Insecure Password Storage Practices**
1. **Storing Passwords in Plaintext**:
2. **Using Deprecated Encryption**:
3. **Using Weak Hashing Algorithms**:
   
---

## Hashing for authentication**
- Hashing is used for authentication as it stores the hash value of the password using a secure hashing function? instead of storing the actual password. This process means that the user’s actual password is not stored in the database, and if the database is leaked, the attacker will have to crack each password to find out what the password was.
- Encryption is not used to store passwords as encryption requires storing a key; if the key is compromised, all passwords are exposed.

### Rainbow Tables
- A Rainbow Table is a lookup table of hashes to plaintexts, so you can quickly find out what password a user had just from the hash. A rainbow table trades the time to crack a hash for hard disk space, but it takes time to create.
- Websites like **CrackStation** and **Hashes.com** internally use massive rainbow tables to provide fast password cracking for hashes without salts. Doing a lookup in a sorted list of hashes is quicker than trying to crack the hash.

**Example: Rainbow Table**

![image](https://github.com/user-attachments/assets/91f1fbc9-fb69-4cd2-9452-47c9d51398a5)

### Salting as a process in protecting against Rainbow Tables
- To protect against rainbow tables, we add a salt to the passwords. The salt is a randomly generated value stored in the database and should be unique to each user. In theory, you could use the same salt for all users, but duplicate passwords would still have the same hash and a rainbow table could still be created for passwords with that salt.
- The salt is added to either the start or the end of the password before it’s hashed, and this means that every user will have a different password hash even if they have the same password. Hash functions like Bcrypt and Scrypt handle this automatically.
- Salts don’t need to be kept private.
  
- **Process of securely storing passwords**:
  1. Select a secure hashing algorithm (e.g., Argon2, Bcrypt, Scrypt).  
  2. Add a unique salt to the password.  
  3. Concatenate password and salt, hash the result.  
  4. Store the hash and salt.  

---

## Linux Password Hash
- In Linux, Passwords hashes are stored in `/etc/shadow` which is normally only readable by root.
- The shadow file contains the password information of each account in lines and each line contains nine fields, separated by colons (:). The first two fields are the login name and the encrypted password. More information about the other fields can be found by executing man 5 shadow on a Linux system.

**Format of encrypted password:**
  ```
  $prefix$options$salt$hash
  ```
Example: `$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4`
- `$y$` → Hashing Algorithm used to generate the algorithm: In this case, yescrypt.
- `j9T` → Parameter passed to the algorithm.
- `76UzfgEM5PnymhQ7TlJey1` → Salt used.
- `/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4` → Hash value.

## Windows Password Hash
- MS Windows passwords are hashed using NTLM, a variant of MD4. They’re visually identical to MD4 and MD5 hashes, so it’s very important to use context to determine the hash type.
- On MS Windows, password hashes are stored in the SAM (Security Accounts Manager). MS Windows tries to prevent normal users from dumping them, but tools like mimikatz exist to circumvent MS Windows security. Notably, the hashes found there are split into NT hashes and LM hashes.
  
---

## **Hash Cracking**
- You can’t “decrypt” password hashes. They’re not encrypted. You have to crack the hashes by hashing many different inputs, potentially adding the salt if there is one and comparing it to the target hash. Once it matches, you know what the password was.
- Eg of tools used for hash cracking: **Hashcat** and **John the Ripper**
 
### Hashcat 
Hashcat is recommended to be run on host compiuter to make the most of the system's GPU as Hashcat is a GPU-based hash cracking software.

**Syntax**

  ```
  hashcat -m <hash_type> -a <attack_mode> hashfile wordlist
  ```
- m <hash_type> specifies the hash-type in numeric format. For example, -m 1000 is for NTLM. Check the official documentation (man hashcat) and example page to find the hash type code to use.
- a <attack_mode> specifies the attack-mode. For example, -a 0 is for straight, i.e., trying one password from the wordlist after the other.
- hashfile is the file containing the hash you want to crack.
- wordlist is the security word list you want to use in your attack.

**Example:**
  
  ```bash
  hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt
  ```
This command treat the hash as Bcrypt and try the passwords in the rockyou.txt file.

## Hashing for Integrity Checking**
- Verify file integrity using hash values (e.g., `sha256sum`).
- Finding Duplicates**: Compare file hashes to detect duplicate files. If two documents have the same hash, they are the same document. This is very convenient for finding and deleting duplicate files.

### HMAC (Keyed-Hash Message Authentication Code)**:
- HMAC (Keyed-Hash Message Authentication Code) is a type of message authentication code (MAC) that uses a cryptographic hash function in combination with a secret key to verify the authenticity and integrity of data.
- An HMAC can be used to ensure that the person who created the HMAC is who they say they are, i.e., authenticity is confirmed; moreover, it proves that the message hasn’t been modified or corrupted, i.e., integrity is maintained. This is achieved through the use of a secret key to prove authenticity and a hashing algorithm to produce a hash and prove integrity.

**How HMAC Works:**
1. The secret key is padded to the block size of the hash function.
2. The padded key is XORed with a constant (usually a block of zeros or ones).
3. The message is hashed using the hash function with the XORed key.
4. The result from Step 3 is then hashed again with the same hash function but using the padded key XORed with another constant.
5. The final output is the HMAC value, typically a fixed-size string.

![image](https://github.com/user-attachments/assets/37566d05-f391-48fd-bb0b-b0415c3fbf55)

HMAC function can also be calculated using the following expression:

``HMAC(K,M) = H((K⊕opad)||H((K⊕ipad)||M))`` where M and K represent the message and the key, respectively.
 
---

## **Encoding vs. Encryption vs. Hashing**
- **Encoding**: Converts data to a compatible format (e.g., Base64). Reversible.  
- **Encryption**: Protects confidentiality using a cipher and key. Reversible with key.  
- **Hashing**: One-way process to generate a fixed-size digest. Irreversible.  

---
