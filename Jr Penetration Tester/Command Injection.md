
# Command Injection 

## Overview
Command injection is a web vulnerability allowing attackers to execute commands on the server’s OS through a vulnerable application. It's also referred to as Remote Code Execution (RCE).

## Key Concepts
- **Executed with App Privileges**: Commands are run with the same privileges as the application.
- **Highly Impactful**: Can be used to access sensitive data, files, and gain control over the system.

## Example Scenario
- User input passed into shell command without proper validation.
- Input like `; whoami` could be executed on the server.

## Real-World Data
- Contrast Security’s AppSec report (2019): Command injection in top 10 vulnerabilities.
- OWASP also lists it among top web vulnerabilities.

## Code Example (PHP)
```php
$title = $_GET['title'];
$output = shell_exec("grep $title songtitle.txt");
echo $output;
```
- Vulnerable due to direct use of user input in a shell command.

## Code Example (Python Flask)
```python
from flask import Flask
import subprocess

app = Flask(__name__)

@app.route('/<cmd>')
def run(cmd):
    return subprocess.getoutput(cmd)
```
- Executes whatever command is passed in the URL.

## Shell Operators
- `;`, `&`, `&&` can be used to chain commands.

## Detection Types
### Blind Command Injection
- No visible output.
- Use time-based payloads like `ping`, `sleep`, `timeout`.
- Redirect output using `>` and read it later.

### Verbose Command Injection
- Immediate feedback on the web page.
- Example: `curl http://vulnerable.app/process.php?search=The%20Beatles;whoami`

## Useful Payloads
### Linux
| Payload | Description |
|--------|-------------|
| `whoami` | Check user |
| `ls` | List directory |
| `ping` | Test delay |
| `sleep` | Test delay (alternative) |
| `nc` | Spawn reverse shell |

### Windows
| Payload | Description |
|--------|-------------|
| `whoami` | Check user |
| `dir` | List directory |
| `ping` | Test delay |
| `timeout` | Test delay (alternative) |

## Prevention
### Avoid Vulnerable Functions
- Functions like `exec`, `passthru`, `system` in PHP.

### Input Sanitisation
- Allow only specific patterns/characters.
- Example using `filter_input()` in PHP to validate numeric input.

### Filter Bypass
- Filters may be bypassed using encoding (e.g., hex).
- Logic flaws in sanitisation can be exploited.

## Summary
- Identify and test for command injection vulnerabilities.
- Use OS-specific payloads.
- Implement robust input sanitisation and avoid dangerous functions.
- Apply knowledge in practical scenarios.
