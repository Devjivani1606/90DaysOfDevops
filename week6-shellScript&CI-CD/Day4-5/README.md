#  DevOps Challenge - Week 6
## Advanced Shell Scripting & CI/CD Pipelines (Day 4–5)

Transitioning from scripting fundamentals to production-grade automation requires understanding stream manipulation, system diagnostic scripting, and connecting scripts to modern CI/CD systems like GitHub Actions. 

This section covers advanced text-processing utilities, automated cron scheduling, and executing shell scripts natively inside automated pipelines.

---

# Topics Covered

## 1. Advanced Input/Output & Stream Redirections
* Understanding Standard Input (stdin), Standard Output (stdout), and Standard Error (stderr).
* Redirection operators (`>`, `>>`, `2>`, `2>&1`) and `/dev/null`.

## 2. Text Processing & Data Extraction
* Connecting commands using Pipes (`|`).
* Utilizing CLI text filters: `grep` (pattern matching), `awk` (column scanning), and `sed` (stream editor/substitution).

## 3. Production Automation: System Monitoring
* Writing a dynamic System Resource Monitor script (CPU, Memory, Disk).
* Automating script schedules using Cron daemon (`crontab`).

## 4. Shell Scripts in CI/CD Pipelines
* CI/CD core automation architectures.
* Writing a GitHub Actions workflow that executes local shell scripts.

---

# I/O Streams and Redirection

Every process in Linux opens three standard data streams:

```text
                        +----------------------+
                        |   Linux Command      |
                        +----------------------+
                        /          |           \
           0: stdin    /           | 1: stdout  \  2: stderr
                      v            v             v
                [ Keyboard ]  [ Terminal ]  [ Error Log / ]
               (or input file)  (or file)   (Terminal Screen)
```

### Stream Table & Code Examples
* **`0` (stdin)**: Standard input.
* **`1` (stdout)**: Standard output.
* **`2` (stderr)**: Standard error.

```bash
# Redirect stdout to overwrite a file
echo "Deploying v1.0.0" > deploy.log

# Append stdout to a file
echo "Deploy complete!" >> deploy.log

# Redirect stderr to a file (ignoring stdout)
ls /root 2> error.log

# Redirect both stdout and stderr to the same file
./backup.sh > backup.log 2>&1

# Discard all output (sent to black hole /dev/null)
ping -c 3 8.8.8.8 > /dev/null 2>&1
```

---

# Text Processing Toolkit

Power-user automation relies on combining small tools using pipes (`|`) to filter and process texts.

### 1. `grep` (Search text using patterns)
```bash
# Search for errors in a log file (case insensitive)
grep -i "error" syslog.log

# Count the number of matches
grep -c "CRITICAL" syslog.log
```

### 2. `awk` (Process columns and fields)
```bash
# Print the 2nd and 4th fields of a file (space delimited)
cat users.txt | awk '{print $2, $4}'

# Print the username of users with Bash shell from /etc/passwd (colon delimited)
awk -F: '$7 == "/bin/bash" {print $1}' /etc/passwd
```

### 3. `sed` (Find and replace stream text)
```bash
# Substitute 'localhost' with server IP in a config file
sed -i 's/localhost/192.168.1.50/g' config.env
```

---

# System Health Monitoring Script

Here is a practical, production-ready script that monitors system disk usage and sends an alert if it exceeds a defined threshold.

### `monitor.sh`
```bash
#!/bin/bash

# Configuration
THRESHOLD=80
ADMIN_EMAIL="admin@example.com"
DISK_USAGE=$(df -h / | grep -v Filesystem | awk '{print $5}' | cut -d'%' -f1)

# Check Disk Usage
if [ "$DISK_USAGE" -gt "$THRESHOLD" ]; then
    echo "WARNING: Disk space on root partition is at ${DISK_USAGE}%!" | mail -s "Disk Space Alert!" $ADMIN_EMAIL
    echo "[$(date)] Disk space critical: ${DISK_USAGE}%" >> /var/log/sys_monitor.log
else
    echo "[$(date)] Disk space normal: ${DISK_USAGE}%" >> /var/log/sys_monitor.log
fi
```

### Automating with Cron Jobs
To schedule this script to run every hour:
```bash
# Open the crontab editor
crontab -e

# Add the following line to execute the script every hour on the hour
0 * * * * /usr/local/bin/monitor.sh
```

---

# Shell Scripts in CI/CD

In modern DevOps, pipelines orchestrate deployments. These pipelines often run shell scripts on target agents/runners.

### GitHub Actions Integration Example
Below is a GitHub Actions workflow (`.github/workflows/deploy.yml`) that triggers on a push to the `main` branch, spins up a Linux runner, runs security checks, and calls a deployment shell script:

```yaml
name: Deploy Web Application

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      # Step 1: Checkout the source code from repository
      - name: Checkout Source Code
        uses: actions/checkout@v3

      # Step 2: Make the script executable
      - name: Grant Execute Permissions to Script
        run: chmod +x scripts/deploy.sh

      # Step 3: Run the shell script using secrets/environment variables
      - name: Execute Deployment Script
        env:
          DB_PASSWORD: ${{ secrets.PROD_DB_PASSWORD }}
          DEPLOY_ENV: "production"
        run: ./scripts/deploy.sh
```

---

# Learning Outcome

After completing Day 4–5, I can:

- ✅ Manage Linux standard streams using redirects (`>`, `>>`, `2>`, `2>&1`) and output discarding (`/dev/null`).
- ✅ Combine command outputs via Pipes (`|`) to construct powerful command chains.
- ✅ Parse, filter, and modify text streams on the fly using `grep`, `awk`, and `sed`.
- ✅ Build automation scripts to monitor disk usage and output automated system diagnostics.
- ✅ Configure automated task schedules using Cron schedules (`crontab`).
- ✅ Design a simple GitHub Actions workflow to run custom Shell Scripts automatically during code deployments.

---

# Next Topics Goals

- **AWS Cloud Administration (Week 7)**

---

# Motivation Corner

> **"A command-line wizard is someone who knows how to pipe multiple simple tools together to solve a complex system issue in a single line."**

> **"CI/CD pipelines are just shell scripts wrapped in pretty YAML configurations."**

---

# Challenge Motto

```
Write the Script
       ↓
Filter with Pipes & Grep
       ↓
Trigger with CI/CD YAML
       ↓
Continuous Automated Delivery
```
 Fast pipelines. Zero-downtime deployments. Reliable systems.
