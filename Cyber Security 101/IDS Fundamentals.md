# IDS Fundamentals

## **Overview of IDS**
- Firewalls protect network boundaries, but IDS is needed to monitor traffic inside the network.
- IDS functions like surveillance cameras, detecting malicious activities even after bypassing the firewall.
- IDS generates alerts for security administrators but does not take action itself.

## **Types of IDS**
### **Deployment Modes**
1. **Host Intrusion Detection System (HIDS)**
   - Installed on individual hosts.
   - Detects threats specific to the host.
   - Resource-intensive, hard to manage in large networks.

2. **Network Intrusion Detection System (NIDS)**
   - Monitors traffic across the entire network.
   - Provides a centralized view of threats.

### **Detection Modes**
1. **Signature-Based IDS**
   - Detects threats using a database of known attack signatures.
   - Cannot detect zero-day attacks.
   - Example: Snort.

2. **Anomaly-Based IDS**
   - Learns normal network behavior and detects deviations.
   - Can detect zero-day attacks but generates false positives.

3. **Hybrid IDS**
   - Combines both signature-based and anomaly-based detection.
   - Leverages strengths of both approaches.

## **Snort IDS**
- Open-source IDS developed in 1998.
- Supports both signature-based and anomaly-based detection.
- Configurable with built-in and custom rules.

### **Modes of Snort**
| **Mode** | **Description** | **Use Case** |
|----------|---------------|-------------|
| Packet Sniffer Mode | Reads and displays network packets without analysis. | Used for network monitoring and troubleshooting. |
| Packet Logging Mode | Logs network traffic for later analysis in PCAP format. | Useful for forensic investigations. |
| Network Intrusion Detection System (NIDS) Mode | Monitors network traffic in real-time and detects known attack patterns. | Proactive threat monitoring. |

- Snort configuration files are located in `/etc/snort`.
- The primary configuration file is `snort.conf`.
- Built-in rule files are in the `rules` directory.

## **Snort Rule Format**
Example rule:
```
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
```
**Components of a Rule:**
1. **Action** – `alert` (notifies on detection).
2. **Protocol** – `ICMP` (used for ping requests).
3. **Source IP/Port** – `any` (matches any source).
4. **Destination IP/Port** – `$HOME_NET any` (matches any destination in the home network).
5. **Metadata:**
   - `msg` – Alert message displayed.
   - `sid` – Unique rule identifier.
   - `rev` – Rule revision number.

## **Creating and Testing Custom Snort Rules**
1. Edit the local rule file:
   ```bash
   sudo nano /etc/snort/rules/local.rules
   ```
2. Add a custom rule:
   ```bash
   alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
   ```
3. Save and exit (`CTRL+X`, then `Y`).
4. Run Snort for real-time detection:
   ```bash
   sudo snort -q -l /var/log/snort -i lo -A console -c /etc/snort/snort.conf
   ```
5. Test by pinging the loopback address:
   ```bash
   ping 127.0.0.1
   ```
6. Snort will generate alerts if the rule is triggered.

## **Analyzing PCAP Files with Snort**
- Snort can analyze historical network traffic stored in a PCAP file.
- Run Snort on a PCAP file:
  ```bash
  sudo snort -q -l /var/log/snort -r Task.pcap -A console -c /etc/snort/snort.conf
  ```
- Replace `Task.pcap` with the actual PCAP file path.
