---
title: Software Licenses & Open Source
theme: simple
highlightTheme: github
revealOptions:
  transition: 'none'
  controls: false
  progress: true
  center: true
---

<style>
.reveal {
  font-size: 32px;
}
.reveal h1 {
  font-size: 2.2em;
  margin-bottom: 0.5em;
}
.reveal h2 {
  font-size: 1.6em;
  margin-bottom: 0.8em;
}
.reveal p {
  margin: 0.4em 0;
}
.reveal ul {
  margin: 0.5em 0;
}
.reveal li {
  margin: 0.3em 0;
}
.reveal pre {
  font-size: 0.75em;
  margin: 0.8em 0;
  box-shadow: none;
}
.reveal code {
  padding: 0.1em 0.3em;
}
.reveal .slides {
  padding-top: 0;
}
.reveal h2 {
  margin-top: 0;
}
</style>

## Software Licenses & Open Source

Understanding code ownership and freedom

---

## What You'll Learn Today

**By end of class, you will:**

1. Understand why licenses matter (legally & philosophically)
2. Choose appropriate license for your projects
3. Recognize GPL vs permissive vs proprietary differences
4. Understand who controls "open source" in 2025
5. Make informed decisions about code sharing

**And:** Every project you publish will have a LICENSE file!

---

## Why Licenses Matter

**No license = All rights reserved**

```
your-repo/
  README.md
  awesome_code.py
  # No LICENSE file...
```

**Legal reality:**
- Nobody can legally use your code
- Nobody can modify it
- Nobody can redistribute it
- Even on public GitHub!

---

## The Default State

**Without explicit license:**
```python
def amazing_function():
    """This looks public but legally isn't."""
    return "All rights reserved by default"
```

Copyright law grants you exclusive rights automatically.

**To share code, you must explicitly grant permissions.**

---

## Common Myths


**Myth 1:** "Open source = no money"
**Reality:** Red Hat made $3.4B/year, IBM paid $34B for it

**Myth 2:** "Corporations don't contribute to OSS"
**Reality:** 90%+ of Linux kernel is corporate contributions

**Myth 3:** "Open source AI exists"
**Reality:** Debatable - most "open" AI lacks training data

---

## The License Spectrum

```
Most Restrictions ←──────────────────→ No Restrictions

Proprietary   GPL/AGPL   MIT/Apache   Unlicense
(many rules)  (copyleft) (one rule:    (zero rules)
                         attribution)
```

**Different philosophies, different freedoms**

---

## Permissive Licenses: MIT

**Most popular on GitHub (44.7% in 2025)**

```
Copyright (c) 2025 Your Name

Permission is hereby granted, free of charge...
```

**In plain English:**
- Do whatever you want
- Just keep the copyright notice
- Can be used in proprietary software
- No obligation to share your changes

---

## MIT in Practice (1980)

**What you CAN do:**
- Use in commercial products
- Modify as you wish
- Keep modifications private
- Sell software using MIT code

**What you MUST do:**
- Include original copyright notice
- Include license text

**Used by:** NumPy, Pandas, Matplotlib

---


## Quick Detour: Copyright vs Patents

**Two different types of protection:**

| Copyright | Patent |
|-----------|--------|
| Protects **expression** | Protects **ideas/methods** |
| Protects **the code itself** | Protects **how it works** |
| Automatic (when you write) | Must apply & be granted |
| Lasts 70+ years | Lasts ~20 years |

---

## Copyright vs Patents: Concrete Example

**You write a new sorting algorithm:**
```python
def quick_sort(arr):
    """My implementation of quicksort"""
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left) + middle + quick_sort(right)
```

**Copyright protects:** This specific code (the expression)
**Patent could protect:** The quicksort method itself (the algorithm)

---

## The Critical Difference

**Copyright:**
```python
# Someone can't copy your code
def quick_sort(arr):  # ← This exact code is protected
    if len(arr) <= 1:
        return arr
    # ... your implementation
```

