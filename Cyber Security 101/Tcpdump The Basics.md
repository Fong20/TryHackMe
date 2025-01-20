
# Tcpdump: The Basics

## Overview
Tcpdump is a powerful command-line tool for capturing and analyzing network packets. It allows for real-time monitoring or saving of packet captures for later analysis. 

## Basic tcpdump info
- To test if tcpdump is installed, Run the command `tcpdump` in the terminal without any arguments.
- However, if we want to capture any packets, we must be specific about what interface to listen to, where to write the captured packets, and how to display the packets.
- In tcpdump, we need **root privileges to capture packets, `sudo tcpdump`** while **root privileges are not required to read packets from packet capture file.**
  
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
  
### Avoid resolving DNS and Port Resolution
By default, tcpdump will resolve IP addresses and print friendly domain names where possible. To avoid making such DNS lookups, we can use the following argument:

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
Considering the number of packets seen by our network card, it is impossible to see everything at once; we need to be specific and capture what we are interested in inspecting.

Tcpdump supports filtering to capture packets which we are interested in inspecting. There are several ways of filtering to capture the required packets:

1. Filtering By Host
2. Filtering By Port
3. Filtering By Protocol
4. Usage of Logical Operators

### Filtering By Host
- `host IP` or `host HOSTNAME`: Capture packets to/from a specific host.
- `src host IP`: Capture packets which are sent from a source.
- `dst host IP`: Capture packets which are sent to a destination.

**Example:**

In the terminal below, we capture all the packets exchanged with example.com and save them to http.pcap.

