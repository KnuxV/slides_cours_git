---
title: Pytest
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

## Why Unit Testing Matters

---


**1. Catches Bugs Early**
- Fix bugs when they're cheap (development) vs. expensive (production)
- Verify individual pieces work before integration
- Fewer surprises, less firefighting  

---

**2. Supports Confident Refactoring**
- Change code without fear of breaking things
- Tests act as a safety net
- Essential for maintaining clean code over time

---

**3. Improves Code Quality**
- Forces you to think about design and edge cases
- Encourages modular, testable code
- Better structure leads to better maintainability

---

**4. Speeds Up Debugging**
- Failed test tells you exactly what broke and where
- No need to trace through entire application
- Targeted feedback = faster fixes

**5. Documents Expected Behavior**
- Tests show how functions should behave
- Live documentation that never gets outdated
- New team members learn from tests

**6. Essential for Automation and CI/CD**
- Foundation of continuous integration pipelines
- Automated quality gates prevent broken code from shipping
- Industry standard in modern development

**7. Reduces Technical Debt**
- Short-term time savings from skipping tests = long-term pain
- Stable foundation supports growth
- Maintainable codebase over time

---

## What is pytest?

**Most popular Python testing framework**

**Why pytest over unittest (built-in)?**
- ✅ Simple: Just use `assert` (no `self.assertEqual()`)
- ✅ Powerful: Fixtures, parametrization, plugins
- ✅ Clear: Better error messages
- ✅ Flexible: Works with any Python code

**Installation:**
```bash
pip install pytest
```

**Basic usage:**
```bash
pytest                    # Run all tests
pytest -v                 # Verbose output
pytest test_file.py       # Run specific file
```

---

## Test Discovery

**pytest automatically finds tests:**

**Naming conventions:**
- Test files: `test_*.py` or `*_test.py`
- Test functions: `def test_*()`
- Test classes: `class Test*`

**Directory structure:**
```
project/
├── main.py
├── data/
│   └── sample.csv
├── tests/
│   ├── __init__.py          # Makes it a package
│   ├── test_mymodule.py
│   └── conftest.py          # Shared fixtures
└── README.md
```

**Run from project root:**
```bash
pytest tests/
```

---

## Writing Your First Test

**Anatomy of a test:**
```python
# tests/test_calculator.py

def add(a, b):
    return a + b

def test_add_positive_numbers():
    result = add(2, 3)
    assert result == 5

def test_add_negative_numbers():
    result = add(-1, -1)
    assert result == -2
```

**Key points:**
1. Import the function you're testing
2. Test function name starts with `test_`
3. Use plain Python `assert`
4. One logical assertion per test (usually)

---

## Understanding assert

**assert is Python's built-in testing tool:**
```python
assert expression, "Optional error message"
```

**If the expression is `False`, Python raises an `AssertionError` and the test fails.**

---

**Common assertions:**
```python
# Equality
assert result == 5
assert result != 0

# Type checking
assert isinstance(result, list)
assert type(result) is int

# Boolean
assert result is True
assert result is not None

# Membership
assert 'x' in result
assert 10 not in result

# Comparisons
assert len(result) > 0
assert result >= 5
```

---

## pytest's Enhanced assert

**pytest shows detailed failure information:**
```python
def test_string_comparison():
    expected = "Hello, World!"
    actual = "Hello, world!"
    assert expected == actual
```

**Output:**
```
>   assert expected == actual
E   AssertionError: assert 'Hello, World!' == 'Hello, world!'
E     - Hello, World!
E     ?        ^
E     + Hello, world!
E     ?        ^
```

---

## Structure Your Test Cases Clearly

**Good test structure (Arrange-Act-Assert):**
```python
def test_calculate_discount():
    # Arrange: Set up test data
    original_price = 100
    discount_percent = 20
    
    # Act: Execute the function
    result = calculate_discount(original_price, discount_percent)
    
    # Assert: Verify the result
    assert result == 80
```