**Patent:**
```python
# If patented, no one can use the METHOD, even with different code
def my_own_quicksort(array):  # ← Different code
    # Implements same algorithm ← Still violates patent!
```

**Copyright:** "Don't copy my code"  
**Patent:** "Don't use my method, even if you write your own code"

---



**Apache 2.0 explicitly handles this** →


---

## Apache License 2.0

**Like MIT, but with patent protection**

```
Key difference: Explicit patent grant
```

**Why it matters:**
- Contributors can't sue you for patent infringement
- Enterprise-friendly (legal clarity)
- Still permissive (like MIT)

**Used by:** Android (AOSP), Kubernetes, TensorFlow

---

## Copyleft: GPL v3

**"Share-alike" philosophy**

```
If you use GPL code, your code must be GPL too
```

**The four freedoms:**
1. Run the program for any purpose
2. Study how it works (access to source)
3. Redistribute copies
4. Improve and share improvements

**Designed by Richard Stallman, 1989**

---

## GPL in Practice

**What this means:**
```
You modify GPL code → Must release as GPL
You link GPL library → Must release as GPL
You distribute GPL software → Must provide source
```

**Strategic impact:**
- Forces improvements to stay open source
- Prevents "embrace and extend"
- Companies either contribute back or avoid it

**Used by:** Linux kernel, GCC, GIMP, Bash

---

## AGPL: The Network Clause

**GPL + network usage = AGPL**

```
Problem: Run modified GPL software on server
         Users access via web
         No "distribution" → No GPL trigger
         
Solution: AGPL considers network use as distribution
```

**Perfect for SaaS/web apps in 2025**

**If you modify AGPL code and host it, you must share source.**

---

## The SaaS Problem

**GPL was designed for distributed software**

```
Traditional (1990s):
Company → Ships software → Customer
GPL triggers: Must provide source!

Modern (2020s):
Company → Runs on server → Customer uses via web
GPL doesn't trigger: No distribution!
```

**Example:** Use GPL database in your SaaS
- Database code stays on YOUR server
- Users access via browser
- GPL: No obligation to share

---

## Why AGPL Matters (2025)

**The network loophole closed:**

```
MongoDB (2018): Was AGPL
AWS: Offers "DocumentDB" (MongoDB-compatible)

```

**Pattern repeating:** Elasticsearch, Redis, others

**Tension:** OSS creators vs cloud providers

---



## Quick Comparison

| License | Commercial Use | Keep Changes Private | Must Share Source |
|---------|---------------|---------------------|------------------|
| MIT | ✅ | ✅ | ❌ |
| Apache 2.0 | ✅ | ✅ | ❌ |
| GPL v3 | ✅ | ❌ | ✅ |
| AGPL | ✅ | ❌ | ✅ (even SaaS) |

---

## License Compatibility Matters

**Can you mix licenses in one project?**

```python
# your_project.py (MIT licensed)

import requests      # Apache 2.0 - OK! ✅
import numpy         # BSD - OK! ✅
import some_gpl_lib  # GPL v3 - PROBLEM! ❌

# Entire project becomes GPL!
```


---




## Public Domain: Unlicense

**"I give up all rights"**

```
This is free and unencumbered software 
released into the public domain.

Anyone is free to copy, modify, publish, use...
```

**Complete freedom, zero restrictions**

But... no warranty, no liability protection in all jurisdictions

---

## The Philosophy Wars

**Two movements, same code, different values**

---

## How We Got Here: The Bell Labs Story

**1969-1972: Unix & C created at Bell Labs (AT&T)**
- Dennis Ritchie, Ken Thompson
- Source shared with universities (~$150)
- BUT: Restricted AT&T license

**The problem:**
- Could read the code
- Could learn from it
- Could NOT freely modify and share

**This frustrated Richard Stallman (MIT, 1983)**

---

## Why GPL Exists

**Stallman's experience (early 1980s):**

```
Laser printer driver bug at MIT lab
Wanted to fix it
Source code? Proprietary, unavailable
Forced to live with bug

→ "This is unethical"
→ Started GNU Project (1983)
→ Created GPL (1989)
```

