
# Tcpdump: The Basics

## Overview
Tcpdump is a powerful command-line tool for capturing and analyzing network packets. It allows for real-time monitoring or saving of packet captures for later analysis. 

## Basic Usage
- **Run without arguments:** Test if `tcpdump` is installed.
- **Key components to specify:** 
  - Network interface (`-i INTERFACE`).
  - Output file for captured packets (`-w FILE`).
  - Display settings and filters.

## Specify the Network Interface
- `-i INTERFACE`: Listen on a specific network interface.
- `-i any`: Listen on all available interfaces.
- Example to view interfaces: `ip a s`.

## Save and Read Captured Packets
- `-w FILE`: Save captured packets to a `.pcap` file.
- `-r FILE`: Read packets from a `.pcap` file for analysis.

## Limit Captures
- `-c COUNT`: Capture a specific number of packets.
- `CTRL-C`: Interrupt packet capture.

## Prevent DNS and Port Resolution
- `-n`: Do not resolve IP addresses.
- `-nn`: Do not resolve both IP addresses and port numbers.

## Verbose Output
- `-v`: Slightly verbose output (e.g., TTL, packet length).
- `-vv` or `-vvv`: Increase verbosity.

## Filtering Packets
### By Host
- `host IP` or `host HOSTNAME`: Capture packets to/from a specific host.
- `src host IP`: Capture packets from a source.
- `dst host IP`: Capture packets to a destination.

### By Port
- `port PORT_NUMBER`: Filter packets by port.
- `src port PORT_NUMBER`: Filter packets by source port.
- `dst port PORT_NUMBER`: Filter packets by destination port.

### By Protocol
- Examples: `ip`, `ip6`, `tcp`, `udp`, `icmp`.

### Logical Operators
- `and`: Both conditions true (e.g., `host 1.1.1.1 and tcp`).
- `or`: Either condition true (e.g., `udp or icmp`).
- `not`: Negate condition (e.g., `not tcp`).

## Advanced Filtering
### By Length
- `greater LENGTH`: Packets ≥ specified length.
- `less LENGTH`: Packets ≤ specified length.

### By TCP Flags
- `tcp[tcpflags] == tcp-syn`: Only SYN flag set.
- `tcp[tcpflags] & tcp-syn != 0`: At least SYN flag set.
- `tcp[tcpflags] & (tcp-syn|tcp-ack) != 0`: At least SYN or ACK flags set.

## Additional Options
- `-q`: Brief packet information.
- `-e`: Include MAC addresses.
- `-A`: Print packets in ASCII.
- `-xx`: Display packets in hexadecimal.
- `-X`: Show packets in both hexadecimal and ASCII.

## Examples
1. **Capture 50 packets on `eth0` verbosely:**
   ```bash
   tcpdump -i eth0 -c 50 -v
   ```
2. **Save packets from `wlo1` to `data.pcap`:**
   ```bash
   tcpdump -i wlo1 -w data.pcap
   ```
3. **Filter DNS traffic on `ens5`:**
   ```bash
   tcpdump -i ens5 port 53 -n
   ```
4. **Filter HTTPS traffic to `example.com`:**
   ```bash
   tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
   ```

## Reading Captured Files
- Read and display 5 packets:
  ```bash
  tcpdump -r traffic.pcap -c 5 -n
  ```
- Count packets from source `192.168.124.1`:
  ```bash
  tcpdump -r traffic.pcap src host 192.168.124.1 -n | wc
  ```

## Binary Operations in Filters
- Use binary operations (`&`, `|`, `!`) with protocol headers.
- Syntax: `proto[expr:size]` (e.g., `tcp[tcpflags]`).

### Examples:
1. **Multicast packets:**
   ```bash
   ether[0] & 1 != 0
   ```
2. **IP packets with options:**
   ```bash
   ip[0] & 0xf != 5
   ```

## Reference
For advanced filtering, consult the manual:
```bash
man pcap-filter
```
