# 🐧 How Linux Actually Works

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
