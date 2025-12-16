---
title: Python __main__
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

## Python `__main__`

Making modules both importable and executable  
---
<div style="text-align: center;">
<code>
if __name__ == "__main__":  
    # Do something
</code>

</div>

---

## The Problem

**calculator.py:**
```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

# Test our functions
print("Testing calculator...")
print(f"2 + 3 = {add(2, 3)}")
print(f"5 - 2 = {subtract(5, 2)}")
```

---

**What happens when we import it?**

```python
# main.py
from calculator import add

result = add(10, 5)
print(f"Result: {result}")
```

**Output:**
```
Testing calculator...
2 + 3 = 5
5 - 2 = 3
Result: 15
```

❌ **Problem:** Test output appears even though we just wanted to import!

---

## The Solution: `__name__`

**Every Python module has a special variable `__name__`:**

- When **run directly**: `__name__ == "__main__"`
- When **imported**: `__name__ == "calculator"` (module name)

---

**Fixed calculator.py:**
```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

# Only run if executed directly
if __name__ == "__main__":
    print("Testing calculator...")
    print(f"2 + 3 = {add(2, 3)}")
    print(f"5 - 2 = {subtract(5, 2)}")
```

---

**Now when we import:**

```python
# main.py
from calculator import add

result = add(10, 5)
print(f"Result: {result}")
```

**Output:**
```
Result: 15
```

✅ **Success:** No unwanted test output!

---

**But we can still run calculator.py directly:**

```bash
$ python calculator.py
```

**Output:**
```
Testing calculator...
2 + 3 = 5
5 - 2 = 3
```

