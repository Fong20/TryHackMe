# AOC Day 17: Log Analysis using Splunk

## Scenario Summary
- Marta May Ware reports the main server disconnected from the Wareville network. CCTV logs suggest no entries into the data centre, despite the apparent sabotage.
- CCTV cameras are owned by Byte, a loyal dog, ensuring data integrity.
- Investigation involves Splunk to identify the culprit via analysis of custom log files.

---

## Learning Objectives
1. **Extract custom fields in Splunk**:
   - Parse CCTV logs and web logs for actionable data.
2. **Search Processing Language (SPL)**:
   - Use SPL queries to filter and visualize data.
3. **Timeline and field adjustments**:
   - Overcome issues in log parsing and improper event timelines.

---

## Splunk Investigation Steps
### 1. Initial Log Analysis
- **Data sources**:
  - `web_logs`: Logs of web interactions with the CCTV server.
  - `cctv_logs`: Logs of application-level CCTV activity.
- SPL query to fetch CCTV logs:  
  ```
  index=* sourcetype=cctv_logs
  ```
- Issues: Unparsed logs and inaccurate timestamps.

---

### 2. Field Extraction
- **Extract custom fields**:
  - Timestamp, Event, User_id, UserName, Session_id.
- SPL-generated regex for field extraction:  
  ```
  ^(?P<timestamp>\d+\-\d+\-\d+\s+\d+:\d+:\d+)\s+(?P<Event>(Login\s\w+|\w+))\s+(?P<user_id>\d+)?\s?(?P<UserName>\w+)\s+.*?(?P<Session_id>\w+)$
  ```
- Save and validate patterns for accurate parsing.

---

### 3. Event Exploration
- **Visualize event counts by user**:  
  ```
  index=cctv_feed | stats count(Event) by UserName
  ```
  Use pie charts for visualization.
- **Identify rare events**:
  ```
  index=cctv_feed | rare Event
  ```
  - Notable findings: Failed login attempts and footage deletion.

---

### 4. Session ID Correlation
- Investigate failed logins:
  ```
  index=cctv_feed *failed* | table _time UserName Event Session_id
  ```
- Cross-reference session IDs with deletion events:
  ```
  index=cctv_feed *Delete*
  ```

---

### 5. Web Logs Correlation
- Identify suspicious IP:  
  ```
  index=web_logs *rij5uu4gt204q0d3eb7jj86okt*
  ```
  - Found IP: `10.11.105.33`.
- Further session ID correlation:  
  ```
  index=web_logs clientip="10.11.105.33" | table _time clientip status uri ur_path file
  ```
  - Session IDs linked to IP reveal suspicious logouts and activity.

---

## Findings
1. **Attack Summary**:
   - Multiple brute-force attempts on user accounts.
   - Successful login achieved, leading to:
     - Watching and downloading of CCTV streams.
     - Deletion of camera recordings.
2. **Attacker Identification**:
   - Correlated session IDs across CCTV and web logs revealed the attacker’s user name and activities.
   - Attack timeline reconstructed.

---

## Conclusion
The attack involved brute-force logins, unauthorized access, and deliberate deletion of CCTV footage. The correlation of session IDs and suspicious IP addresses through Splunk logs identified the attacker.
