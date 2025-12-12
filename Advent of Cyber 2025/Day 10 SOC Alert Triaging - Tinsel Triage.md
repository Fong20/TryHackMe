# SOC Alert Triaging - Tinsel Triage

## Key Concepts
-   Alert Triaging identifies which alerts need fast response.
-   Four triage dimensions:
    -   Severity – how bad?
    -   Time – when?
    -   Context – where in attack lifecycle?
    -   Impact – who/what is affected?

## Triaging Workflow
1.  Review alert severity.
2.  Check timestamps & frequency.
3.  Identify attack stage (recon → priv escalation → exfil).
4.  Identify affected assets.
5.  Decide: escalate, investigate more, or close as false positive.
6.  Document decisions.

## Investigation Workflow
-   Review alert entities & detection logic.
-   Check logs for unusual patterns.
-   Correlate alerts by user/IP/host.
-   Build a timeline.
-   Determine next action.
-   Document findings.

## Microsoft Sentinel Steps

-   Navigate to Sentinel → Incidents.
-   Review high-severity alerts first.
-   Example alert: Linux PrivEsc — Kernel Module Insertion
    -   3 related events
    -   3 entities
    -   Privilege Escalation stage

## Related Alerts Example

  Alert                             Meaning
  --------------------------------- -----------------
  Root SSH Login from External IP   Initial access
  SUID Discovery                    PrivEsc attempt
  Kernel Module Insertion           Persistence

### KQL Query (PoC)

    set query_now = datetime(2025-10-30T05:09:25.9886229Z);
    Syslog_CL
    | where host_s == 'app-02'
    | project _timestamp_t, host_s, Message

### Findings from Logs (app-02)

-   cp command used to create shadow file backup
-   User Alice added to sudoers
-   backupuser modified by root
-   malicious module inserted: malicious_mod.ko
-   Successful SSH login by root

## Conclusion

-   Events suggest privilege escalation + persistence
-   Activity is highly suspicious and requires escalation
