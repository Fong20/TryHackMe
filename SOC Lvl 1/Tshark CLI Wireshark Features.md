# TShark: Advanced Features & Command-Line Wireshark

## 1. Overview
- **TShark** = Command-line version of Wireshark.
- Supports **Wireshark GUI features** via CLI.
- **Three Key Points:**
  1. Applies to all packets unless filtered.
  2. Mirrors Wireshark packet operations.
  3. Output headers explain parameters used.

---

## 2. Colourised Output
```bash
tshark -r colour.pcap --color
```
- Enables Wireshark-like coloured output.
- Helps spot anomalies faster.

---

## 3. Protocol Hierarchy
### Full hierarchy:
```bash
tshark -r demo.pcapng -z io,phs -q
```
### Focus on UDP:
```bash
tshark -r demo.pcapng -z io,phs,udp -q
```
- Displays packet protocol tree summary (frames, bytes, etc.).
- Useful for identifying dominant protocols.

---

## 4. Packet Lengths Tree
```bash
tshark -r demo.pcapng -z plen,tree -q
```
- Shows distribution of packet sizes.
- Helps detect unusually large/small packets.

---

## 5. Endpoints
### IPv4 Example:
```bash
tshark -r demo.pcapng -z endpoints,ip -q
```
| Filter | Purpose |
|---------|----------|
| eth | Ethernet |
| ip | IPv4 |
| ipv6 | IPv6 |
| tcp | TCP (IPv4 & IPv6) |
| udp | UDP (IPv4 & IPv6) |
| wlan | Wi-Fi |

---

## 6. Conversations
### IPv4 Example:
```bash
tshark -r demo.pcapng -z conv,ip -q
```
- Summarises traffic between two nodes.
- Shows total frames, bytes, start time, duration.

---

## 7. Expert Info
```bash
tshark -r demo.pcapng -z expert -q
```
- Displays Wireshark’s “Expert Info” diagnostics.
- Categorises anomalies (Sequence, Retransmissions, etc.).

---

## 8. IPv4 & IPv6 Statistics
```bash
tshark -r demo.pcapng -z ptype,tree -q
```
- Shows protocol distribution (TCP, UDP, etc.).

### Host & Address Views:
```bash
tshark -r demo.pcapng -z ip_hosts,tree -q
tshark -r demo.pcapng -z ip_srcdst,tree -q
```

### Destination & Port Summary:
```bash
tshark -r demo.pcapng -z dests,tree -q
```

---

## 9. DNS Statistics
```bash
tshark -r demo.pcapng -z dns,tree -q
```
- Summarises DNS activity (rcode, opcode, queries).

---

## 10. HTTP Statistics
```bash
tshark -r demo.pcapng -z http,tree -q
tshark -r demo.pcapng -z http2,tree -q
tshark -r demo.pcapng -z http_srv,tree -q
tshark -r demo.pcapng -z http_req,tree -q
tshark -r demo.pcapng -z http_seq,tree -q
```
- Provides packet counts, request/response details, and status codes.

---

## 11. Follow Streams
| Protocol | Example |
|-----------|----------|
| TCP | `-z follow,tcp,ascii,0 -q` |
| UDP | `-z follow,udp,ascii,0 -q` |
| HTTP | `-z follow,http,ascii,0 -q` |

Example:
```bash
tshark -r demo.pcapng -z follow,tcp,ascii,1 -q
```
- Displays readable stream data (client-server exchange).

---

## 12. Export Objects
Extract files from captured traffic:
```bash
tshark -r demo.pcapng --export-objects http,/path/to/folder -q
```
Supported protocols:
- DICOM, HTTP, IMF, SMB, TFTP

---

## 13. Credentials Extraction
```bash
tshark -r credentials.pcap -z credentials -q
```
- Finds **cleartext credentials** (FTP, HTTP, IMAP, POP, SMTP).

---

## 14. Advanced Filtering

### Operators
| Filter | Description |
|---------|--------------|
| contains | Case-sensitive search within packet data |
| matches | Case-insensitive regex search |

---

### “Contains” Example
Find “Apache” servers:
```bash
tshark -r demo.pcapng -Y 'http.server contains "Apache"'
```

### “Matches” Example
Find all `GET` or `POST` requests:
```bash
tshark -r demo.pcapng -Y 'http.request.method matches "(GET|POST)"'
```

---

## 15. Extract Fields
Extract selected data fields:
```bash
tshark -r demo.pcapng -T fields -e ip.src -e ip.dst -E header=y
```
- Use `-e` for each field.
- Add `-E header=y` to print field headers.

---

## 16. Common Use Cases

### 🖥️ Extract Hostnames
```bash
tshark -r hostnames.pcapng -T fields -e dhcp.option.hostname | awk NF | sort -r | uniq -c | sort -r
```
- Extracts and counts unique DHCP hostnames.

### 🌐 Extract DNS Queries
```bash
tshark -r dns-queries.pcap -T fields -e dns.qry.name | awk NF | sort -r | uniq -c | sort -r
```

### 🧭 Extract User Agents
```bash
tshark -r user-agents.pcap -T fields -e http.user_agent | awk NF | sort -r | uniq -c | sort -r
```
- Reveals browsers, tools (e.g., sqlmap, Nmap scripts, etc.)

---

## 17. Linux Output Management Tips
| Command | Purpose |
|----------|----------|
| `awk NF` | Remove empty lines |
| `sort -r` | Reverse sort |
| `uniq -c` | Count unique entries |

---

## 18. Key Takeaways
- `-z` handles **statistics and analytical views**.
- `-T fields` extracts **custom field data**.
- Combine with `awk`, `sort`, `uniq` for **clean, analyzable outputs**.
- Mirrors Wireshark GUI but allows **automation, scripting, and remote analysis**.

---

✅ **End of Notes – TShark Advanced CLI Reference**
