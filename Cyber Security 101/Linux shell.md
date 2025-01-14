
# Linux CLI, Shells, and Scripting

## Introduction to CLI vs. GUI
- **GUI**: User-friendly, menu-driven interaction with OS.
- **CLI**: Command-line interaction; efficient and resource-friendly.
- **Shell**: Acts as an intermediary in CLI, providing features for command execution.

## Popular Linux Commands
- `pwd`: Print the current working directory.
- `cd <directory>`: Change directory.
- `ls`: List directory contents.
- `cat <file>`: Display file contents.
- `grep <pattern> <file>`: Search for a pattern in a file.

## Identifying and Changing Shells
- Check the current shell: `echo $SHELL`.
- List installed shells: `cat /etc/shells`.
- Switch shell: Enter shell name (e.g., `zsh`).
- Change default shell: `chsh -s <shell_path>`.

## Overview of Common Linux Shells
| Feature            | Bash                     | Fish                     | Zsh                     |
|--------------------|--------------------------|--------------------------|--------------------------|
| **Full Name**      | Bourne Again Shell       | Friendly Interactive Shell | Z Shell                 |
| **Scripting**      | Widely compatible, extensive docs | Limited compared to others | Advanced scripting     |
| **Tab Completion** | Basic                    | Advanced suggestions     | Extensible with plugins |
| **Customization**  | Basic                    | Interactive customization | Advanced (oh-my-zsh)    |
| **User-friendliness** | Less user-friendly but familiar | Most user-friendly      | User-friendly with customization |
| **Syntax Highlighting** | Not available         | Built-in                 | Via plugins             |

## Writing Shell Scripts
1. **File Creation**: Use a text editor, e.g., `nano script_name.sh`.
2. **Shebang**: Specify the interpreter, e.g., `#!/bin/bash`.
3. **Make Executable**: `chmod +x script_name.sh`.
4. **Execution**: `./script_name.sh`.

### Examples

#### Variables
```bash
#!/bin/bash
echo "What's your name?"
read name
echo "Welcome, $name"
```

#### Loops
```bash
#!/bin/bash
for i in {1..10}; do
  echo $i
done
```

#### Conditional Statements
```bash
#!/bin/bash
echo "Please enter your name:"
read name
if [ "$name" = "Stewart" ]; then
  echo "Welcome Stewart! Here is the secret: THM_Script"
else
  echo "Sorry! You are not authorized."
fi
```

#### Comments
- Add `#` before lines for explanations.
```bash
# This script demonstrates a conditional statement.
#!/bin/bash
# Prompt for user input
echo "Enter your name:"
read name
# Check if the input matches the required value
if [ "$name" = "Admin" ]; then
  echo "Access granted."
else
  echo "Access denied."
fi
```

## Advantages of Shell Scripting
- Automates repetitive tasks.
- Enables bulk operations with minimal effort.

## Notes
- Scripts require execution permissions to run.
- Always use comments for clarity, especially in complex scripts.

---
