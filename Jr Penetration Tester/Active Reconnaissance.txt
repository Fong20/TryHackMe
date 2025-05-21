
# Active Reconnaissance
- Active reconnaissance requires you to make some kind of contact with your target.
- Eg: phone call or a visit to the target company, usually as part of social engineering, visiting their website or checking if their firewall has an SSH port open.
- Active reconnaissance begins with direct connections made to the target machine. Any such connection might leave information in the logs showing the client IP address, time of the connection, and duration of the connection, among other things. 
- However, not all connections are suspicious. It is possible to let your active reconnaissance appear as regular client activity. Consider web browsing; no one would suspect a browser connected to a target web server among hundreds of other legitimate users.

## Active Reconnaissance tools
### 🧭 Web Browsers & Developer Tools
- **Default Ports**:
  - HTTP: TCP 80
  - HTTPS: TCP 443
  - Example: `https://127.0.0.1:8834/` accesses port 8834 on localhost.

- **Developer Tools Shortcuts**:
  - Linux/Windows: `Ctrl+Shift+I`
  - macOS: `Option + Command + I`

- **Browser Extensions for Pentesting**:
  - **FoxyProxy**: Switch proxies easily.
  - **User-Agent Switcher and Manager**: Mimic other OS/browsers.
  - **Wappalyzer**: Identify web technologies.

### 📡 Ping
- **Purpose**: Check if a system is online.
- **Linux/macOS**: `ping -c 10 MACHINE_IP`
- **Windows**: `ping -n 10 MACHINE_IP`
- **Output Insights**: Packet loss, average reply time.

### 🌍 Traceroute
- **Purpose**: Discover network path and hops.
- **Linux/macOS**: `traceroute MACHINE_IP`
- **Windows**: `tracert MACHINE_IP`
- **Mechanism**:
  - TTL field is decreased per hop.
  - ICMP "Time Exceeded" helps map routers.

### 📞 Telnet
- **Default Port**: 23 (insecure - plaintext).
- **Use in Pentesting**:
  - Check banners: `telnet MACHINE_IP 80`
  - Example HTTP request:
    ```
    GET / HTTP/1.1
    host: telnet
    ```

### 🔧 Netcat (nc)
- **Client Usage**: `nc MACHINE_IP PORT`
- **Server Usage**: `nc -lvnp PORT`
  - Options:
    - `-l`: Listen
    - `-v`: Verbose
    - `-n`: Numeric IPs only
    - `-p`: Port
    - `-k`: Keep open after client disconnects

- **HTTP Banner Grab**:
  ```
  nc MACHINE_IP 80
  GET / HTTP/1.1
  host: netcat
  ```

## 🧪 Summary of Common Commands

| Command       | Example                             |
|---------------|-------------------------------------|
| ping          | `ping -c 10 MACHINE_IP` (Linux/macOS) |
| ping          | `ping -n 10 MACHINE_IP` (Windows)   |
| traceroute    | `traceroute MACHINE_IP`             |
| tracert       | `tracert MACHINE_IP` (Windows)      |
| telnet        | `telnet MACHINE_IP PORT`            |
| netcat client | `nc MACHINE_IP PORT`                |
| netcat server | `nc -lvnp PORT`                     |
