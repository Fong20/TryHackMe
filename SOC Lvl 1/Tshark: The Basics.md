# Tshark: The Basics

## Overview
- **TShark**: Open-source command-line network traffic analyzer by Wireshark developers.  
- Works similarly to **tcpdump** but supports **Wireshark filters** and more advanced analysis.
- Ideal for:
  - Data carving
  - In-depth packet analysis
  - Automation & scripting

---

## 🎯 Learning Objectives
1. Filter traffic with TShark  
2. Implement Wireshark filters in TShark  
3. Automate packet filtering with TShark  

---

## ⚙️ Common Command-Line Tools Used with TShark
| Tool | Purpose |
|------|----------|
| capinfos | Provides capture file details |
| grep | Searches text patterns |
| cut | Cuts specific fields from lines |
| uniq | Removes duplicate lines |
| nl | Adds line numbers |
| sed | Stream editing |
| awk | Pattern scanning and text processing |

---

## 💻 TShark CLI & Parameters

| Parameter | Description | Example |
|------------|--------------|----------|
| -h | Help page | tshark -h |
| -v | Show version | tshark -v |
| -D | List available interfaces | tshark -D |
| -i | Select interface | tshark -i 1 |
| *(no param)* | Default sniffing | tshark |

---

## 📡 Sniffing Examples

### List interfaces
```
sudo tshark -D
```

### Sniff traffic (default)
```
tshark
```

### Sniff using specific interface
```
tshark -i 2
```

---

## 📂 Read & Write Operations

### Read a Capture File
```
tshark -r demo.pcapng
```

### Limit output by packet count
```
tshark -r demo.pcapng -c 2
```

### Write captured packets to a file
```
tshark -w write-demo.pcap
```

### Combine read and write
```
tshark -r demo.pcapng -c 1 -w write-demo.pcap
```

---

## 🔍 View Packet Bytes

Show packet data in hex and ASCII:
```
tshark -r write-demo.pcap -x
```

---

## 🧾 Verbosity

| Mode | Description | Example |
|-------|--------------|----------|
| Default | 1-line summary | tshark -r demo.pcapng -c 1 |
| Verbose | Detailed Wireshark-like output | tshark -r demo.pcapng -c 1 -V |

---

## ⏱️ Capture Conditions

| Parameter | Description | Example |
|------------|--------------|----------|
| -a | Autostop conditions | tshark -w test.pcap -a duration:1 |
| -b | Ring buffer control (loops) | tshark -w test.pcap -b filesize:10 |

**Combined Example**
```
tshark -w autostop-demo.pcap -a duration:2 -a filesize:5 -a files:5
```

---

## 🎚️ Filtering

### Capture vs Display Filters
| Filter Type | Purpose | Flag | Syntax Example |
|--------------|----------|------|----------------|
| Capture | Filter before saving packets | -f | tshark -f "host 10.10.10.10" |
| Display | Filter while viewing | -Y | tshark -Y "ip.addr == 10.10.10.10" |

---

### Capture Filter Examples

| Filter Type | Example |
|--------------|----------|
| Host | tshark -f "host 10.10.10.10" |
| Network | tshark -f "net 10.10.10.0/24" |
| Port | tshark -f "port 80" |
| Port Range | tshark -f "portrange 80-100" |
| Source IP | tshark -f "src host 10.10.10.10" |
| Destination IP | tshark -f "dst host 10.10.10.10" |
| Protocol | tshark -f "tcp" |
| MAC Address | tshark -f "ether host F8:DB:C5:A2:5D:81" |
| ICMP Protocol (IP Proto 1) | tshark -f "ip proto 1" |

---

### Display Filter Examples

| Filter Category | Example |
|-----------------|----------|
| IP | tshark -Y 'ip.addr == 10.10.10.10' |
| IP Range | tshark -Y 'ip.addr == 10.10.10.0/24' |
| Source IP | tshark -Y 'ip.src == 10.10.10.10' |
| Destination IP | tshark -Y 'ip.dst == 10.10.10.10' |
| TCP Port | tshark -Y 'tcp.port == 80' |
| Source TCP Port | tshark -Y 'tcp.srcport == 80' |
| HTTP Packets | tshark -Y 'http' |
| HTTP Response Code 200 | tshark -Y 'http.response.code == 200' |
| DNS Packets | tshark -Y 'dns' |
| DNS “A” Query | tshark -Y 'dns.qry.type == 1' |

---

### Count Filtered Packets
Add line numbers to output:
```
tshark -r demo.pcapng -Y 'http' | nl
```

---

## 🧰 Traffic Generation Tools

| Tool | Example | Purpose |
|------|----------|----------|
| curl | curl tryhackme.com | Generate HTTP traffic |
| nc (TCP) | nc 10.10.10.10 4444 -vw 5 | Create TCP traffic |
| nc (UDP) | nc -u 10.10.10.10 4444 -vw 5 | Create UDP traffic |

---

✅ **Key Takeaways**
- Use -f for live capture filters, -Y for display filters.
- Combine with shell tools (grep, nl, awk) for automation.
- Use -V for in-depth analysis, -x for byte-level view.
- Manage captures efficiently using -a (autostop) & -b (ring buffer).
