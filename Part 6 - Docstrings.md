---
title: Python Docstrings
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
</style>

# Python Docstrings

Document your code!

---

## What's a Docstring?

A string literal right after a function/class/module definition

```python
def add(a, b):
    """Add two numbers together."""
    return a + b
```

Access with `help()` or `.__doc__`

---

## Basic Format

```python
def greet(name):
    """
    Greet a person by name.
    
    Args:
        name: The person's name
        
    Returns:
        A greeting string
    """
    return f"Hello, {name}!"
```

---

## Different Styles

**Google Style:**
```python
def func(arg1, arg2):
    """Summary line.
    
    Args:
        arg1: Description
        arg2: Description
        
    Returns:
        Description
    """
```

---

**NumPy Style:**
```python
def func(arg1, arg2):
    """Summary line.
    
    Parameters
    ----------
    arg1 : type
        Description
    arg2 : type
        Description
        
    Returns
    -------
    type
        Description
    """
```

---

- Pick one, be consistent!  
- You IDE (pycharm, vscharm) can pre-generate for you  
- AI is a good use for this

---

## Why Docstrings?

- Your future self will thank you
- Others can understand your code
- IDEs can show hints
- Auto-generate documentation

```python
help(greet)  # Shows your docstring!
print(greet.__doc__)
```



