# How Linux Actually Works

Most beginners use Linux commands without understanding what happens behind the scenes.

As a DevOps Engineer, understanding the internal workflow of Linux helps in troubleshooting, performance tuning, and system administration.

---

# What Happens When a Computer Starts?

When you press the power button, several components work together before you see the login screen.

```text
Power ON
    │
    ▼
BIOS / UEFI
    │
    ▼
Bootloader (GRUB)
    │
    ▼
Linux Kernel
    │
    ▼
systemd (PID 1)
    │
    ▼
Services Start
    │
    ▼
Login Screen / Terminal
```

---

## Step 1: Power On

The CPU starts executing firmware instructions stored in the motherboard.

Modern systems use:

* BIOS (older systems)
* UEFI (modern systems)

Responsibilities:

* Hardware Initialization
* Memory Check
* CPU Detection
* Storage Detection

---

## Step 2: Bootloader (GRUB)

The bootloader loads the Linux Kernel into memory.

Example:

```text
GRUB
 ├── Ubuntu
 ├── Fedora
 └── Recovery Mode
```

Responsibilities:

* Locate Kernel
* Load Kernel into RAM
* Pass Boot Parameters

---

## Step 3: Linux Kernel Starts

The Kernel is the heart of Linux.

Responsibilities:

* Process Management
* Memory Management
* Device Management
* File System Management
* Network Management

Without the kernel, Linux cannot function.

---

## Step 4: Init System Starts

Modern Linux uses:

```text
systemd
```

Check PID 1:

```bash
ps -p 1
```

Output:

```text
PID TTY      TIME CMD
1   ?        00:00 systemd
```

systemd becomes the first user-space process.

---

## Step 5: Services Start

systemd starts required services:

Examples:

* SSH
* NetworkManager
* Docker
* Cron
* Nginx

View Running Services:

```bash
systemctl list-units --type=service
```

---

## Step 6: Login Screen Appears

Linux finally presents:

* GUI Login Screen
* Terminal Login

User enters credentials and starts a shell session.

---

# Linux Architecture

```text
+----------------------+
|     Applications     |
+----------------------+
           │
+----------------------+
|        Shell         |
+----------------------+
           │
+----------------------+
|       Kernel         |
+----------------------+
           │
+----------------------+
|      Hardware        |
+----------------------+
```

---

## Hardware Layer

Physical components:

* CPU
* RAM
* SSD/HDD
* Network Card

---

## Kernel Layer

Acts as a bridge between software and hardware.

Example:

When you run:

```bash
cat file.txt
```

The shell asks the kernel.

The kernel accesses the disk.

The file content is returned to the shell.

---

## Shell Layer

The shell is a command interpreter.

Examples:

```text
Bash
Zsh
Sh
Fish
```

Check Current Shell:

```bash
echo $SHELL
```

---

## Application Layer

Examples:

```text
Chrome
Docker
Nginx
VS Code
Python
Node.js
```

Applications cannot directly access hardware.

Everything must go through the kernel.

---

# How a Linux Command Works

Example:

```bash
ls
```

Internal Flow:

```text
User
 │
 ▼
Shell
 │
 ▼
Kernel
 │
 ▼
File System
 │
 ▼
Directory Data
 │
 ▼
Terminal Output
```

---

# What is a Process?

A process is a running instance of a program.

Examples:

```bash
nginx
docker
python app.py
```

Check Processes:

```bash
ps -ef
```

---

# What is PID?

PID = Process ID

Every running process gets a unique number.

Example:

```bash
ps -ef
```

Output:

```text
root     1010  1  0 nginx
ubuntu   2020  1  0 python
```

Here:

```text
1010 -> PID
2020 -> PID
```

---

# What is systemd?

systemd is the service manager in modern Linux.

Check Status:

```bash
systemctl status
```

Examples:

```bash
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
```

---

# Environment Variables

Environment variables store information that programs can access.

View Variables:

```bash
env
```

Example:

```bash
echo $HOME
echo $PATH
echo $USER
```

---

# Why PATH is Important

Example:

```bash
python
```

Linux searches directories listed in:

```bash
echo $PATH
```

Without PATH, Linux wouldn't know where commands are located.

---

# Alias Command

Aliases create command shortcuts.

Create Alias:

```bash
alias ll='ls -al'
```

Now:

```bash
ll
```

works as:

```bash
ls -al
```

---

## View Aliases

```bash
alias
```

---

## Remove Alias

```bash
unalias ll
```

---

## Permanent Alias

Edit:

```bash
nano ~/.bashrc
```

Add:

```bash
alias k='kubectl'
alias gs='git status'
alias gp='git push'
```

Reload:

```bash
source ~/.bashrc
```

---


# Linux vs Windows - Architecture Comparison

Most beginners use Linux and Windows commands without understanding their architectural differences.

For a DevOps Engineer, knowing these differences helps in:

* Troubleshooting
* Performance Tuning
* Writing Automation Scripts
* Understanding System Behavior

---

# Windows Architecture Overview

Windows uses a layered architecture with a monolithic kernel.

```text
+------------------------------+
|       Applications           |
+------------------------------+
               │
+------------------------------+
|     Windows Subsystem        |
|      (WSL / .NET)           |
+------------------------------+
               │
+------------------------------+
|      Services Manager        |
+------------------------------+
               │
+------------------------------+
|        Windows Kernel        |
|  (Monolithic Architecture)   |
+------------------------------+
               │
+------------------------------+
|           Hardware           |
+------------------------------+
```

---

## 1. Windows Kernel

Windows uses a monolithic kernel.

Components:

