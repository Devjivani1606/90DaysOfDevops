# DevOps Challenge - Week 4
## Python for DevOps & Automation (Day 4–7)

In the first half of this week, we covered basic Python syntax, data structures, and foundational concepts. 

Now, we will focus on applying Python to practical DevOps tasks: system automation, handling configuration files (JSON & YAML), interacting with REST APIs, and writing robust scripts to automate day-to-day operations.

---

# Topics Covered

## 1. System Automation Modules
Python provides powerful built-in libraries to interact with the underlying Operating System.

* **`os`**: Path manipulations, working directories, and reading environment variables.
* **`sys`**: Handling system arguments and command-line inputs.
* **`subprocess`**: Executing shell commands and capturing stdout/stderr.
* **`shutil`**: High-level file operations (copying, moving, and archiving files/directories).

## 2. Handling Configuration Formats (JSON & YAML)
DevOps tools rely heavily on structured data formats.
* Reading and writing JSON files.
* Reading and parsing YAML configuration files.

## 3. Web APIs & HTTP Requests
* Consuming external REST APIs using the `requests` library.
* Parsing API JSON responses.

---

# System Automation Modules

```text
               +--------------------------------------+
               |          Python Script               |
               +--------------------------------------+
                 /         |               \        \
                /          |                \        \
               v           v                 v        v
         [os module]  [sys module]    [subprocess]  [shutil]
              │            │                 │          │
              ▼            ▼                 ▼          ▼
         Env / Paths  CLI Args & Exec    Bash Cmds   File Ops
```

---

## 1. The `os` Module
Used to interact with files, directories, and environment variables.

### Working with Environment Variables
```python
import os

# Get an environment variable
db_host = os.getenv("DB_HOST", "localhost")
print(f"Database Host: {db_host}")

# Set an environment variable
os.environ["APP_STAGE"] = "Production"
```

### File and Path Manipulations
Always use `os.path` to ensure scripts run on both Linux and Windows.
```python
import os

# Join paths cleanly
log_dir = os.path.join("/var", "log", "nginx")
print(f"Log Directory Path: {log_dir}")

# Check if path exists
if os.path.exists(log_dir):
    print("Log directory exists!")
```

---

## 2. The `sys` Module
Provides access to variables and functions that interact with the Python interpreter.

### CLI Arguments (`sys.argv`)
```python
import sys

# sys.argv[0] is the script name. Subsequent elements are arguments.
if len(sys.argv) < 2:
    print("Error: Missing argument. Usage: python script.py <filename>")
    sys.exit(1)

filename = sys.argv[1]
print(f"Processing file: {filename}")
```

---

## 3. The `subprocess` Module
Used to execute shell commands directly from Python. This replaces the old `os.system`.

### Running Commands and Capturing Output
```python
import subprocess

# Run a command and capture its output
result = subprocess.run(["df", "-h"], capture_output=True, text=True)

if result.returncode == 0:
    print("Command Output:\n", result.stdout)
else:
    print("Error executing command:\n", result.stderr)
```

---

## 4. The `shutil` Module
Used for file operations like copying, moving, and creating archives.

### Archiving a Directory
```python
import shutil

# Compress a folder into a zip file
shutil.make_archive("backup_logs", "zip", "/var/log/nginx")
print("Logs archived successfully.")
```

---

#  Handling JSON and YAML

## Parsing JSON
```python
import json

# Parse JSON string
json_data = '{"name": "nginx-container", "port": 80, "active": true}'
config = json.loads(json_data)
print(config["name"])  # Output: nginx-container

# Write to JSON file
with open("config.json", "w") as f:
    json.dump(config, f, indent=4)
```

## Parsing YAML
To parse YAML, we use the `pyyaml` library:
```bash
pip install pyyaml
```
```python
import yaml

# Read and parse YAML file
with open("deployment.yaml", "r") as f:
    data = yaml.safe_load(f)

print(f"Deploying application: {data['metadata']['name']}")
```

---

