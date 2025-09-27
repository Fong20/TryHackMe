# Zeek

## Overview
- **Zeek**: Open-source + commercial passive network traffic analyzer.
- Developed by **Lawrence Berkeley Labs**, enterprise fork by **Corelight**.
- Provides **50+ logs across 7 categories** for forensics, traffic analysis, and security monitoring.

---

## Network Monitoring vs Network Security Monitoring (NSM)
- **Network Monitoring**: IT-focused (uptime, device health, performance, troubleshooting).
- **NSM**: Security-focused (detect anomalies, rogue hosts, malicious traffic, suspicious usage). SOC-oriented.

---

## Zeek vs Snort
| Tool | Focus | Pros | Cons |
|------|-------|------|------|
| **Zeek** | NSM + IDS framework. In-depth traffic analysis, scripting. | In-depth visibility, event correlation, detect complex threats. | Harder to use, requires external/manual analysis. |
| **Snort** | IDS/IPS, signature-based detection. | Easy rule writing, Cisco support, prevention capability. | Limited complex threat detection. |

---

## Zeek Architecture
- **Event Engine**: Packet processing (IP addresses, sessions, files).
- **Policy Script Interpreter**: Correlation via scripts.

---

## Zeek Frameworks
- Logging, Notice, Input, Config, Intelligence  
- Cluster, Broker, Supervisor, GeoLocation  
- File Analysis, Signature, Summary, NetControl, TLS Decryption  

---

## Running Zeek
### Check version:
```bash
zeek -v
```

### Manage service with ZeekControl (requires root):
```bash
sudo su
zeekctl status
zeekctl start
zeekctl stop
```

### Process pcap:
```bash
zeek -C -r sample.pcap
```
- Logs saved in working directory.
- Default logs path: `/opt/zeek/logs/`

---

## Key Zeek Log Categories
- **Network**: conn.log, dns.log, http.log, ssh.log, ssl.log, etc.
- **Files**: files.log, x509.log, pe.log.
- **Detection**: intel.log, notice.log, signatures.log.
- **Observations**: known_hosts.log, software.log.
- **Misc & Diagnostics**: weird.log, stats.log, cluster.log.

### Correlation
- Logs linked via **UID**.
- Daily logs: `known_hosts.log`, `software.log`.  
- Per session: `notice.log`, `intel.log`.

---

## CLI Tools for Log Analysis
- **Basics**: `cat`, `head`, `tail`, `history`, `!!`
- **Filters**:
  ```bash
  cat file | cut -f 1
  cat file | grep 'keyword'
  sort | uniq -c
  ```
- **Advanced**:
  ```bash
  sed -n '10,15p' file
  awk 'NR == 11 {print $0}' file
  ```
- **Special Zeek Tool**:
  ```bash
  cat conn.log | zeek-cut uid proto id.orig_h id.orig_p id.resp_h id.resp_p
  ```

---

## Zeek Signatures
- **Structure**: ID, Conditions, Action
- Conditions:
  - Header (src-ip, dst-port, proto…)
  - Content (payload, http-request, ftp)
- Run with signature:
  ```bash
  zeek -C -r sample.pcap -s sample.sig
  ```

---

## Zeek Scripts
- Locations:
  - Base: `/opt/zeek/share/zeek/base`
  - Site: `/opt/zeek/share/zeek/site`
  - Policy: `/opt/zeek/share/zeek/policy`
- Config file: `/opt/zeek/share/zeek/site/local.zeek`
- Run script:
  ```bash
  zeek -C -r sample.pcap script.zeek
  ```

### Examples
- Extract new connections:
  ```zeek
  event new_connection(c: connection)
      {
          print "New Connection Found!", c$id$orig_h, c$id$resp_h;
      }
  ```

- Detect signature hits:
  ```zeek
  event signature_match(sig: string, data: string)
      {
          if (sig == "ftp-admin")
              print "Signature hit!", sig;
      }
  ```

---

## Framework Examples
### File Hashing
```zeek
@load /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek
```
```bash
cat files.log | zeek-cut md5 sha1 sha256
```

### File Extraction
```bash
zeek -C -r case1.pcap /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek
```

### Intelligence Framework
- Intel file: `/opt/zeek/intel/zeek_intel.txt`
```txt
#fields	indicator	indicator_type	meta.source	meta.desc
smart-fax.com	Intel::DOMAIN	zeek-intel-test	Zeek-Intelligence-Framework-Test
```

Run:
```bash
zeek -C -r case1.pcap intelligence-demo.zeek
```

---

## Zeek Package Manager (zkg)
- Commands:
  ```bash
  zkg install <pkg>
  zkg list
  zkg remove <pkg>
  zkg refresh
  zkg upgrade
  ```
- Example:
  ```bash
  zkg install zeek/cybera/zeek-sniffpass
  ```

### Package Usage
- From script:
  ```zeek
  @load /opt/zeek/share/zeek/site/zeek-sniffpass
  ```
- From CLI:
  ```bash
  zeek -Cr http.pcap zeek-sniffpass
  ```

---

✅ Summary:  
Zeek is more than an IDS—it’s an event-driven **network analysis and scripting framework**. It generates structured logs, supports signatures, has a flexible scripting language, and integrates with frameworks + packages to extend capabilities.  