---

## Keep Tests Independent

**Each test should run in isolation:**

❌ **Bad: Tests depend on each other**
```python
total = 0  # Shared state!

def test_increment():
    global total
    total += 1
    assert total == 1

def test_increment_again():
    global total
    total += 1
    assert total == 2  # Fails if test_increment doesn't run first!
```


---

## Test Edge Cases and Exceptions

**Don't just test the happy path:**
```python
def divide(a, b):
    return a / b

# Happy path
def test_divide_positive():
    assert divide(10, 2) == 5

# Edge cases
def test_divide_by_one():
    assert divide(10, 1) == 10

def test_divide_zero():
    assert divide(0, 5) == 0

# Exception handling
def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(10, 0)
```

---

**Think about:**
- Empty inputs (`[]`, `""`, `None`)
- Boundary values (0, -1, max int)
- Invalid inputs
- Errors that should be raised

---

## pytest.raises() for Exceptions

**Testing that code raises expected errors:**
```python
import pytest

def validate_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    return age

def test_negative_age_raises_error():
    with pytest.raises(ValueError) as exc_info:
        validate_age(-5)
    

```

---

## Parametrized Tests

**Problem: Testing multiple similar cases**

❌ **Repetitive:**
```python
def test_is_even_2():
    assert is_even(2) is True

def test_is_even_4():
    assert is_even(4) is True

def test_is_even_100():
    assert is_even(100) is True
```

---

✅ **Parametrized:**
```python
@pytest.mark.parametrize("number,expected", [
    (2, True),
    (4, True),
    (100, True),
    (3, False),
    (99, False),
    (0, True),
])
def test_is_even(number, expected):
    assert is_even(number) == expected
```

---

## Parametrize Syntax

**Basic structure:**
```python
@pytest.mark.parametrize("param_names", [
    (value1, value2, ...),
    (value1, value2, ...),
])
def test_function(param_names):
    # Test logic
```

---

**Multiple parameters:**
```python
@pytest.mark.parametrize("input,expected", [
    ("hello", 5),
    ("", 0),
    ("test", 4),
])
def test_string_length(input, expected):
    assert len(input) == expected
```

**Each tuple becomes a separate test case**

---

## Parametrize Output

**Running parametrized tests:**
```bash
pytest test_file.py -v
```

**Output:**
```
test_is_even[2-True] PASSED
test_is_even[4-True] PASSED
test_is_even[100-True] PASSED
test_is_even[3-False] PASSED
test_is_even[99-False] PASSED
test_is_even[0-True] PASSED
```

---

## Introduction to Fixtures

**Fixtures provide reusable setup code:**
```python
import pytest

@pytest.fixture
def sample_data():
    """Setup: Create test data"""
    data = [1, 2, 3, 4, 5]
    return data

def test_sum(sample_data):
    assert sum(sample_data) == 15

def test_length(sample_data):
    assert len(sample_data) == 5

def test_max(sample_data):
    assert max(sample_data) == 5
```

---

**How it works:**
1. pytest sees `sample_data` parameter in test
2. Calls the `@pytest.fixture` function
3. Passes returned value to test
4. Runs cleanup after test (if needed)

---

## Fixture Benefits

**Why use fixtures?**

✅ **Reduce duplication:**
- Setup code written once, used everywhere
- No copy-paste across tests

✅ **Isolation:**
- Each test gets fresh data
- No shared state between tests

---

✅ **Clarity:**
- Setup logic separated from test logic
- Test functions stay focused

✅ **Automatic cleanup:**
- Resources cleaned up after test
- No manual teardown needed

---

## Built-in Fixture: tmp_path

