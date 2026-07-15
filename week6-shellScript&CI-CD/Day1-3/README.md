#  DevOps Challenge - Week 6
## Shell Scripting Fundamentals (Day 1–3)

Shell scripting is one of the most powerful skills in a DevOps engineer's toolkit. It allows you to automate repetitive tasks, orchestrate complex workflows, manage server configurations, and glue different tools together in CI/CD pipelines.

By learning Bash scripting, you gain direct control over the Linux operating system, allowing you to perform operations at scale without manual intervention.

---

# Topics Covered

## 1. Introduction to Bash & Scripting Basics
* What is Shell Scripting & Bash?
* Script structure: Shebang (`#!/bin/bash`) and execution permissions (`chmod +x`).
* Variables (User-defined vs Environment variables) and reading input.

## 2. Conditional Logic & Control Flow
* Using test operators for strings, numbers, and files.
* Constructing `if-elif-else` conditions.
* Implementing `case` statements for clean decision-making branching.

## 3. Loops and Iteration
* Writing `for` loops (iterating over ranges, arrays, and command outputs).
* Utilizing `while` loops (reading files line-by-line, monitoring loops).

## 4. Functions & Arguments (Positional Parameters)
* Modularizing code using functions.
* Handling CLI arguments (`$1`, `$2`, `$@`, `$#`).
* Managing exit codes (`$?`) and custom error status handling.

---

# Shell Script Execution Lifecycle

```text
       +------------------------------------------------+
       |               Bash Script File                 |
       |                (my_script.sh)                  |
       +------------------------------------------------+
                               │
            Run Command:       ▼
            ./my_script.sh or bash my_script.sh
                               │
                               ▼
       +------------------------------------------------+
       |               Shebang Parser                   |
       |           Reads: #!/bin/bash                  |
       +------------------------------------------------+
                               │
             Launches:         ▼
       +------------------------------------------------+
       |             Bash Interpreter Process           |
       |  Loads: Environment, Aliases, System Variables |
       +------------------------------------------------+
                               │
             Executes:         ▼
       +------------------------------------------------+
       |          Line-by-Line Execution Flow           |
       |    Runs Commands -> Captures Exit Codes ($?)   |
       +------------------------------------------------+
```

---

# Scripting Basics & Variables

To run a shell script, it must start with a **Shebang** (`#!`) which tells the OS which interpreter to use. It must also have execution permissions.

### 1. Structure of a Script
Create `setup.sh`:
```bash
#!/bin/bash

# This is a comment
echo "Setting up the environment..."
```

### 2. Permissions and Execution
```bash
# Give execution permissions to the script
chmod +x setup.sh

# Run the script
./setup.sh
```

### 3. Variables and User Input
Shell variables are untyped (treated as strings by default). Do not use spaces around the `=` sign during assignment.

```bash
#!/bin/bash

# System / Environment Variables
echo "Current User: $USER"
echo "Home Directory: $HOME"

# User-Defined Variables
APP_NAME="WebApp"
PORT=8080
echo "Deploying $APP_NAME on port $PORT..."

# Reading User Input
echo -n "Enter your environment (dev/prod): "
read ENV_TYPE
echo "Configuring for $ENV_TYPE environment."
```

---

# Conditional Logic

Conditional statements allow you to perform decisions based on tests. Bash uses `[ ]` (or `[[ ]]` for advanced features) to evaluate test conditions.

### Test Operators Reference

| Operator | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| `-eq` / `-ne` | Numeric | Equal / Not Equal | `[ $A -eq $B ]` |
| `-gt` / `-lt` | Numeric | Greater Than / Less Than | `[ $A -gt $B ]` |
| `-z` / `-n` | String | Is Empty / Is Not Empty | `[ -z "$STR" ]` |
| `=` / `!=` | String | Equal / Not Equal | `[ "$A" = "$B" ]` |
| `-f` / `-d` | File | Is Regular File / Is Directory | `[ -f "/etc/passwd" ]` |
| `-r` / `-w` | File | Is Readable / Is Writable | `[ -w "logs.txt" ]` |

