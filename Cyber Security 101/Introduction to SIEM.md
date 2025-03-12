# Introduction to Security Information and Event Management (SIEM)

## 1. What is SIEM?
SIEM (Security Information and Event Management) is a tool that:
- Collects data from various network devices and endpoints.
- Stores logs centrally for analysis.
- Correlates events for security monitoring and incident response.

---

## 2. Why is SIEM Needed?
SIEM provides:
- **Network visibility**: Better insight into network activities.
- **Real-time threat detection**: Alerts on suspicious activity.
- **Incident investigation**: Allows security teams to analyze past events.

---

## 3. Types of Log Sources

### Host-Centric Log Sources
Logs that capture events related to individual hosts, e.g.:
- **Windows Event Logs**
- **Sysmon Logs**
- **Osquery Logs**
- **Example Activities**:
  - User accessing a file.
  - Process execution.
  - PowerShell execution.

### Network-Centric Log Sources
Logs generated when network communication occurs, e.g.:
- **SSH, VPN, HTTP/s, FTP Logs**
- **Example Activities**:
  - SSH connection attempts.
  - File accessed via FTP.
  - Web traffic analysis.

### Windows Machine Logs

Windows records every event that can be viewed through the Event Viewer utility. It assigns a unique ID to each type of log activity, making it easy for the analyst to examine and keep track of. To view events in a Windows environment, type Event Viewer in the search bar, and it takes you to the tool where different logs are stored and can be viewed, as shown below. These logs from all windows endpoints are forwarded to the SIEM solution for monitoring and better visibility.

### Linux Workstation

Linux OS stores all the related logs, such as events, errors, warnings, etc. Which are then ingested into SIEM for continuous monitoring. Some of the common locations where Linux store logs are:

- /var/log/httpd : Contains HTTP Request  / Response and error logs.
- /var/log/cron   : Events related to cron jobs are stored in this location.
- /var/log/auth.log and /var/log/secure : Stores authentication related logs.
- /var/log/kern : This file stores kernel related events.

### Web Server Logs

It is important to keep an eye on all the requests/responses coming in and out of the webserver for any potential web attack attempt. In Linux, common locations to write all apache related logs are /var/log/apache or /var/log/httpd.

---

## 4. Importance of SIEM
SIEM helps by:
- **Centralizing log collection & analysis**
- **Correlating logs for threat detection**
- **Providing real-time alerts & monitoring**
- **Generating data insights & visualizations**
- **Investigating past incidents efficiently**

---

## 5. Log Ingestion Methods in SIEM
Different ways logs are ingested into SIEM:
1. **Agent / Forwarder**: Installed on endpoints to collect logs (e.g., Splunk Forwarder).
2. **Syslog**: Standardized protocol for log collection.
3. **Manual Upload**: Offline data ingestion for analysis.
4. **Port-Forwarding**: Endpoints send logs to SIEM via designated ports.

---

## 6. SIEM Capabilities
SIEM provides:
- **Event correlation across log sources.**
- **Host and network activity visibility.**
- **Threat hunting & investigation tools.**
- **Alerting and security incident response.**

---

## 7. SOC Analyst Responsibilities
SOC Analysts use SIEM to:
- Monitor and investigate security alerts.
- Identify and reduce false positives.
- Tune SIEM rules for better accuracy.
- Ensure compliance and reporting.

---

## 8. SIEM Dashboards
Dashboards present log data in visual formats with key insights such as:
- **Alert highlights**
- **System notifications**
- **Failed login attempts**
- **Rules triggered**
- **Top domains visited**

---

## 9. Correlation Rules in SIEM
SIEM uses logical expressions to detect threats, e.g.:
- **Multiple failed login attempts → Alert for brute force attack.**
- **USB plugged in → Alert if USB is restricted.**
- **Large outbound traffic → Alert for potential data exfiltration.**

### Example Correlation Rules
#### Rule 1: Event Log Cleared Detection
**Condition:**  
If **Log Source = WinEventLog** AND **EventID = 104** → Trigger alert for **Event Log Cleared**.

#### Rule 2: Suspicious Command Execution Detection
**Condition:**  
If **Log Source = WinEventLog** AND **EventID = 4688** AND **NewProcessName = "whoami"** → Trigger alert for **WHOAMI Execution Detected**.

---

## 10. Alert Investigation Process
Once an alert is triggered:
1. **Analyst reviews the alert on the dashboard.**
2. **Events and logs are examined to check for false positives.**
3. **Response actions are taken based on findings:**
   - False alarm → Rule tuning needed.
   - True positive → Further investigation required.
   - If confirmed malicious:
     - **Isolate affected system**
     - **Block suspicious IP addresses**
