---

#  How SSH Works

SSH (Secure Shell) is a secure protocol used to connect and manage remote Linux servers over a network.

## Why SSH is Used

- Remote Server Management
- Cloud Instance Access (AWS EC2, Azure VM, GCP VM)
- Secure Communication
- Application Deployment
- Automation Scripts

---

## SSH Working Flow

```text
Your Laptop
     │
     │ SSH Request (Port 22)
     ▼
Remote Linux Server
     │
Authentication
(Password / SSH Key)
     │
     ▼
Encrypted Secure Session
     │
     ▼
Execute Commands Remotely
```

### Step-by-Step Working

1. User sends SSH connection request.
2. Server responds with its public key.
3. Client verifies the server identity.
4. Authentication occurs using:
   - Password
   - SSH Key Pair
5. Secure encrypted tunnel is established.
6. User can execute commands on the remote server.

---

## Basic SSH Command

```bash
ssh username@server-ip
```

Example:

```bash
ssh ubuntu@192.168.1.10
```

---

## Generate SSH Key Pair

```bash
ssh-keygen -t ed25519
```

Files Generated:

```text
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

- Private Key → Keep Secret
- Public Key → Share with Server

---

## Copy Public Key to Server

```bash
ssh-copy-id ubuntu@server-ip
```

---

## Login Using SSH Key

```bash
ssh ubuntu@server-ip
```

---

# ⚙️ Process Management

A process is a running instance of a program.

Examples:

```bash
chrome
nginx
python app.py
node server.js
```

Each running program creates a process.

---

## Process Lifecycle

```text
New
 ↓
Ready
 ↓
Running
 ↓
Waiting
 ↓
Ready
 ↓
Running
 ↓
Terminated
 ↓
Zombie
```

---

## Common Process States

| State | Description |
|---------|------------|
| R | Running |
| S | Sleeping |
| D | Waiting for I/O |
| T | Stopped |
| Z | Zombie |

---

# Process Commands

## View Current Processes

```bash
ps
```

---

## Detailed Process List

```bash
ps -ef
```

or

```bash
ps aux
```

---

## Monitor Running Processes

```bash
top
```

Displays:

- CPU Usage
- Memory Usage
- Running Processes
- Load Average

---

## Advanced Process Monitor

```bash
htop
```

Installation:

```bash
sudo apt install htop
```

---

## Find Specific Process

```bash
ps -ef | grep nginx
```

Example:

```bash
ps -ef | grep python
```

---

## Get Process ID (PID)

```bash
pidof nginx
```

Example:

```bash
pidof sshd
```

---

## Kill a Process

```bash
kill PID
```

Example:

```bash
kill 1234
```

---

## Force Kill Process

```bash
kill -9 PID
```

Example:

```bash
kill -9 1234
```

---

## Kill Process Using Name

```bash
pkill nginx
```

Example:

```bash
pkill node
```

---

## Run Process in Background

```bash
python app.py &
```

---

## Show Background Jobs

```bash
jobs
```

---

## Bring Background Job to Foreground

```bash
fg
```

---

## View Process Tree

```bash
pstree
```

---

## Check CPU Information

```bash
lscpu
```

---

## Check Memory Usage

```bash
free -h
```

---

# 🧪 Hands-On Practice

## Practice 1

Create a process:

```bash
sleep 300
```

Find the process:

```bash
ps -ef | grep sleep
```

Kill the process:

```bash
kill PID
```

---

## Practice 2

Monitor system resources:

```bash
top
```

Observe:

- CPU Usage
- Memory Usage
- Running Processes

---

## Practice 3

Run process in background:

```bash
sleep 500 &
```

Check jobs:

```bash
jobs
```

Bring it back:

```bash
fg
```

---

# Learning Outcome

After completing this section, I can:

✅ Understand SSH Working

✅ Connect to Remote Linux Servers

✅ Generate and Use SSH Keys

✅ Understand Process Lifecycle

✅ Monitor Running Processes

✅ Kill and Manage Processes

✅ Work with Background Jobs

✅ Troubleshoot Linux Processes