**pytest provides useful fixtures automatically:**
```python
def test_file_operations(tmp_path):
    """
    tmp_path: Provides a unique temporary directory
    for this test. Automatically cleaned up after test.
    """
    # Create a file
    test_file = tmp_path / "test.txt"
    with open(test_file, "w") as f:
        f.write("Hello, pytest!")
    
    # Read it back
    with open(test_file, "r") as f:
        content = f.read()
    
    assert content == "Hello, pytest!"
    
    # No cleanup needed - pytest does it automatically
```

---

## Other Useful Built-in Fixtures

**capsys - Capture stdout/stderr:**
```python
def test_print_output(capsys):
    print("Hello!")
    captured = capsys.readouterr()
    assert "Hello!" in captured.out
```


---


## Running Tests: Essential Commands
```bash
# Run all tests
pytest

# Verbose output (show each test name)
pytest -v

# Very verbose (show print statements)
pytest -vv -s

# Run specific file
pytest tests/test_mymodule.py

# Run specific test
pytest tests/test_mymodule.py::test_function_name

# Run tests matching pattern
pytest -k "calculate"

# Stop at first failure
pytest -x

# Show local variables on failure
pytest -l
```

---

## Test Organization Best Practices

**Recommended structure:**
```
project/
├── main.py
├── data/
│   └── sample.csv
├── tests/
│   ├── __init__.py              # Important!
│   ├── test_mymodule.py
│   └── conftest.py              # Shared fixtures
├── pytest.ini                    # Optional config
└── README.md
```

---

**Key points:**
- `tests/__init__.py` makes it a package
- `conftest.py` for shared fixtures
- Run `pytest` from project root
- Separate unit tests from integration tests

---

## conftest.py for Shared Fixtures

**tests/conftest.py:**
```python
import pytest

@pytest.fixture
def common_data():
    """Available to all tests in tests/ directory"""
    return {"key": "value"}

@pytest.fixture
def temp_csv(tmp_path):
    """Create a temporary CSV for testing"""
    csv_file = tmp_path / "test.csv"
    with open(csv_file, "w", encoding="utf-8") as f:
        f.write("col1,col2\n")
        f.write("1,2\n")
    return csv_file
```

---

## Test Coverage

**Measure how much code is tested:**
```bash
# Install coverage plugin
pip install pytest-cov

# Run tests with coverage
pytest --cov=main

# Generate HTML report
pytest --cov=main --cov-report=html

# Open htmlcov/index.html in browser
```

**Coverage shows:**
- Which lines were executed during tests
- Which branches were taken
- Percentage of code covered

---


## Hands-On Practice

**Clone the repository:**
```bash
git clone https://gitlab.unistra.fr/cours_test/intro_test
cd intro_test
```
**Your tasks:**
1. Run the existing tests (`pytest -v`)
2. Fix `test_negative_numbers.py`
3. Complete `test_get_list_no_dates.py`
4. Add your own test cases

**See README.md for detailed instructions**

---


## Exercise 2: Test-Driven Development (TDD)

**Clone the repository:**
```bash
git clone https://gitlab.unistra.fr/cours_test/testing_username_password
cd testing_username_password
```

**Your mission: Build validators from scratch using TDD**

**The TDD cycle:**
1. 🔴 **RED** - Write a failing test first
2. 🟢 **GREEN** - Write minimal code to make it pass
3. 🔵 **REFACTOR** - Clean up (tests still passing)

**Two functions to implement:**
- `is_password_strong(password: str) -> bool`
- `is_email_valid(email: str) -> bool`

**Start with behavior, then test, then implement!**

See `README.md` for detailed requirements and step-by-step guide.

---

## Exercise 3: Real-World Project Testing

**Continue with the class project:**
```bash
https://github.com/KnuxV/nlp-steamlit-app
```

**Your mission: Add tests to existing codebase**

**Tasks:**
- Add new features
- Add the corresponding tests

**This is collaborative:**
- Work together
- One can do the function
- One can do the test

**Resources:**
- pytest documentation: https://docs.pytest.org/
- Repository README for detailed tasks
- Ask your instructor for help