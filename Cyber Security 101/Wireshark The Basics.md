
# Wireshark The Basics

### Overview
- **Wireshark**: Open-source, cross-platform network packet analyzer.
- **Purpose**: Analyze live traffic and packet captures (PCAP).
- **Use Cases**:
  - Detect and troubleshoot network problems.
  - Identify security anomalies (e.g., rogue hosts, suspicious traffic).
  - Learn protocol details like response codes and payloads.
- **Important**: Wireshark is not an IDS. It does not modify packets but relies on analysts’ knowledge to interpret data.

---

### Graphical User Interface (GUI) Sections
1. **Toolbar**: Menu for filtering, sorting, exporting, and merging.
2. **Display Filter Bar**: Main query and filtering section.
3. **Recent Files**: Quick access to recently used PCAP files.
4. **Capture Filter and Interfaces**: Sniffing points (e.g., lo, eth0).
5. **Status Bar**: Shows processed files, packet counts, and detailed statuses.

---

### Packet Views
- **Packet List Pane**: Summary (source/destination, protocol, packet info).
- **Packet Details Pane**: Protocol breakdown for a selected packet.
- **Packet Bytes Pane**: Hex/ASCII representation of a packet.

---

### Features and Functionalities

#### **Traffic Sniffing**
- Use the blue button to start, red to stop, and green to restart sniffing.

#### **File Operations**
- **Merge PCAP Files**: Combine two PCAPs via *File > Merge*.
- **View File Details**: Access metadata like file hash, capture time, and interface stats via *Statistics > Capture File Properties*.

#### **Packet Numbers**
- Unique numbers help locate and track specific packets.

#### **Find Packets**
- **Search Inputs**: Display filter, Hex, String, Regex.
- **Search Fields**: Packet List, Details, or Bytes panes.

#### **Mark and Comment Packets**
- **Marking**: Temporary; highlights packets in black.
- **Comments**: Persistent across sessions; useful for collaboration.

#### **Exporting Data**
- Export specific packets or objects (e.g., HTTP, SMB files).

#### **Time Display Format**
- Default: Seconds since the start of capture.
- Common preference: UTC time for clarity (*View > Time Display Format*).

#### **Expert Info**
- Severity-based categorization:
  - **Chat (Blue)**: Informational.
  - **Note (Cyan)**: Notable events (e.g., application errors).
  - **Warn (Yellow)**: Warnings (e.g., unusual error codes).
  - **Error (Red)**: Serious issues like malformed packets.

#### **Packet Filtering**
- Two filter types:
  1. **Capture Filters**: Apply during live packet capture.
  2. **Display Filters**: Apply during packet viewing.

---

### Advanced Features

#### **Filtering and Colorization**
- **Apply as Filter**: Right-click a value to filter traffic based on it.
- **Conversation Filter**: Filter related packets (e.g., IP, ports).
- **Colorize Packets**: Use coloring rules for quick anomaly detection.

#### **Customize Columns**
- Add specific fields to the packet list pane via *Right-Click > Apply as Column*.

#### **Follow Stream**
- Reconstruct application-level traffic (e.g., TCP/UDP/HTTP streams).
- Server-originated packets: Blue; client-originated: Red.

---

### Key Functionalities Overview
| Feature                 | Shortcut/Menu Path                      | Notes                                      |
|-------------------------|-----------------------------------------|-------------------------------------------|
| **Start Sniffing**      | Blue shark button                      | Captures live network traffic.            |
| **Merge Files**         | *File > Merge*                         | Combines multiple PCAPs.                  |
| **Find Packets**        | *Edit > Find Packet*                   | Search with display filters, regex, etc.  |
| **Add Comments**        | *Right-Click > Packet Comment*         | Persistent across sessions.               |
| **Follow Stream**       | *Analyze > Follow Stream*              | View raw traffic, e.g., HTTP or TCP data. |
| **Export Objects**      | *File > Export Objects*                | For supported protocols (HTTP, SMB, etc.).|

---
