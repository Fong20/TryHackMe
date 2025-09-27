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
  
In addition to Linux command-line tools, one auxiliary program called zeek-cut reduces the effort of extracting specific columns from log files. Each log file provides "field names" in the beginning. This information will help you while using zeek-cut. Make sure that you use the "fields" and not the "types".

**Example:**

Extract the uid, protocol, source and destination hosts, and source and destination ports from the conn.log by first reading the logs with the cat command and then extract the event of interest fields with zeek-cut auxiliary to compare the difference.
  
  ```bash
  cat conn.log | zeek-cut uid proto id.orig_h id.orig_p id.resp_h id.resp_p
  ```

---

## Zeek Signatures
Zeek supports signatures to have rules and event correlations to find noteworthy activities on the network. Zeek signatures use low-level pattern matching and cover conditions similar to Snort rules. Unlike Snort rules, Zeek rules are not the primary event detection point. Zeek has a scripting language and can chain multiple events to find an event of interest.

- **Structure**: ID, Conditions, Action
- Conditions:
  - Header (src-ip, dst-port, proto…)
  - Content (payload, http-request, ftp)

- Runz Zeek with signature:
  ```bash
  zeek -C -r sample.pcap -s sample.sig
  ```

---

## Zeek Scripts
Zeek has its own event-driven scripting language, which is as powerful as high-level languages and allows us to investigate and correlate the detected events.

- Locations:
  - Base: `/opt/zeek/share/zeek/base`
  - Site: `/opt/zeek/share/zeek/site`
  - Policy: `/opt/zeek/share/zeek/policy`
- Config file: `/opt/zeek/share/zeek/site/local.zeek`

- Run Zeek with script:
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

## Zeek Framework 
Zeek has 15+ frameworks that help analysts to discover the different events of interest.

### File Framework, grabbing file hashes

```zeek
zeek -C -r case1.pcap hash-demo.zeek
```

or

```zeek
zeek -C -r case1.pcap /opt/zeek/share/zeek/policy/frameworks/files/hash-all-files.zeek 
```

Using zeek-cut to obtain md5, sha1, and sha256 of file hash
```bash
cat files.log | zeek-cut md5 sha1 sha256
```

### File Framework, extracting files
The file framework can extract the files from the pcap. A new folder called "extract_files" is automatically created, and all detected files are located in it.

```bash
zeek -C -r case1.pcap /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek
```

### Intelligence Framework
- The intelligence framework can work with data feeds to process and correlate events and identify anomalies. The intelligence framework requires a feed to match and create alerts from the network traffic. 
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
Zeek Package Manager helps users install third-party scripts and plugins to extend Zeek functionalities with ease. The package manager is installed with Zeek and available with the zkg command. Users can install, load, remove, update and create packages with the "zkg" tool. 

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

#### 1. Cleartext Submission of Password, zeek-sniffpass
The package finds cleartext password submissions, provided notice, and grabbed the usernames.

- From script:
  ```zeek
  @load /opt/zeek/share/zeek/site/zeek-sniffpass
  ```
- From CLI:
  ```bash
  zeek -Cr http.pcap zeek-sniffpass
  ```

#### 2. Geolocation Data, "geoip-conn"
This package provides geolocation information for the IP addresses in the conn.log file. It depends on "GeoLite2-City.mmdb" database created by MaxMind. This package provides location information for only matched IP addresses from the internal database.   

- From CLI:
  ```bash
  zeek -Cr case1.pcap geoip-conn
  ```
  
---


✅ Summary:  
Zeek is more than an IDS—it’s an event-driven **network analysis and scripting framework**. It generates structured logs, supports signatures, has a flexible scripting language, and integrates with frameworks + packages to extend capabilities.  
