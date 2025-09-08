# Snort

## Overview
- **SNORT**: Open-source, rule-based **Network Intrusion Detection and Prevention System (NIDS/NIPS)**.  
- Developed by **Martin Roesch**, open-source contributors, and **Cisco Talos** team.  
- Functions: **Sniffer**, **Logger**, **IDS/IPS**.  

---

## IDS vs IPS
- **IDS (Detection)**: Passive → Detects suspicious events & raises alerts.
  - **NIDS**: Monitors traffic across network.
  - **HIDS**: Monitors single endpoint traffic.  
- **IPS (Prevention)**: Active → Blocks or terminates malicious events.
  - **NIPS**: Protects entire subnet.
  - **NBA**: Behavior-based, requires training/baselining.
  - **WIPS**: Protects wireless traffic.
  - **HIPS**: Active protection on endpoint device.  

---

## Detection / Prevention Techniques
1. **Signature-based** → Matches known patterns.  
2. **Behavior-based** → Detects anomalies (new threats).  
3. **Policy-based** → Detects policy violations.  

---

## Snort Capabilities
- Live traffic analysis  
- Attack & probe detection  
- Packet logging  
- Protocol analysis  
- Real-time alerting  
- Pre-processors, modules, plugins  
- Cross-platform (Linux & Windows)  

---

## Snort Modes
1. **Sniffer Mode** → Displays packets in console.  
   ```bash
   sudo snort -v -i eth0
   ```
   Options:  
   - `-v` verbose  
   - `-d` packet data  
   - `-e` headers  
   - `-X` hex output  
   - `-i` interface  

2. **Logger Mode** → Logs packets.  
   ```bash
   sudo snort -dev -l .
   sudo snort -dev -K ASCII
   sudo snort -r logname.log
   ```
   - `-l` log dir (default: `/var/log/snort`)  
   - `-K ASCII` → Human-readable logs  
   - `-r` read log files  
   - `-n` limit number of packets  

3. **IDS/IPS Mode**  
   ```bash
   sudo snort -c /etc/snort/snort.conf -T   # test config
   sudo snort -c /etc/snort/snort.conf -N   # no logging
   sudo snort -c /etc/snort/snort.conf -A console
   ```
   - `-c` config file  
   - `-T` test config  
   - `-N` disable logging  
   - `-D` background mode  
   - `-A [console|cmg|fast|full|none]` alert modes  

4. **IPS Mode**  
   ```bash
   sudo snort -Q --daq afpacket -i eth0:eth1
   ```
   Requires **two interfaces**.  

5. **PCAP Mode**  
   ```bash
   snort -r capture.pcap
   snort --pcap-single=sample.pcap
   ```

---

## Snort Rules Basics
**Format:**
```
action protocol src_ip src_port direction dst_ip dst_port (options)
```

### Actions
- `alert` → Generate alert + log  
- `log` → Log only  
- `drop` → Block + log  
- `reject` → Block + log + reset connection  

### Protocols
- Supports: **IP, TCP, UDP, ICMP**  
- Application traffic filtered via **ports**  

### Examples
- Alert on ICMP from host:
  ```snort
  alert icmp 192.168.1.56 any <> any any (msg:"ICMP Packet From"; sid:100001; rev:1;)
  ```
- Alert on port 21 (FTP):
  ```snort
  alert tcp any any <> any 21 (msg:"FTP Detected"; sid:100002; rev:1;)
  ```
- Exclude subnet:
  ```snort
  alert icmp !192.168.1.0/24 any <> any any (msg:"ICMP Outside Subnet"; sid:100003; rev:1;)
  ```

---

## Rule Options
- **General**
  - `msg` → Alert message  
  - `sid` → Unique rule ID  
  - `rev` → Revision number  
  - `reference` → CVE or link  

- **Payload**
  - `content` → Match ASCII/HEX  
  - `nocase` → Case-insensitive  
  - `fast_pattern` → Optimize multiple content rules  

- **Non-Payload**
  - `id` → Match IP ID field  
  - `flags` → Match TCP flags (`S`, `A`, `F`, etc.)  
  - `dsize` → Match payload size  
  - `sameip` → Source = Destination  

---

## Snort Configuration
- **Config files:**
  - `/etc/snort/snort.conf` → Main config  
  - `/etc/snort/rules/local.rules` → User rules  

- **snort.conf sections**:
  - Step 1: Set network vars (`HOME_NET`, `EXTERNAL_NET`)  
  - Step 2: Configure decoder (DAQ modules)  
  - Step 6: Output plugins  
  - Step 7: Custom ruleset (`include $RULE_PATH/local.rules`)  

- **DAQ Modules**:
  - `pcap` → Sniffer mode  
  - `afpacket` → IPS inline  
  - `ipq`, `nfq`, `ipfw`, `dump`  

---

## Snort Components
1. Packet Decoder  
2. Pre-processors  
3. Detection Engine  
4. Logging & Alerting  
5. Output Plugins  

---

## Rulesets
- **Community Rules** → Free, public  
- **Registered Rules** → Free, requires registration, 30-day delay  
- **Subscriber Rules** → Paid, updated twice weekly  

---

✅ **Key takeaway**:  
- **IDS = Detect only, IPS = Detect + Prevent**  
- **Snort** is flexible (sniffer, logger, IDS, IPS, PCAP analysis).  
- **Rules** are powerful, customizable, and essential for detection.  
