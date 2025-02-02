
# Metasploit: Introduction

## Overview
- **Metasploit**: A widely used exploitation framework for penetration testing.
- **Versions**:
  - **Metasploit Pro**: Commercial version with GUI for automation and management.
  - **Metasploit Framework**: Open-source, command-line-based.

---

## Main Components
1. **msfconsole**: Main command-line interface.
2. **Modules**:
   - **Auxiliary**: Tools like scanners, crawlers, fuzzers.
   - **Encoders**: Encode payloads to bypass signature-based AVs.
   - **Evasion**: Modules for bypassing AVs directly.
   - **Exploits**: Organized by target system.
   - **NOPs**: Used as buffers to maintain consistent payload sizes.
   - **Payloads**: Executable code to achieve the attacker's goal.

3. **Payload Categories**:
   - **Adapters**: Convert payloads into other formats.
   - **Singles**: Self-contained payloads (e.g., add user, launch notepad).
   - **Stagers**: Set up connection channels between attacker and target.
   - **Stages**: Large payloads downloaded by stagers.

4. **Tools**:
   - **msfvenom**: Payload creation.
   - **pattern_create** and **pattern_offset**: Exploit development.

---

## Key Concepts
- **Vulnerability**: Flaws in design or code.
- **Exploit**: Code leveraging vulnerabilities.
- **Payload**: Code run on the target system to achieve desired outcomes (e.g., reverse shell).

---

## Metasploit Workflow
1. **Searching for Modules**:
   - Use the `search` command with parameters like CVE, exploit name, or target system.
   - Example: `search type:auxiliary telnet`.

2. **Setting Module Parameters**:
   - `set PARAMETER_NAME VALUE`
   - Common parameters:
     - **RHOSTS**: Target system IP address.
     - **RPORT**: Target port.
     - **PAYLOAD**: Payload to use.
     - **LHOST**: Attacking machine IP.
     - **LPORT**: Local port for reverse shell.
     - **SESSION**: ID of existing session.

   - **Global Settings**:
     - `setg PARAMETER_NAME VALUE`: Sets parameters globally.
     - `unsetg PARAMETER_NAME`: Clears global values.

3. **Running Modules**:
   - `exploit` or `run` to execute a module.
   - `exploit -z`: Run and background the session.
   - Use `check` to confirm vulnerability without exploitation.

4. **Managing Sessions**:
   - `background`: Background a session.
   - `sessions`: List active sessions.
   - `sessions -i SESSION_NUMBER`: Interact with a session.

---

## Helpful Commands
- **help**: Displays help.
- **history**: View previously typed commands.
- **show options**: Display module parameters.
- **info**: Detailed information about a module.
- **back**: Exit current context.

---

## Tab Completion
- Auto-completes commands or parameters (e.g., typing `he` + `TAB` = `help`).
