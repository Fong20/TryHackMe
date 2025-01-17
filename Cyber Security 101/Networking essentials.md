
# Networking Essentials

## **Dynamic Host Configuration Protocol (DHCP)**

- **Purpose**: Automates IP address configuration, subnet mask, router (gateway), and DNS server settings.
- **Advantages**:
  - Reduces manual configuration.
  - Avoids IP address conflicts.
- **Ports Used**: 
  - UDP port 67 (server listens).
  - UDP port 68 (client sends).
- **DORA Process**:
  1. **Discover**: Client broadcasts a `DHCPDISCOVER` message.
  2. **Offer**: Server responds with a `DHCPOFFER` message.
  3. **Request**: Client sends a `DHCPREQUEST` message to accept.
  4. **Acknowledge**: Server confirms with a `DHCPACK` message.

### **Example DHCP Packet Exchange**:
```bash
tshark -r DHCP-G5000.pcap -n
1   0.000000      0.0.0.0 → 255.255.255.255 DHCP Discover - Transaction ID 0xfb92d53f
2   0.013904 192.168.66.1 → 192.168.66.133 DHCP Offer    - Transaction ID 0xfb92d53f
3   4.115318      0.0.0.0 → 255.255.255.255 DHCP Request  - Transaction ID 0xfb92d53f
4   4.228117 192.168.66.1 → 192.168.66.133 DHCP ACK      - Transaction ID 0xfb92d53f
```

---

## **Address Resolution Protocol (ARP)**

- **Purpose**: Resolves IP addresses to MAC addresses on the same Ethernet/WiFi network.
- **ARP Process**:
  1. Host sends an `ARP Request` to the broadcast MAC address (`ff:ff:ff:ff:ff:ff`).
  2. Target responds with an `ARP Reply`, providing its MAC address.
- **Packet Example**:
```bash
tshark -r arp.pcapng -Nn
1 0.000000000 cc:5e:f8:02:21:a7 → ff:ff:ff:ff:ff:ff ARP Who has 192.168.66.1? Tell 192.168.66.89
2 0.003566632 44:df:65:d8:fe:6c → cc:5e:f8:02:21:a7 ARP 192.168.66.1 is at 44:df:65:d8:fe:6c
```

---

## **Internet Control Message Protocol (ICMP)**

### **Ping**:
- Tests connectivity and measures **round-trip time (RTT)**.
- **Command**: 
  ```bash
  ping 192.168.11.1 -c 4
  ```
- **Example Output**:
  - 4 packets sent, 4 received, 0% packet loss.
  - RTT: min/avg/max/mdev.

### **Traceroute**:
- Discovers routes between a host and a target system.
- Uses **TTL (Time-to-Live)** and ICMP `Time Exceeded` messages.
- **Command**:
  ```bash
  traceroute example.com
  ```
- **Key Observations**:
  - Some routers may not respond (indicated by `*`).
  - Responding routers reveal IP or domain names.

---

## **Network Address Translation (NAT)**

- **Purpose**: Allows multiple private IPs to share a single public IP for Internet access.
- **Mechanism**:
  - Maintains a translation table of internal to external IP and port mappings.
- **Advantages**:
  - Conserves IPv4 address space.

---

## **Routing Protocols**

1. **OSPF (Open Shortest Path First)**:
   - Finds the most efficient route by sharing link-state information.
2. **EIGRP (Enhanced Interior Gateway Routing Protocol)**:
   - Cisco proprietary; calculates efficient routes based on metrics.
3. **BGP (Border Gateway Protocol)**:
   - Manages routing across multiple networks; used on the Internet.
4. **RIP (Routing Information Protocol)**:
   - Simple protocol; uses hop count to determine routes.

---
