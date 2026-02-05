# Appendix A: Python Quick Reference

## Data Types
| Type | Mutable | Example |
|------|---------|---------|
| `int` | No | `42`, `0xFF`, `0b1010` |
| `float` | No | `3.14`, `1e-5` |
| `complex` | No | `3+4j` |
| `str` | No | `"hello"`, `'world'` |
| `bytes` | No | `b"data"` |
| `bytearray` | Yes | `bytearray(b"data")` |
| `list` | Yes | `[1, 2, 3]` |
| `tuple` | No | `(1, 2, 3)` |
| `set` | Yes | `{1, 2, 3}` |
| `frozenset` | No | `frozenset({1, 2})` |
| `dict` | Yes | `{"a": 1, "b": 2}` |
| `bool` | No | `True`, `False` |
| `None` | No | `None` |

## Common Operators
```python
# Arithmetic
+, -, *, /, //, %, **
# Comparison
==, !=, <, >, <=, >=
# Logical
and, or, not
# Bitwise
&, |, ^, ~, <<, >>
# Identity/Membership
is, is not, in, not in
# Assignment (augmented)
+=, -=, *=, /=, //=, **=, &=, |=, ^=
# Walrus operator (3.8+)
:= (assignment expression)
```

## String Methods
```python
s.upper()      # "HELLO"
s.lower()      # "hello"
s.strip()      # Remove whitespace
s.split()      # Split to list
s.join(list)   # Join from list
s.replace(a,b) # Replace a with b
s.startswith() # Check prefix
s.endswith()   # Check suffix
s.find()       # Find index (-1 if not found)
s.count()      # Count occurrences
f"{var}"       # f-string formatting
```

## List/Dict/Set Comprehensions
```python
# List comprehension
[x**2 for x in range(10)]
[x for x in items if x > 0]

# Dict comprehension
{k: v for k, v in pairs}
{x: x**2 for x in range(5)}

# Set comprehension
{x for x in items if x > 0}

# Generator expression
(x**2 for x in range(10))
```

## Control Flow
```python
# If/elif/else
if condition:
    pass
elif other:
    pass
else:
    pass

# For loop
for item in iterable:
    pass

for i, item in enumerate(items):
    pass

for key, value in d.items():
    pass

# While loop
while condition:
    pass

# Match statement (3.10+)
match value:
    case pattern1:
        pass
    case pattern2:
        pass
```

## Functions
```python
def func(a, b, *args, **kwargs):
    """Docstring."""
    return result

# Lambda
lambda x: x * 2

# Default values
def func(x, y=10):
    pass

# Type hints
def func(x: int, y: str = "default") -> bool:
    pass
```

## Classes
```python
class MyClass:
    class_attr = "shared"
    
    def __init__(self, value):
        self.value = value
    
    def method(self):
        return self.value
    
    @classmethod
    def from_string(cls, s):
        return cls(int(s))
    
    @staticmethod
    def helper():
        pass
    
    @property
    def computed(self):
        return self.value * 2
```

## Exception Handling
```python
try:
    risky_operation()
except ValueError as e:
    handle_error(e)
except (TypeError, KeyError):
    handle_multiple()
else:
    success_only()
finally:
    always_run()

# Raise exceptions
raise ValueError("message")
raise CustomError() from original
```

## Context Managers
```python
with open("file.txt") as f:
    data = f.read()

with resource1 as r1, resource2 as r2:
    use(r1, r2)

# Custom context manager
@contextmanager
def my_context():
    setup()
    try:
        yield value
    finally:
        cleanup()
```

## File I/O
```python
# Reading
with open("file.txt", "r", encoding="utf-8") as f:
    content = f.read()
    lines = f.readlines()
    for line in f:
        process(line)

# Writing
with open("file.txt", "w", encoding="utf-8") as f:
    f.write("content")

# Modes: r, w, a, x, r+, w+, rb, wb
```

## Common Built-ins
```python
len(x)          # Length
type(x)         # Type
isinstance(x,T) # Type check
range(n)        # Range object
enumerate(x)    # Index-value pairs
zip(a, b)       # Combine iterables
map(f, x)       # Apply function
filter(f, x)    # Filter by predicate
sorted(x)       # Sorted copy
reversed(x)     # Reversed iterator
sum(x)          # Sum
min(x), max(x)  # Min/max
any(x), all(x)  # Boolean tests
abs(x)          # Absolute value
round(x, n)     # Round to n decimals
```

## Common Imports
```python
import os                  # OS interface
import sys                 # System-specific
import json                # JSON handling
import datetime            # Date/time
import re                  # Regex
import collections         # Specialized containers
import itertools           # Iteration tools
import functools           # Higher-order functions
import pathlib             # Path handling
import logging             # Logging
import unittest            # Testing
import typing              # Type hints
```

## Decorators
```python
@decorator
def func():
    pass

# Common decorators
@staticmethod
@classmethod
@property
@functools.lru_cache()
@contextlib.contextmanager
@dataclass

# Creating decorators
def decorator(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        # before
        result = func(*args, **kwargs)
        # after
        return result
    return wrapper
```

## Generators
```python
def generator():
    yield 1
    yield 2
    yield 3

# Usage
for value in generator():
    print(value)

next(gen)  # Get next value

# Generator expression
gen = (x**2 for x in range(10))
```

## Async/Await
```python
async def async_func():
    result = await some_coroutine()
    return result

# Running
asyncio.run(async_func())

# Concurrent execution
results = await asyncio.gather(
    coro1(),
    coro2(),
    coro3()
)
```

## Testing
```python
# unittest
import unittest

class TestCase(unittest.TestCase):
    def test_something(self):
        self.assertEqual(a, b)
        self.assertTrue(condition)
        self.assertRaises(Error, func)

# pytest
def test_something():
    assert a == b

@pytest.fixture
def data():
    return setup_data()
```

## Virtual Environments
```bash
# Create
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Unix)
source venv/bin/activate

# Install packages
pip install package
pip install -r requirements.txt

# Freeze
pip freeze > requirements.txt
```

## Type Hints (typing module)
```python
from typing import (
    List, Dict, Set, Tuple,
    Optional, Union, Any,
    Callable, Generator,
    TypeVar, Generic
)

x: List[int]
x: Dict[str, int]
x: Optional[str]  # str | None
x: Union[int, str]
x: Callable[[int], str]

T = TypeVar('T')
def first(items: List[T]) -> T:
    return items[0]
```
