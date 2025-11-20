---
title: Python Virtual Environments
theme: simple
highlightTheme: monokai
revealOptions:
  transition: 'slide'
  controls: true
  progress: true
---


# Python Virtual Environments

Quick intro to `venv`

---

## The Problem

**Dependency Hell:**
- Project A needs pandas 1.5
- Project B needs pandas 2.0
- Both break

---

**Polluting Global Python:**
- Installing packages globally = messy system
- Hard to track what's needed per project
- Conflicts everywhere

---

## The Solution: virtual envs

Isolated Python environments per project

Each project = its own packages 

---

## Basic Commands

```bash
# Create venv
python3 -m venv venv

# Activate
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Install packages
pip install pandas numpy

# Save dependencies
pip freeze > requirements.txt

# Install from requirements
pip install -r requirements.txt

# Deactivate
deactivate
```

---

## Installing packages


```bash
pip install pandas
```

No sudo/admin access needed 

---

## That's It!

📚 Full guide: [knuxv.github.io/advanced_programming_python/lessons/02-python-env](https://knuxv.github.io/advanced_programming_python/lessons/02-python-env)
