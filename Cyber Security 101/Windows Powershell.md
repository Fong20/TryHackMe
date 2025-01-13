
# Windows Powershell

### **PowerShell Objects**
- **Definition**: Objects represent items with **properties** (characteristics) and **methods** (actions). Example: A "car" object might have:
  - **Properties**: Color, Model, FuelLevel
  - **Methods**: Drive(), HonkHorn(), Refuel()
- In PowerShell, cmdlets return objects (not plain text), making data manipulation more flexible.

---

### **Launching PowerShell**
- **Windows GUI Methods**:
  - **Start Menu**: Search for "PowerShell."
  - **Run Dialog**: Press `Win + R`, type `powershell`, and hit Enter.
  - **File Explorer**: Type `powershell` in the address bar.
  - **Task Manager**: File > Run new task > `powershell`.
- **From Command Prompt**: Type `powershell` and press Enter.

---

### **Cmdlet Syntax**
- **Verb-Noun Format**:
  - **Verb**: Describes the action (e.g., `Get`, `Set`, `Install`).
  - **Noun**: Specifies the object (e.g., `Content`, `Location`, `Module`).
- **Examples**:
  - `Get-Content`: Retrieves file content.
  - `Set-Location`: Changes the current directory.

---

### **Discovering Commands**
- **`Get-Command`**: Lists all available cmdlets, functions, aliases, and scripts.
  ```powershell
  Get-Command
  Get-Command -CommandType "Function"  # Filter by type
  ```
- **`Get-Help`**: Provides information on cmdlets, including usage and examples.
  ```powershell
  Get-Help Get-Date -Examples
  ```
- **`Get-Alias`**: Lists PowerShell aliases (shortcuts for cmdlets).
  - Examples:
    - `dir` → `Get-ChildItem`
    - `cd` → `Set-Location`
    - `cat` → `Get-Content`

---

### **Extending PowerShell**
- **Online Repositories**:
  - Use `Find-Module` to search for new modules:
    ```powershell
    Find-Module -Name "PowerShell*"
    ```
  - Use `Install-Module` to download and install modules:
    ```powershell
    Install-Module -Name "PowerShellGet"
    ```
- **Example**:
  - **Module**: PowerShellGet (manages discovering and installing PowerShell artifacts).

---

### **Additional Features**
- Cmdlets can be filtered and extended with options like `-Property` or wildcards (`*`).
- Aliases and cmdlet consistency help bridge the gap for users transitioning from traditional shells (e.g., Command Prompt).


### **Navigation and File Management**
- **`Get-ChildItem`**: Lists files/directories in a specified path (like `dir` or `ls`).
  - If no `-Path` is provided, lists the current directory's contents.
- **`Set-Location`**: Changes the working directory (like `cd`).
  ```powershell
  Set-Location -Path ".\Documents"
  ```

### **Creating and Deleting Items**
- **`New-Item`**: Creates files or directories.
  ```powershell
  New-Item -Path ".\folder\file.txt" -ItemType "File"
  New-Item -Path ".\folder\subfolder" -ItemType "Directory"
  ```
- **`Remove-Item`**: Deletes files or directories (equivalent to `del` or `rmdir`).
  ```powershell
  Remove-Item -Path ".\folder\file.txt"
  ```

### **Copying and Moving Items**
- **`Copy-Item`**: Copies files or directories.
  ```powershell
  Copy-Item -Path ".\source.txt" -Destination ".\destination.txt"
  ```
- **`Move-Item`**: Moves files or directories.
  ```powershell
  Move-Item -Path ".\source.txt" -Destination ".\new_folder"
  ```

### **Reading and Filtering**
- **`Get-Content`**: Reads the contents of a file (like `cat` or `type`).
  ```powershell
  Get-Content -Path ".\file.txt"
  ```
- **`Sort-Object`**: Sorts objects by a property.
  ```powershell
  Get-ChildItem | Sort-Object Length
  ```
- **`Where-Object`**: Filters objects based on conditions.
  ```powershell
  Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"
  ```
- **`Select-Object`**: Selects specific properties from objects.
  ```powershell
  Get-ChildItem | Select-Object Name, Length
  ```

### **Advanced Filtering**
- **Comparison Operators**:
  - `-eq`: Equal to
  - `-ne`: Not equal to
  - `-gt`: Greater than
  - `-lt`: Less than
  - `-ge`: Greater than or equal to
  - `-le`: Less than or equal to
- **Pattern Matching**:
  ```powershell
  Get-ChildItem | Where-Object -Property "Name" -like "ship*"
  ```

### **System and Network Information**
- **`Get-ComputerInfo`**: Retrieves detailed system information.
- **`Get-LocalUser`**: Lists local user accounts.
- **`Get-NetIPConfiguration`**: Displays network configurations.
- **`Get-NetIPAddress`**: Shows all configured IP addresses.

### **Monitoring and Analysis**
- **`Get-Process`**: Displays running processes with details.
- **`Get-Service`**: Lists services and their statuses.
- **`Get-NetTCPConnection`**: Displays active TCP connections.
- **`Get-FileHash`**: Computes the hash of a file (useful for integrity checks).
  ```powershell
  Get-FileHash -Path ".\file.txt"
  ```

### **Piping and Automation**
- Piping (`|`) in PowerShell passes objects, enabling detailed manipulation.
- Example: Display the largest file in a directory:
  ```powershell
  Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1
  ```

### **Remote Commands**
- **`Invoke-Command`**: Executes commands on remote systems.
  ```powershell
  Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Culture }
  ```

### **Scripting in PowerShell**
- Automates repetitive tasks and complex workflows.
- Useful for system administrators, incident responders, and penetration testers.
- Example: Automating remote tasks with a script:
  ```powershell
  Invoke-Command -FilePath "C:\scripts\task.ps1" -ComputerName Server01
  ```