### `if-elif-else` Example
```bash
#!/bin/bash

FILE_PATH="/var/log/syslog"

if [ -f "$FILE_PATH" ]; then
    echo "Log file exists."
    if [ -w "$FILE_PATH" ]; then
        echo "Log file is writable."
    else
        echo "Log file is read-only."
    fi
else
    echo "Log file does not exist!"
fi
```

### `case` Branching Example
```bash
#!/bin/bash

echo "Select an action:"
echo "1) Start Service"
echo "2) Stop Service"
echo "3) Restart Service"
read -p "Enter choice [1-3]: " CHOICE

case $CHOICE in
    1)
        echo "Starting service..."
        ;;
    2)
        echo "Stopping service..."
        ;;
    3)
        echo "Restarting service..."
        ;;
    *)
        echo "Invalid option chosen."
        exit 1
        ;;
esac
```

---

# Loops & Iterations

Loops are used to repeat tasks, process collections of data, or monitor processes continuously.

### 1. `for` Loop Examples
```bash
# Iterating over a range of numbers
for i in {1..5}; do
    echo "Creating directory: app_v$i"
done

# Iterating over files in a directory
for FILE in *.conf; do
    echo "Backing up config file: $FILE"
    cp "$FILE" "$FILE.bak"
done
```

### 2. `while` Loop Examples
```bash
# Reading a file line by line
LINE_NUM=1
while read -r LINE; do
    echo "Line $LINE_NUM: $LINE"
    LINE_NUM=$((LINE_NUM + 1))
done < user_list.txt

# Infinite loop for service check
while true; do
    if pgrep nginx > /dev/null; then
        echo "Nginx is running..."
    else
        echo "Nginx is DOWN! Alerting..."
    fi
    sleep 10
done
```

---

# Functions and Arguments

Functions make scripts modular, reusable, and easy to maintain. Positional parameters handle inputs passed when running scripts or calling functions.

```text
  Command:   ./deploy.sh   frontend   v2.1.0
                 ↑            ↑          ↑
              Script         $1         $2     (Positional Arguments)
```

### Modular Script with Functions and Arguments
```bash
#!/bin/bash

# Function definition
log_message() {
    local LEVEL=$1
    local MSG=$2
    # Output formatted log with current date and time
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] [$LEVEL] $MSG"
}

# Main Script logic using positional parameters
if [ $# -lt 2 ]; then
    log_message "ERROR" "Missing arguments. Usage: $0 <environment> <version>"
    exit 1
fi

ENV=$1
VERSION=$2

log_message "INFO" "Starting deployment of version $VERSION to $ENV..."

# Simulated action
mkdir -p "/opt/deploy/$ENV/$VERSION"
if [ $? -eq 0 ]; then
    log_message "SUCCESS" "Deployment directories initialized successfully."
else
    log_message "ERROR" "Failed to create deployment directories!"
    exit 2
fi
```

---

# Learning Outcome

After completing Day 1–3, I can:

- ✅ Write and execute custom Bash scripts using shebang (`#!/bin/bash`) and execution permissions (`chmod +x`).
- ✅ Declare, manipulate, and interpolate user-defined and system environment variables.
- ✅ Handle dynamic user inputs interactively within shell scripts using `read`.
- ✅ Implement complex conditional logic using `if-elif-else` statements and test operators.
- ✅ Structure robust branching code blocks with `case` menus.
- ✅ Leverage `for` and `while` loops to process lists, directory structures, and file streams.
- ✅ Modularize scripts using functions and handle script parameters using positional arguments (`$1`, `$2`, `$#`, `$@`).
- ✅ Manage application flow control via exit codes (`$?`).

---

# Next Topics Goals

- **Advanced Shell Automation & CI/CD Pipelines (Day 4–5)**

---

# Motivation Corner

> **"If you have to do it more than once, write a script to do it."**

> **"Scripts are executable documentation. They ensure complex system operations are run exactly the same way, every single time."**

---

# Challenge Motto

```
Identify the Chore
         ↓
Write the Bash Code
         ↓
Grant Execution Permissions
         ↓
Automate with One Keypress
```
 Automate everything. Fail fast. Recover faster.