**Goal:** Ensure users always have source code access

---

## The GCC Revolution (1987)

<div style="display: flex; gap: 2em; justify-content: center;">

<div style="flex: 1;">

**Before GCC:**
- Compilers cost $1000s
- Tied to expensive hardware
- Proprietary

</div>

<div style="flex: 1;">

**After GCC:**
- Free compiler
- Anyone could compile code
- Portable (multiple platforms)
- GPL licensed

</div>

</div>

**Impact:** Made free software movement viable
- Linux (1991) used GCC
- Your code today uses GCC/Clang lineage

---

## Free Software Movement

**Founded by Richard Stallman, 1983**

```
"Free as in freedom, not free beer"
```

**Core belief:** Software freedom is a moral imperative

**The GNU Project:**
- Started in 1983 to create free Unix
- GNU = "GNU's Not Unix" (recursive acronym)
- Combined with Linux kernel (1991) → GNU/Linux

---

## Richard Stallman & GNU

**1983:** Launches GNU Project at MIT

**1985:** Founds Free Software Foundation (FSF)

**1989:** Creates GPL (first copyleft license)

**Philosophy:**
- Users should control their computing
- Source code access is a human right
- Proprietary software is unethical

**Still active in 2025, touring universities worldwide**

---

## The Four Essential Freedoms

**According to FSF:**

**Freedom 0:** Use the program for any purpose

**Freedom 1:** Study how it works (source access)

**Freedom 2:** Redistribute copies to help others

**Freedom 3:** Improve and share your improvements

**All four required to be "free software"**

---

## Open Source Movement

**Started 1998 (15 years after Free Software)**

```
Same licenses, different pitch
```

**Key difference:**
- Pragmatic, not ideological
- Business-friendly messaging
- Focus on practical benefits
- "Better code through transparency"

**Founded by:** Eric S. Raymond, Bruce Perens

---

## Free Software vs Open Source

| Free Software | Open Source |
|--------------|-------------|
| Ethical stance | Pragmatic approach |
| User freedom first | Better software first |
| Avoid "proprietary" | Avoid "closed source" |
| GPL preferred | Any OSI license OK |
| FSF (Stallman) | OSI (Raymond) |

**Same code, different philosophy**

Stallman: "Open source misses the point"

---

## Who Actually Writes Open Source?

**Surprise: It's corporations**

---

## Linux Kernel: The Numbers

**Kernel 6.15 (May 2025):**
- 2,068 developers contributed
- 14,612 changes

**Top corporate contributors:**
- Intel: 13.1%
- Red Hat: 11.9%
- Oracle, Meta, Google, Huawei, AMD...
- "Unknown" developers: ~8%

**Google made 94% of Chromium commits in 2024**

---

## Who Pays for Open Source?

**Linux kernel contributors are paid employees:**

```
Top companies by contribution:
- Intel      (chip optimization)
- Red Hat    (enterprise Linux)
- Oracle     (database/cloud)
- Meta       (infrastructure)
- Google     (Android/Chrome)
- Microsoft  (Azure/WSL)
```

**"Linux is not written by hobbyists in basements"**

---

## Why Companies Contribute

**Not altruism - strategic:**

**Intel contributes to Linux kernel:** 
→ Optimizations for Intel chips
→ Linux runs on Intel hardware
→ Win-win

**Google open sources Android:**
→ Everyone makes phones with it
→ Google controls mobile ecosystem
→ Makes money from ads/services

**Microsoft contributes to Linux (2020s):**
→ Azure runs Linux (70%+ of VMs)
→ Need it to work well
→ Competitive with AWS

---



---

## Alternative: The Service Model

**Red Hat's approach (1993-2019, $34B to IBM):**

```
Product: Red Hat Enterprise Linux (RHEL)
License: GPL (must be open source)
Price: FREE (source code available)

But selling:
✅ Support contracts ($1000s/year)
✅ Certification
✅ Guaranteed patches
✅ Training
✅ Phone support
```

