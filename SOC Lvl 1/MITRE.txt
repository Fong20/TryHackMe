
# MITRE 

## Introduction to MITRE
- MITRE is a US-based non-profit organization contributing to multiple fields, including cybersecurity, AI, health informatics, and space security.
- Known for managing the CVE (Common Vulnerabilities and Exposures) list.
- Mission: Solve problems for national safety, stability, and well-being.

## Core Cybersecurity Projects

### 1. MITRE ATT&CK® Framework
- **Definition**: Knowledge base of adversary tactics and techniques based on real-world observations.
- **Origin**: Started in 2013 as Fort Meade Experiment (FMX).
- **Coverage**: Initially for Windows, now includes macOS and Linux.
- **Use Cases**: Blue teams (defensive) and red teams (offensive).
- **Components**:
  - Tactics: Adversary's goals.
  - Techniques: Methods to achieve goals.
  - Procedures: Specific execution of techniques.
- **Navigator Tool**: Allows visualization of matrices for different threat groups or tools.

### 2. CAR (Cyber Analytics Repository)
- **Definition**: Knowledge base of analytics based on ATT&CK®, including pseudocode and tool-specific queries (e.g., Splunk, EQL).
- **Purpose**: Deeper analytic insight beyond ATT&CK’s mitigation/detection summaries.
- **Examples**:
  - `CAR-2020-09-001`: Scheduled Task - File Access.
  - `CAR-2014-11-004`: Remote PowerShell Sessions.

### 3. MITRE ENGAGE
- **Focus**: Adversary Engagement through Cyber Denial and Cyber Deception.
- **Matrix Categories**:
  - Prepare
  - Expose
  - Affect
  - Elicit
  - Understand
- **Resources**: Starter Kit, Engage Matrix Explorer.

### 4. MITRE D3FEND
- **Definition**: Knowledge graph of cybersecurity countermeasures (still in beta).
- **Stands for**: Detection, Denial, and Disruption Framework Empowering Network Defense.
- **Example Artifact**: Decoy File with details on definition, operation, considerations, and examples.

### 5. AEP (ATT&CK® Emulation Plans)
- **Provided by**: MITRE ENGENUITY via CTID.
- **Function**: Publicly available emulation plans for threat groups (e.g., APT3, APT29, FIN6).
- **Purpose**: Evaluate defensive effectiveness through controlled adversary emulation.

## CTID (Center for Threat-Informed Defense)
- **Members**: Includes companies like Microsoft, Verizon, AttackIQ, Red Canary, Splunk.
- **Goal**: Collaborate on research to improve global cyber defense using ATT&CK-based resources.

## Summary
- These MITRE tools/resources provide a robust foundation for defenders and attackers (red teamers).
- Encourages a common language and framework for threat emulation, detection, and analysis.
- Essential for roles like SOC Analyst, Detection Engineer, Cyber Threat Analyst, etc.
- Supports the concept of purple teaming: collaborative red and blue team efforts.

