
# AOC Day 20: Network Analysis using Wireshark
---

#### **Introduction**
- **Scenario**: Investigation of a compromised system using a PCAP file from a victim's machine.
- **Tools Used**: Wireshark and CyberChef.

---

#### **Key Concepts**
1. **C2 Communication**:
   - A compromised machine interacts with a Command and Control (C2) server.
   - Payload: A malicious program installed on the victim's machine to:
     - Execute commands.
     - Exfiltrate data.
     - Send status updates (beacons).

2. **Wireshark**:
   - Open-source tool for analyzing network traffic.
   - **Capabilities**:
     - Analyzes and organizes traffic regardless of protocol.
     - Reconstructs network conversations.
     - Filters traffic for targeted analysis.
     - Exports and examines transferred objects.
   - **Basic Filters**:
     - `ip.src == <IP>` to narrow results to traffic from a specific IP.
   - **Packet Inspection**:
     - Focus on specific frames to see details in hexadecimal and ASCII formats.
     - Follow HTTP streams to reconstruct client-server communication.

3. **CyberChef**:
   - A "Swiss Army Knife" for encoding, decoding, encrypting, and decrypting data.
   - Decrypting Beacons:
     - **Steps**:
       1. Select **AES Decrypt** operation.
       2. Configure encryption mode and key.
       3. Input the encrypted data.
       4. Click "Bake" to decrypt.

---

#### **Procedure**
1. **Analyze PCAP File**:
   - Open the file in Wireshark.
   - Filter outbound traffic from the victim's machine: `ip.src == 10.10.229.217`.
   - Identify suspicious packets:
     - Example: POST `/initial` and `/exfiltrate`.

2. **Follow HTTP Stream**:
   - Examine back-and-forth client-server communication.
   - Extract key data:
     - Frame 440: "I am in Mayor!" sent to destination IP.
     - Frame 457: Command for gathering user information.
     - Frame 476: Exfiltration of data.

3. **Decrypt Beacons**:
   - Locate beacon packets (regular intervals of communication to C2 server).
   - Use CyberChef:
     - Select `AES Decrypt` in ECB mode.
     - Use provided decryption key.
     - Input encrypted string and process to reveal message.

---

#### **Takeaways**
- **C2 Behavior**:
  - Regular beaconing indicates active communication.
  - Commands provide insights into attacker goals (reconnaissance, execution, data theft).
- **Wireshark Insights**:
  - Effective in dissecting malicious traffic.
  - Highlighted the progression of the attack lifecycle.
- **CyberChef Role**:
  - Essential for decrypting sensitive data to understand attacker intentions.

---

#### **Conclusion**
The investigation highlights the need for robust traffic analysis skills and tools like Wireshark and CyberChef to identify and counter advanced cyber threats like Mayor Malware's schemes. Further steps include fortifying defenses and analyzing patterns for broader implications. 

---
