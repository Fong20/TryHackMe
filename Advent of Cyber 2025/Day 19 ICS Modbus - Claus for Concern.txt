# ICS Modbus - Claus for Concern

## Scenario Overview
- TBFC drone fleet delivers wrong items (Easter eggs instead of Christmas gifts).
- Root cause: **Industrial Control System (ICS) compromise** via **Modbus TCP (port 502)**.
- Attacker signature: **EGGSPLOIT v6.66 – King Malhare**.
- Attack manipulates PLC registers/coils while falsifying sensor data.

---

## Key Components Explained

### SCADA
- Supervisory system that monitors and controls industrial processes.
- TBFC SCADA manages:
  - Package selection
  - Delivery zones
  - CCTV monitoring
  - Inventory verification
  - Protection & logging mechanisms

### PLC (Programmable Logic Controller)
- Industrial computer running automation logic.
- Reads sensors, controls actuators in real time.
- Communicates using Modbus TCP.

### Modbus Protocol
- Simple request/response protocol.
- **No authentication, encryption, or authorization**.
- Anyone with network access can read/write registers.

---

## Modbus Data Mapping (Critical)

### Holding Registers (Writable)
- **HR0** – Package Type  
  - `0 = Christmas Gifts`  
  - `1 = Chocolate Eggs`  
  - `2 = Easter Baskets`
- **HR1** – Delivery Zone  
  - `1–9 = Normal`  
  - `10 = Ocean Dump`
- **HR4** – System Signature  
  - `666 = Eggsploit`

### Coils (Boolean Flags)
- **C10** – Inventory Verification  
- **C11** – Protection / Override (TRAP)  
- **C12** – Emergency Dump  
- **C13** – Audit Logging  
- **C14** – Christmas Restored (auto)  
- **C15** – Self-Destruct Armed

⚠️ **Never change HR0 while C11 = True** → triggers self-destruct.

---

## Reconnaissance Findings

### Nmap
- `22/tcp` – SSH
- `80/tcp` – HTTP (CCTV feed)
- `502/tcp` – Modbus TCP (PLC)

### CCTV
- Live view confirms Easter eggs on conveyor belts.
- Status shows **Compromised**.

### Live Modbus State
- HR0 = `1` → Eggs
- HR1 = `5` → Normal zone
- HR4 = `666` → Eggsploit detected
- C10 = `False` → Inventory checks disabled
- C11 = `True` → Protection active (trap armed)
- C13 = `False` → Logging disabled
- C15 = `False` → Self-destruct not yet armed

---

## Proof-of-Concept: Modbus Recon (Python)

```python
from pymodbus.client import ModbusTcpClient

client = ModbusTcpClient("10.49.164.143", port=502)
client.connect()

# Read package type
res = client.read_holding_registers(0, 1, slave=1)
print(res.registers[0])  # 1 = Eggs
```

---

## Attack Mechanics
- Attacker directly wrote Modbus values:
  - Forced HR0 to Eggs
  - Disabled verification & logging
  - Enabled protection trap
- Trap logic:
  - Change HR0 while C11=True
  - Arms C15 → countdown → C12 dump to ocean

---

## Safe Remediation Order (CRITICAL)

1. **Disable Protection** – `C11 = False`
2. Set Package Type – `HR0 = 0`
3. Enable Inventory Verification – `C10 = True`
4. Enable Audit Logging – `C13 = True`
5. Verify:
   - C15 = False
   - C12 = False
   - C14 = True

---

## Proof-of-Concept: Safe Restore Script

```python
client.write_coil(11, False, slave=1)   # Disable protection
client.write_register(0, 0, slave=1)   # Christmas gifts
client.write_coil(10, True, slave=1)   # Inventory check
client.write_coil(13, True, slave=1)   # Logging
```

---

## Outcome
- Christmas deliveries restored 🎄
- CCTV updates to normal operations
- Flag retrieved from PLC registers
- Demonstrates real-world ICS risks:
  - Legacy protocols
  - No authentication
  - High physical impact

---

## Key Takeaways
- Always **understand PLC logic before writing values**.
- Modbus TCP is powerful but dangerous if exposed.
- Order of operations in ICS remediation matters.
- Visual monitoring (CCTV) is vital during incident response.
