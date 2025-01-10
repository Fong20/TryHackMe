# Active Directory Basics

## Overview
- A **Windows domain** allows centralised management of users, computers, and resources in a network.
- Key component: **Active Directory (AD)** hosted on a **Domain Controller (DC)**.

---

## Key Concepts

### Advantages of Windows Domains:
1. **Centralised Identity Management**:
   - Manage user accounts centrally via AD.
2. **Security Policy Management**:
   - Apply uniform security policies across users and devices.

---

## Active Directory Objects

### Users:
- **Types**:
  - **People**: Represent employees.
  - **Services**: Minimal privilege accounts for running services.
- Security Principals: Authenticated and assigned privileges in the domain.

### Machines:
- Each computer in a domain has a **machine account**.
  - Format: `MachineName$`.
  - Local administrator rights on its own device.
  - Passwords are 120-character random and auto-rotated.

### Security Groups:
- Allow grouped access to resources.
- Users/machines inherit privileges from their group memberships.
- Common default groups:
  - **Domain Admins**: Full domain control.
  - **Backup Operators**: Can bypass file permissions.
  - **Domain Users/Computers**: All users/computers in the domain.

### Organizational Units (OUs):
- Container objects to organise users/machines.
  - Reflect organisational structure for applying policies.
  - Users can belong to only one OU.

---

## Authentication Protocols

### Kerberos:
Default protocol for recent Windows domains.

**Process:**
  1. User requests a **Ticket Granting Ticket (TGT)** from the Key Distribution Center (KDC).

     ![image](https://github.com/user-attachments/assets/3ff9d754-8622-4c14-865d-3d1cffc78f51)

  2. Use TGT to request **Ticket Granting Service (TGS)** for specific resources.

     ![image](https://github.com/user-attachments/assets/d5719b18-0d50-4dd0-ab15-c151c509e6f2)

  3. Present TGS to the target service for access.

     ![image](https://github.com/user-attachments/assets/a9491ba6-b80c-4425-8307-5ce387103bc0)

**Advantages:**
- Avoids transmitting passwords across the network.

### NetNTLM:
- Legacy protocol using challenge-response mechanism.

  **Process:**
  1. Server sends a challenge.
  2. Client responds using NTLM hash and challenge data.
  3. Verification occurs at the DC.

  ![image](https://github.com/user-attachments/assets/f1ed4319-d810-44e6-bed3-e27b9edaf4f6)

---

## Advanced Domain Configurations

### Trees:
- A hierarchy of domains sharing the same namespace.
- Example:
  - Root: `thm.local`.
  - Subdomains: `uk.thm.local`, `us.thm.local`.
- Benefits:
  - Segmentation of resources and policies by regions or branches.
  - Independent administration of subdomains.

![image](https://github.com/user-attachments/assets/cdd4e76a-0971-4e5b-8bf6-d1cdb7dc3e75)

### Forests:
- Combination of domain trees with different namespaces.
- Example:
  - Tree 1: `thm.local`.
  - Tree 2: `mht.local`.
- Joined by **trust relationships**.

![image](https://github.com/user-attachments/assets/6b2bc39c-1887-454f-928e-e4be943d5046)

---

## Trust Relationships
- Enable cross-domain resource access.
- Types:
  1. **One-Way Trust**:
     - Domain A trusts B: Users in B can access resources in A.

       ![image](https://github.com/user-attachments/assets/268d906a-d012-4595-88f5-57e58a4ae582)

  2. **Two-Way Trust**:
     - Mutual access between domains.
- Trust does not grant automatic access; permissions still need to be defined.

---

## Tools

### Active Directory Users and Computers (ADUC):
- Interface for managing:
  - Users.
  - Groups.
  - OUs.
  - Computers.
- Allows creation, modification, and password resets.