![image](https://github.com/user-attachments/assets/5b2679ea-6244-4807-8cf9-c326fc363623)

### Filtering By Port
- `port PORT_NUMBER`: Filter packets by port.
- `src port PORT_NUMBER`: Filter packets which are sent by source port.
- `dst port PORT_NUMBER`: Filter packets which are sent to the destination port.

Example: **Capturing DNS traffic on interface `ens5`:**

   ```bash
   tcpdump -i ens5 port 53 -n
   ```

Based on the screenshot below, the terminal below shows two DNS queries: the first query requests the IPv4 address used by example.org, while the second requests the IPv6 address associated with example.org.

![image](https://github.com/user-attachments/assets/6ba440a6-242d-4248-83cd-124da2a4e5cb)

### Filtering By Protocol
- Tcpdump supports packet capture filtering through types of protocols
- Examples: `ip`, `ip6`, `tcp`, `udp`, `icmp`.

**Example: Filtering packet capture to ICMP packets.**
-  Based on the below screenshot, we can see an ICMP echo request and reply, which is a possible indication that someone is running the ping command.
-  There is also an ICMP time exceeded; this might be due to running the traceroute command 

![image](https://github.com/user-attachments/assets/f1aa359e-42d7-4ac4-848a-04dac25ac5a0)

### Usage of Logical Operators
- `and`: Captures packets where both conditions are true. (e.g., `host 1.1.1.1 and tcp` captures tcp traffic associated with the host 1.1.1.1.).
- `or`: Captures packets where either one of the conditions is true (e.g., `udp or icmp` captures UDP or ICMP traffic.).
- `not`: Captures packets when the condition is not true (e.g., `not tcp` captures all packets except TCP segments; we expect to find UDP, ICMP, and ARP packets among the results.).

**Example: Listen on interfcace eth0, Filter HTTPS traffic to `example.com` (tcp and port 443) and save the packet capture to a file name https.pcap**

   ```bash
   tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
   ```

### Summary of filtering

![image](https://github.com/user-attachments/assets/bdafb4c0-db23-4e4c-952a-bd450e66a089)


## Advanced Filtering
Besides basic filtering, there are many more ways to filter packets.

1. Filtering by Length
2. Filtering by content of Header Bytes
3. Filtering by TCP Flags
   
### Filtering By Length
- `greater LENGTH`: Filters Packets ≥ specified length.
- `less LENGTH`: Filters Packets ≤ specified length.

### Filtering by content of Header Bytes
Using pcap-filter, Tcpdump allows you to refer to the contents of any byte in the header using the following syntax proto[expr:size], where:

- **proto** refers to the protocol. For example, arp, ether, icmp, ip, ip6, tcp, and udp refer to ARP, Ethernet, ICMP, IPv4, IPv6, TCP, and UDP respectively.
- **expr** indicates the byte offset, where 0 refers to the first byte.
- **size** indicates the number of bytes that interest us, which can be one, two, or four. It is optional and is one by default.

**Example 1:**

 ```bash
   ether[0] & 1 != 0
   ```

This command takes the first byte in the Ethernet header and the decimal number 1 (i.e., 0000 0001 in binary) and applies the & (the And binary operation). It will return true if the result is not equal to the number 0 (i.e., 0000 0000). The purpose of this filter is to show packets sent to a multicast address. A multicast Ethernet address is a particular address that identifies a group of devices intended to receive the same data.

**Example 2:**

 ```bash
   ip[0] & 0xf != 5
   ```

This command takes the first byte in the IP header and compares it with the hexadecimal number F (i.e., 0000 1111 in binary). It will return true if the result is not equal to the (decimal) number 5 (i.e., 0000 0101 in binary). The purpose of this filter is to catch all IP packets with options.

### Filtering By TCP Flags
Example of tcp flags: 
- tcp-syn TCP SYN (Synchronize)
- tcp-ack TCP ACK (Acknowledge)
- tcp-fin TCP FIN (Finish)
- tcp-rst TCP RST (Reset)
- tcp-push TCP Push

**Commands:**
- `tcp[tcpflags] == tcp-syn`: capture TCP packets with only the SYN (Synchronize) flag set, while all the other flags are unset.
- `tcp[tcpflags] & tcp-syn != 0`: capture TCP packets with at least the SYN (Synchronize) flag set..
- `tcp[tcpflags] & (tcp-syn|tcp-ack) != 0`: capture TCP packets with at least the SYN (Synchronize) or ACK (Acknowledge) flags set.

## Displaying packets
Tcpdump is a rich program with many options to customize how the packets are printed and displayed.

**Commands to modify the information displayed:**
- `-q`: Brief packet information.

The following example shows the timestamp, along with the source and destination IP addresses and source and destination port numbers.

![image](https://github.com/user-attachments/assets/ef566384-338c-4d44-8680-5d21d075acd6)

- `-e`: Include MAC addresses.

If you are on an Ethernet or WiFi network and want to include the MAC addresses in Tcpdump output, all you need to do is to add -e. This is convenient when you are learning how specific protocols, such as ARP and DHCP function. It can also help you track the source of any unusual packets on your network.

![image](https://github.com/user-attachments/assets/32552616-0dc4-4077-80b4-03b3877f7af8)

- `-A`: Print packets in ASCII.

ASCII stands for American Standard Code for Information Interchange; ASCII codes represent text. In other words, you can expect -A to display all the bytes mapped to English letters, numbers, and symbols.

![image](https://github.com/user-attachments/assets/015a19aa-e46f-4fee-8e6e-92acfba0b46b)

- `-xx`: Display packets in hexadecimal.

ASCII format works well when the packet contents are plain-text English. It won’t work if the contents have undergone encryption or even compression. Furthermore, it won’t work for languages that don’t use the English alphabet. Hence, we need another way to display the packet contents regardless of format. Being 8 bits, any octet can be displayed as two hexadecimal digits. (Each hexadecimal digit represents 4 bits.) To display the packets in hexadecimal format, we must add -xx as shown in the terminal below.

![image](https://github.com/user-attachments/assets/bad69c5d-051f-4fc7-b560-4928ff573536)

- `-X`: Show packets in both hexadecimal and ASCII.

If we would like to display the captured packets in both hexadecimal and ASCII formats, Tcpdump makes it easy with the -X option.

![image](https://github.com/user-attachments/assets/aa528381-ae61-40e4-93fc-f782f46a7175)

