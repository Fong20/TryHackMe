# Race Conditions - Toy to The World

## Scenario Overview
- TBFC released a limited-edition SleighToy (10 units).
- Due to a timing flaw, multiple customers successfully purchased the 'last' item.
- Root cause: a **race condition** during checkout.
- Attackers (Bandit Bunnies) exploited simultaneous requests to oversell stock.

---

## Learning Objectives
- Understand race conditions in web applications.
- Identify and exploit race conditions via concurrent requests.
- See how shared resources (inventory) can be manipulated.
- Learn mitigation techniques.

---

## What is a Race Condition?
A race condition occurs when:
- Two or more actions run concurrently.
- The final outcome depends on execution order.
- Lack of proper synchronization causes inconsistent or insecure results.

**Common Impacts:**
- Oversold inventory
- Duplicate transactions
- Incorrect balances
- Unauthorized changes

---

## Types of Race Conditions

### 1. Time-of-Check to Time-of-Use (TOCTOU)
- System checks a condition (e.g., stock available).
- Data changes before it is used.
- Example: two users buy the “last” item simultaneously.

### 2. Shared Resource Race
- Multiple processes modify the same data at once.
- Final value depends on which write happens last.
- Example: two updates to inventory overwrite each other.

### 3. Atomicity Violation
- Operations that should be indivisible are split.
- Another request executes mid-process.
- Example: payment recorded but order confirmation fails.

---

## Exploitation Walkthrough (PoC)

### Environment Setup
1. Open Firefox on AttackBox.
2. Enable **FoxyProxy → Burp profile**.
3. Launch **Burp Suite**:
   - Temporary project
   - Start Burp
4. Turn **Intercept OFF** in Proxy tab.

---

### Legitimate Request
1. Visit: http://10.49.179.229
2. Login:
   - Username: attacker
   - Password: attacker@123
3. Add SleighToy to cart.
4. Checkout → Confirm & Pay.
5. Observe successful purchase.

---

### Capturing the Request
1. In Burp:
   - Proxy → HTTP history
2. Find POST request to:
   - `/process_checkout`
3. Right-click → **Send to Repeater**

---

### Race Condition Exploit
1. In Repeater:
   - Create a **tab group** (e.g., `cart`)
2. Duplicate the checkout request (e.g., 15 copies).
3. Use:
   - **Send group in parallel (last-byte sync)**
4. Send all requests simultaneously.

**Result:**
- Multiple orders confirmed.
- Inventory reduced incorrectly (may go negative).

---

## Why It Works
- Stock validation happens before update.
- Requests are processed concurrently.
- No locking or atomic transaction protection.

---

## Mitigation Techniques
- Use **atomic database transactions**.
- Revalidate stock immediately before commit.
- Implement **idempotency keys** for checkout.
- Apply **rate limiting** and concurrency controls.
- Use database-level locking where appropriate.

---

## Key Takeaway
Even milliseconds matter. Without proper synchronization, concurrent requests can break business logic and lead to serious security and financial issues.
