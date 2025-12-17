---
title: GitHub Actions Basics
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

## GitHub Actions

Automate tests and documentation on every push

---

## The Concept

**Every time you push code → Actions run automatically**

```
git push
   ↓
GitHub runs your tests
   ↓
GitHub builds your docs
   ↓
✅ Everything published!
```

**Why?**
- Catch bugs before they go live
- Documentation always up-to-date
- Free hosting on GitHub Pages

---

## What are GitHub Actions?

**Automated tasks that run in the cloud:**

- **Trigger:** When something happens (push, PR, etc.)
- **Jobs:** What to do (run tests, build docs)
- **Steps:** Individual commands to execute

**Example:** "Every time I push, run my tests"

---

## Where Do They Live?

**All workflows go in one place:**

```
your-repo/
  .github/
    workflows/
      tests.yml      ← Test automation
      docs.yml       ← Doc generation
      demo.yml       ← Any workflow
```

Create this structure in your repo!

---

## Anatomy of a Workflow

```yaml
name: Tests                    # What is this?
on: [push]                     # When to run?
jobs:                          # What to do?
  test:                        # Job name
    runs-on: ubuntu-latest     # Where to run?
    steps:                     # Individual steps
      - uses: actions/checkout@v6    # Get code
      - run: pytest tests/           # Run tests
```

**That's it!** Just YAML configuration.

---

## Example 1: Running Tests

**Create `.github/workflows/tests.yml`:**

```yaml
name: Tests
on:
  push:
    branches:
      - main
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: actions/setup-python@v6
        with:
          python-version: '3.14'
      - run: pip install pytest
      - run: pytest tests/
```

Push this → Tests run automatically!

---

## Example 2: Building Docs

**Create `.github/workflows/docs.yml`:**

```yaml
name: Documentation
on:
  push:
    branches:
      - main
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: actions/setup-python@v6
      - run: pip install pdoc
      - run: pdoc your_module.py -o docs/
```

Your docs are generated on every push!

---

## Publishing to GitHub Pages

**Add deployment step to `docs.yml`:**

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: actions/setup-python@v6
      - run: pip install pdoc
      - run: pdoc your_module.py -o docs/
      - uses: actions/upload-pages-artifact@v4
        with:
          path: docs/
  
  deploy:
    needs: build
    runs-on: ubuntu-latest
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
    steps:
      - uses: actions/deploy-pages@v4
```

---

## Enable GitHub Pages

**In your repo settings:**

1. Go to **Settings** → **Pages**
2. Source: **GitHub Actions**
3. Save

**Done!** Your docs will be at:
`https://username.github.io/repo-name/`

---

## Common Actions

**`actions/checkout@v6`**  
Gets your code from the repo

**`actions/setup-python@v6`**  
Installs Python

**`actions/upload-pages-artifact@v4`**  
Prepares files for GitHub Pages

**`actions/deploy-pages@v4`**  
Publishes to GitHub Pages

---

## Installing Dependencies

**If you have a `requirements.txt`:**

```yaml
steps:
  - uses: actions/checkout@v6
  - uses: actions/setup-python@v6
  - run: pip install -r requirements.txt
  - run: pip install pdoc
  - run: pdoc your_module.py -o docs/
```

**Important:** Install dependencies before running pdoc!

---

## Multiple Modules

**Document several files at once:**

```yaml
- run: pdoc module1.py module2.py module3.py -o docs/
```

**Or your entire package:**

```yaml
- run: pdoc . -o docs/
```

pdoc will document everything it finds!

---

## Checking Status

**After pushing, check:**

1. Go to your repo on GitHub
2. Click **Actions** tab
3. See your workflows running
4. Green ✅ = Success
5. Red ❌ = Failed (click to see why)

**Real-time feedback on every push!**

---

## Complete Tests Workflow

```yaml
name: Tests
on:
  push:
    branches:
      - main
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: actions/setup-python@v6
        with:
          python-version: '3.14'
      - run: pip install pytest
      - run: pip install -r requirements.txt
      - run: pytest tests/
```

---

## Complete Docs Workflow

```yaml
name: Documentation
on:
  push:
    branches:
      - main
permissions:
  contents: read
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: actions/setup-python@v6
        with:
          python-version: '3.14'
      - run: pip install -r requirements.txt
      - run: pip install pdoc
      - run: pdoc module.py --docformat google -o docs/
      - uses: actions/upload-pages-artifact@v4
        with:
          path: docs/
  deploy:
    needs: build
    runs-on: ubuntu-latest
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/deploy-pages@v4
```

---

## The Workflow

```
1. Create .github/workflows/
     ↓
2. Add tests.yml and docs.yml
     ↓
3. Push to GitHub
     ↓
4. Enable GitHub Pages in Settings
     ↓
5. Every push → tests run + docs update!
```

---

## Practice Exercise

**Set up your repo with:**
1. `.github/workflows/tests.yml` - Run pytest on push
2. `.github/workflows/docs.yml` - Generate docs with pdoc
3. Enable GitHub Pages in repo settings
4. Push some changes and watch Actions run!

**Check:** Visit your docs at `username.github.io/repo-name`

---

## Tips

**Test locally first:**
```bash
pytest tests/          # Before pushing
pdoc your_module.py    # Check docs work
```

---

**Start simple:**
- One workflow at a time
- Add complexity gradually
- Copy examples and modify

**Debug failures:**
- Click the red ❌ in Actions tab
- Read the error logs
- Fix and push again