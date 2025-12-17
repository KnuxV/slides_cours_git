---
title: Python Arguments (argv & argparse)
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

## Command-Line Arguments

Making scripts interactive through the terminal

---

## What are CLI Arguments?

**Pass information to your script when you run it:**
```bash
$ python script.py input.txt --verbose --output result.txt
              ↑          ↑            ↑          ↑
           argument   argument    argument   argument
```

**Why?**
- Reusable scripts without hardcoding values
- Automation-friendly (can be scripted)
- Professional tool behavior

---

## Two Approaches

**1. `sys.argv`** - Basic, manual parsing
- Simple list of arguments
- Everything is a string
- You handle all the logic

**2. `argparse`** - Professional, automatic
- Built-in help messages
- Type conversion
- Error handling
- The standard way

---

## sys.argv - The Basics
```python
# script.py
import sys

print(f"Script name: {sys.argv[0]}")
print(f"First argument: {sys.argv[1]}")
print(f"All arguments: {sys.argv[1:]}")
```

**Running it:**
```bash
$ python script.py hello world
Script name: script.py
First argument: hello
All arguments: ['hello', 'world']
```

---

## sys.argv - Simple Example
```python
# greet.py
import sys

if len(sys.argv) < 2:
    print("Usage: python greet.py <name>")
    sys.exit(1)

name = sys.argv[1]
print(f"Hello, {name}!")
```

**Usage:**
```bash
$ python greet.py Alice
Hello, Alice!

$ python greet.py
Usage: python greet.py <name>
```

---

## Problem with sys.argv

**Gets messy quickly:**
- No automatic help
- Manual type conversion
- Manual error checking
- Hard to add optional flags
```python
# This becomes complicated fast...
if len(sys.argv) > 2 and sys.argv[2] == '--loud':
    # ...
```

**Solution:** Use `argparse`!

---

## argparse - The Better Way
```python
import argparse

# 1. Create parser
parser = argparse.ArgumentParser(description='Greet someone')

# 2. Define arguments
parser.add_argument('name', help='Person to greet')
parser.add_argument('--loud', action='store_true', 
                    help='Greet loudly')

# 3. Parse
args = parser.parse_args()

# 4. Use
greeting = f"Hello, {args.name}!"
if args.loud:
    greeting = greeting.upper()
print(greeting)
```

---

**Free features:**
```bash
$ python greet.py --help
usage: greet.py [-h] [--loud] name

Greet someone

positional arguments:
  name        Person to greet

optional arguments:
  -h, --help  show this help message and exit
  --loud      Greet loudly
```
```bash
$ python greet.py Alice
Hello, Alice!

$ python greet.py Bob --loud
HELLO, BOB!
```

---

## argparse - Types of Arguments

**Positional (required):**
```python
parser.add_argument('filename')
# Usage: python script.py data.txt
```

**Optional flag (boolean):**
```python
parser.add_argument('--verbose', action='store_true')
# Usage: python script.py --verbose
```

**Optional with value:**
```python
parser.add_argument('--output', type=str)
# Usage: python script.py --output result.txt
```

---

## argparse - Type Conversion
```python
parser.add_argument('--count', type=int, default=10)
parser.add_argument('--ratio', type=float)
parser.add_argument('--format', 
                    choices=['json', 'csv', 'xml'],
                    default='json')
```

**Usage:**
```bash
$ python script.py --count 5 --format csv
```

Automatic validation:
```bash
$ python script.py --count hello
error: argument --count: invalid int value: 'hello'
```

---

## Complete Example
```python
import argparse

def main():
    parser = argparse.ArgumentParser(
        description='Process a file'
    )
    
    # Required
    parser.add_argument('input_file', 
                        help='File to process')
    
    # Optional
    parser.add_argument('-o', '--output',
                        help='Output file')
    parser.add_argument('-v', '--verbose',
                        action='store_true',
                        help='Verbose output')
    parser.add_argument('--format',
                        choices=['json', 'csv'],
                        default='json')
    
    args = parser.parse_args()
    
    # Use the arguments
    print(f"Processing {args.input_file}")
    if args.verbose:
        print(f"Output format: {args.format}")
    # ... rest of logic

if __name__ == "__main__":
    main()
```

---

## Common Patterns


**Short + long options:**
```python
parser.add_argument('-o', '--output')  # Both work
args = parser.parse_args()
# args.output

```

**Default values:**
```python
parser.add_argument('--port', type=int, default=8080,
                    help='Port (default: %(default)s)')
```

---

## Key Takeaways

✅ Use `sys.argv` for **very simple** scripts (1-2 arguments)

✅ Use `argparse` for **everything else**

✅ `argparse` gives you:
- Automatic `--help`
- Type conversion
- Error messages
- Clean, readable code

📚 **Full guide:** [Link to complete class notes]

---

## Practice Exercise

**Create `counter.py`:**
- Takes a filename as required argument
- Has `--word` flag to count words (default: count lines)
- OR '--method' with a choices=['words', 'lines']
```bash
$ python counter.py data.txt
100 lines

$ python counter.py data.txt --word 
Counting words in data.txt
Total: 1523 words

$ python counter.py myfile.txt --method words
Total: 100 words
```