```text
NT Kernel
 ├── Hardware Abstraction Layer (HAL)
 ├── Executive Services
 ├── Kernel
 ├── Object Manager
 ├── Process Manager
 ├── Virtual Memory Manager
 ├── Security Reference Monitor
 └── I/O Manager
```

---

## 2. Services Manager

Equivalent to systemd in Linux.

Starts and manages services:

* Network Services
* Security Services
* System Services

Command:

```powershell
Get-Service
```

---

## 3. Windows Subsystem (WSL)

**WSL 2** runs a real Linux kernel inside a lightweight virtual machine.

Allows running:

* Linux GUI apps
* Docker
* Linux tools

This makes the difference between Windows and Linux less visible in daily usage.

---

# Linux Architecture Overview

Linux uses a layered architecture with a modular kernel.

```text
+------------------------------+
|     Applications           |
+------------------------------+
               │
+------------------------------+
|          Shell             |
|  (Bash, Zsh, Fish)          |
+------------------------------+
               │
+------------------------------+
|         Linux Kernel         |
|  (Modular Architecture)     |
+------------------------------+
               │
+------------------------------+
|        Hardware            |
+------------------------------+
```

---

## 1. Linux Kernel

The Linux kernel is modular.

Components:

```text
Linux Kernel
 ├── Process Management
 ├── Memory Management
 ├── File System Management
 ├── Device Drivers
 ├── Network Stack
 ├── IPC (Inter-Process Communication)
 └── Security Subsystem
```

---

## 2. Shell

The shell is the command interpreter.

Common shells:

* Bash
* Zsh
* Fish
* Sh

Check current shell:

```bash
echo $SHELL
```

---

## 3. Services Management

Uses:

```text
systemd
```

Check status:

```bash
systemctl status
```

Services:

* SSH
* Docker
* Nginx
* Cron

---

# Key Architectural Differences

| Feature | Linux | Windows |
|---------|-------|---------|
| Kernel Type | Monolithic (Modular) | Monolithic |
| Primary Shell | Bash, Zsh | PowerShell, CMD |
| Services Manager | systemd | Services Manager |
| File System | ext4, XFS, Btrfs | NTFS |
| Case Sensitivity | Yes | No |
| User/Group Management | Robust | Basic |
| Process Model | Fork, Exec | CreateProcess |
| Package Management | apt, yum, pacman | MSI, EXE, Winget |
| Scripting | Shell Scripts | Batch, PowerShell |

---

# 🔍 Detailed Comparison

## 1. Kernel Architecture

**Linux** is **modular**.

* Load modules dynamically
* Remove modules easily
* Smaller memory footprint

**Windows** is **monolithic**.

* Kernel code is loaded entirely
* Harder to modify
* Larger memory footprint

---

## 2. Process Creation

In **Linux**:

```text
fork() -> Creates child process
exec() -> Replaces with new program
```

Faster and more memory efficient.

In **Windows**:

```text
CreateProcess()
```

Loads the entire executable.

---

## 3. File System

**Linux** supports multiple file systems:

* ext4 (standard)
* XFS
* Btrfs
* NTFS (can read/write)

**Windows** primarily uses:

* NTFS
* FAT32
* exFAT

---

## 4. Case Sensitivity

**Linux** is **case-sensitive**:

```bash
File.txt ≠ file.txt
```

**Windows** is **case-insensitive**:

```text
File.txt == file.txt
```

This causes many issues when moving applications between systems.

---

## 5. User and Group Management

**Linux**:

* Powerful user/group system
* Granular permissions
* Easy to manage

```bash
useradd devops
groupadd developers
gpasswd -a devops developers
```

**Windows**:

* Limited user/group management
* Relies on ACLs
* Harder to script

---

## 6. Package Management

**Linux** has native package managers:

* apt (Debian/Ubuntu)
* yum, dnf (RedHat/CentOS)
* pacman (Arch)

**Windows**:

* MSI installers
* EXE installers
* Winget (modern)
* Chocolatey (third-party)

For automation, Linux package managers are far superior.

---

# DevOps Perspective

## 1. Shell Scripting

**Linux** uses **Bash** for automation:

```bash
#!/bin/bash
echo "Starting deployment..."

# Check disk space
if [ $(df / | tail -1 | awk '{print $5}' | sed 's/%//') -gt 90 ]; then
  echo "Disk space low"
fi
```

**Windows** uses:

```powershell
# PowerShell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

PowerShell is powerful but less universal than Bash.

---

## 2. Docker on Both Systems

**Linux**:

```bash
docker run -d nginx
```

Native and efficient.

**Windows**:

* WSL 2 backend (better)
* Hyper-V backend (older)

Requires extra layers, consuming more resources.

---

## 3. File Paths

**Linux**:

```text
/var/log/nginx/access.log
```

Forward slashes.

**Windows**:

```text
C:\Program Files\nginx\access.log
```

Backslashes (need escaping).

Cross-platform scripts must handle both:

```python
import os
path = os.path.join("var", "log", "nginx")
```

---

## 4. Permissions

**Linux**:

```text
-rwxr-xr-x
```

Owner/Group/Others.

**Windows** uses:

```text
Access Control Lists (ACLs)
```

More complex.

For DevOps:

```bash
chmod 644 config.txt



# Learning Outcome

After completing this module, I can:

✅ Understand Linux Boot Process

✅ Understand BIOS, UEFI and GRUB

✅ Understand Linux Kernel Responsibilities

✅ Understand systemd and Services

✅ Understand Shell and Command Execution

✅ Understand Processes and PIDs

✅ Understand Environment Variables

✅ Use PATH Effectively

✅ Create and Manage Aliases

✅ Understand What Happens Behind the Scenes in Linux
