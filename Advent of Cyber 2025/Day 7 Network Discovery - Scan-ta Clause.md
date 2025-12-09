# Day 7 Network Discovery - Scan-ta Clause

## Overview
- QA server `tbfc-devqa01` at **10.48.179.201** compromised by HopSec.
- Goal: discover open services, extract 3 keys, access admin panel, enumerate internal services, and retrieve final flag.

---

## Nmap Scanning

### Basic Scan
```bash
nmap 10.48.179.201
```
**Findings:**
- 22/tcp open (SSH)
- 80/tcp open (HTTP)

---

### Full Port Scan with Banner Grabbing
```bash
nmap -p- --script=banner 10.48.179.201
```
**Findings:**
- 22/tcp → SSH-2.0-OpenSSH_9.6p1 Ubuntu
- 80/tcp → HTTP
- **21212/tcp → FTP (vsFTPd 3.0.5)**
- **25251/tcp → TBFC maintd v0.2**

---

## Extracting Key 1 (FTP on port 21212)
```bash
ftp 10.48.179.201 21212
Name: anonymous

ls
get tbfc_qa_key1 -
```
**→ KEY 1 obtained here**

---

## Extracting Key 2 (Custom TBFC Service on port 25251)
```bash
nc -v 10.48.179.201 25251
TBFC maintd v0.2
Type HELP for commands.

# run:
GET KEY
```
**→ KEY 2 obtained from TBFC maintd**

---

## UDP Scan for Key 3
```bash
nmap -sU 10.48.179.201
```
**Findings:**
- 53/udp open (DNS)

### Query DNS for key:
```bash
dig @10.48.179.201 TXT key3.tbfc.local +short
```
**→ KEY 3 obtained here**

---

## Accessing Admin Panel
Navigate to:
```
http://10.48.179.201
```
Enter combined keys in admin panel.

---

## On-Host Discovery (After Gaining Web Console Access)

### Listing listening ports:
```bash
ss -tunlp
```

**Important internal ports:**
- 8000 (localhost)
- 3306 (MySQL)
- 7681 (local service)

---

## Extracting Final Flag from MySQL
```bash
mysql -D tbfcqa01 -e "show tables;"
mysql -D tbfcqa01 -e "select * from flags;"
```

**→ Final FLAG obtained here**

---

End of notes.
