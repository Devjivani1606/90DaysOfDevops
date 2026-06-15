# 🚀 DevOps Challenge - Week 1
## Linux Fundamentals

This repository contains my Week 1 learning journey in the DevOps Challenge.

Duration: 3 Days

---

# Topics Covered

## 1. Introduction to Linux

Linux is an open-source operating system that manages hardware resources and provides services for applications.

### Key Points

- Open Source
- Secure and Stable
- Multi-user Operating System
- Widely used in Servers and Cloud Platforms

---

## 2. Linux Architecture

```
Applications
     ↓
    Shell
     ↓
   Kernel
     ↓
 Hardware
```

### Components

### Kernel

The core of Linux responsible for:

- Process Management
- Memory Management
- Device Management
- File System Management

### Shell

Acts as an interface between the user and the kernel.

Examples:

- Bash
- Zsh
- Sh

### Bootloader

Loads the Linux Kernel during system startup.

Example:

GRUB (Grand Unified Bootloader)

---

## 3. Connecting to Linux Servers

### SSH

Used to securely access remote Linux servers.

```bash
ssh username@server-ip
```

### RDP

Used mainly for graphical remote access.

---

## 4. Process Management

A process is a running instance of a program.

### Process Lifecycle

```
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

# File and Directory Commands

## Create Directory

```bash
mkdir project
```

## Create File

```bash
touch file.txt
```

## Print Current Directory

```bash
pwd
```

## List Files

```bash
ls
ls -l
```

## Remove File

```bash
rm file.txt
```

## Remove Directory

```bash
rm -r foldername
```

---

# Viewing File Content

## cat

Display complete file content.

```bash
cat file.txt
```

## less

View file page by page.

```bash
less file.txt
```

## more

View file content page by page.

```bash
more file.txt
```

## tail

Display last lines of a file.

```bash
tail file.txt
```

### Real-Time Monitoring

```bash
tail -f logs.txt
```

---

# Writing into Files

## echo

Print text on screen

```bash
echo "Hello Linux"
```

### Save Output into File

```bash
echo "Hello Linux" > hello.txt
```

### Append Content

```bash
echo "New Line" >> hello.txt
```

---

# File Operations

## Copy Files

```bash
cp source.txt destination.txt
```

## Move Files

```bash
mv file.txt backup/
```

## Rename Files

```bash
mv old.txt new.txt
```

---

# File Statistics

## Word Count Command

```bash
wc file.txt
```

Output shows:

- Lines
- Words
- Characters

Examples:

```bash
wc -l file.txt
wc -w file.txt
wc -c file.txt
```

---

# Soft Link vs Hard Link

## Soft Link

Create symbolic link.

```bash
ln -s original.txt softlink.txt
```

Characteristics:

- Points to original file path
- Breaks if original file is deleted
- Can link directories

---

## Hard Link

```bash
ln original.txt hardlink.txt
```

Characteristics:

- Shares same inode
- Works even if original file name is deleted
- Cannot link directories

---

# Hands-On Tasks Performed

- Created files and folders
- Navigated Linux file system
- Used cat, less, more and tail
- Worked with file permissions
- Created soft links
- Created hard links
- Practiced file copy and move operations
- Explored process lifecycle

---

# Learning Outcome

After completing this week I can:

✅ Navigate Linux systems

✅ Manage files and directories

✅ Understand Linux architecture

✅ Understand process lifecycle

✅ Use basic Linux commands confidently

✅ Work with soft links and hard links

✅ Monitor files using tail

---

# 📅 Next Week Goals

- Linux Advace comand

---
