# Firewall Fundamentals

## What is a Firewall?
- A firewall acts as a security guard for digital devices, inspecting incoming and outgoing network traffic.
- It allows or denies traffic based on predefined rules to prevent unauthorized access.
- Modern firewalls offer advanced functionalities beyond simple rule-based filtering.

## Types of Firewalls
| Firewall Type  | Characteristics |
|---------------|----------------|
| Stateless Firewall | - Operates on OSI Layer 3 & 4. \n - Does not track previous connections. \n - Matches packets solely based on predefined rules. \n - Efficient for high-speed networks but lacks context awareness. |
| Stateful Firewall | - Operates on OSI Layer 3 & 4. \n - Keeps track of previous connections in a state table. \n - Can apply complex rules based on connection history. |
| Proxy Firewall | - Operates on OSI Layer 7. \n - Inspects packet contents. \n - Acts as an intermediary between users and the Internet. \n - Provides content filtering and application control. |
| Next-Generation Firewall (NGFW) | - Operates on OSI Layers 3 to 7. \n - Provides deep packet inspection. \n - Includes an intrusion prevention system. \n - Uses heuristic analysis for anomaly detection. \n - Decrypts SSL/TLS traffic for inspection. |

## Firewall Rules and Components
- **Source Address**: The IP address sending traffic.
- **Destination Address**: The IP address receiving traffic.
- **Port**: The communication port number.
- **Protocol**: The communication protocol (TCP, UDP, etc.).
- **Action**: Defines whether traffic is **Allowed**, **Denied**, or **Forwarded**.
- **Direction**: Specifies if the rule applies to **Inbound**, **Outbound**, or **Forwarded** traffic.

### Types of Actions
| Action | Description |
|--------|------------|
| Allow | Permits traffic matching the rule. |
| Deny | Blocks traffic matching the rule. |
| Forward | Redirects traffic to another destination. |

### Directionality of Rules
| Rule Type  | Purpose |
|------------|---------|
| Inbound Rules | Control traffic entering the network. |
| Outbound Rules | Control traffic leaving the network. |
| Forward Rules | Redirect traffic to a specific internal address. |

---

## Hands-On: Windows Defender Firewall
### Key Features
- **Network Profiles**
  - **Private Network**: Used for home/trusted networks.
  - **Public Network**: Used for untrusted locations like cafés or airports.

### Creating a Custom Firewall Rule in Windows Defender
1. Open **Windows Defender Firewall**.
2. Go to **Advanced Settings**.
3. Select **Outbound Rules** → Click **New Rule**.
4. Choose **Custom** → Click **Next**.
5. Select **All Programs** → Click **Next**.
6. Choose **TCP** and enter ports **80,443** → Click **Next**.
7. Select **Block the connection** → Click **Next**.
8. Apply to all network profiles → Click **Next**.
9. Name the rule and finish.
10. Verify the rule in the **Outbound Rules** list.

---

## Hands-On: Linux Firewalls
### Netfilter-Based Firewall Utilities
| Utility  | Description |
|---------|------------|
| iptables | Widely used command-line utility for configuring rules. |
| nftables | Successor to iptables with enhanced features. |
| firewalld | Provides pre-built network zones for easier management. |
| ufw (Uncomplicated Firewall) | Simplifies firewall rule creation for beginners. |

### Basic ufw Commands
- **Check Firewall Status**  
  ```bash
  sudo ufw status
  ```
- **Enable Firewall**  
  ```bash
  sudo ufw enable
  ```
- **Allow All Outgoing Traffic**  
  ```bash
  sudo ufw default allow outgoing
  ```
- **Deny Incoming SSH Traffic**  
  ```bash
  sudo ufw deny 22/tcp
  ```
- **List All Rules**  
  ```bash
  sudo ufw status numbered
  ```
- **Delete a Rule (e.g., Rule #2)**  
  ```bash
  sudo ufw delete 2
  ```

---

