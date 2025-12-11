---
title: Python Unit Testing
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

## Python Unit Testing

---

### The Cost of Bugs
**Real-world disasters caused by inadequate testing:**

- **Ariane 5 Rocket (1996)** - €370M explosion
  - 64-bit float → 16-bit integer overflow
  - Reused code from Ariane 4 without proper testing

- **Therac-25 (1985-87)** - 6 patients killed
  - Radiation therapy machine overdosed patients
  - Race condition in poorly tested software

- **Knight Capital (2012)** - $440M loss in 45 minutes
  - Untested deployment flag caused algorithmic trading chaos

**The lesson:** Testing isn't optional bureaucracy—it's risk management.

---

## What is Software Testing?

**Definition:** Systematic verification that code behaves as expected under various conditions.

**Core objectives:**
- **Catch bugs early** → 4-5x cheaper to fix before production (IBM)
- **Document behavior** → Tests are executable specifications
- **Enable refactoring** → Change code confidently without breaking things
- **Facilitate collaboration** → Clear expectations for team members

**Simple analogy:**
```python
def calculate_price(items, discount):
    return sum(items) * discount  
    # Bug: should be * (1 - discount)
```

---

### QA Teams - The Traditional Approach

**What is QA (Quality Assurance)?**
- Dedicated team responsible for finding bugs before release
- Manual testing: clicking through interfaces, following test scripts
- Automated testing: Running test suites on staging environments

**Traditional workflow:**
```
Developers write code 
→ QA tests it 
→ Bugs reported back 
→ Developers Fix 
→ Repeat
```

---

**Limitations of QA-only approach:**
- ❌ Slow feedback loop (days/weeks, not minutes)
- ❌ Expensive to maintain large QA teams
- ❌ Developers don't think about testing while coding
- ❌ "Throw it over the wall" mentality

**Modern shift:**  
✅ Developers write tests themselves (shift-left testing)  
✅ QA focuses on complex integration/UX scenarios  
✅ Automated tests catch regressions instantly  

---

## Test-Driven Development (TDD)

**The TDD cycle (Red-Green-Refactor):**

```
1. 🔴 RED: Write a failing test first
2. 🟢 GREEN: Write minimal code to pass
3. 🔵 REFACTOR: Clean up while tests still pass
```

---

**Example:**
```python
# Step 1: Write test first (it fails)
def test_calculate_tva():
    assert calculate_vat(100, 0.20) == 120

# Step 2: Write code to pass
def calculate_tva(price, rate):
    return price + price*rate

# Step 3: Refactor if needed
def calculate_tva(price: float, rate: float) -> float :
    return price * (1 + rate)
```

---

## Continuous Integration (CI)

**What is CI?**
Automatically running tests on every code change before merging.

**Typical CI workflow:**
```
Developer pushes code → CI server pulls code → Runs all tests
                                              ↓
                                    ✅ Pass → Merge allowed
                                    ❌ Fail → Merge blocked
```

**Popular CI tools:**
- GitHub Actions (integrated with GitHub)
- GitLab CI (integrated with GitLab)

---

**Example GitHub Actions:**
```yaml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: pip install pytest
      - run: pytest
```

**Benefits:**
- No broken code reaches production
- Tests run on every commit (not just "when I remember")
- Catches platform-specific bugs (tests run on Linux/Windows/Mac)
- Team confidence: green CI = safe to deploy

---

### The Testing Pyramid

**Visual representation of test distribution:**

```
         /\
        /  \
       /E2E \          End-to-End (few, slow, expensive)
      /------\         - Full user workflows
     /        \        - Browser automation
    /          \    
   / Integration\     Integration (moderate)
  /--------------\   - Multiple components together
 /   Unit Tests   \   - API + Database + Auth
/                  \
                        Unit (many, fast, cheap)
                          - Individual functions
                          - Pure logic testing
```

---

### Types of Testing 

**1. Unit Tests** 
- Test individual functions/methods in isolation
- Fast (milliseconds), many tests (hundreds/thousands)
- Example: `test_calculate_discount()`

---

**2. Integration Tests**
- Test multiple components working together
- Example: API endpoint + database + cache
- Slower (seconds), fewer tests

---

**3. End-to-End (E2E) Tests**
- Test complete user workflows through UI
- Example: Login → Browse → Add to cart → Checkout
- Slowest (minutes), fewest tests
- Tools: Selenium

---

**4. UI/UX Tests**
- Visual rendering, accessibility, responsiveness
- Does button render on mobile? Can screen readers navigate?



---

**5. Others (brief mention):**
- **Performance tests:** Load testing, stress testing
- **Security tests:** Penetration testing, vulnerability scans
- **Regression tests:** Ensure old bugs stay fixed


---

### Transition to Practical Section

**Next up:** 
- pytest basics (assertions, fixtures, parametrize)
- Live coding examples
- Hands-on exercises with real Python code

