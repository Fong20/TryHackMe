
# Nmap The Basics 

## Target Specification
- **IP Range**: Specify IPs like `192.168.0.1-10`.
- **Subnet**: Use CIDR notation, e.g., `192.168.0.1/24`.
- **Hostname**: Use a domain name like `example.thm`.

## Discovering Live Hosts
- **Ping Scan (-sn)**: Determines active hosts without probing services.
  - Example: `nmap -sn 192.168.66.0/24`
  - For directly connected networks, Nmap sends ARP requests.
  - For remote networks, ICMP or TCP/UDP requests are used.
- **List Targets (-sL)**: Lists targets without scanning.

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

## Command Reference Summary
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
