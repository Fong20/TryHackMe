
# Nmap The Basics 

## Overview:
Nmap is an open-source flexible network scanner that can be adapted to various scenarios and setups such as discover live hosts on a network and execute port scanning.

Note: Nmap is prefarably run as root `sudo` to prevent any restriction with Nmap’s abilities. Running Nmap as a local (non-root) user would limit us to fundamental types of scans such as ICMP echo and TCP connect scans

##  Target Specification
We need to identify the target to be scanned to discover live hosts in a network. There are three ways to discover live hosts:
- **IP Range**: Scan all the IP addresses in a certain range, this is done by using `-`  Eg:`192.168.0.1-10` scans all the IP addresses from 192.168.0.1 to 192.168.0.10.
- **Subnet**: Scan all the IP addresses in a certain subnet, this is done by using `/` Eg: `192.168.0.1/24` would be equivalent to 192.168.0.0-255
- **Hostname**: Use a domain name like `example.thm`.

## Discovering Live Hosts
- Nmap can be used to discover live hosts in a local network or remote network by using ping scan through the command `nmap -sn`. 
- Local network refers to the network we are directly connected to, such as an Ethernet or WiFi network. For directly connected networks (local network), Nmap sends ARP requests. When a device responds to the ARP request, Nmap labels it with “Host is up”.
- Remote network means that there consists of at least one router which separates our system from this network. For remote networks, ICMP or TCP/UDP requests are used by Nmap.

**Example: Scanning local network**

In the below diagram, `nmap -sn 192.168.66.0/24` scans the 192.168.66.0/24 network.

![image](https://github.com/user-attachments/assets/b6483073-1dd8-459f-9944-03074e3fb610)

Because we are scanning the local network, where we are connected via Ethernet or WiFi, we can look up the MAC addresses of the devices. Consequently, we can figure out the network card vendors, which is beneficial information as it can help us guess the type of target device(s).

**Example: Scanning remote network**

![image](https://github.com/user-attachments/assets/0d107cf0-3d7e-4ff6-8bb1-2f17cf1de051)

### Listing targets to be scanned without scanning
-  Nmap offers an option to list targets to be scanned without actually scanning them by using the option `-sL`. This option helps confirm the targets before running the actual scan.
-  Example, `nmap -sL 192.168.0.1/24` will list the 256 targets that will be scanned. 

## Port Scanning
- **TCP Connect Scan (-sT)**: Completes the full three-way handshake.
- **SYN Scan (-sS)**: Sends only a SYN packet, avoiding full handshake; stealthy.
- **UDP Scan (-sU)**: Discovers services on UDP ports.
- **Fast Scan (-F)**: Scans the top 100 most common ports.
- **Port Range (-p)**: Specify ports, e.g., `-p10-1024` or `-p-` (all ports).

## Service Detection
- **OS Detection (-O)**: Identifies operating system details.
- **Service Version Detection (-sV)**: Detects versions of services on open ports.
- **Aggressive Scan (-A)**: Combines OS detection, version scanning, and traceroute.

## Controlling Scan Behavior
- **Treat Hosts as Online (-Pn)**: Scans all targets regardless of discovery results.
- **Timing Templates (-T<0-5>)**: Adjusts scan speed.
  - Options: `paranoid (0)`, `sneaky (1)`, `polite (2)`, `normal (3)`, `aggressive (4)`, `insane (5)`.
- **Parallel Probes**:
  - `--min-parallelism` and `--max-parallelism` control probe concurrency.
- **Packet Rate**:
  - `--min-rate` and `--max-rate` set packet sending rates.
- **Host Timeout (--host-timeout)**: Limits time per host.

## Real-Time Feedback
- **Verbose Output (-v)**: Provides detailed progress. Levels: `-v`, `-vv`, `-vvvv`.
- **Debugging (-d)**: Enables detailed logs. Levels: `-d`, `-d9`.

## Saving Scan Results
- **Output Formats**:
  - `-oN <file>`: Normal human-readable format.
  - `-oX <file>`: XML format.
  - `-oG <file>`: Grepable format.
  - `-oA <base>`: Saves all formats.

## Notes on Permissions
- Running as **root** or with **sudo** enables advanced scan types like SYN scans. Non-root users default to TCP connect scans.

## Summary of important Nmap commands

| Option                          | Description                                    |
|---------------------------------|------------------------------------------------|
| -sL                             | List targets without scanning                 |
| -sn                             | Ping scan – host discovery only               |
| -sT                             | TCP connect scan                              |
| -sS                             | TCP SYN scan                                  |
| -sU                             | UDP scan                                      |
| -F                              | Fast mode – scans top 100 common ports        |
| -p[range]                       | Specify port range (e.g., `-p1-65535`)        |
| -Pn                             | Treat all hosts as online                     |
| -O                              | OS detection                                  |
| -sV                             | Service version detection                     |
| -A                              | Aggressive scan                               |
| -T<0-5>                         | Timing template                               |
| --min-parallelism <numprobes>   | Minimum parallel probes                       |
| --max-parallelism <numprobes>   | Maximum parallel probes                       |
| --min-rate <number>             | Minimum packet rate                           |
| --max-rate <number>             | Maximum packet rate                           |
| --host-timeout <time>           | Set max time for a host                       |
| -v                              | Verbose output                                |
| -d                              | Debugging output                              |
| -oN <file>                      | Save in normal format                         |
| -oX <file>                      | Save in XML format                            |
| -oG <file>                      | Save in grepable format                       |
| -oA <base>                      | Save in all formats                           |
