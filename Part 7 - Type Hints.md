---
title: Python Type Hints
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

# Python Type Hints

Making your code clearer

---

## Type Systems: The Spectrum

**Strong vs Weak Typing**
- Strong: Can't mix types freely
- Weak: Loose type coercion

**Static vs Dynamic Typing**
- Static: Types checked at compile time
- Dynamic: Types checked at runtime

---

## Examples: JavaScript (Weak + Dynamic)

```javascript
// Weak typing = implicit conversions
"5" + 3        // "53" (string)
"5" - 3        // 2 (number) 🤔

// Dynamic typing = runtime checks
let x = 5;
x = "hello";   // No problem!
```

Type chaos! 😱

---

## Examples: Java (Strong + Static)

```java
// Strong typing = no implicit conversions
String text = "5";
int num = 3;
// text + num;  // ERROR at compile time!

// Static typing = must declare types
int x = 5;
x = "hello";  // ERROR at compile time!
```

Compiler catches errors early ✓

---

## Python: Strong + Dynamic

```python
# Strong typing = types don't mix freely
"5" + 3  # TypeError at runtime!

# Dynamic typing = no declarations needed
x = 5
x = "hello"  # Totally fine!
type(x)      # <class 'str'>
```

Best of both worlds... kind of?

---

## Python's Type System

```python
# Variables have no type
x = 5
x = "hello"
x = [1, 2, 3]  # All fine!

# But OBJECTS have types
type(5)         # <class 'int'>
type("hello")   # <class 'str'>
type([1, 2])    # <class 'list'>

# Strong typing enforced at runtime
5 + "hello"     # TypeError!
```

---

## The Problem

```python
def process_data(data):
    return data.upper()

process_data("hello")  # Works!
process_data(42)       # Runtime error! 💥
```

<hr>

What does this function expect? 🤷

No way to know without:
- Reading the code
- Reading docs
- Trial and error

---

## The Solution: Type Hints

```python
def process_data(data: str) -> str:
    return data.upper()

process_data("hello")  # Clear expectations!
process_data(42)       # IDE warns you!
```

Type hints are **documentation** + **tooling support**

---

## Important: Hints Don't Enforce!

```python
def add(a: int, b: int) -> int:
    return a + b

# This still runs! 🤯
result = add("hello", "world")
print(result)  # "helloworld"
```

Python **ignores** type hints at runtime

Use `mypy` if you want to force it.

---

## Basic Type Hints: Variables

```python
# Simple types
name: str = "Alice"
age: int = 25
height: float = 1.75
is_student: bool = True

# Collections
numbers: list = [1, 2, 3]
coords: tuple = (10, 20)
user: dict = {"name": "Bob"}
```

---

## Basic Type Hints: Functions

```python
def greet(name: str) -> str:
    return f"Hello, {name}!"

def add(a: int, b: int) -> int:
    return a + b

def print_items(items: list) -> None:
    for item in items:
        print(item)
```

`-> None` for functions that don't return anything

---

## Generic Collections (Python 3.9+)

```python
# List of specific type
numbers: list[int] = [] # Empty, but we know we want int
names: list[str] = [] # same for str

# Dict with key and value types
scores: dict[str, int] = {"Alice": 95, "Bob": 87}

```

---

## Union Types: The Pipe `|`

```python
# Can be int OR float
def process(value: int | float) -> str:
    return f"Value is {value}"

# Can be str OR None
name: str | None = None
name = "Alice"

# Multiple options
result: int | float | str = 42
```

The `|` means "or" - available in Python 3.10+

---

## Optional Values

```python
# These are equivalent:
name: str | None = None
name: Optional[str] = None  # Older style

def find_user(id: int) -> dict | None:
    # Might return a dict, might return None
    if id > 0:
        return {"id": id, "name": "User"}
    return None
```

---

## Practical Example

```python
def calculate_average(numbers: list[float]) -> float:
    return sum(numbers) / len(numbers)

def format_name(
    first: str,
    last: str,
    middle: str | None = None
) -> str:
    if middle:
        return f"{first} {middle} {last}"
    return f"{first} {last}"

# Clear what to pass!
avg = calculate_average([1.5, 2.3, 3.7])
name = format_name("John", "Doe")
```

---

## Why Use Type Hints?

**Better IDE support** - autocomplete, errors

**Self-documenting** - clear what's expected

**Catch bugs early** - with mypy/pyright

**Easier refactoring** - know what breaks


---

## Checking Types: mypy

```bash
pip install mypy

# Check your code
mypy script.py
```

```python
# script.py
def add(a: int, b: int) -> int:
    return a + b

result = add("5", "3")  # mypy catches this!
```

---

## Advanced Types: Iterable

```python
from collections.abc import Iterable

def sum_all(items: Iterable[int]) -> int:
    """Works with list, tuple, set, generator..."""
    return sum(items)

# All of these work!
sum_all([1, 2, 3])           # list
sum_all((1, 2, 3))           # tuple
sum_all({1, 2, 3})           # set
sum_all(range(1, 4))         # range
sum_all(x for x in [1,2,3])  # generator
```

`Iterable` = anything you can loop over

---

## Advanced Types: Callable

```python
from collections.abc import Callable

def apply_twice(
    func: Callable[[int], int],
    value: int
) -> int:
    """Apply a function twice."""
    return func(func(value))

def double(x: int) -> int:
    return x * 2

result = apply_twice(double, 5)  # 20
```

`Callable[[arg_types], return_type]`

---

## Using Classes as Types

```python
class User:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age
    
def count_young_user(lst_user: list[User]) -> int:
    return len([user for user in lst_user if user.age < 20])


# Create instances
alice:User = User("Alice", 25) #useless here
bob = User("Bob", 36)
tot_younsters = count_young_user([alice, bob])  
```