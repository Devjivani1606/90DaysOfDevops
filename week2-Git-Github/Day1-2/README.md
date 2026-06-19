# Git & GitHub Fundamentals

## Overview

Git is a distributed version control system used to track changes in source code and collaborate with other developers.

GitHub is a cloud platform that hosts Git repositories and enables collaboration, code review, project management, and CI/CD integration.

---

# Why Git?

Before Git, developers faced problems such as:

* Overwriting each other's code
* Losing previous versions
* Difficulty tracking changes
* No collaboration workflow

Git solves these problems by maintaining a complete history of changes.

---

# Git vs GitHub

| Git                    | GitHub                        |
| ---------------------- | ----------------------------- |
| Version Control System | Cloud Hosting Platform        |
| Installed locally      | Runs on the internet          |
| Tracks code changes    | Stores Git repositories       |
| Works offline          | Requires internet for syncing |

---

# How Git Works

Git tracks changes using snapshots rather than storing complete copies every time.

## Git Architecture

```text
Working Directory
        │
        ▼
    Staging Area
        │
        ▼
      Local Repo
        │
        ▼
    Remote Repo
      (GitHub)
```

### Working Directory

Where files are created and modified.

### Staging Area

Temporary area where selected changes are prepared for commit.

### Local Repository

Stores commit history on your local machine.

### Remote Repository

Repository hosted on GitHub.

---

# Git Workflow

```text
Create File
    │
git add
    │
git commit
    │
git push
    │
GitHub Repository
```

Example:

```bash
git add .
git commit -m "Added login feature"
git push origin main
```

---

# Installing Git

Check Version:

```bash
git --version
```

Ubuntu:

```bash
sudo apt update
sudo apt install git
```

---

# Initial Git Configuration

Set Username:

```bash
git config --global user.name "Your Name"
```

Set Email:

```bash
git config --global user.email "you@example.com"
```

View Configuration:

```bash
git config --list
```

---

# Creating a Repository

Initialize Git:

```bash
git init
```

This creates a hidden `.git` directory that stores Git metadata.

---

# Basic Git Commands

## Check Status

```bash
git status
```

Shows:

* Modified files
* New files
* Staged files

---

## Add Files

Add Single File:

```bash
git add file.txt
```

Add All Files:

```bash
git add .
```

---

## Commit Changes

```bash
git commit -m "Initial Commit"
```

A commit is a snapshot of your project.

---

## View Commit History

```bash
git log
```

Compact Format:

```bash
git log --oneline
```

---

## View Differences

```bash
git diff
```

Compare staged changes:

```bash
git diff --staged
```

# Learning Outcome

After completing this module, I can:

✅ Understand Version Control

✅ Understand Git Architecture

✅ Create and Manage Repositories

✅ Track Changes

✅ Create Commits

✅ Work with Branches

✅ Push and Pull Code

✅ Clone Repositories

✅ Follow a Basic Git Workflow
