
# Networking Core Protocols

## **Domain Name System (DNS)**
- **Purpose**: Maps domain names to IP addresses, eliminating the need to memorize IPs.
- **Layer**: Application Layer (Layer 7 of OSI model).
- **Ports**:
  - UDP port 53 (default)
  - TCP port 53 (fallback)
- **Common DNS Records**:
  - **A Record**: Maps hostname to IPv4 address (e.g., `example.com -> 172.17.2.172`).
  - **AAAA Record**: Maps hostname to IPv6 address.
  - **CNAME Record**: Maps one domain name to another (e.g., `www.example.com -> example.com`).
  - **MX Record**: Specifies mail server for a domain.

### **Tools for DNS Lookup**
- **nslookup**: Query DNS for records.
- **tshark**: Analyze DNS query packets (e.g., `tshark -r dns-query.pcapng`).

---

## **WHOIS Records**
- **Purpose**: Publicly available data on domain registrants (e.g., name, email, address).
- **Tools**: Command-line `whois` for domain lookup.
- **Privacy**: Can use services to hide personal info from WHOIS.

---

## **HTTP and HTTPS**
- **Purpose**: Protocols for web communication.
- **Ports**:
  - HTTP: TCP port 80
  - HTTPS: TCP port 443
- **Common HTTP Methods**:
  - **GET**: Retrieve data (e.g., HTML or image).
  - **POST**: Submit new data (e.g., form submission).
  - **PUT**: Create/update resources.
  - **DELETE**: Delete specified resource.

---

## **File Transfer Protocol (FTP)**
- **Purpose**: Transfers files efficiently.
- **Ports**: 
  - Command: TCP port 21
  - Data Transfer: Separate connection.
- **Commands**:
  - `USER` / `PASS`: Login.
  - `RETR`: Download file.
  - `STOR`: Upload file.
- **Example Session**:
  ```
  ftp MACHINE_IP
  USER anonymous
  PASS <empty>
  ls
  get coffee.txt
  quit
  ```

---

## **Email Protocols**
### **SMTP (Simple Mail Transfer Protocol)**
- **Purpose**: Send emails from clients to servers or between servers.
- **Port**: TCP port 25 (default).
- **Commands**:
  - `HELO`/`EHLO`: Start SMTP session.
  - `MAIL FROM`: Specify sender.
  - `RCPT TO`: Specify recipient.
  - `DATA`: Begin sending email content.
  - `.`: End email content.

### **POP3 (Post Office Protocol v3)**
- **Purpose**: Retrieve emails from a server to a single client.
- **Port**: TCP port 110.
- **Commands**:
  - `USER` / `PASS`: Authenticate.
  - `STAT`: Get message count and size.
  - `LIST`: List messages.
  - `RETR <msg#>`: Retrieve message.
  - `DELE <msg#>`: Mark message for deletion.
  - `QUIT`: End session.

### **IMAP (Internet Message Access Protocol)**
- **Purpose**: Synchronize emails across multiple devices.
- **Port**: TCP port 143.
- **Commands**:
  - `LOGIN <username> <password>`: Authenticate.
  - `SELECT <mailbox>`: Open mailbox.
  - `FETCH <msg#> body[]`: Retrieve message.
  - `MOVE <msg#>`: Move message.
  - `LOGOUT`: End session.

---

## **Comparison: POP3 vs. IMAP**
- **POP3**: Emails are downloaded and often deleted from the server (single device use).
- **IMAP**: Emails stay on the server, allowing synchronization across devices.

---

## **Practical Terminal Examples**
### **FTP Session**
```
ftp MACHINE_IP
USER anonymous
PASS <empty>
ls
type ascii
get coffee.txt
quit
```

### **SMTP Session**
```
telnet MACHINE_IP 25
HELO client.thm
MAIL FROM: <user@client.thm>
RCPT TO: <recipient@server.thm>
DATA
From: user@client.thm
To: recipient@server.thm
Subject: Test Email

Hello!
.
QUIT
```

### **POP3 Session**
```
telnet MACHINE_IP 110
USER strategos
PASS <password>
STAT
LIST
RETR 1
QUIT
```

### **IMAP Session**
```
telnet MACHINE_IP 143
LOGIN strategos <password>
SELECT inbox
FETCH 1 body[]
LOGOUT
```
