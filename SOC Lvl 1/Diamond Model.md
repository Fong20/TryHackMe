
# Diamond Model

## Overview
- Developed by Sergio Caltagirone, Andrew Pendergast, and Christopher Betz in 2013.
- Represents cyber intrusion activity using four core features: **Adversary**, **Infrastructure**, **Capability**, and **Victim**.
- Structured as a diamond to illustrate the relationships between core elements.
- Includes optional meta-features: **Timestamp**, **Phase**, **Result**, **Direction**, **Methodology**, **Resources**, **Social-Political**, and **Technology**.

## Core Features

### 1. Adversary
- Also known as attacker, hacker, or threat actor.
- Responsible for utilizing a capability against a victim.
- **Adversary Operator**: Executes the intrusion.
- **Adversary Customer**: Entity that benefits from the intrusion.
- May control multiple operators with varied capabilities and infrastructure.

### 2. Victim
- The target of the adversary; can be a person, organization, or asset.
- **Victim Personae**: Individuals or entities being targeted.
- **Victim Assets**: Attack surfaces such as systems, IPs, emails, etc.

### 3. Capability
- Tools, skills, or techniques used by adversary (e.g., malware, phishing).
- **Capability Capacity**: Vulnerabilities that can be exploited.
- **Adversary Arsenal**: Combined capabilities of an adversary.

### 4. Infrastructure
- Physical or logical systems used to deliver/maintain capabilities.
- Examples: C2 servers, domains, malicious USBs.
- **Type 1 Infrastructure**: Controlled by adversary.
- **Type 2 Infrastructure**: Controlled by intermediary (possibly unaware).
- **Service Providers**: Enable adversary infrastructure (e.g., ISPs, registrars).

## Meta-Features

### Timestamp
- Records the date/time of events.
- Helps identify patterns and link events.

### Phase (Cyber Kill Chain)
1. Reconnaissance  
2. Weaponization  
3. Delivery  
4. Exploitation  
5. Installation  
6. Command & Control  
7. Actions on Objective  

### Result
- Outcome of adversary action: `success`, `failure`, or `unknown`.
- Related to CIA Triad: Confidentiality, Integrity, Availability.

### Direction
- Describes the path of the intrusion (e.g., Victim-to-Infrastructure).

### Methodology
- General type of attack: phishing, DDoS, breach, etc.

### Resources
- Needed to perform intrusion: software, knowledge, info, hardware, funds, facilities, access.

### Social-Political Component
- Describes intent (e.g., financial gain, hacktivism, espionage).
- Victim may offer "products" (e.g., computing power for crypto-mining).

### Technology
- Links **Capability** and **Infrastructure**.
- Example: Watering-hole attacks (compromise websites likely visited by victims).

## Benefits
- Provides real-time intelligence for network defense.
- Facilitates correlation, classification, and forecasting of adversary operations.
- Helps communicate complex intrusion scenarios to non-technical audiences.