**Revenue (2019):** $3.4 billion/year

**Not from software, but from SERVICE**

---

## GPL Forces This Model

**The paradox:**

```
GPL says: "Can't sell the software"
           (Anyone can copy and share)

But CAN sell: Services around it
              Support, training, customization

Companies must compete on service quality
Not on code ownership
```

**Examples:**
- Canonical (Ubuntu)
- SUSE (Linux)
- Many others

---

## Python's Corporate Backing

**Major sponsors and contributors:**
- Google (YouTube, infrastructure)
- Microsoft (hired Guido van Rossum in 2020)
- Meta (Instagram, PyTorch)
- Amazon (AWS, data tools)

**Guido van Rossum worked at:**
- Google (2005-2012)
- Dropbox (2012-2019)
- Microsoft (2020-present)

---

## The Chromium Reality

**Google's dominance:**

```
2024 Chromium statistics:
- 100,000+ commits by Google
- 94% of all contributions
- "Hundreds of millions of dollars annually"
```

**Who uses Chromium:**
- Chrome (Google)
- Edge (Microsoft)
- Opera, Brave, Vivaldi...

**36 million lines of code**

---

## Chromium: Open Source?

**Yes... but:**

✅ Source code is public (BSD license)  
✅ Anyone can build it  
✅ Can be modified and redistributed  

---

❌ Google makes all key decisions  
❌ Complexity makes external contribution difficult  
❌ Takes 7-8 hours to build on normal hardware  
❌ Realistically need Google's infrastructure  
 
**"Open source, but Google-controlled"**


---

## VS Code vs VSCodium

**Similar story:**

**VS Code:**
- Microsoft's product
- Includes telemetry
- Microsoft branding
- Proprietary marketplace

---

**VSCodium:**
- Built from VS Code source (MIT)
- No telemetry
- No Microsoft tracking
- Different extension marketplace

**Lesson: Source ≠ Product**

---

## The Bitter Truth: Technical Quality ≠ Success

**Open source alternatives exist...**

```
Proprietary          vs    Open Source
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
WhatsApp                  Signal
Zoom                      Jitsi, BigBlueButton  
GitHub                    Gitea, Forgejo
Google Drive              Nextcloud, seafile
Gmail                     ProtonMail
```

**All the open source ones work well!**

**So why does everyone use the proprietary ones?**

---

## Network Effects Beat Technology

**WhatsApp vs Signal:**

```
Signal:
✅ Better privacy (end-to-end encrypted)
✅ Open source (can audit)
✅ Non-profit
✅ No data collection

WhatsApp:
✅ 2 billion users (everyone you know is there)

Result: WhatsApp wins
Not because it's better
Because everyone uses it
```

**Network effects > Technical superiority**

---



## Your University's Open Source

**Université de Strasbourg uses:**
- Seafile (open source) for file storage
- BigBlueButton (open source) for teaching
- Gitlab's unistra server

---



## "Open Source AI" - What Does It Mean?

**Meta's Llama 3.1 (2024):**
```
✅ Model weights (MIT license)
✅ Training code
❌ Training data (secret)

Is this "open source"?
```


---

## Corporate Open Source Strategy

**Why companies release open source:**

```
✅ Get free contributions
✅ Set industry standards
✅ Attract developers
✅ Build ecosystem around their products
✅ Commodity complementary products
```

**Example:** Google open-sources Android
→ Everyone uses it
→ Google controls mobile web
→ Google makes money from ads

---

## Practical: Adding a License

**On GitHub:**

1. Create repository
2. Click "Add file" → "Create new file"
3. Type "LICENSE" as filename
4. GitHub shows license picker
5. Choose license (MIT, GPL, etc.)
6. Commit

**Or use:** https://choosealicense.com

---

## Choosing Your License

**Quick decision tree:**

```
Want max adoption?
  → MIT or Apache 2.0

Want improvements to stay open?
  → GPL v3

Building web service?
  → AGPL

Just share, don't care?
  → Unlicense or CC0
```
