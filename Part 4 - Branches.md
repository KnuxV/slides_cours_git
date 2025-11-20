--- 
title: Part 4 - Branches (Parallel Universes)
theme: simple
highlightTheme: github
---

# Part 4 – Branches
## Parallel Universes in Git

---
## Why do branches exist?

You want to add a new feature …  
but you **don’t want to break the working code** right now.

**Solution: work on the side → in a branch**

```
main:        A---B---C
                  \
feature:           D---E---F
```

---
## Real-life example

- `main` → the version that works (what the teacher sees)
- `login-page` → you are building the login system
- `dark-mode` → your friend is adding dark theme
- `bugfix-typo` → someone is fixing small typos

Everyone works at the same time → no problem!

---
## Visualising branches

```bash
git branch          # shows you this:
  dark-mode
  login-page
* main              # ← the star = where you are right now
```

The star moves when you change branch.

---
## Basic branch commands (the only 3 you need)

```bash
# 1. Create + switch in one command (most common)
git switch -c new-feature

# 2. Just switch to an existing branch
git switch main
git switch login-page

# 3. List all branches
git branch
```

That’s literally it for 95 % of your life.

---
## The safe workflow (memorise this)

```bash
git switch -c my-cool-feature   # create branch + jump there
# → code code code
git add .
git commit -m "finished something"
git switch main                 # go back to main
git merge my-cool-feature       # bring the work into main
```

---
## Merging = bringing work together

Two possible outcomes:

### 1. Fast-forward (perfect world)
Git just moves the `main` pointer → no problem

### 2. Merge conflict (we’ll fix it together in 2 minutes)

---
## Fast-forward merge (most of the time)

```
Before:
main → A---B---C
                \
feature          D---E

After git merge feature:
main → A---B---C---D---E
```

Git just says “ok, cool” and moves on.

---
## When a conflict happens

Both branches changed the **same lines** in the **same file**.

Git stops and says:
> “Hey human, I’m not smart enough. You decide!”

You’ll see this in the terminal:
```
CONFLICT (content): Merge conflict in scrabble_score.py
Automatic merge failed; fix conflicts and then commit the result.
```

---
## How to fix a conflict (3 steps – always the same)

1. Open the file → you see this:
```python
<<<<<<< HEAD
# code from main
=======
# code from the feature branch
>>>>>>> my-cool-feature
```

2. Edit the file → keep what you want (usually both parts)
   Delete the `<<<<<<<`, `=======`, `>>>>>>>` lines

3. Save → then tell Git you’re done:
```bash
git add scrabble_score.py
git commit -m "Merged feature with small fix"
```

That’s it. Conflict gone forever.

---
## Golden rule

**Never work directly on main for new stuff**  
Always create a branch → life becomes 100× calmer.

```bash
# Good
git switch -c login-page

# Dangerous (don’t do this for big changes)
# working directly on main
```

---
## Quick cheat-sheet (put this on your wall)

```bash
git switch -c name        # new branch + jump
git switch name           # change branch
git branch                # see branches
git merge name            # bring branch into current one
```

---
## Recap – The complete safe workflow

```bash
git switch main
git switch -c cool-new-thing
# code code code
git add . && git commit -m "…"
git switch main
git merge cool-new-thing
git push                  # send everything to GitLab
```

---
## Now go do the Scrabble exercise!
https://gitlab.unistra.fr/cours_git/exercise_scrabble

You have exactly this situation:
- `main`
- `letter-multi` (already merged)
- `word-multiplier` → will conflict!

Follow the README → you already know everything you need.

You’ve got this!