
# Tcpdump: The Basics

## Overview
Tcpdump is a powerful command-line tool for capturing and analyzing network packets. It allows for real-time monitoring or saving of packet captures for later analysis. 

## Basic Usage
- **Run without arguments:** Test if `tcpdump` is installed.
- **Key components to specify:** 
  - Network interface (`-i INTERFACE`).
  - Output file for captured packets (`-w FILE`).
  - Display settings and filters.

In tcpdump, we need root privileges to capture packets while root privileges are not required to read packets from packet capture file.

### Specify the Network Interface
ip address show command, `ip a s` is used to list available network interfaces. Once we have identified the network interface we want to listen, we can use the following commands:

- `-i INTERFACE`: Listen on a specific network interface.

If we wish to listen on all available interfaces, we can use the following command:

- `-i any`: Listen on all available interfaces.

### Save Captured Packets
We can save the captured packets in a pcap file and the saved packets can be inspected later using another program, such as Wireshark.

- `-w FILE`: Save captured packets to a `.pcap` file.

Example: **Save packets from `wlo1` to `data.pcap`:**

   ```bash
   tcpdump -i wlo1 -w data.pcap
   ```

### Read Captured Packets
Tcpdump can be used to read packets from a file which is very useful for learning about protocol behaviour. You can capture network traffic over a suitable time frame to inspect a specific protocol, then read the captured file while applying filters to display the packets you are interested in. Furthermore, it might be a packet capture file that contains a network attack that took place, and you inspect it to analyze the attack.

- `-r FILE`: Read packets from a `.pcap` file for analysis.

### Limit Captures
We can specify the number of packets to capture in tcpdump by using the following command:
- `-c COUNT`: Capture a specific number of packets.

**Example: Read and display 5 packets:**

  ```bash
  tcpdump -r traffic.pcap -c 5 -n
  ```

Without specifying a count, the packet capture will continue till you interrupt it, by pressing CTRL-C. 
- `CTRL-C`: Interrupt packet capture.

### Counting the number of packets captured
We can count the number of lines of packets captured by piping the output via the wc command.

**Example: Count the amount of packets from source `192.168.124.1`:**
  ```bash
  tcpdump -r traffic.pcap src host 192.168.124.1 -n | wc
  ```
  
### Prevent DNS and Port Resolution
Tcpdump will resolve IP addresses and print friendly domain names where possible. To avoid making such DNS lookups, we can use the following argument:

- `-n`: Do not resolve IP addresses to domain name.

Similarly, if we don’t want port numbers to be resolved, such as port 80 being resolved to http, you can use the following command to stop both DNS and port number lookups.

- `-nn`: Do not resolve both IP addresses and port numbers.

### Verbose Output
If we want to print more details about the packets, we can use -v to produce a slightly more verbose output. According to the Tcpdump manual page (man tcpdump), the addition of -v will print “the time to live, identification, total length and options in an IP packet” among other checks. The -vv will produce more verbose output; the -vvv will provide even more verbosity; check the manual page for details.

- `-v`: Slightly verbose output (e.g., TTL, packet length).
- `-vv` or `-vvv`: Increase verbosity.

Example: **Capture 50 packets on `eth0` verbosely:**

   ```bash
   tcpdump -i eth0 -c 50 -v
   ```

## Filtering Packets
### By Host
- `host IP` or `host HOSTNAME`: Capture packets to/from a specific host.
- `src host IP`: Capture packets from a source.
- `dst host IP`: Capture packets to a destination.

### By Port
- `port PORT_NUMBER`: Filter packets by port.
- `src port PORT_NUMBER`: Filter packets by source port.
- `dst port PORT_NUMBER`: Filter packets by destination port.

Example: **Filter DNS traffic on `ens5`:**

   ```bash
   tcpdump -i ens5 port 53 -n
   ```

### By Protocol
- Examples: `ip`, `ip6`, `tcp`, `udp`, `icmp`.

Example: **Filter HTTPS traffic to `example.com`:**
   ```bash
   tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
   ```

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


