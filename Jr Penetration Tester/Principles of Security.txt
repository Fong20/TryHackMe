
# Principles of Security

## Defence in Depth
- Security strategy using multiple, varied layers to protect systems and data.
- Provides redundancy in security to prevent single points of failure.

## CIA Triad
- **Confidentiality:** Protects data from unauthorized access.
  - Example: HR having exclusive access to employee records.
- **Integrity:** Ensures data is accurate and unchanged unless authorized.
  - Techniques: Access control, hash verifications, digital signatures.
- **Availability:** Ensures data is accessible to authorized users when needed.
  - Techniques: Redundant systems, SLAs for uptime, access management.

## Access Control Concepts
- **Privileged Identity Management (PIM):** Assigns roles based on user's function.
- **Privileged Access Management (PAM):** Manages system role privileges and security policies.
- **Principle of Least Privilege:** Users get only necessary access.

## Security Models

### Bell-La Padula Model (Confidentiality)
- Rule: **No write down, no read up**
- Suited for environments with hierarchical roles (e.g., military, government).
- Pros: Real-world mapping, simplicity.
- Cons: Users know of data they can’t access, relies heavily on trust.

### Biba Model (Integrity)
- Rule: **No write up, no read down**
- Suitable for integrity-critical environments (e.g., software development).
- Pros: Simplicity, addresses integrity.
- Cons: Complex access levels, operational delays.

## Threat Modelling
- **Purpose:** Identify, improve and test security protocols.
- **Phases:** Preparation, Identification, Mitigations, Review.
- **Frameworks:** STRIDE, PASTA

### STRIDE Model
| Principle              | Description |
|------------------------|-------------|
| Spoofing               | Authenticate users/requests to avoid impersonation. |
| Tampering              | Protect integrity of accessed data (e.g., tamper-evident seals). |
| Repudiation            | Use logging to track activity. |
| Information Disclosure | Restrict data visibility to authorized users. |
| Denial of Service      | Prevent abuse that could crash systems. |
| Elevation of Privilege | Prevent unauthorized access level escalation. |

## Incident Response (IR)
- **Incident:** A breach or violation of information security.
- **Team:** CSIRT (Computer Security Incident Response Team)

### Six Phases of IR
| Phase         | Description |
|---------------|-------------|
| Preparation   | Ensure resources/plans are ready. |
| Identification| Confirm the nature of the threat. |
| Containment   | Isolate the threat. |
| Eradication   | Remove the threat. |
| Recovery      | Restore operations. |
| Lessons Learned | Analyze incident and improve response. |
