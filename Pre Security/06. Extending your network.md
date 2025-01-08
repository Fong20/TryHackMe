
# Networking Concepts: Port Forwarding, Firewalls, VPNs, Routers, and Switches

## **Port Forwarding**
- **Definition**: Enables applications/services (e.g., web servers) to be accessible from the Internet by forwarding requests to specific ports on a private network device.
- **Example**: A webserver on `192.168.1.10:80` is accessible publicly via `82.62.51.70` with port forwarding.
- **Key Points**:
  - Configured at the router level.
  - Differs from firewalls, which control whether traffic on specific ports is allowed.

## **Firewalls**
- **Function**: Regulate traffic entering/exiting a network based on rules.
- **Factors for Rule Creation**:
  - Source of traffic.
  - Destination of traffic.
  - Target port.
  - Protocol type (UDP, TCP).
- **Types**:
  1. **Stateful Firewalls**:
     - Evaluate entire connections.
     - Resource-intensive but dynamic.
     - Example: Block all traffic from a misbehaving host.
  2. **Stateless Firewalls**:
     - Inspect individual packets using static rules.
     - Efficient but limited by rule accuracy.
     - Effective against high-traffic attacks like DDoS.

## **Virtual Private Network (VPN)**
- **Purpose**: Secure communication across separate networks using encrypted tunnels.
- **Benefits**:
  - Connects geographically distant networks (e.g., businesses with multiple offices).
  - Enhances privacy by encrypting traffic (useful on public Wi-Fi).
  - Offers anonymity for users like journalists.
- **Examples**:
  - TryHackMe uses VPNs for secure access to vulnerable machines.
- **Technologies**:
  - **PPP**: Handles authentication and encryption.
  - **PPTP**: Extends PPP data across networks; easy to set up but weak encryption.
  - **IPSec**: Strong encryption for data over the Internet but complex to configure.

## **Router**
- **Role**: Connects networks and routes data between them.
- **Operation**:
  - Operates at Layer 3 of the OSI model.
  - Selects paths based on factors like shortest route, reliability, or speed.
- **Configuration**: Features tools for setting rules like port forwarding and firewalling.

## **Switch**
- **Function**: Connects multiple devices within a network.
- **Types**:
  1. **Layer 2 Switch**:
     - Operates at OSI Layer 2.
     - Forwards frames based on MAC addresses.
  2. **Layer 3 Switch**:
     - Combines Layer 2 switching and Layer 3 routing.
     - Routes packets between IP networks.
- **VLAN (Virtual LAN)**:
  - Divides devices into virtual groups for better security.
  - Devices can share resources (e.g., Internet) but may not communicate across VLANs.
