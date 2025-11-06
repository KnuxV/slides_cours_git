---
words:
  2025-11-06: 2477
title: Part 2 - Basic Commands & First Repository
theme: simple
highlightTheme: github
---

### Remote Repositories & Collaboration

*Time to push your code to the cloud!*

---

### Remote Repositories Explained

**Local Repository** = On your computer
**Remote Repository** = On a server

```
Your Computer          Internet          GitLab Server
[Local Repo]    ←→    [Network]    ←→   [Remote Repo]
   git push →                              ← git pull
```

---

**Why remote?**
- Backup your code
- Collaborate with others
- Access from anywhere

---

### University GitLab Setup

**URL:** `https://gitlab.unistra.fr`

**Login:** Use your **ernest credentials**
- Username: Your ernest username
- Password: Your ernest password

**Let's log in now**

---

### Authentication: Two Options

#### **Option 1: HTTPS + Personal Access Token**  

### **Option 2: SSH Keys** 



---

### Creating a Token

**Follow along on GitLab:**

1. Click your profile picture (top right)
2. Preferences → Access Tokens --> Add new token
3. Token name: `Salle 404` 
4. Expiration: Choose a date (e.g., end of semester)
5. Scopes: `read_repository` `write_repository`
6. Click Create personal access token
7. COPY THE TOKEN NOW (you won't see it again!)

---

### Save Your Token

**Important:**
- Copy token to a text file (temporarily)
- You'll use it as your password when pushing
- If you lose it, create a new one
- **Never share it** (treat like a password)

---

### Credential Caching

```bash
git config --global credential.helper store

# Or for whole day (28800 seconds = 8 hours)
git config --global credential.helper 'cache --timeout=28800'
```
**Security note:**
- ✅ OK on university computers (your session only)
- ❌ Don't use on shared/public computers
- Token still expires on your chosen date

**After first use, Git will remember your token**

---

### SSH Keys 

**If you want to set up SSH:**

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@unistra.fr"

# Copy public key
cat ~/.ssh/id_ed25519.pub

# Add to GitLab: Profile → SSH Keys → Paste
```

**Benefits:** No passwords ever needed!
**Read**: [More information here](https://docs.gitlab.com/user/ssh/?tab=Linux+%28requires+the+xclip+package%29)


---

## Part 1: Push Existing Local Repo

---

### The Scenario

**You have:**
- ✅ Local Git repo on your computer
- ✅ Multiple commits
- ✅ Working project

**You want:**
- Push it to GitLab
- Make it accessible online
- Have a backup



---

### Step 1: Create Empty Repo on GitLab

**On `gitlab.unistra.fr`:**

1. Click **New Project** (or **+** button)
2. **Create blank project**
3. Project name: `my-first-website`
4. Visibility: **Public** (or Private if you want)
5. **UNCHECK** "Initialize repository with a README"
6. Click **Create project**

---

### Why Uncheck README?

**We already have commits locally!**

```
If GitLab creates README:
  GitLab has: [README commit]
  You have:   [Your commits]
  
Result: Conflict when pushing! 
```

**Empty repo = Clean push** 


---

### Understanding Remote URLs

**Two formats:**

```bash
# HTTPS (we use this)
https://gitlab.unistra.fr/username/repo.git

# SSH (for later)
git@gitlab.unistra.fr:username/repo.git
```

**HTTPS URL = Token authentication**

---

### Step 2: Link Local to Remote

**In your terminal, in your project folder:**

```bash
# Make sure you're in the right place
pwd
# Should show: /path/to/my-first-website

# Add remote
git remote add origin https://gitlab.unistra.fr/YOUR_USERNAME/my-first-website.git
```

---

### What is "origin"?

**origin** = Default name for your main remote repository

```
origin = nickname for the long GitLab URL

Instead of typing:
  https://gitlab.unistra.fr/username/repo.git
  
You can type:
  origin
```

---

**You can have multiple remotes, but origin is the standard name**
```git
git remote add github github_url
git remote add gitlab gitlab_url

# now we could do something like:
git push github main # push the code to github 
```

---

### Verify Remote Added

```bash
git remote -v
```

**Output:**
```
origin  https://gitlab.unistra.fr/username/my-first-website.git (fetch)
origin  https://gitlab.unistra.fr/username/my-first-website.git (push)
```

**Both fetch and push pointing to same URL** ✅

---

### Step 3: Push Your Code!

```bash
git push -u origin main
```

**Breaking it down:**
- `git push` = Send commits to remote
- `-u` = Set upstream (remember this branch)
- `origin` = The remote we just added
- `main` = The branch to push

**First time only needs `-u`, later just `git push`**

---

### Authentication Time

**When you push, GitLab asks:**

```
Username for 'https://gitlab.unistra.fr': your_username
Password for 'https://your_username@gitlab.unistra.fr': 
```

**Password = Your Personal Access Token **

---

### Results

**Output:**
```
Enumerating objects: 15, done.
Counting objects: 100% (15/15), done.
Writing objects: 100% (15/15), 1.23 KiB | 1.23 MiB/s, done.
Total 15 (delta 0), reused 0 (delta 0)
To https://gitlab.unistra.fr/username/my-first-website.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

**Your code should be on GitLab** 


---

### Common Issues & Fixes

**"remote: HTTP Basic: Access denied"**
- Wrong token or username
- Regenerate token and try again

**"fatal: not a git repository"**
- You're in wrong folder
- `cd` to your project folder

---

## Part 2: Clone Your Own Empty Repo

### Start fresh from GitLab

---

### Different Workflow

**Before:** Local → Remote (push existing work)

**Now:** Remote → Local (start from GitLab)

```
1. Create empty repo on GitLab
2. Clone it to your computer
3. Add files
4. Push changes back
```

**This is how you'd start a NEW project**

---

### Step 1: Create New Empty Repo

**On GitLab:**

1. **New Project** → **Create blank project**
2. Name: `git-practice`
3. Visibility: Private
4. **Check** or not "Initialize repository with a README"
5. Click **Create project**

---

### Step 2: Get Clone URL

**On your new project page:**

Look for the **Clone** button (top right)

**Click it and copy the HTTPS URL:**
```
https://gitlab.unistra.fr/username/git-practice.git
```

---

### Step 3: Clone to Your Computer

**In terminal (NOT in existing repo):**

```bash
# Go to your projects folder
cd ~
cd projects  # or wherever you keep code

# Clone the repo
git clone https://gitlab.unistra.fr/username/git-practice.git

# Move into it
cd git-practice
```

---

### What Just Happened?

```bash
git clone <url>
```

**Git did 5 things:**
1. Created `git-practice` folder
2. Initialized Git inside (`.git/`)
3. Added `origin` remote automatically
4. Downloaded all commits/files
5. Checked out main branch

**It's a complete copy!**

---

### Verify the Clone

```bash
# Check remote (should already be set!)
git remote -v

# Check commits
git log --oneline

# List files
ls -la
```

**You should see:**
- `origin` pointing to GitLab
- Initial commit with README
- README.md file

---

### Step 4: Add Some Files

**Create a simple webpage:**

```bash
touch rdm_script.py
```

**Add content:**
```python
import random
print(random.random())
```

---

### Step 5: Commit Locally

```bash
git status
git add rdm_script.py
git commit -m "Add random script"
```

**So far, this is all local **

---

### Step 6: Push to GitLab

```bash
git push
```

**That's it** No `-u origin main` needed because:
- Clone already set up tracking
- Git remembers where to push

---

### Pull Changes from GitLab

**Let's edit on GitLab web interface:**

1. Click `README.md` on GitLab
2. Click **Edit** button
3. Add a line: `## This project practices Git!`
4. Scroll down, write commit message
5. Click **Commit changes**

**Now GitLab has a commit you don't have locally**

---

### Pull the Changes

**In terminal:**

```bash
git pull
```

**Output:**
```
remote: Enumerating objects: 5, done.
Updating a1b2c3d..e4f5g6h
Fast-forward
 README.md | 2 ++
 1 file changed, 2 insertions(+)
```

**Check README.md - you have the new line!**

---

### Understanding Push & Pull

```
       git push →
[Your Computer]     [GitLab]
       ← git pull

Push = Send your commits to GitLab
Pull = Get commits from GitLab
```

**Always pull before you push** (good habit)

---

### The Push/Pull Cycle

```bash
# Start your work
git pull

# Make changes
# ... edit files ...

# Commit locally
git add .
git commit -m "Your changes"

# Send to GitLab
git push
```

**This is the daily workflow** 

---

## Practice: Clone & Work (5 min)

**Your turn:**

1. Create new empty repo on GitLab (with README)
2. Clone it to your computer
3. Add 2-3 files
4. Commit them
5. Push to GitLab
6. Edit README on GitLab web
7. Pull changes locally

**Quick exercise** 

---

## Part 3: Clone Someone Else's Repo

### Exploring public code

---

### Why Clone Others' Code?

**Reasons:**
- Learn from others
- Explore open source
- Use libraries/tools
- Review code

**You can clone any public repo**

---

### Permissions Matter

**When you clone someone else's repo:**

✅ You CAN:
- Clone (download) it
- Read/Execute all the code
- Make local modifications/commits

❌ You CANNOT:
- Push to their repo
- Change their code online

**Read-only access** 🔒

---

### Let's Clone a Public Repo


```
https://github.com/KnuxV/advanced_programming_python
```


**Everyone clone it:**

```bash
cd ~/projects
git clone https://github.com/KnuxV/advanced_programming_python
cd git-demo
```

---

### Explore the Cloned Repo

```bash
# View the files
ls -la

# Check commit history
git log --oneline

# Check remote
git remote -v

# View a file
cat README.md
```

**Explore freely - you can't break anything**

---

### Try to Push (It Will Fail!)

```bash
# Make a change
echo "My change" >> README.md

# Commit it
git add README.md
git commit -m "Try to add my change"

# Try to push
git push
```

**Output:**
```
remote: You are not allowed to push code to this project.
or something like that
```


---

### What If You Want to Contribute?

**That's where FORKING comes in!** →



---

## Part 4: Fork Workflow

### Make your own copy to modify

---

### What is Forking?

**Fork = Copy someone's repo to YOUR account**

```
Their GitLab Account        Your GitLab Account
[Original Repo]      →      [Forked Copy]
   (read-only)                (you own it!)
```

**After forking:**
- ✅ You can push to YOUR fork
- ✅ You can make any changes
- ✅ You can suggest changes back (Merge Request)

---

### Fork vs Clone

**Clone:**
- Downloads to your computer
- Still points to original
- Can't push

**Fork:**
- Creates YOUR copy on GitLab
- You own the copy
- Then you clone YOUR fork
- Can push to it!

---

### When to Fork?

**Use forking when:**
- 🐛 You want to fix a bug in someone's project
- ✨ You want to add a feature
- 🎓 You want to customize for your use
- 🤝 You want to contribute back

**Forking enables collaboration!**

---

### Step 1: Fork a Repository

**On the demo repo page:**


1. Go to https://gitlab.unistra.fr/kmichoud/collaboration-fork
2. Look for **Fork** button (top right)
3. Choose your namespace (your username)
4. Click **Fork project**

**GitLab creates a copy in YOUR account** 

---

### Step 2: Clone YOUR Fork

**Your fork has a different URL:**

```bash
# Original (you can't push)
https://git.unistra.fr/kmichoud/collaboration-fork.git

# Your fork (you CAN push!)
https://gitlab.unistra.fr/YOUR_USERNAME/collaboration-fork.git
```

**Clone YOUR fork:**
```bash
cd ~/projects
git clone https://gitlab.unistra.fr/YOUR_USERNAME/collaboration-fork.git
cd collaboration-fork
```

---

### Step 3: Make Changes

```bash
# Add your name in contributions.md
# Open contributions.md
# Add your name
# Add the date, your name and a random message

# Commit it
git add contributions.md
git commit -m "Add my contribution"
```

---

### Step 4: Push to YOUR Fork

```bash
git push
```

**This time it works** 

**Because you own this fork**

---

### Understanding Fork Relationships

```
[Original Repo]
      ↓ fork
[Your Fork] ← you push here
      ↓ clone
[Your Computer] ← you work here
```

**Your fork is independent but remembers its origin**

---

### Merge Requests (Pull Requests)

**Want to contribute back to original?**

1. Make changes in your fork
2. Push to your fork
3. On GitLab: **Create Merge Request**
4. Original owner reviews
5. They merge (or request changes)

**This is how open source works** 🌟

---

### Creating a Merge Request

**On your fork's GitLab page:**

1. Click **Merge Requests**
2. Click **New merge request**
3. Source: your fork's main branch
4. Target: original repo's main branch
5. Write description of changes
6. Click **Create merge request**

**Now you wait for review**

---

### Practice: Fork & Contribute (8 min)

**Your turn:**

1. Add a new file locally
2. Commit and push to your fork
3. Merge request

**we'll review and merge them all** 

---

### Fork Workflow Summary

```
1. Fork (on GitLab) → Your copy created
2. Clone (your fork) → Download to computer
3. Branch (optional) → Separate feature work
4. Change → Make your edits
5. Commit → Save locally
6. Push → Upload to your fork
7. Merge Request → Propose changes to original
```

**This is professional open-source workflow!**

---

## Part 5: Merge, Rebase & Conflicts

### When collaboration gets messy

---

### Why Conflicts Happen

**Two people edit the same line:**

```
Person A:                  Person B:
<h1>Hello World</h1>      <h1>Hi There</h1>
      ↓ push                    ↓ push
      
Git: "Wait, which one?!" 
```

**Conflict = Git can't auto-merge**

---

### Conflict Scenario Setup

**Let's create a conflict intentionally:**

**Everyone:**
1. Open your `index.html` on collaboration-fork, locally
2. Change the `<p>` text to something unique
3. Commit it
4. **DON'T PUSH YET!**

---

### Simulate Conflict

**Now I'll push a change to the collaboration-fork:**

(Instructor pushes conflicting change to demo repo)

**Now when you try to pull:**

```bash
git pull
```

**CONFLICT**

---

### Anatomy of a Conflict

**Git adds markers to your file:**

```html
<<<<<<< HEAD
<h1>My Version</h1>
=======
<h1>Their Version</h1>
>>>>>>> a1b2c3d
```

**Understanding the markers:**
- `<<<<<<< HEAD` → Your changes
- `=======` → Divider
- `>>>>>>> hash` → Their changes (from remote)

---

### Conflict Markers Explained

```html
<<<<<<< HEAD (your current commit)
<h1>Hello World</h1>
=======
<h1>Hi There</h1>
>>>>>>> a1b2c3d (incoming commit)
```

**Git is asking YOU to decide:**
- Keep yours?
- Keep theirs?
- Combine both?
- Write something new?

---

### Resolving a Conflict

**Step 1: Open the conflicted file**

**Step 2: Remove the markers and decide:**

```html
<!-- Before (conflict) -->
<<<<<<< HEAD
<h1>Hello World</h1>
=======
<h1>Hi There</h1>
>>>>>>> a1b2c3d

<!-- After (resolved) -->
<h1>Hello There, World!</h1>
```

---

### Step 3: Mark as Resolved

```bash
# After editing the file
git add index.html

# Commit the resolution
git commit -m "Resolve merge conflict in heading"

# Now push
git push
```

**Conflict resolved** 

---


### Checking for Conflicts

```bash
# Before you commit
git status

# Shows conflicted files
both modified: index.html
```

**Won't let you commit until resolved**


---

### Checking What Changed During Pull

```bash
# Before pulling
git fetch origin
git diff main origin/main

# See what would change without merging
```

**Fetch = download, but don't merge yet**

---

### Commands Summary

```bash
git remote add origin <url>  # Link local to remote
git push -u origin main      # First push
git push                     # Subsequent pushes
git pull                     # Get remote changes
git clone <url>              # Download repo
git merge                    # Combine branches
git rebase                   # Replay commits
```

---

### Workflow Checklist

**Daily workflow:**
```
1. git pull          (get latest)
2. [make changes]    (do your work)
3. git status        (check what changed)
4. git add .         (stage changes)
5. git commit -m ""  (save locally)
6. git push          (upload to GitLab)
```
