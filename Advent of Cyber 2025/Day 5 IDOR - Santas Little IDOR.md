# IDOR - Santas Little IDOR

## Key Concepts

- **IDOR (Insecure Direct Object Reference)**: Authorization bypass caused by direct references (IDs, numbers, hashes). Allows attackers to access objects they shouldn't.
- **Authentication vs Authorization**
  - Authentication = verify identity (username/password → session).
  - Authorization = verify permissions.
  - Authorization cannot occur before authentication.
- **Privilege Escalation**
  - Vertical: Gain higher privileges (e.g., user → admin).
  - Horizontal: Access peer user data (common in IDOR).

## Example Scenario

- Web app uses request parameter: `packageID=1001`.
- Backend SQL query:
  ```
  SELECT person, address, status
  FROM Packages
  WHERE packageID = value;
  ```
- Sequential IDs → attacker changes to 1002, 1003, etc → horizontal privilege escalation.

## IDOR Patterns Observed

### 1. Direct Numeric IDOR
- Local storage contains:
  ```
  auth_user: {"user_id": 10}
  ```
- Changing `user_id` to 11 reveals another user's dashboard.

### 2. Encoded IDs
- Endpoint uses Base64:
  ```
  /get_child?child_id=Mg==
  ```
- `Mg==` = Base64 for `2`. IDOR still possible by encoding values.

### 3. Hashed IDs
- Edit child endpoint uses MD5/SHA-like hash for reference.
- Hash can be replicated if input is known → still IDOR.

### 4. UUIDv1 Predictable IDs
- Vouchers appear random but decoded as UUIDv1.
- UUIDv1 includes timestamp → attacker can regenerate all UUIDs in a known timeframe → brute force valid vouchers.

## Fixing IDOR

- Always enforce server-side authorization checks:
  - Verify: *Does this user own this object?*
- Avoid depending on obfuscation (Base64, hashes).
- Use non-sequential, random identifiers **with** permission checks.
- Add logging & alerting for unauthorized access attempts.
- Test by trying to access another user's data → ensure denied.

