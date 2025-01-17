
# Networking Secure Protocols

## 1. Early Network Vulnerabilities
- Packet capturing allowed attackers to intercept cleartext data (e.g., chats, emails, passwords).
- Promiscuous mode on network cards captured all packets.
- Modern services rarely transmit login credentials in cleartext.

---

## 2. Evolution of Secure Communication Protocols
- **SSL (Secure Sockets Layer):**
  - Developed by Netscape Communications.
  - First public version: SSL 2.0 (1995).
  - Replaced by TLS (Transport Layer Security) in 1999.
- **TLS:**
  - Upgraded version of SSL with improved security.
  - Latest version: TLS 1.3 (2018).
  - Operates at the OSI model’s transport layer for confidentiality and integrity.
  - Enabled secure communication for HTTP, DNS, MQTT, SIP, and others.

---

## 3. TLS Implementation
- **Certificate System:**
  - Servers obtain signed TLS certificates from Certificate Authorities (CAs).
  - Free alternatives like Let’s Encrypt exist.
  - Self-signed certificates lack third-party authentication.
- **HTTPS:**
  - Combines HTTP with TLS for encrypted communication.
  - Process:
    1. TCP three-way handshake.
    2. TLS session establishment.
    3. Encrypted HTTP data exchange.
  - Port numbers:
    - HTTP: 80
    - HTTPS: 443
- TLS also secures SMTP, POP3, IMAP, transforming them into SMTPS, POP3S, IMAPS.

---

## 4. SSH (Secure Shell)
- Developed in 1995 to replace insecure TELNET.
- Benefits:
  - Secure authentication (e.g., public keys, 2FA).
  - End-to-end encryption and data integrity.
  - Tunneling for protocols (e.g., creating VPN-like connections).
  - X11 Forwarding for GUI applications.
- Port numbers:
  - TELNET: 23
  - SSH: 22
  - SFTP (SSH File Transfer Protocol): 22

---

## 5. VPN (Virtual Private Network)
- **Purpose:**
  - Connect remote branches/users securely to a main network.
  - Encrypts traffic, masking IP addresses and bypassing censorship.
- **Functionality:**
  - Routes traffic through encrypted tunnels.
  - Useful for accessing resources or bypassing geographical restrictions.
- **Key Features:**
  - Some VPNs route all traffic through the tunnel; others don’t.
  - DNS and IP leak tests are necessary for privacy assurance.
- **Legal Concerns:**
  - VPN usage may be restricted in certain countries; legal checks are essential.

---

## 6. Comparison of Security Methods
- **TLS:**
  - Adds encryption to protocols without altering their base layers.
  - Example protocols: HTTPS, SMTPS, POP3S, IMAPS.
- **SSH:**
  - Secure alternative for remote access and file transfer.
  - Can create tunnels for plaintext protocols.
- **VPN:**
  - Securely connects remote networks or devices to a central network.
  - Ensures traffic privacy and integrity.
