# Advanced Topics

After understanding basic Git operations, the next step is learning automation and collaboration features used in real-world projects.

---

# Branching and Merging

Branches allow developers to work on features independently without affecting the main codebase.

## Why Branches?

* Feature Development
* Bug Fixes
* Experimentation
* Team Collaboration

View Branches:

```bash
git branch
```

Create Branch:

```bash
git branch feature-login
```

Switch Branch:

```bash
git checkout feature-login
```

Create and Switch:

```bash
git checkout -b feature-login
```

View All Branches:

```bash
git branch -a
```

---

## Merge Branch

Switch to Main:

```bash
git checkout main
```

Merge Feature Branch:

```bash
git merge feature-login
```

Delete Branch:

```bash
git branch -d feature-login
```

---

## Merge Conflicts

A merge conflict occurs when two branches modify the same line of code.

Typical Workflow:

```bash
git pull
git merge feature-login
```

Resolve conflict manually and then:

```bash
git add .
git commit
```

---

# Git Hooks

Git Hooks are scripts that automatically run before or after specific Git events.

Location:

```text
.git/hooks/
```

Examples:

* pre-commit
* commit-msg
* post-commit
* pre-push
* post-merge

---

## Why Git Hooks?

* Code Quality Checks
* Security Validation
* Linting
* Testing Before Commit
* Commit Message Validation

---

## Example: Pre-Commit Hook

Create Hook:

```bash
touch .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit
```

Example Script:

```bash
#!/bin/bash

echo "Running tests..."
npm test

if [ $? -ne 0 ]; then
    echo "Tests failed"
    exit 1
fi
```

Now commits will fail if tests fail.

---

# GitHub Actions

GitHub Actions is GitHub's built-in CI/CD platform.

It automates:

* Testing
* Building
* Deployment
* Security Scanning
* Notifications

---

## How GitHub Actions Works

```text
Developer Pushes Code
          │
          ▼
GitHub Repository
          │
          ▼
GitHub Action Workflow Triggered
          │
          ▼
Run Tests
          │
          ▼
Build Application
          │
          ▼
Deploy Application
```

---

## Workflow Location

```text
.github/
└── workflows/
    └── ci.yml
```

---

## Simple GitHub Action

Create:

```text
.github/workflows/ci.yml
```

Example:

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Display Message
        run: echo "GitHub Actions Working"
```

---

## Common Triggers

Push Event:

```yaml
on:
  push:
```

Pull Request Event:

```yaml
on:
  pull_request:
```

Manual Trigger:

```yaml
on:
  workflow_dispatch:
```

---

## Common Use Cases

### Run Tests

```yaml
run: npm test
```

### Build Application

```yaml
run: npm run build
```

### Deploy Application

```yaml
run: ./deploy.sh
```

---

# CI/CD Pipeline Example

```text
Developer
    │
git push
    │
    ▼
GitHub
    │
    ▼
GitHub Actions
    │
    ▼
Unit Tests
    │
    ▼
Build
    │
    ▼
Docker Image
    │
    ▼
Deployment
```

---

# GitHub Features Useful for DevOps

## Pull Requests

Code review before merging.

## Issues

Track bugs and tasks.

## Projects

Kanban-style project management.

## Releases

Version management.

## Secrets

Store credentials securely.

Examples:

* AWS Access Keys
* Docker Hub Tokens
* API Keys

---

# GitHub Secrets

Repository Settings:

```text
Settings
 └── Secrets and Variables
      └── Actions
```

Used in workflows:

```yaml
${{ secrets.AWS_ACCESS_KEY_ID }}
```

---

# Learning Outcome

After completing this module, I can:

✅ Track Code Changes Using Git

✅ Work with Local and Remote Repositories

✅ Collaborate Using GitHub

✅ Create and Manage Branches

✅ Resolve Merge Conflicts

✅ Understand Git Hooks

✅ Automate Tasks Using Git Hooks

✅ Build CI/CD Pipelines Using GitHub Actions

✅ Use GitHub Secrets Securely

✅ Understand Modern DevOps Git Workflow
