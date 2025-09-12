# NetworkMiner 

## Overview
- **Tool**: NetworkMiner (open-source Network Forensic Analysis Tool – NFAT)
- **Platforms**: Windows (native), also works on Linux, MacOS, FreeBSD
- **Purpose**: Passive network forensics, traffic overview, detecting hosts/OS/ports, parsing PCAPs, reassembling files/certs
- **Users**: Incident response, law enforcement, companies

---

## Uses in Forensics
- Detect malicious activities, breaches, anomalies
- Provides:
  - Host context (IP, MAC, hostname, OS)
  - Indicators (traffic spikes, port scans)
  - Attack tools (e.g., Nmap detection)

---

## Supported Data Types
1. **Live Traffic**
2. **Traffic Captures (PCAP)**
3. **Log Files**

---

## Features
- **Traffic sniffing**: Capture & log packets (Windows only; limited reliability)
- **Parsing PCAP files**: Extract detailed packet contents
- **Protocol analysis**
- **OS fingerprinting** (via Satori & p0f)
- **File extraction** (images, HTML, emails)
- **Credential grabbing** (Kerberos, NTLM, RDP, HTTP, IMAP, FTP, SMTP, MSSQL)
- **Cleartext keyword parsing**

---

## Editions
- **Free Edition**: Basic functionality
- **Professional Edition**: Extra features (OSINT lookups, advanced options)

---

## Operating Modes
1. **Sniffer Mode**  
   - Windows only  
   - Not reliable as primary sniffer → use Wireshark/tcpdump instead
2. **Packet Parsing/Processing**  
   - Quick overview of captures before deeper analysis

---

## Pros & Cons
**Pros**  
- OS fingerprinting  
- Easy file extraction  
- Credential grabbing  
- Cleartext keyword parsing  
- Fast overview  

**Cons**  
- Weak at active sniffing  
- Not good for large PCAPs  
- Limited filtering  
- Not built for deep/manual analysis  

---

## Comparison: NetworkMiner vs Wireshark
| Feature | NetworkMiner | Wireshark |
|---------|--------------|-----------|
| Purpose | Quick overview, mapping, data extraction | Deep packet analysis |
| GUI | ✅ | ✅ |
| Sniffing | ✅ (limited) | ✅ |
| PCAP handling | ✅ | ✅ |
| OS fingerprinting | ✅ | ❌ |
| Keyword/param discovery | ✅ | Manual |
| Credential discovery | ✅ | ✅ |
| File extraction | ✅ | ✅ |
| Filtering | Limited | ✅ |
| Packet decoding | Limited | ✅ |
| Protocol analysis | ❌ | ✅ |
| Payload analysis | ❌ | ✅ |
| Statistics | ❌ | ✅ |
| Cross-platform | ✅ | ✅ |
| Host categorization | ✅ | ❌ |

**Best Practice**: Use NetworkMiner for quick overview → then Wireshark for deep analysis.

---

## Interface Breakdown

### Menus
- **File**: Load PCAP (drag/drop, receive via IP)  
- **Tools**: Clear dashboard  
- **Help**: Updates, version info  

### Case Panel
- Lists investigated PCAP files  
- Reload, metadata, remove  

### Hosts
- Shows IP, MAC, OS, open ports, packets, sessions  
- OS detection: Satori + p0f  
- Sort, recolor, right-click copy  

### Sessions
- Frame number, addresses, ports, protocol, start time  
- Search bar supports: `"ExactPhrase"`, `"AllWords"`, `"AnyWord"`, `"RegExe"`

### DNS
- Frame no., timestamp, client/server, ports, TTL, query/answer  
- Alexa Top 1M (pro only)  

### Credentials
- Extracts Kerberos, NTLM, RDP, HTTP, IMAP, FTP, SMTP, MSSQL  
- Exported creds can be cracked with **Hashcat** or **John the Ripper**

### Files
- Extracted files: name, ext, size, addresses, ports, protocol, timestamp  
- Pro-only: OSINT hash lookup, sample submission  

### Images
- Extracted from PCAPs, preview & zoom, metadata shown  

### Parameters
- Name, value, frame no., addresses, ports, timestamp  

### Keywords
- Extracted cleartext keywords, searchable  
- Must reload after updating search terms  

### Messages
- Emails, chats, messages  
- Sender/receiver, attachments, attributes  

### Anomalies
- Not a full IDS, but detects some exploits (EternalBlue, spoofing)  

---

## Version Differences
- **After v2.0**:  
  - MAC address correlation (detect conflicts)  
  - Extended parameter processing  
- **Up to v1.6**:  
  - Detailed packet handling  
  - Frame processing  
  - Cleartext tab (all extracted cleartext in one place, but no packet linkage)  

---

## Key Takeaways
- Do **not** use NetworkMiner as a primary sniffer.  
- Best use: **initial investigation** → overview, extract files/creds, spot anomalies.  
- For in-depth analysis, switch to **Wireshark** or **tcpdump**.  

---

✅ Finished "NetworkMiner Room"
