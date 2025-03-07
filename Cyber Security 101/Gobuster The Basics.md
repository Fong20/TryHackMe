# Gobuster: The Basics

Gobuster is a directory, subdomain, and virtual host brute-forcing tool, commonly included in penetration testing distributions like Kali Linux.

---

## **Usage and Commands**

### **Basic Help Command**
```bash
gobuster --help
```
Displays available commands and flags.

### **Available Commands**
- **dir** – Directory and file enumeration mode.
- **dns** – DNS subdomain enumeration mode.
- **fuzz** – Fuzzing mode (replaces "FUZZ" in requests).
- **gcs** – Google Cloud Storage bucket enumeration.
- **s3** – AWS S3 bucket enumeration.
- **tftp** – TFTP enumeration mode.
- **vhost** – Virtual Host enumeration mode.

### **Common Flags**
| Short Flag | Long Flag            | Description |
|------------|----------------------|-------------|
| `-t`       | `--threads`          | Number of concurrent threads (default 10). |
| `-w`       | `--wordlist`         | Specifies the wordlist for brute force. |
| `--delay`  |                      | Time to wait between requests to avoid detection. |
| `--debug`  |                      | Enables debug output. |
| `-o`       | `--output`           | Saves results to a file. |

---

## **Gobuster Directory Enumeration (`dir` mode)**

### **Basic Usage**
```bash
gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
```
- `dir`: Directory enumeration mode.
- `-u`: Target URL.
- `-w`: Wordlist used for brute-forcing.
- `-t`: Number of threads.

### **Useful Flags**
| Short Flag | Long Flag            | Description |
|------------|----------------------|-------------|
| `-c`       | `--cookies`          | Pass a cookie (e.g., session ID). |
| `-x`       | `--extensions`       | Specify file extensions to search for (e.g., `.php, .js`). |
| `-H`       | `--headers`          | Add custom headers to requests. |
| `-k`       | `--no-tls-validation` | Bypass TLS certificate validation. |
| `-s`       | `--status-codes`      | Show only specific status codes (e.g., `200, 301`). |
| `-b`       | `--status-codes-blacklist` | Hide specific status codes. |
| `-U`       | `--username`         | Set a username for authenticated requests. |
| `-P`       | `--password`         | Set a password for authenticated requests. |

---

## **Gobuster DNS Enumeration (`dns` mode)**

### **Basic Usage**
```bash
gobuster dns -d example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```
- `dns`: Subdomain enumeration mode.
- `-d`: Target domain.
- `-w`: Wordlist.

---

## **Gobuster Virtual Host Enumeration (`vhost` mode)**

### **Basic Usage**
```bash
gobuster vhost -u "http://MACHINE_IP" --domain example.thm -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain --exclude-length 250-320
```
- `vhost`: Virtual host enumeration mode.
- `-u`: Target URL.
- `--domain`: Specifies the domain to enumerate.
- `--append-domain`: Appends the base domain to each word in the wordlist.
- `--exclude-length`: Excludes responses of specific lengths.

---

## **Summary**
- **`dir` mode**: Enumerates directories and files.
- **`dns` mode**: Enumerates DNS subdomains.
- **`vhost` mode**: Enumerates virtual hosts.

Gobuster is a powerful tool for reconnaissance in penetration testing.
