---
words:
  2025-11-06: 823
title: Part 1 - Introduction & Setup
theme: simple
highlightTheme: github
---
# Version Control with Git

## From Chaos to Control

*A 3-hour journey into the world's most popular version control system*

---

## The Problem: Before Git


**Sound familiar?**
- `project_final.html`
- `project_final_v2.html`
- `project_ACTUAL_final.html`
- `project_final_working_copy.html`

---

## Real Developer problems

 *"I made changes yesterday and everything worked... Now it's broken and I don't remember what I changed!"*

 *"My colleague edited the same file I was working on. Now whose changes do we keep?"*

*"I want to try something experimental but I'm afraid to break my working code..."*

---

## What is Version Control?

**Version Control = Time Machine for Code**

A system that:
- Takes snapshots of your work over time
- Tracks WHO changed WHAT and WHEN
- Lets you rewind to any previous state
- Coordinates work between multiple people
- Allows parallel experimentation

---

## Why Git Specifically?

### Git is EVERYWHERE

- **90%+ of software projects** use Git
- **100 million+** developers worldwide
- Created by **Linus Torvalds** (Linux creator) in 2005
- Powers: Linux, Android, Microsoft, Google, Facebook, NASA...

---

## Git: The Industry Standard

```
Companies using Git:
✓ Google      ✓ Microsoft    ✓ Amazon
✓ Meta        ✓ Netflix      ✓ Apple
✓ Spotify     ✓ Tesla        ✓ NASA
✓ Your future employer (probably)
```

**Not knowing Git in 2025 is like not knowing email in 2000**

---

## Git vs GitHub vs GitLab

####  What's the difference ?

**Git** = The tool (version control system)
- Lives on YOUR computer
- Command-line program or GUI
- Works offline

**GitHub/GitLab** = The cloud storage + collaboration
- Websites that host Git repositories
- Add features: issues, pull requests, CI/CD
- Make collaboration easier

---

## Analogy Time

**Git** ~ Microsoft Word
- The program that does the work
- Runs on your computer
- Saves your documents

**GitHub/GitLab** ~ Google Drive / Dropbox
- Cloud storage for your documents
- Share with others
- Collaborate online


---

## GitHub vs GitLab

Both are Git hosting platforms, but:

| Feature    | GitHub          | GitLab             |
| ---------- | --------------- | ------------------ |
| Owner      | Microsoft       | Independent        |
| Popularity | #1 (100M users) | #2 (30M users)     |
| CI/CD      | Actions         | Built-in pipelines |
<split even>

The university of Strasbourg self hosts its own Gitlab via gitlab.unistra.fr

As a student you have an account by default, use your regular username/password to connect
</split>
---

## What Git Tracks

**Files Git loves:**

- Source code (`.py`, `.js`, `.html`, `.css`)
- Configuration (`.json`, `.yml`, `.toml`)
- Documentation (`.md`, `.txt`)
- Small data files

**Files Git hates:**

- Large binaries (videos, giant datasets)
- Generated files (compiled code, `node_modules/`)
- Secrets (passwords, API keys)

---

## Git's Superpowers

### 1. Time Travel 
Go back to any previous version

### 2. Parallel Universes 
Work on features in isolation (branches)

### 3. Collaboration 
Merge work from multiple people

### 4. Audit Trail 
See exactly who changed what and why

---

## Setup Time! 

**Let's get Git on your machine**

Check if you already have it:
```bash
git --version
```

See a version number? **You're good!**  
Don't see it? **Let's install...**

---

## Installation

**macOS:**
```bash
# Option 1: Xcode Command Line Tools
xcode-select --install

# Option 2: Homebrew
brew install git
```

**Linux (Debian/Ubuntu):**
```bash
sudo apt update
sudo apt install git
```

Already Installed on the machine in the lab

---

## Installation (continued)

**Windows:**

1. Download from: [git-scm.com](https://git-scm.com)
2. Run installer (accept defaults)
3. Use **Git Bash** terminal

**Verify installation:**
```bash
git --version
# Should show: git version 2.40+ or similar
```

---

## Configure Git: Your Identity

Git needs to know who you are!

**Set your name:**
```bash
git config --global user.name "Your Name"
```

**Set your email:**
```bash
git config --global user.email "your.email@example.com"
```

**Use your real email** - this will appear in commit history

---

## Why Configure?

Every change (commit) you make includes:
- **WHO** made the change (your name)
- **WHEN** it was made (timestamp)
- **WHAT** changed (the code)
- **WHY** it changed (your message)

**Your name/email = Your signature on every change**

---

## Verify Your Configuration

```bash
# Check all settings
git config --list

# Check specific settings
git config user.name
git config user.email
```


---

## Optional: Make Git Pretty 

```bash
# Colorful output
git config --global color.ui auto

# Better default branch name
git config --global init.defaultBranch main

# Credential caching (avoid retyping passwords)
git config --global credential.helper cache
```

---

## Quick Vocabulary

Before we dive in, know these terms:

- **Repository (repo)**: A project tracked by Git
- **Commit**: A saved snapshot of your work
- **Clone**: Download a repo from the internet
- **Push**: Upload your changes to the cloud
- **Pull**: Download changes from the cloud
- **Branch**: Parallel version of your code

*Don't worry, we'll practice each one!*

---

## The Git Workflow (Preview)

```
1. Make changes to files
   ↓
2. Stage changes (git add)
   ↓
3. Commit changes (git commit)
   ↓
4. Push to GitHub/GitLab (git push)
```

**We'll practice this A LOT today**
