
# John the Ripper: The Basics

### **1. Dictionary Attack**
- **Process:** Compare hashed passwords with pre-hashed words from a dictionary/wordlist.
- **Tool:** `John the Ripper` (commonly referred to as "John").
- **Command Syntax:**
  ```bash
  john --wordlist=[path to wordlist] [path to hash file]
  ```
  - Example:
    ```bash
    john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
    ```

---

### **2. Identifying Hash Types**
- **Tool:** `hash-identifier`
  - Install:
    ```bash
    wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py
    ```
  - Run:
    ```bash
    python3 hash-id.py
    ```
  - Example Output:
    ```
    HASH: 2e728dd31fb5949bc39cac5a9f066498
    Possible Hashes: MD5, Domain Cached Credentials.
    ```
- **Using Specific Hash Format in John:**
  ```bash
  john --format=[format] --wordlist=[path to wordlist] [path to hash file]
  ```
  - Example:
    ```bash
    john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
    ```

---

### **3. Cracking /etc/shadow Password Hashes**
- **Unshadow Tool:** Combines `/etc/passwd` and `/etc/shadow`.
  ```bash
  unshadow [path to passwd] [path to shadow] > [output file]
  ```
  - Example:
    ```bash
    unshadow local_passwd local_shadow > unshadowed.txt
    ```
- **Cracking with John:**
  ```bash
  john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
  ```

---

### **4. Single Crack Mode**
- **Uses:** Heuristics (username-based password guesses).
- **Command:**
  ```bash
  john --single --format=[format] [path to file]
  ```
  - Example:
    ```bash
    john --single --format=raw-sha256 hashes.txt
    ```
- **File Format Requirement:**
  - Change format to `username:hash`.
  - Example:
    ```
    mike:1efee03cdcb96d90ad48ccc7b8666033
    ```

---

### **5. Custom Rules for Mangling**
- **Defining Rules:**
  - Located in `john.conf` (e.g., `/etc/john/john.conf`).
  - Example Rule:
    ```conf
    [List.Rules:PoloPassword]
    cAz"[0-9][!£$%@]"
    ```
    - `c`: Capitalize first letter.
    - `Az`: Append defined characters.
    - `[0-9]`: Include numbers.
    - `[!£$%@]`: Include special characters.
- **Usage:**
  ```bash
  john --wordlist=[path to wordlist] --rule=PoloPassword [path to file]
  ```

---

### **6. Specialized Tools**
#### **a. Zip2John**
- **Command:**
  ```bash
  zip2john [zip file] > [output file]
  ```
  - Example:
    ```bash
    zip2john zipfile.zip > zip_hash.txt
    ```
- **Cracking:**
  ```bash
  john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
  ```

#### **b. Rar2John**
- **Command:**
  ```bash
  rar2john [rar file] > [output file]
  ```
  - Example:
    ```bash
    rar2john rarfile.rar > rar_hash.txt
    ```
- **Cracking:**
  ```bash
  john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
  ```

#### **c. SSH2John**
- **Command:**
  ```bash
  ssh2john [id_rsa file] > [output file]
  ```
  - Example:
    ```bash
    /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt
    ```
- **Cracking:**
  ```bash
  john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
  ```
