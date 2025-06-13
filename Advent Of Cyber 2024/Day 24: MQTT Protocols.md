
# AOC Day 24: MQTT Protocols

## **Learning Objectives**
1. Understand the MQTT protocol basics.
2. Analyze MQTT traffic using Wireshark.
3. Reverse engineer a simple network protocol.

---

## **Key Topics**

### **Smart Devices and IoT**
- **Benefits**: Simplifies daily tasks with remote control (e.g., HVAC systems, smart vacuums).
- **Risks**: Network-dependent devices are vulnerable to unauthorized access without proper security measures.
- **Mitigation**: Employ network isolation, authentication mechanisms, and monitor IoT communication.

### **IoT Communication**
- IoT devices use various programming languages but communicate using protocols like **HTTP** or **MQTT**.

---

### **MQTT Protocol**
- **Definition**: Message Queuing Telemetry Transport, widely used in IoT for publish/subscribe messaging.
- **Components**:
  - **MQTT Clients**: Publish or subscribe to messages (e.g., temperature sensors, HVAC controllers).
  - **MQTT Broker**: Receives and distributes messages between clients.
  - **MQTT Topics**: Organize messages by subject (e.g., `home/temperature`, `home/heater`).

---

## **Practical Setup**

### **Environment Setup**
1. Start the provided VM and ensure Wireshark is installed.
2. Locate MQTT scripts in the directory: `~/Desktop/MQTTSIM/`.

#### **Files in MQTTSIM**
- **Walkthrough**: `hvac.py`, `walkthrough.sh`.
- **Challenge**: `challenge.pcapng`, `challenge.sh`, `lights.py`.

---

### **Analyzing MQTT with Wireshark**
1. Start Wireshark.
2. Select the `any` network interface.
3. Filter by `mqtt` to view only MQTT traffic.
4. Run `walkthrough.sh` to initiate MQTT broker and client scripts.

#### **Observed Communication**
- **Connect Command**: Initial handshake between broker and clients.
- **Subscribe Command**: Clients subscribe to topics (e.g., `home/temperature`).
- **Published Messages**:
  - `home/temperature`: Contains temperature readings.
  - `home/heater`: Indicates heater state (e.g., "on" or "off").

---

## **Challenge: Turn On the Lights**

1. **Setup**:
   - Run `challenge.sh` from the `~/Desktop/MQTTSIM/challenge/` directory.
   - Analyze `challenge.pcapng` in Wireshark to find the topic and message for turning on lights.
   
2. **Use `mosquitto_pub` Command**:
   - Publish a message to the broker to activate lights:
     ```
     mosquitto_pub -h localhost -t "<topic>" -m "<message>"
     ```
   - Replace `<topic>` and `<message>` based on findings from packet capture.

3. **Steps**:
   - Identify the correct topic and message in Wireshark.
   - Test the command with the discovered parameters while `challenge.sh` is running.
   - Verify success with the lights controller interface (a flag will appear).

---

### **Command Reference**
- **Example**:
  ```
  mosquitto_pub -h localhost -t "home/lights" -m "on"
  ```
- **Flags**:
  - `-h`: Hostname of MQTT broker (e.g., `localhost`).
  - `-t`: Topic to publish to (e.g., `home/lights`).
  - `-m`: Message content (e.g., `on` or `off`).

---

**End of Notes**
