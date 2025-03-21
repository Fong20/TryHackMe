# Logs Fundamentals

## Introduction
- Attackers leave minimal traces to avoid detection.
- Investigators analyze digital traces (logs) to determine attack execution and perpetrators.

## Importance of Logs
- Logs are digital footprints recording system activities.
- Used to track normal and malicious activities.
- Essential for security monitoring, forensics, and troubleshooting.

## Use Cases of Logs
| Use Case | Description |
|-------------|----------------|
| Security Events Monitoring | Detects anomalous behavior via real-time monitoring. |
| Incident Investigation & Forensics | Provides detailed insights into system activities for root cause analysis. |
| Troubleshooting | Helps diagnose and resolve system/application errors. |
| Performance Monitoring | Assesses application performance trends. |
| Auditing & Compliance | Maintains activity trails for regulatory compliance. |

---

## Types of Logs
| Log Type | Usage | Examples |
|-------------|---------|-----------|
| System Logs | Tracks OS-related activities. | System startup/shutdown, driver loading, system errors. |
| Security Logs | Detects security incidents. | Authentication attempts, user account changes, policy modifications. |
| Application Logs | Logs application-specific events. | User interactions, application updates, error reports. |
| Audit Logs | Tracks system changes and user actions. | Data access, system changes, policy enforcement. |
| Network Logs | Monitors network traffic. | Incoming/outgoing traffic, connection attempts, firewall logs. |
| Access Logs | Logs access to resources. | Webserver access logs, API access logs. |

---

## Windows Event Log Analysis
- **Event Viewer** is a built-in Windows tool for log inspection.
- Key fields in logs:
  - **Description**: Activity details.
  - **Log Name**: File category.
  - **Logged**: Timestamp of the event.
  - **Event ID**: Unique identifier for events.

### Common Event IDs
| Event ID | Description |
|-------------|----------------|
| 4624 | Successful login |
| 4625 | Failed login attempt |
| 4634 | User logged off |
| 4720 | User account creation |
| 4724 | Password reset attempt |
| 4722 | User account enabled |
| 4725 | User account disabled |
| 4726 | User account deleted |

- **Filtering Logs in Event Viewer**
  - Use "Filter Current Log" to search for specific event IDs.
  - Example: Filter event ID **4624** to find successful logins.

---

## Web Server Access Logs
- Logs all website requests with details such as:
  - **IP Address**: Origin of request.
  - **Timestamp**: Time of access.
  - **Request Type**: HTTP method (GET, POST, etc.).
  - **URL**: Requested resource.
  - **Status Code**: Server response (200, 404, etc.).
  - **User-Agent**: Browser & OS details.

---

## Log Analysis Using Linux Commands
### Displaying Logs
- `cat access.log` → View log file contents.
- `cat access1.log access2.log > combined.log` → Merge multiple logs.

### Searching Logs
- `grep "192.168.1.1" access.log` → Find entries related to a specific IP.

### Paginated Log Viewing
- `less access.log` → View logs one page at a time.
  - **Navigation**:
    - **Spacebar** → Next page.
    - **b** → Previous page.
    - **/** → Search within logs.
    - **n** → Next match.
    - **N** → Previous match.

---

This summary provides a structured overview of log analysis, its significance, and practical methods for investigation.
