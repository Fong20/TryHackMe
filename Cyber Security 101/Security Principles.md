# Security Principles

## 1. Security Triad: CIA
- **Confidentiality**: Ensures only authorized parties access data.  
  *Example*: Protecting credit card details in online shopping.
- **Integrity**: Ensures data is unaltered; detects changes if they occur.  
  *Example*: Preventing tampering with medical records.
- **Availability**: Ensures systems/services are accessible when needed.  
  *Example*: Online store uptime for order placement.

## 2. Beyond CIA: Additional Principles
- **Authenticity**: Verifies the source of data (e.g., genuine shopping orders).
- **Nonrepudiation**: Prevents denial of actions (e.g., order confirmation).
- **Parkerian Hexad (6 elements)**:
  - *Utility*: Data must be usable (e.g., losing decryption keys renders data useless).
  - *Possession*: Protects against unauthorized control (e.g., ransomware encrypting data).

## 3. Attacks (DAD Triad)
- **Disclosure**: Unauthorized data exposure (opposite of confidentiality).
- **Alteration**: Unauthorized data modification (opposite of integrity).
- **Destruction/Denial**: Service/data unavailability (opposite of availability).

## 4. Security Models
### Bell-LaPadula (Confidentiality)
- *No read up*: Lower clearance can’t read higher-level data.
- *No write down*: Higher clearance can’t write to lower levels.

### Biba (Integrity)
- *No read down*: Higher integrity subjects can’t read lower integrity data.
- *No write up*: Lower integrity subjects can’t modify higher integrity data.

### Clark-Wilson (Integrity)
- Uses *Constrained Data Items (CDIs)* and *Transformation Procedures (TPs)* to enforce rules.

## 5. Security Principles
### Defence-in-Depth
- Multi-layered security (e.g., locks, cameras, gates).

### ISO/IEC 19249 Principles
- **Domain Separation**: Group components by security attributes (e.g., OS privilege levels).
- **Layering**: Abstract levels with security policies (e.g., OSI model).
- **Encapsulation**: Hide implementations (e.g., OOP methods).
- **Redundancy**: Ensure availability (e.g., RAID 5, dual power supplies).
- **Virtualization**: Sandboxing for security boundaries.

### Design Principles
- **Least Privilege**: Minimal permissions for tasks.
- **Attack Surface Minimization**: Disable unused services.
- **Centralized Validation/Services**: Unified security checks (e.g., authentication servers).
- **Error Handling**: Fail-safe designs; avoid info leaks in errors.

## 6. Trust Models
- **Trust but Verify**: Audit logs/automated checks (e.g., IDS/IPS).
- **Zero Trust**: "Never trust, always verify." Microsegmentation, no implicit trust (e.g., internal networks).

## 7. Key Terms
- **Vulnerability**: Weakness (e.g., unpatched software).
- **Threat**: Potential danger (e.g., exploit code for the vulnerability).
- **Risk**: Likelihood × impact of threat exploitation.

## 8. Shared Responsibility Model (Cloud)
- **IaaS**: User manages OS/apps; provider handles hardware/network.
- **SaaS**: Provider manages everything; user only uses the app.

---

### Summary
- **CIA** (Confidentiality, Integrity, Availability) and **DAD** (Disclosure, Alteration, Destruction) are foundational.
- Security models (**Bell-LaPadula**, **Biba**, **Clark-Wilson**) enforce CIA.
- Principles like **Defence-in-Depth** and **Zero Trust** mitigate risks.
- **ISO/IEC 19249** standardizes architectural/design best practices.
- **Risk = Vulnerability + Threat + Impact**.
