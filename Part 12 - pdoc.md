---
title: Python Documentation with pdoc
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

## Documentation with pdoc

Auto-generate API documentation from your docstrings

---

## The Concept

**pdoc reads docstrings → generates HTML documentation**

```python
def greet(name: str) -> str:
    """Say hello to someone."""
    return f"Hello {name}!"
```

↓

Beautiful HTML documentation automatically!

**Why?**
- No manual documentation writing
- Always in sync with code
- Professional-looking output

---

## What are Docstrings?

**Special strings that document your code:**
```python
def calculate_tax(amount: float, rate: float) -> float:
    """
    Calculate tax on an amount.
    
    Args:
        amount: The base amount
        rate: Tax rate as decimal (e.g., 0.2 for 20%)
    
    Returns:
        The tax amount
    """
    return amount * rate
```

The string right after the definition = docstring

---

## Where to Add Docstrings

**1. Module level** (top of file):
```python
"""
This module handles user authentication.
Provides login, logout, and password functions.
"""
import bcrypt
```

**2. Functions:**
```python
def login(username: str) -> bool:
    """Check if user credentials are valid."""
```

**3. Classes:**
```python
class User:
    """Represents a user account."""
```

---

## Variable Docstrings

**Module-level variables:**
```python
MAX_RETRIES = 3
"""Maximum number of connection attempts."""
```

**Class attributes:**
```python
class Config:
    timeout: int = 30
    """Request timeout in seconds."""
```

**Instance variables:**
```python
def __init__(self):
    self.count: int = 0
    """Number of processed items."""
```

---

## Installing & Using pdoc

**Install:**
```bash
pip install pdoc
```

**Generate docs (live preview):**
```bash
pdoc your_module.py
# Opens browser with auto-reload
```

**Save to HTML:**
```bash
pdoc your_module.py -o ./docs
# Creates docs/your_module.html
```

---

## Complete Example

```python
"""
Calculator module for basic math operations.
"""

def add(a: float, b: float) -> float:
    """
    Add two numbers.
    
    Args:
        a: First number
        b: Second number
    
    Returns:
        Sum of a and b
    """
    return a + b

def divide(a: float, b: float) -> float:
    """
    Divide two numbers.
    
    Raises:
        ZeroDivisionError: If b is zero
    """
    if b == 0:
        raise ZeroDivisionError("Cannot divide by zero")
    return a / b
```

---

## What You Get

✅ Clean HTML pages  
✅ Automatic cross-linking between functions/classes  
✅ Mobile-friendly design  
✅ Built-in search functionality  
✅ Live reload during development  
✅ Markdown support in docstrings  

---

## Markdown in Docstrings

**You can use Markdown formatting:**
```python
def process_data(data: list) -> dict:
    """
    Process input data.
    
    This function:
    - Validates input
    - Transforms data  
    - Returns **summary**
    
    Example:
    ```python
    result = process_data([1, 2, 3])
    ```
    
    See `validate()` for validation details.
    """
    pass
```
---

## The Workflow

```
1. Write your code
     ↓
2. Add docstrings
     ↓
3. Run: pdoc your_module.py
     ↓
4. Preview in browser
     ↓
5. Export: pdoc your_module.py -o ./docs
```

---


## Practice Exercise

**Create `calculator.py` with:**
- Module docstring explaining what it does
- Two functions: `add()` and `multiply()`
- Each function has a docstring with Args and Returns
- Run `pdoc calculator.py` to see the result

**Bonus:** Add a `Calculator` class with docstrings