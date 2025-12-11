# Python Comprehensive Cheatsheet

> Quick reference for all Python concepts covered in the curriculum

---

## Table of Contents
1. [Core Syntax](#1-core-syntax)
2. [Data Types](#2-data-types)
3. [Control Flow](#3-control-flow)
4. [Functions](#4-functions)
5. [Object-Oriented Programming](#5-object-oriented-programming)
6. [File Operations](#6-file-operations)
7. [Exception Handling](#7-exception-handling)
8. [Modules & Packages](#8-modules--packages)
9. [Decorators & Generators](#9-decorators--generators)
10. [Regular Expressions](#10-regular-expressions)
11. [Concurrency](#11-concurrency)
12. [NumPy](#12-numpy)
13. [Pandas](#13-pandas)
14. [Data Visualization](#14-data-visualization)
15. [Machine Learning](#15-machine-learning)
16. [Web Development](#16-web-development)
17. [Testing](#17-testing)
18. [Best Practices](#18-best-practices)

---

## 1. Core Syntax

### Variables & Assignment
```python
# Variable assignment
x = 10
name = "Python"
is_valid = True

# Multiple assignment
a, b, c = 1, 2, 3
x = y = z = 0

# Swap values
a, b = b, a

# Type annotations (Python 3.5+)
count: int = 0
name: str = "Python"
values: list[int] = [1, 2, 3]
```

### Operators
```python
# Arithmetic
+  -  *  /  //  %  **
# // = floor division, % = modulo, ** = power

# Comparison
==  !=  <  >  <=  >=

# Logical
and  or  not

# Bitwise
&  |  ^  ~  <<  >>

# Membership
in  not in

# Identity
is  is not

# Walrus operator (Python 3.8+)
if (n := len(data)) > 10:
    print(f"Too long: {n}")
```

---

## 2. Data Types

### Numbers
```python
# Integer
x = 42
binary = 0b1010      # 10
octal = 0o12         # 10
hexadecimal = 0xFF   # 255

# Float
pi = 3.14159
scientific = 1.5e-10

# Complex
z = 3 + 4j
z.real  # 3.0
z.imag  # 4.0

# Decimal (precise)
from decimal import Decimal
price = Decimal('19.99')
```

### Strings
```python
# Creation
s = "Hello"
s = 'World'
s = """Multiline
string"""

# f-strings (Python 3.6+)
name = "Python"
f"Hello, {name}!"
f"{value:.2f}"       # format float
f"{number:,}"        # thousands separator
f"{text:>10}"        # right align
f"{text:<10}"        # left align
f"{text:^10}"        # center

# Common Methods
s.upper()            # "HELLO"
s.lower()            # "hello"
s.strip()            # remove whitespace
s.split(",")         # split to list
",".join(["a","b"])  # join to string
s.replace("a", "b")  # replace
s.find("sub")        # index or -1
s.startswith("He")   # True/False
s.endswith("lo")     # True/False
s.isdigit()          # all digits?
s.isalpha()          # all letters?

# Slicing
s[0]      # first char
s[-1]     # last char
s[1:4]    # slice
s[::2]    # every 2nd char
s[::-1]   # reverse
```

### Lists
```python
# Creation
lst = [1, 2, 3]
lst = list(range(10))

# Access
lst[0]              # first
lst[-1]             # last
lst[1:3]            # slice

# Methods
lst.append(4)       # add end
lst.extend([5,6])   # add multiple
lst.insert(0, 0)    # add at index
lst.remove(2)       # remove first occurrence
lst.pop()           # remove & return last
lst.pop(0)          # remove & return at index
lst.index(3)        # find index
lst.count(2)        # count occurrences
lst.sort()          # sort in-place
lst.reverse()       # reverse in-place
sorted(lst)         # return sorted copy
len(lst)            # length

# List Comprehension
[x**2 for x in range(10)]
[x for x in lst if x > 0]
[x if x > 0 else 0 for x in lst]
```

### Tuples
```python
# Creation (immutable)
t = (1, 2, 3)
t = 1, 2, 3
single = (1,)       # single element needs comma

# Unpacking
a, b, c = t
a, *rest = t        # a=1, rest=[2,3]
a, *middle, z = [1,2,3,4,5]

# Named Tuples
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(3, 4)
p.x, p.y

# typing.NamedTuple
from typing import NamedTuple
class Point(NamedTuple):
    x: float
    y: float
```

### Dictionaries
```python
# Creation
d = {'a': 1, 'b': 2}
d = dict(a=1, b=2)

# Access
d['a']              # KeyError if missing
d.get('a')          # None if missing
d.get('a', 0)       # default if missing

# Methods
d.keys()            # dict_keys
d.values()          # dict_values
d.items()           # dict_items (k,v pairs)
d.update({'c': 3})  # merge
d.pop('a')          # remove & return
d.setdefault('x', 0)  # get or set default

# Dict Comprehension
{k: v for k, v in items}
{x: x**2 for x in range(5)}

# DefaultDict
from collections import defaultdict
d = defaultdict(list)
d['key'].append(1)

# Counter
from collections import Counter
Counter(['a','a','b','c'])
# Counter({'a': 2, 'b': 1, 'c': 1})
```

### Sets
```python
# Creation
s = {1, 2, 3}
s = set([1, 2, 3])

# Methods
s.add(4)            # add element
s.remove(2)         # remove (KeyError if missing)
s.discard(2)        # remove (no error)
s.pop()             # remove arbitrary

# Operations
s1 | s2             # union
s1 & s2             # intersection
s1 - s2             # difference
s1 ^ s2             # symmetric difference
s1.issubset(s2)
s1.issuperset(s2)

# Set Comprehension
{x**2 for x in range(5)}
```

---

## 3. Control Flow

### Conditionals
```python
# if-elif-else
if condition:
    pass
elif other_condition:
    pass
else:
    pass

# Ternary operator
value = x if condition else y

# Match statement (Python 3.10+)
match command:
    case "quit":
        exit()
    case "hello" | "hi":
        print("Hello!")
    case ["go", direction]:
        move(direction)
    case {"action": action}:
        perform(action)
    case _:
        print("Unknown")
```

### Loops
```python
# For loop
for item in iterable:
    pass

for i, item in enumerate(lst):
    pass

for key, value in dict.items():
    pass

for a, b in zip(list1, list2):
    pass

# While loop
while condition:
    pass

# Loop control
break           # exit loop
continue        # next iteration

# For-else / While-else
for item in items:
    if found(item):
        break
else:
    print("Not found")  # runs if no break
```

### Comprehensions
```python
# List
[expr for item in iterable]
[expr for item in iterable if condition]
[expr1 if condition else expr2 for item in iterable]

# Dict
{key: value for item in iterable}

# Set
{expr for item in iterable}

# Generator (lazy)
(expr for item in iterable)

# Nested
[[j for j in range(3)] for i in range(3)]
[x for sublist in nested for x in sublist]  # flatten
```

---

## 4. Functions

### Basic Functions
```python
# Definition
def function_name(param1, param2):
    """Docstring"""
    return result

# Default arguments
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}"

# Keyword arguments
def func(a, b, *, c, d):  # c,d must be keyword
    pass

# *args and **kwargs
def func(*args, **kwargs):
    for arg in args:
        print(arg)
    for key, value in kwargs.items():
        print(f"{key}={value}")

# Unpack arguments
func(*[1, 2, 3])          # unpack list
func(**{'a': 1, 'b': 2})  # unpack dict
```

### Lambda Functions
```python
# Anonymous functions
square = lambda x: x**2
add = lambda x, y: x + y

# With built-ins
sorted(items, key=lambda x: x.name)
list(filter(lambda x: x > 0, numbers))
list(map(lambda x: x**2, numbers))
```

### Higher-Order Functions
```python
# map - apply function to each element
list(map(str.upper, words))

# filter - keep elements matching condition
list(filter(lambda x: x > 0, numbers))

# reduce - accumulate
from functools import reduce
reduce(lambda a, b: a + b, [1,2,3,4])  # 10

# sorted with key
sorted(students, key=lambda s: s.grade)
sorted(items, key=lambda x: (x.name, x.age))  # multi-key

# partial - pre-fill arguments
from functools import partial
double = partial(multiply, 2)
```

### Type Hints
```python
from typing import List, Dict, Optional, Union, Callable, Any

def greet(name: str) -> str:
    return f"Hello, {name}"

def process(items: List[int]) -> Dict[str, int]:
    pass

def maybe_value(x: Optional[str] = None) -> str:
    return x or "default"

def handler(callback: Callable[[int, int], int]) -> None:
    pass

# Type aliases
Vector = List[float]
def scale(v: Vector, factor: float) -> Vector:
    pass
```

---

## 5. Object-Oriented Programming

### Classes
```python
class Person:
    # Class variable
    species = "Human"
    
    def __init__(self, name: str, age: int):
        # Instance variables
        self.name = name
        self.age = age
        self._protected = "protected"
        self.__private = "private"
    
    def greet(self) -> str:
        return f"Hi, I'm {self.name}"
    
    @classmethod
    def from_birth_year(cls, name: str, year: int):
        return cls(name, 2024 - year)
    
    @staticmethod
    def is_adult(age: int) -> bool:
        return age >= 18
    
    @property
    def email(self) -> str:
        return f"{self.name.lower()}@example.com"
    
    @email.setter
    def email(self, value: str):
        self.name = value.split('@')[0]
    
    def __str__(self) -> str:
        return f"Person({self.name}, {self.age})"
    
    def __repr__(self) -> str:
        return f"Person(name={self.name!r}, age={self.age})"
```

### Inheritance
```python
class Animal:
    def __init__(self, name: str):
        self.name = name
    
    def speak(self) -> str:
        raise NotImplementedError

class Dog(Animal):
    def speak(self) -> str:
        return "Woof!"

class Cat(Animal):
    def speak(self) -> str:
        return "Meow!"

# Multiple inheritance
class FlyingCar(Car, Aircraft):
    def __init__(self):
        Car.__init__(self)
        Aircraft.__init__(self)
        # or use super() with MRO
```

### Abstract Base Classes
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        pass
    
    @abstractmethod
    def perimeter(self) -> float:
        pass

class Circle(Shape):
    def __init__(self, radius: float):
        self.radius = radius
    
    def area(self) -> float:
        return 3.14159 * self.radius ** 2
    
    def perimeter(self) -> float:
        return 2 * 3.14159 * self.radius
```

### Dataclasses
```python
from dataclasses import dataclass, field
from typing import List

@dataclass
class Product:
    name: str
    price: float
    quantity: int = 0
    tags: List[str] = field(default_factory=list)
    
    def total_value(self) -> float:
        return self.price * self.quantity

@dataclass(frozen=True)  # immutable
class Point:
    x: float
    y: float
```

### Magic Methods
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    # Representation
    def __str__(self): return f"({self.x}, {self.y})"
    def __repr__(self): return f"Vector({self.x}, {self.y})"
    
    # Comparison
    def __eq__(self, other): return self.x == other.x and self.y == other.y
    def __lt__(self, other): return self.magnitude() < other.magnitude()
    
    # Arithmetic
    def __add__(self, other): return Vector(self.x + other.x, self.y + other.y)
    def __sub__(self, other): return Vector(self.x - other.x, self.y - other.y)
    def __mul__(self, scalar): return Vector(self.x * scalar, self.y * scalar)
    def __neg__(self): return Vector(-self.x, -self.y)
    
    # Container
    def __len__(self): return 2
    def __getitem__(self, i): return (self.x, self.y)[i]
    def __iter__(self): yield self.x; yield self.y
    def __contains__(self, val): return val in (self.x, self.y)
    
    # Callable
    def __call__(self): return self.magnitude()
    
    # Context manager
    def __enter__(self): return self
    def __exit__(self, *args): pass
    
    # Hashing
    def __hash__(self): return hash((self.x, self.y))
```

---

## 6. File Operations

### Reading & Writing
```python
# Read entire file
with open('file.txt', 'r') as f:
    content = f.read()

# Read lines
with open('file.txt', 'r') as f:
    lines = f.readlines()  # list of lines

# Read line by line (memory efficient)
with open('file.txt', 'r') as f:
    for line in f:
        process(line.strip())

# Write
with open('file.txt', 'w') as f:  # overwrite
    f.write("Hello\n")

with open('file.txt', 'a') as f:  # append
    f.write("World\n")

# Binary
with open('file.bin', 'rb') as f:
    data = f.read()
```

### pathlib
```python
from pathlib import Path

# Create path
p = Path('/home/user/file.txt')
p = Path.cwd() / 'data' / 'file.txt'

# Properties
p.name          # 'file.txt'
p.stem          # 'file'
p.suffix        # '.txt'
p.parent        # Path('/home/user')
p.exists()
p.is_file()
p.is_dir()

# Operations
p.read_text()
p.write_text("content")
p.mkdir(parents=True, exist_ok=True)
list(p.glob('*.txt'))
list(p.rglob('*.py'))  # recursive
```

### JSON
```python
import json

# Read
with open('data.json') as f:
    data = json.load(f)

# Write
with open('data.json', 'w') as f:
    json.dump(data, f, indent=2)

# String conversion
json_str = json.dumps(data)
data = json.loads(json_str)
```

### CSV
```python
import csv

# Read
with open('data.csv') as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row['column_name'])

# Write
with open('data.csv', 'w', newline='') as f:
    writer = csv.DictWriter(f, fieldnames=['name', 'age'])
    writer.writeheader()
    writer.writerow({'name': 'Alice', 'age': 30})
```

---

## 7. Exception Handling

### Try-Except
```python
try:
    result = risky_operation()
except ValueError as e:
    print(f"Value error: {e}")
except (TypeError, KeyError) as e:
    print(f"Type or Key error: {e}")
except Exception as e:
    print(f"Unexpected: {e}")
    raise  # re-raise
else:
    print("No exception occurred")
finally:
    cleanup()
```

### Custom Exceptions
```python
class ValidationError(Exception):
    def __init__(self, message: str, field: str):
        super().__init__(message)
        self.field = field

raise ValidationError("Invalid email", field="email")
```

### Context Managers for Resources
```python
from contextlib import contextmanager

@contextmanager
def managed_resource():
    resource = acquire_resource()
    try:
        yield resource
    finally:
        release_resource(resource)

with managed_resource() as r:
    use(r)
```

---

## 8. Modules & Packages

### Imports
```python
# Import module
import math
math.sqrt(16)

# Import specific items
from math import sqrt, pi
sqrt(16)

# Import with alias
import numpy as np
from datetime import datetime as dt

# Import all (avoid)
from math import *

# Relative imports (in packages)
from . import sibling_module
from .. import parent_module
from .sibling import function
```

### Virtual Environments
```bash
# Create
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Unix)
source venv/bin/activate

# Install packages
pip install package_name
pip install -r requirements.txt

# Freeze
pip freeze > requirements.txt
```

---

## 9. Decorators & Generators

### Decorators
```python
# Basic decorator
def log_calls(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Returned: {result}")
        return result
    return wrapper

@log_calls
def add(a, b):
    return a + b

# Decorator with arguments
def repeat(times):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(times):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(times=3)
def greet(name):
    print(f"Hello, {name}!")

# Class decorator
def singleton(cls):
    instances = {}
    @functools.wraps(cls)
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance
```

### Generators
```python
# Generator function
def count_up(n):
    i = 0
    while i < n:
        yield i
        i += 1

# Use
for num in count_up(5):
    print(num)

# Generator expression
squares = (x**2 for x in range(10))

# Generator with send
def accumulator():
    total = 0
    while True:
        value = yield total
        if value is not None:
            total += value

acc = accumulator()
next(acc)           # start generator
acc.send(10)        # 10
acc.send(5)         # 15

# yield from
def chain(*iterables):
    for it in iterables:
        yield from it
```

### Context Managers
```python
# Class-based
class Timer:
    def __enter__(self):
        self.start = time.time()
        return self
    
    def __exit__(self, *args):
        self.elapsed = time.time() - self.start
        print(f"Elapsed: {self.elapsed:.2f}s")

with Timer() as t:
    slow_operation()

# contextlib
from contextlib import contextmanager

@contextmanager
def temp_directory():
    dirpath = tempfile.mkdtemp()
    try:
        yield dirpath
    finally:
        shutil.rmtree(dirpath)

# Suppress exceptions
from contextlib import suppress

with suppress(FileNotFoundError):
    os.remove('file.txt')
```

---

## 10. Regular Expressions

### Basics
```python
import re

# Match at beginning
re.match(r'pattern', string)

# Search anywhere
re.search(r'pattern', string)

# Find all
re.findall(r'pattern', string)

# Find all with groups
re.finditer(r'pattern', string)

# Replace
re.sub(r'pattern', 'replacement', string)

# Split
re.split(r'pattern', string)

# Compile for reuse
pattern = re.compile(r'pattern')
pattern.match(string)
```

### Pattern Syntax
```python
# Character classes
.       # any char (except newline)
\d      # digit [0-9]
\D      # non-digit
\w      # word char [a-zA-Z0-9_]
\W      # non-word
\s      # whitespace
\S      # non-whitespace
[abc]   # a, b, or c
[^abc]  # not a, b, c
[a-z]   # range

# Quantifiers
*       # 0 or more
+       # 1 or more
?       # 0 or 1
{n}     # exactly n
{n,}    # n or more
{n,m}   # between n and m

# Anchors
^       # start of string
$       # end of string
\b      # word boundary

# Groups
(...)       # capturing group
(?:...)     # non-capturing group
(?P<name>...)  # named group

# Lookahead/Lookbehind
(?=...)     # positive lookahead
(?!...)     # negative lookahead
(?<=...)    # positive lookbehind
(?<!...)    # negative lookbehind

# Examples
r'\b\w+@\w+\.\w+\b'     # simple email
r'^\d{3}-\d{3}-\d{4}$'  # phone
r'https?://\S+'          # URL
```

---

## 11. Concurrency

### Threading
```python
import threading

def worker(n):
    print(f"Worker {n}")

# Create and start thread
t = threading.Thread(target=worker, args=(1,))
t.start()
t.join()  # wait for completion

# Thread pool
from concurrent.futures import ThreadPoolExecutor

with ThreadPoolExecutor(max_workers=4) as executor:
    futures = [executor.submit(task, arg) for arg in args]
    results = [f.result() for f in futures]

# Lock
lock = threading.Lock()
with lock:
    shared_resource += 1
```

### Multiprocessing
```python
from multiprocessing import Pool, Process, Queue

# Process pool
with Pool(4) as pool:
    results = pool.map(function, iterable)

# Single process
p = Process(target=function, args=(arg,))
p.start()
p.join()

# Process pool executor
from concurrent.futures import ProcessPoolExecutor

with ProcessPoolExecutor(max_workers=4) as executor:
    results = list(executor.map(function, items))
```

### Async/Await
```python
import asyncio

async def fetch_data(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.json()

async def main():
    # Run single coroutine
    result = await fetch_data(url)
    
    # Run multiple concurrently
    results = await asyncio.gather(
        fetch_data(url1),
        fetch_data(url2),
        fetch_data(url3)
    )

# Run async function
asyncio.run(main())

# Async context manager
async with aiohttp.ClientSession() as session:
    pass

# Async iterator
async for item in async_generator():
    process(item)

# Semaphore (limit concurrent)
semaphore = asyncio.Semaphore(10)
async with semaphore:
    await limited_operation()
```

---

## 12. NumPy

### Array Creation
```python
import numpy as np

# From list
arr = np.array([1, 2, 3])
arr = np.array([[1, 2], [3, 4]])

# Special arrays
np.zeros((3, 4))
np.ones((3, 4))
np.empty((3, 4))
np.eye(3)               # identity matrix
np.full((3, 4), 7)      # filled with 7

# Sequences
np.arange(0, 10, 2)     # [0, 2, 4, 6, 8]
np.linspace(0, 1, 5)    # 5 points from 0 to 1

# Random
np.random.rand(3, 4)    # uniform [0, 1)
np.random.randn(3, 4)   # standard normal
np.random.randint(0, 10, (3, 4))
np.random.choice([1, 2, 3], size=10)
np.random.seed(42)      # reproducibility
```

### Array Operations
```python
# Shape
arr.shape
arr.reshape(2, 6)
arr.flatten()
arr.ravel()

# Indexing
arr[0]                  # first element
arr[-1]                 # last element
arr[1:3]                # slice
arr[::2]                # every 2nd
arr[arr > 5]            # boolean indexing

# 2D indexing
arr[0, 1]               # row 0, col 1
arr[:, 0]               # all rows, col 0
arr[0:2, 1:3]           # slice

# Math operations (element-wise)
arr + 1
arr * 2
arr ** 2
np.sqrt(arr)
np.exp(arr)
np.log(arr)

# Matrix operations
np.dot(a, b)            # dot product
a @ b                   # matrix multiply
np.transpose(arr)       # or arr.T
np.linalg.inv(arr)      # inverse
np.linalg.det(arr)      # determinant
```

### Statistics
```python
arr.mean()
arr.std()
arr.var()
arr.min(), arr.max()
arr.sum()
arr.cumsum()
np.median(arr)
np.percentile(arr, 75)

# Along axis
arr.mean(axis=0)        # column means
arr.mean(axis=1)        # row means
```

---

## 13. Pandas

### Data Structures
```python
import pandas as pd

# Series
s = pd.Series([1, 2, 3], index=['a', 'b', 'c'])

# DataFrame from dict
df = pd.DataFrame({
    'name': ['Alice', 'Bob'],
    'age': [25, 30]
})

# Read data
df = pd.read_csv('file.csv')
df = pd.read_excel('file.xlsx')
df = pd.read_json('file.json')
df = pd.read_sql(query, connection)
```

### Selection
```python
# Column
df['column']
df.column
df[['col1', 'col2']]

# Row
df.loc['label']         # by label
df.iloc[0]              # by position
df.loc[0:5]             # label slice
df.iloc[0:5]            # position slice

# Both
df.loc['row', 'col']
df.iloc[0, 1]

# Boolean
df[df['age'] > 25]
df.query('age > 25')
df[df['name'].isin(['Alice', 'Bob'])]
```

### Manipulation
```python
# Add column
df['new_col'] = values
df.assign(new_col=lambda x: x.a + x.b)

# Rename
df.rename(columns={'old': 'new'})

# Drop
df.drop('column', axis=1)
df.drop([0, 1], axis=0)
df.dropna()
df.drop_duplicates()

# Sort
df.sort_values('column')
df.sort_values(['a', 'b'], ascending=[True, False])
df.sort_index()

# Group
df.groupby('column').mean()
df.groupby(['a', 'b']).agg({'c': 'sum', 'd': 'mean'})

# Merge
pd.merge(df1, df2, on='key')
pd.merge(df1, df2, left_on='a', right_on='b', how='left')
pd.concat([df1, df2])

# Pivot
df.pivot_table(values='val', index='row', columns='col', aggfunc='mean')
df.melt(id_vars=['id'], value_vars=['a', 'b'])
```

### Common Operations
```python
# Info
df.head()
df.tail()
df.info()
df.describe()
df.shape
df.dtypes
df.columns
df.index

# Missing data
df.isna()
df.fillna(value)
df.dropna()
df.interpolate()

# Apply
df['col'].apply(func)
df.apply(func, axis=1)
df.applymap(func)

# String methods
df['col'].str.lower()
df['col'].str.contains('pattern')
df['col'].str.split(',').str[0]

# DateTime
df['date'] = pd.to_datetime(df['date'])
df['date'].dt.year
df['date'].dt.month
df.set_index('date').resample('M').mean()
```

---

## 14. Data Visualization

### Matplotlib
```python
import matplotlib.pyplot as plt

# Basic plot
plt.plot(x, y)
plt.title('Title')
plt.xlabel('X')
plt.ylabel('Y')
plt.legend(['line1', 'line2'])
plt.show()

# Subplots
fig, axes = plt.subplots(2, 2, figsize=(10, 8))
axes[0, 0].plot(x, y)
axes[0, 0].set_title('Plot 1')
plt.tight_layout()

# Plot types
plt.bar(x, y)
plt.barh(x, y)
plt.scatter(x, y)
plt.hist(data, bins=30)
plt.pie(sizes, labels=labels)
plt.boxplot(data)

# Customization
plt.style.use('seaborn')
plt.figure(figsize=(10, 6))
plt.grid(True)
plt.savefig('plot.png', dpi=300)
```

### Seaborn
```python
import seaborn as sns

# Distribution
sns.histplot(data, x='column', kde=True)
sns.kdeplot(data, x='column')
sns.boxplot(data, x='category', y='value')
sns.violinplot(data, x='category', y='value')

# Relationship
sns.scatterplot(data, x='x', y='y', hue='category')
sns.regplot(data, x='x', y='y')
sns.pairplot(data)

# Categorical
sns.countplot(data, x='category')
sns.barplot(data, x='category', y='value')

# Heatmap
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')

# Styling
sns.set_theme(style='whitegrid')
sns.set_palette('husl')
```

---

## 15. Machine Learning

### scikit-learn Basics
```python
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score, mean_squared_error

# Split data
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Scale features
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

### Common Models
```python
# Classification
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.svm import SVC

model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)
predictions = model.predict(X_test)
accuracy = accuracy_score(y_test, predictions)

# Regression
from sklearn.linear_model import LinearRegression
from sklearn.ensemble import RandomForestRegressor

model = LinearRegression()
model.fit(X_train, y_train)
predictions = model.predict(X_test)
rmse = mean_squared_error(y_test, predictions, squared=False)

# Clustering
from sklearn.cluster import KMeans

kmeans = KMeans(n_clusters=3)
clusters = kmeans.fit_predict(X)
```

### Pipelines
```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder

# Create pipeline
pipeline = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', RandomForestClassifier())
])

pipeline.fit(X_train, y_train)
pipeline.predict(X_test)

# Column transformer
preprocessor = ColumnTransformer([
    ('num', StandardScaler(), numerical_columns),
    ('cat', OneHotEncoder(), categorical_columns)
])
```

### Cross-Validation
```python
from sklearn.model_selection import cross_val_score, GridSearchCV

# Cross-validation
scores = cross_val_score(model, X, y, cv=5)
print(f"Mean: {scores.mean():.3f} (+/- {scores.std()*2:.3f})")

# Grid search
param_grid = {
    'n_estimators': [100, 200],
    'max_depth': [10, 20, None]
}
grid_search = GridSearchCV(model, param_grid, cv=5)
grid_search.fit(X_train, y_train)
print(grid_search.best_params_)
```

---

## 16. Web Development

### FastAPI
```python
from fastapi import FastAPI, HTTPException, Depends
from pydantic import BaseModel

app = FastAPI()

class Item(BaseModel):
    name: str
    price: float

# GET endpoint
@app.get("/items/{item_id}")
async def get_item(item_id: int):
    return {"item_id": item_id}

# POST endpoint
@app.post("/items/")
async def create_item(item: Item):
    return item

# Query parameters
@app.get("/items/")
async def list_items(skip: int = 0, limit: int = 10):
    return items[skip:skip + limit]

# Error handling
@app.get("/items/{item_id}")
async def get_item(item_id: int):
    if item_id not in db:
        raise HTTPException(status_code=404, detail="Not found")
    return db[item_id]

# Dependency injection
async def get_db():
    db = Database()
    try:
        yield db
    finally:
        db.close()

@app.get("/items/")
async def get_items(db = Depends(get_db)):
    return db.get_all()
```

---

## 17. Testing

### pytest
```python
import pytest

# Basic test
def test_addition():
    assert 1 + 1 == 2

# Fixtures
@pytest.fixture
def sample_data():
    return {'key': 'value'}

def test_with_fixture(sample_data):
    assert 'key' in sample_data

# Parametrize
@pytest.mark.parametrize("input,expected", [
    (1, 1),
    (2, 4),
    (3, 9),
])
def test_square(input, expected):
    assert input ** 2 == expected

# Exception testing
def test_raises():
    with pytest.raises(ValueError):
        raise ValueError("error")

# Mocking
from unittest.mock import Mock, patch

def test_with_mock():
    mock_func = Mock(return_value=42)
    assert mock_func() == 42

@patch('module.function')
def test_with_patch(mock_func):
    mock_func.return_value = 'mocked'
    assert module.function() == 'mocked'
```

---

## 18. Best Practices

### Code Style (PEP 8)
```python
# Naming conventions
variable_name = 1           # snake_case
CONSTANT_NAME = 1           # UPPER_SNAKE_CASE
ClassName = 1               # PascalCase
_private_var = 1            # leading underscore
__name_mangled = 1          # double underscore

# Line length: max 79 (code), 72 (docstrings)
# Indentation: 4 spaces

# Imports order:
# 1. Standard library
# 2. Third-party
# 3. Local
import os
import sys

import numpy as np
import pandas as pd

from mypackage import mymodule
```

### Project Structure
```
my_project/
├── src/
│   └── my_package/
│       ├── __init__.py
│       ├── module1.py
│       └── module2.py
├── tests/
│   ├── __init__.py
│   ├── test_module1.py
│   └── test_module2.py
├── docs/
├── requirements.txt
├── setup.py
├── pyproject.toml
└── README.md
```

### Documentation
```python
def process_data(data: list[dict], threshold: float = 0.5) -> list[dict]:
    """Process and filter data based on threshold.
    
    Args:
        data: List of dictionaries containing 'value' key.
        threshold: Minimum value to include (default: 0.5).
    
    Returns:
        Filtered list of dictionaries with value >= threshold.
    
    Raises:
        ValueError: If data is empty.
    
    Examples:
        >>> process_data([{'value': 0.7}], 0.5)
        [{'value': 0.7}]
    """
    if not data:
        raise ValueError("Data cannot be empty")
    return [d for d in data if d.get('value', 0) >= threshold]
```

### Performance Tips
```python
# Use generators for large data
(x**2 for x in range(1000000))  # instead of list

# Use set for membership testing
if item in large_set:  # O(1) vs O(n) for list

# Use local variables in loops
local_func = some_module.func
for item in items:
    local_func(item)  # faster than some_module.func(item)

# Use join for string concatenation
''.join(strings)  # instead of += in loop

# Use list comprehension
[x**2 for x in items]  # faster than append loop

# Use slots for memory
class Point:
    __slots__ = ['x', 'y']

# Use @lru_cache for memoization
from functools import lru_cache
@lru_cache(maxsize=128)
def expensive_func(n):
    return n ** n
```

---

## Quick Reference Cards

### Common Imports
```python
# Data Science
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn import ...

# Web
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
import httpx

# Testing
import pytest
from unittest.mock import Mock, patch

# Standard Library
import os, sys, json, csv, re
from pathlib import Path
from datetime import datetime
from collections import defaultdict, Counter, deque
from itertools import chain, combinations, permutations
from functools import lru_cache, partial, reduce
from typing import List, Dict, Optional, Callable
```

### Keyboard Shortcuts (Jupyter)
```
Shift+Enter    - Run cell
Ctrl+Enter     - Run cell, stay
Alt+Enter      - Run cell, insert below
A              - Insert cell above
B              - Insert cell below
D,D            - Delete cell
M              - Cell to Markdown
Y              - Cell to Code
Tab            - Autocomplete
Shift+Tab      - Docstring
```

---

*This cheatsheet accompanies the Python Mastery Curriculum*