# API Integrations (HTTP Requests)

DevOps scripts often interact with APIs (GitHub, Slack, Jira, Cloud Providers). We use the `requests` library.

```bash
pip install requests
```

### Making a GET Request
```python
import requests

response = requests.get("https://api.github.com/repos/kubernetes/kubernetes")

if response.status_code == 200:
    repo_data = response.json()
    print(f"Kubernetes Stars: {repo_data['stargazers_count']}")
    print(f"Open Issues: {repo_data['open_issues_count']}")
else:
    print(f"Failed to fetch data. Status code: {response.status_code}")
```

---

# Real-World DevOps Automation Scripts

Here are three core scripts you should write and practice.

## 1. Disk Space Alert Script (`disk_monitor.py`)
Monitors disk partition usage and prints a warning if it exceeds a threshold.

```python
import shutil
import sys

THRESHOLD = 80  # Threshold percentage

total, used, free = shutil.disk_usage("/")
percent_used = (used / total) * 100

print(f"Disk Usage: {percent_used:.2f}% (Used: {used // (2**30)}GB, Free: {free // (2**30)}GB)")

if percent_used > THRESHOLD:
    print(f" WARNING: Disk usage is above {THRESHOLD}%!", file=sys.stderr)
    # In a real environment, you could trigger a Slack notification or email here.
else:
    print(" Disk space is within normal limits.")
```

---

## 2. Log Parser for Errors (`log_parser.py`)
Reads a log file and counts the occurrences of "ERROR" or "CRITICAL".

```python
import os

LOG_FILE = "app.log"

if not os.path.exists(LOG_FILE):
    # Create a dummy log file for testing
    with open(LOG_FILE, "w") as f:
        f.write("INFO: App started\nERROR: Database connection failed\nINFO: Retry 1\nERROR: Timeout occurred\n")

error_count = 0

with open(LOG_FILE, "r") as file:
    for line in file:
        if "ERROR" in line or "CRITICAL" in line:
            print(f"Detected Log Failure: {line.strip()}")
            error_count += 1

print(f"\nTotal Errors Found: {error_count}")
```

---

## 3. Automated Backup Script (`backup.py`)
Backs up a directory into a ZIP archive with a timestamp.

```python
import os
import shutil
from datetime import datetime

SOURCE_DIR = "./source_dir"
BACKUP_DIR = "./backups"

# Create dummy source folder if it doesn't exist
if not os.path.exists(SOURCE_DIR):
    os.makedirs(SOURCE_DIR)
    with open(f"{SOURCE_DIR}/important_data.txt", "w") as f:
        f.write("Important production config.")

# Create backup folder
if not os.path.exists(BACKUP_DIR):
    os.makedirs(BACKUP_DIR)

# Generate unique timestamped archive name
timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
backup_name = f"backup_{timestamp}"
backup_path = os.path.join(BACKUP_DIR, backup_name)

# Create backup archive
shutil.make_archive(backup_path, "zip", SOURCE_DIR)
print(f" Backup created successfully at: {backup_path}.zip")
```

---

# Learning Outcome

After completing Day 4–7, I can:

- ✅ Read and write Environment Variables using `os`
- ✅ Process Command Line Arguments using `sys.argv`
- ✅ Execute Shell Commands and capture their output using `subprocess`
- ✅ Copy, move, and compress files programmatically with `shutil`
- ✅ Work with standard JSON and YAML configuration files
- ✅ Write python scripts to fetch data from HTTP APIs using the `requests` library
- ✅ Design automated DevOps maintenance and monitoring scripts

---

#  Next Week Goals

- **Docker Containers & Image Creation (Week 5)**

---

# Motivation Corner

> **"A manual process is a bug in waiting. Python is your tool to fix it."**

> **"Automate the small things, so you have time to orchestrate the big things."**

---

# Challenge Motto

```
Analyze the Task
       ↓
Write the Script
       ↓
Run the Cronjob
       ↓
Save Countless Manual Hours
```

 Code once. Automate forever.
