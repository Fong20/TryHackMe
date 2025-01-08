
# Bash Scripting Overview

## What is Bash?
- Bash is a scripting language used within the terminal in Linux and macOS.
- It automates tasks like system administration, backups, and more.

---

## Basics of Bash Scripting

### Script Structure
- Always start a script with `#!/bin/bash` to indicate the script uses Bash.

```bash
#!/bin/bash
echo "Hello World"
```

- Run the script:
  ```bash
  chmod +x yourfile.sh
  ./yourfile.sh
  ```

### Linux Commands
- You can execute Linux commands in Bash scripts:
  ```bash
  echo "Running Linux commands..."
  ls
  ```

---

## Variables in Bash

### Declaration and Usage
```bash
name="Jammy"
echo $name
```
- Avoid spaces around `=` when assigning values.
- Use `$` to reference variables.

### Debugging Scripts
- Run with debugging enabled:
  ```bash
  bash -x ./file.sh
  ```

- Insert debugging markers in the script:
  ```bash
  set -x  # Start debugging
  # Commands to debug
  set +x  # Stop debugging
  ```

---

## Parameters and User Input

### Using Command-line Arguments
- `$1`, `$2`, etc., are positional parameters.
```bash
name=$1
echo $name
```

- Example:
  ```bash
  ./example.sh Alex Tony
  ```

### Interactive Input
- Use `read` for user interaction:
  ```bash
  echo "Enter your name:"
  read name
  echo "Hello, $name!"
  ```

---

## Arrays

### Declaration and Access
```bash
transport=('car' 'train' 'bike' 'bus')
echo "${transport[@]}"    # Prints all elements
echo "${transport[1]}"    # Prints the second element
```

### Modify or Remove Elements
```bash
unset transport[1]        # Removes the second element
transport[1]='trainride'  # Updates the second element
```

---

## Conditional Statements

### If Statements
```bash
count=10
if [ $count -eq 10 ]; then
    echo "True"
else
    echo "False"
fi
```

#### Relational Operators:
- `-eq` (equal to), `-ne` (not equal), `-gt` (greater than), `-lt` (less than), `-ge` (greater than or equal).

### File Operations
- Check if a file exists and is writable:
  ```bash
  if [ -f "$1" ] && [ -w "$1" ]; then
      echo "hello" >> "$1"
  else
      echo "hello" > "$1"
  fi
  ```

---

## Example Projects

### Biography Maker
- Collect multiple inputs and store them in variables or arrays.

### Eligibility Checker
- Use conditionals to check age and output eligibility status:
  ```bash
  if [ $age -lt 18 ]; then
      echo "You are not eligible for work."
  else
      echo "Enter your job title:"
      read job
      echo "You work as a $job."
  fi
  ```
