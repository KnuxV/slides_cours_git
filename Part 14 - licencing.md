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

## The License Spectrum

```
Private ←──────────────────────────────→ Public Domain

Proprietary    MIT/Apache    GPL    AGPL    Unlicense
(closed)       (permissive)  (copyleft)    (no restrictions)
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

## MIT in Practice

**What you CAN do:**
- Use in commercial products
- Modify as you wish
- Keep modifications private
- Sell software using MIT code

**What you MUST do:**
- Include original copyright notice
- Include license text

**Used by:** React, Node.js, .NET, Rails, jQuery

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

## Quick Comparison

| License | Commercial Use | Keep Changes Private | Must Share Source |
|---------|---------------|---------------------|------------------|
| MIT | ✅ | ✅ | ❌ |
| Apache 2.0 | ✅ | ✅ | ❌ |
| GPL v3 | ✅ | ❌ | ✅ |
| AGPL | ✅ | ❌ | ✅ (even SaaS) |

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

❌ Google makes all key decisions
❌ Complexity makes external contribution difficult
❌ Takes 7-8 hours to build on normal hardware
❌ Realistically need Google's infrastructure

**"Open source, but Google-controlled"**

---

## The Ungoogled Problem

**Ungoogled-Chromium:** Remove Google dependencies

```bash
# What they remove:
- Google account integration
- Safe Browsing (Google servers)
- Google URL tracking
- Background requests to Google
- Pre-made binaries
```

**Why it exists:** Chromium has deep Google integration

Even "open source" doesn't mean "neutral"

---

## Android: AOSP

**Android Open Source Project**

```
Open source: ✅
Anyone can use: ✅
Google controlled: ✅
```

**What's included in AOSP:**
- Linux kernel
- Basic Android framework
- Core system apps

**What's NOT included:**
- Google Play Store
- Gmail, Maps, Chrome
- Google Mobile Services (GMS)

---

## Android: The Control Mechanism

**2025 update: Now even more closed**

**March 2025:** Google moves all development internal

```
Before: Some commits visible in public AOSP
After:  All development behind closed doors
        Source published only after release
```

**Why?** "Efficiency and avoiding merge conflicts"

**Result:** Can't see what Google is working on

---

## Android: The Licensing Trap

**AOSP is open (Apache 2.0)** ✅

**BUT to be useful, you need:**
- Google Mobile Services (proprietary)
- Google Play Store (proprietary)
- Google apps (proprietary)

**To get GMS license, you must:**
- Follow Google's rules
- Pre-install Google apps
- Meet compatibility requirements
- Pass Google certification

---

## Who Can Use AOSP?

**Success stories:**
- Amazon Fire OS (no Google services)
- Huawei HarmonyOS (US sanctions)
- LineageOS, GrapheneOS (custom ROMs)

**Reality:** Without GMS, you lose:
- Play Store (most apps)
- Google Maps
- Gmail, YouTube
- Push notifications

**"Open source" but practically dependent**

---

## VS Code vs VSCodium

**Similar story:**

**VS Code:**
- Microsoft's product
- Includes telemetry
- Microsoft branding
- Proprietary marketplace

**VSCodium:**
- Built from VS Code source (MIT)
- No telemetry
- No Microsoft tracking
- Different extension marketplace

**Lesson: Source ≠ Product**

---

## Open Source in 2025

**Current tensions:**

---

## Big Tech & Open Source

**The paradox:**

```
Big Tech loves open source...
...because they profit from it

But do they give back proportionally?
```

**Debates in 2025:**
- Cloud providers profiting from OSS
- AI companies training on GPL code
- "Open washing" (calling things open that aren't)

---

## The AI License Crisis

**New question:** Does GPL apply to AI models?

```
Scenario: Train AI on GPL code
Question: Must the AI model be GPL?
Answer:   Legal grey area (2025)
```

**GitHub Copilot lawsuit ongoing**

**Tensions:**
- Copyleft supporters: "Yes, derivative work!"
- AI companies: "No, fair use!"
- Courts: Not decided yet

---

## "Open Source AI" Controversy

**Meta's Llama, DeepSeek R1:**
- Model weights released (MIT license)
- Training code released
- Training data? ❌

**OSI definition:** Must include training data

**Debate:** What does "open source AI" mean?

**2025 status:** No consensus

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

## The Complexity Barrier

**Some projects are "open" but practically closed:**

**Chromium:**
- 36 million lines of code
- 7-8 hour builds on normal hardware
- Requires specialized knowledge
- Difficult to fork meaningfully

**Android:**
- Massive codebase
- Device-specific drivers needed
- Certification requirements
- Ecosystem lock-in (GMS)

**Open source ≠ easy to contribute**

---

## The State in 2025

**What's working:**
- More code is open than ever
- Corporate investment in OSS
- Strong communities (Linux, Python)
- Open source is industry standard

**What's concerning:**
- Concentration of control (Google, Microsoft)
- "Open core" business models
- AI training on OSS (legal uncertainty)
- Complexity as a barrier

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

---

## License in Your Project

**Always include:**

```
your-project/
  LICENSE          ← Full license text
  README.md        ← Mention license
  src/
    main.py        ← Optional: License header
```

**In README:**
```markdown
## License
This project is licensed under the MIT License.
```

---

## What Happens Without License?

**Real example:**

```
Awesome open source tool on GitHub
No LICENSE file
Company wants to use it
Legal says: "No license = can't use"
```

**Your code is useless without a license**

Even if you meant to share it!

---

## The Bigger Picture

**Open source succeeded, but questions remain:**

- Who controls "open" projects?
- Are users truly free?
- Can individuals compete with corporations?
- What happens when complexity = barrier?

**Stallman's 1983 warning is relevant in 2025:**

*"Who controls your computing?"*

---

## Key Takeaways

**1. Always add a license** → No license = useless code

**2. Understand the spectrum** → Permissive vs Copyleft

**3. Corporate dominance is real** → Most OSS written by paid employees

**4. "Open" has many meanings** → Source visibility ≠ community control

**5. The philosophy matters** → Freedom vs pragmatism

---

## The Linux Success Story

**Despite everything:**

```
Started: 1991 (Linus Torvalds, Finnish student)
License: GPL v2 (still, can't upgrade!)
Contributors: 25,000+ developers
Companies: 186+ contributing
Usage: 70% of web servers
         96.3% of top 1M servers
         100% of supercomputers
Market: $15.64 billion projected (2027)
```

**Proof that copyleft can work at massive scale**

---

## Resources

**Learn more:**
- https://choosealicense.com
- https://opensource.org (Open Source Initiative)
- https://www.fsf.org (Free Software Foundation)
- https://tldrlegal.com (License explanations)

**Read:**
- "Free Software, Free Society" (Stallman)
- "The Cathedral and the Bazaar" (Raymond)

---

## Practice Exercise

**Your turn:**

1. Go to https://choosealicense.com
2. Answer the questions
3. Pick a license for a hypothetical project
4. Create a repo and add the LICENSE file

**Discussion questions:**
- Your side project: MIT or GPL? Why?
- A library many will use: Which license?
- A web service (SaaS): Which license?

---

## Final Thought

```python
# From Stallman, 1983
def freedom():
    """
    The question is not
    whether the code is visible.
    
    The question is
    who controls your computing.
    """
    return "Choose wisely"
```

**Your code, your rules, your license.**

**But remember: no license = no sharing.**