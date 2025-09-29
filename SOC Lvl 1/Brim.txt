# Brim

## What is Brim?
- Open-source desktop app for **processing pcap & log files**.  
- Focus: **search & analytics**.  
- Uses **Zeek logs** as main format.  
- Supports **Zeek signatures** + **Suricata rules**.  

### Input Types:
- **Packet Capture Files**: tcpdump, tshark, Wireshark.  
- **Log Files**: Structured logs (Zeek).  

### Built on:
- **Zeek** – log engine.  
- **Zed Language (ZQL)** – querying.  
- **ZNG Data Format** – data storage.  
- **Electron + React** – GUI.  

---

## Why Brim?
- Handles **large pcaps** (>1GB) better than Wireshark.  
- Faster + easier than manually using tcpdump/Zeek.  
- GUI for searching + correlating logs.  

---

## Brim vs Wireshark vs Zeek

| Feature                  | Brim | Wireshark | Zeek |
|---------------------------|------|-----------|------|
| GUI                      | ✔    | ✔         | ✖    |
| Sniffing                 | ✖    | ✔         | ✔    |
| Pcap Processing          | ✔    | ✔         | ✔    |
| Log Processing           | ✔    | ✖         | ✔    |
| Packet Decoding          | ✖    | ✔         | ✔    |
| Filtering                | ✔    | ✔         | ✔    |
| Scripting                | ✖    | ✖         | ✔    |
| Signature Support        | ✔    | ✖         | ✔    |
| File Extraction          | ✖    | ✔         | ✔    |
| Handling >1GB pcaps      | Medium | Low    | Good |
| Ease of Management       | 4/5  | 4/5       | 3/5  |

---

## Brim Interface

- **Landing Page**:
  - **Pools**: imported files.  
  - **Queries**: saved queries.  
  - **History**: executed queries.  

- **Pools & Log Details**:
  - Imports pcap → generates Zeek logs.  
  - Shows timeline of events.  
  - Log detail pane → correlations (src/dst, duration, related logs).  
  - Right-click options: filter, count, sort, whois lookup, open in Wireshark.  

- **Queries & History**:
  - 12 premade queries under "Brim".  
  - Queries can be named, tagged, described.  
  - History auto-saves executed queries.  

---

## Brim Query Reference (ZQL)

| Purpose                   | Syntax/Example |
|----------------------------|----------------|
| Basic Search              | `10.0.0.1` |
| Logical Ops               | `192 and NTP` |
| Filter by Field           | `id.orig_h==192.168.121.40` |
| Specific Log File         | `_path=="conn"` |
| Count                     | `count() by _path` |
| Sort                      | `... | sort -r` |
| Cut Fields                | `_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h` |
| Unique Values             | `... | uniq` |

---

## Custom Queries / Use Cases

- **Communicated Hosts**:  
  `_path=="conn" | cut id.orig_h, id.resp_h | sort | uniq`

- **Frequent Hosts**:  
  `_path=="conn" | cut id.orig_h, id.resp_h | sort | uniq -c | sort -r`

- **Most Active Ports**:  
  `_path=="conn" | cut id.resp_p, service | sort | uniq -c | sort -r count`

- **Long Connections**:  
  `_path=="conn" | cut id.orig_h, id.resp_p, id.resp_h, duration | sort -r duration`

- **Transferred Data**:  
  `_path=="conn" | put total_bytes := orig_bytes + resp_bytes | sort -r total_bytes | cut uid, id, orig_bytes, resp_bytes, total_bytes`

- **DNS Queries**:  
  `_path=="dns" | count() by query | sort -r`

- **HTTP Queries**:  
  `_path=="http" | count() by uri | sort -r`

- **Suspicious Hostnames (DHCP)**:  
  `_path=="dhcp" | cut host_name, domain`

- **Suspicious IPs (subnets)**:  
  `_path=="conn" | put classnet := network_of(id.resp_h) | cut classnet | count() by classnet | sort -r`

- **Detect Files**:  
  `filename!=null`

- **SMB Activity**:  
  `_path=="dce_rpc" OR _path=="smb_mapping" OR _path=="smb_files"`

- **Known Patterns (Zeek/Suricata alerts)**:  
  `event_type=="alert" or _path=="notice" or _path=="signatures"`

---

## Threat Hunting Use Cases

### 1. Malware C2 Detection
- Steps:
  - Review frequently communicated hosts.  
  - Identify suspicious IPs (internal ↔ external).  
  - Check ports & services.  
  - Look at DNS queries → VirusTotal enrichment.  
  - Inspect HTTP requests → detect file downloads.  
  - Confirm with Suricata alerts.  

### 2. Crypto Mining Detection
- Steps:
  - Identify anomalous hosts with frequent comms.  
  - Detect weird ports.  
  - Measure **transferred bytes**.  
  - Confirm with Suricata → mining alerts.  
  - Map to **MITRE ATT&CK** (T1496 Resource Hijacking).  

---

✅ Best practice:  
- Use **field filters** instead of irregular searches.  
- Combine Brim + Zeek + Suricata for layered detection.  
