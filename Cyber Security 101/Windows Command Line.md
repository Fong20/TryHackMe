
# Windows Command Line Interface (CLI)

## GUI vs CLI
- **GUIs** are intuitive and user-friendly.
- **CLIs** have a learning curve but offer faster and more efficient operations once mastered.

### Advantages of CLI
1. **Lower Resource Usage**: Ideal for older hardware or systems with limited resources.
2. **Automation**: Scripts or batch files simplify repetitive tasks.
3. **Remote Management**: CLI supports SSH, working well on low-resource systems and slow networks.

---

## Windows Command Line Basics

### Accessing System Information
- **`ver`**: Displays OS version.
- **`systeminfo`**: Lists detailed system information.
    - Use **`| more`** to paginate long outputs.

### Network Configuration and Troubleshooting
- **`ipconfig`**: Displays network info (IP, subnet mask, default gateway).
    - **`ipconfig /all`**: Shows detailed network configuration.
- **`ping target_name`**: Checks connectivity to a server.
- **`tracert target_name`**: Traces the route to a server.
- **`nslookup`**: Retrieves IP address for a domain.
- **`netstat`**: Displays network connections and listening ports.
    - Options: 
        - **`-a`**: Show all connections and ports.
        - **`-b`**: Show associated programs.
        - **`-o`**: Show process IDs (PIDs).
        - **`-n`**: Use numerical addresses.

---

## Directory Management
- **`cd`**: Display or change the current directory.
    - **`cd ..`**: Move up one level.
- **`dir`**: Lists contents of the current directory.
    - Options:
        - **`/a`**: Show hidden/system files.
        - **`/s`**: Include subdirectories.
- **`mkdir`**: Create a new directory.
- **`rmdir`**: Delete a directory.
- **`tree`**: Visual representation of directories.

---

## File Management
- **`type file.txt`**: Displays contents of a text file.
- **`more file.txt`**: Paginates long text files.
- **`copy`**: Copy files (e.g., `copy file1 file2`).
- **`move`**: Move files (e.g., `move file target_dir`).
- **`erase` or `del`**: Delete files.
- **Wildcards**: Use `*` for multiple files (e.g., `copy *.txt C:\Backup`).

---

## Process Management
- **`tasklist`**: Lists running processes.
    - **`/FI`**: Filter processes (e.g., `tasklist /FI "imagename eq sshd.exe"`).
- **`taskkill /PID pid_number`**: Terminates a process.

---

## Additional Commands
- **`chkdsk`**: Checks file system and disk for errors.
- **`driverquery`**: Lists installed drivers.
- **`sfc /scannow`**: Scans and repairs corrupted system files.

---

## Tips
- Use **`/help` or `/?`** to display help for any command.
- Pipe long outputs with **`| more`** to view one page at a time.
