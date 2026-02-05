# Chapter 17: Standard Library Overview

> **Topics Covered**: datetime, math, statistics, random, re, functools, operator, collections, heapq, bisect, array, typing, dataclasses, enum, subprocess, argparse, shutil, sys, os

---

## Questions

---

**Q17.1: Basic - [datetime Basics]**

What is the output?
```python
from datetime import datetime
now = datetime.now()
print(type(now))
```

A) `<class 'str'>`
B) `<class 'datetime.datetime'>`
C) `<class 'date'>`
D) `<class 'time'>`

**Answer: B**

**Explanation:**
`datetime.now()` returns a datetime object with current date and time. The datetime module has: `datetime`, `date`, `time`, `timedelta`, `timezone`. Use `date.today()` for date only.

---

**Q17.2: Intermediate - [datetime Formatting]**

What is the output?
```python
from datetime import datetime
dt = datetime(2024, 1, 15, 10, 30)
print(dt.strftime("%Y-%m-%d"))
```

A) `2024/01/15`
B) `2024-01-15`
C) `15-01-2024`
D) Error

**Answer: B**

**Explanation:**
`strftime` formats datetime to string. `%Y` = 4-digit year, `%m` = zero-padded month, `%d` = day. Common codes: `%H` (hour 24), `%M` (minute), `%S` (second). `strptime` parses string to datetime.

---

**Q17.3: Intermediate - [timedelta]**

What is the output?
```python
from datetime import datetime, timedelta
start = datetime(2024, 1, 1)
end = start + timedelta(days=30)
print(end.month)
```

A) `1`
B) `2`
C) `30`
D) `31`

**Answer: A**

**Explanation:**
`timedelta` represents duration. Adding 30 days to Jan 1 → Jan 31 (still January). `timedelta(weeks=1, days=2, hours=3)`. Subtraction works too: `datetime - datetime = timedelta`.

---

**Q17.4: Intermediate - [math Module]**

Which math functions are correct?
```python
import math
print(math.ceil(4.1), math.floor(4.9), math.sqrt(16))
```

A) `4, 5, 4`
B) `5, 4, 4.0`
C) `5, 4, 16`
D) Error

**Answer: B**

**Explanation:**
`ceil()` rounds up → 5. `floor()` rounds down → 4. `sqrt()` returns float → 4.0. Also: `math.pi`, `math.e`, `sin`, `cos`, `log`, `pow`, `factorial`, `gcd`.

---

**Q17.5: Intermediate - [statistics Module]**

What is the output?
```python
import statistics
data = [1, 2, 3, 4, 5]
print(statistics.mean(data), statistics.median(data))
```

A) `3, 3`
B) `3.0, 3`
C) `15, 3`
D) `2.5, 2.5`

**Answer: B**

**Explanation:**
`mean()` = average = 3.0 (returns float). `median()` = middle value = 3 (returns same type as input). Also: `mode`, `stdev`, `variance`, `quantiles`. Built-in since Python 3.4.

---

**Q17.6: Basic - [random Module]**

What is the output type?
```python
import random
print(type(random.random()))
```

A) `<class 'int'>`
B) `<class 'float'>`
C) `<class 'random'>`
D) `<class 'decimal'>`

**Answer: B**

**Explanation:**
`random.random()` returns float in [0.0, 1.0). `randint(a, b)` returns int in [a, b]. `choice(seq)` picks one. `shuffle(list)` shuffles in place. Set `random.seed(n)` for reproducibility.

---

**Q17.7: Intermediate - [random.choice and sample]**

What's the difference between `choice` and `sample`?

A) No difference
B) choice picks 1; sample picks k without replacement
C) sample is random, choice isn't
D) choice modifies list

**Answer: B**

**Explanation:**
`choice(seq)` — one random element. `sample(seq, k=3)` — k unique elements. `choices(seq, k=3)` — k elements WITH replacement (may repeat). Different use cases for each.

---

**Q17.8: Intermediate - [re Module Basics]**

What is the output?
```python
import re
result = re.search(r'\d+', 'abc123def')
print(result.group())
```

A) `'abc'`
B) `'123'`
C) `None`
D) `'def'`

**Answer: B**

**Explanation:**
`\d+` matches one or more digits. `search()` finds first match. `.group()` returns matched string. `match()` only checks at start. `findall()` returns all matches as list.

---

**Q17.9: Intermediate - [re Groups]**

What is the output?
```python
import re
pattern = r'(\d+)-(\d+)'
result = re.search(pattern, 'Phone: 123-456')
print(result.groups())
```

A) `('123-456',)`
B) `('123', '456')`
C) `'123-456'`
D) `['123', '456']`

**Answer: B**

**Explanation:**
Parentheses create capture groups. `.groups()` returns tuple of all groups. `.group(0)` = entire match, `.group(1)` = first group, etc. Named groups: `(?P<name>\d+)`.

---

**Q17.10: Intermediate - [re.sub]**

What is the output?
```python
import re
result = re.sub(r'\d+', 'X', 'a1b2c3')
print(result)
```

A) `'aXbXcX'`
B) `'abc'`
C) `'XXX'`
D) `'a1b2c3'`

**Answer: A**

**Explanation:**
`sub(pattern, replacement, string)` replaces all matches. Each number replaced with 'X'. Can use function as replacement: `sub(r'\d+', lambda m: str(int(m.group())*2), s)`.

---

**Q17.11: Intermediate - [functools.reduce]**

What is the output?
```python
from functools import reduce
result = reduce(lambda a, b: a + b, [1, 2, 3, 4])
print(result)
```

A) `[1, 2, 3, 4]`
B) `10`
C) `24`
D) Error

**Answer: B**

**Explanation:**
`reduce` accumulates: ((1+2)+3)+4 = 10. Folds list to single value. `reduce(lambda a,b: a*b, [1,2,3,4])` = 24. Use `sum()`, `max()` for common cases; reduce for custom folding.

---

**Q17.12: Intermediate - [functools.partial]**

What is the output?
```python
from functools import partial

def power(base, exp):
    return base ** exp

square = partial(power, exp=2)
print(square(5))
```

A) `25`
B) `10`
C) Error
D) `power(5, 2)`

**Answer: A**

**Explanation:**
`partial` creates new function with some arguments preset. `square` is `power` with `exp=2` fixed. Calling `square(5)` → `power(5, exp=2)` → 25. Useful for callbacks needing specific arguments.

---

**Q17.13: Intermediate - [operator Module]**

What is the output?
```python
from operator import itemgetter
data = [('a', 3), ('b', 1), ('c', 2)]
sorted_data = sorted(data, key=itemgetter(1))
print([x[0] for x in sorted_data])
```

A) `['a', 'b', 'c']`
B) `['b', 'c', 'a']`
C) `[1, 2, 3]`
D) Error

**Answer: B**

**Explanation:**
`itemgetter(1)` extracts second element (index 1). Sort by values: 1, 2, 3. Order: b, c, a. `attrgetter('name')` for objects. Often faster than lambda for simple access.

---

**Q17.14: Intermediate - [collections.Counter]**

What is the output?
```python
from collections import Counter
c = Counter('abracadabra')
print(c.most_common(2))
```

A) `{'a': 5, 'b': 2}`
B) `[('a', 5), ('b', 2)]`
C) `['a', 'b']`
D) `5`

**Answer: B**

**Explanation:**
`Counter` counts hashable elements. `most_common(n)` returns n most frequent as (element, count) pairs. Also: `c['a']` → count, `c.update()`, `c + other_counter`, `c - other_counter`.

---

**Q17.15: Intermediate - [collections.defaultdict]**

What is the output?
```python
from collections import defaultdict
d = defaultdict(list)
d['key'].append(1)
d['key'].append(2)
print(d['key'])
```

A) Error (key doesn't exist)
B) `[1, 2]`
C) `None`
D) `1`

**Answer: B**

**Explanation:**
`defaultdict(list)` — missing keys get empty list. `d['key']` creates `[]` automatically, then append works. Also: `defaultdict(int)` for counting, `defaultdict(set)` for unique values.

---

**Q17.16: Intermediate - [collections.OrderedDict]**

Is `OrderedDict` still needed in Python 3.7+?

A) Yes, always
B) Regular dicts maintain order now, but OrderedDict has move_to_end and equality comparing order
C) OrderedDict is deprecated
D) Only for legacy code

**Answer: B**

**Explanation:**
Since 3.7, regular dicts maintain insertion order. `OrderedDict` still useful for: `move_to_end(key)`, equality that considers order (`od1 == od2` considers order, `d1 == d2` doesn't). LRU cache patterns.

---

**Q17.17: Intermediate - [heapq Module]**

What is the output?
```python
import heapq
h = [3, 1, 4, 1, 5]
heapq.heapify(h)
print(heapq.heappop(h))
```

A) `5`
B) `1`
C) `3`
D) `4`

**Answer: B**

**Explanation:**
`heapify` transforms list into min-heap in-place. `heappop` removes and returns smallest. Min-heap property: parent ≤ children. For max-heap, negate values. Also: `heappush`, `nlargest`, `nsmallest`.

---

**Q17.18: Intermediate - [bisect Module]**

What is the output?
```python
import bisect
lst = [1, 3, 5, 7]
print(bisect.bisect_left(lst, 4))
```

A) `1`
B) `2`
C) `3`
D) `4`

**Answer: B**

**Explanation:**
`bisect_left` finds insertion point to maintain sorted order. 4 would go between 3 and 5, at index 2. `bisect_right` gives position after existing equal values. `insort` inserts while maintaining order.

---

**Q17.19: Intermediate - [array Module]**

What's the advantage of `array.array` over list?

A) More functionality
B) More memory-efficient for homogeneous numeric data
C) Faster for all operations
D) Can hold any type

**Answer: B**

**Explanation:**
`array.array('i', [1,2,3])` — stores ints as C array (compact). No Python object overhead per element. Useful for large numeric datasets. NumPy arrays are even more powerful for numeric work.

---

**Q17.20: Intermediate - [typing Module]**

What does this do?
```python
def greet(name: str) -> str:
    return f"Hello, {name}"
```

A) Enforces types at runtime
B) Provides type hints for static analysis (no runtime enforcement)
C) Converts types
D) Nothing

**Answer: B**

**Explanation:**
Type hints are metadata — Python doesn't enforce them. Tools like mypy, PyCharm use them for checking. `typing` module adds `List[int]`, `Dict[str, int]`, `Optional[str]`, `Union`, `Callable`, etc.

---

**Q17.21: Intermediate - [dataclasses]**

What is the output?
```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

p = Point(1, 2)
print(p)
```

A) `<Point object at ...>`
B) `Point(x=1, y=2)`
C) `(1, 2)`
D) Error

**Answer: B**

**Explanation:**
`@dataclass` auto-generates `__init__`, `__repr__`, `__eq__`. Clean syntax for data containers. Options: `frozen=True` (immutable), `order=True` (comparison operators). Reduces boilerplate.

---

**Q17.22: Intermediate - [dataclass Features]**

What does `@dataclass(frozen=True)` do?

A) Creates freezable class
B) Makes instances immutable (hashable, can't modify attributes)
C) Freezes memory
D) Optimization only

**Answer: B**

**Explanation:**
`frozen=True` — instances are immutable. `p.x = 3` raises `FrozenInstanceError`. Automatically becomes hashable (can use as dict key/set member). Like a mutable-syntax NamedTuple.

---

**Q17.23: Intermediate - [Enum Basics]**

What is the output?
```python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3

print(Color.RED.name, Color.RED.value)
```

A) `'RED', 'RED'`
B) `'RED', 1`
C) `1, 'RED'`
D) `Color.RED, Color.RED`

**Answer: B**

**Explanation:**
Enum members have `name` (string) and `value`. Access: `Color.RED` or `Color(1)` or `Color['RED']`. Enums are iterable. Prevents magic numbers, provides type safety.

---

**Q17.24: Intermediate - [Enum auto()]**

What is the output?
```python
from enum import Enum, auto

class Status(Enum):
    PENDING = auto()
    APPROVED = auto()
    REJECTED = auto()

print(Status.APPROVED.value)
```

A) `'APPROVED'`
B) `2`
C) `1`
D) `auto`

**Answer: B**

**Explanation:**
`auto()` generates values automatically (1, 2, 3, ...). Convenient when you don't care about specific values. First `auto()` is 1 by default.

---

**Q17.25: Intermediate - [subprocess.run]**

What does `subprocess.run()` do?

A) Runs Python function
B) Runs external command, waits for completion, returns CompletedProcess
C) Creates subprocess object only
D) Runs asynchronously

**Answer: B**

**Explanation:**
`subprocess.run(['ls', '-l'])` runs command and waits. Returns `CompletedProcess` with `returncode`, `stdout`, `stderr`. Use `capture_output=True` to capture output. Modern replacement for os.system.

---

**Q17.26: Intermediate - [subprocess Capture Output]**

What is the output?
```python
import subprocess
result = subprocess.run(['echo', 'Hello'], capture_output=True, text=True)
print(result.stdout.strip())
```

A) `CompletedProcess`
B) `Hello`
C) `['echo', 'Hello']`
D) Nothing

**Answer: B**

**Explanation:**
`capture_output=True` captures stdout/stderr. `text=True` decodes as string (else bytes). `result.stdout` contains "Hello\n". Alternative: `subprocess.check_output()` returns output directly.

---

**Q17.27: Intermediate - [argparse Basics]**

What does argparse do?

A) Parses text
B) Parses command-line arguments with help, validation, types
C) Argument validation
D) Debugging

**Answer: B**

**Explanation:**
```python
parser = argparse.ArgumentParser()
parser.add_argument('--name', required=True)
args = parser.parse_args()
print(args.name)
```
Creates CLI with `--help`, type checking, defaults. Standard library for CLI tools. `--flag` = optional, positional = required.

---

**Q17.28: Intermediate - [sys.argv]**

What is `sys.argv`?

A) System arguments
B) List of command-line arguments (first is script name)
C) Argument count
D) Environment variables

**Answer: B**

**Explanation:**
`python script.py arg1 arg2` → `sys.argv = ['script.py', 'arg1', 'arg2']`. First element is script path. For simple cases; use argparse for robust CLI parsing.

---

**Q17.29: Intermediate - [sys.path]**

What is `sys.path`?

A) Current directory
B) List of directories Python searches for imports
C) System PATH
D) File path

**Answer: B**

**Explanation:**
When you `import module`, Python searches directories in `sys.path`. Includes: script's directory, PYTHONPATH, site-packages. `sys.path.insert(0, 'dir')` adds to search path at runtime.

---

**Q17.30: Intermediate - [os.environ]**

What is the output?
```python
import os
os.environ['MY_VAR'] = 'test'
print(os.environ.get('MY_VAR', 'default'))
```

A) `default`
B) `test`
C) `None`
D) Error

**Answer: B**

**Explanation:**
`os.environ` is dict-like for environment variables. Set, get, delete variables. Changes affect current process and children. `os.getenv('VAR', 'default')` shorthand for .get().

---

**Q17.31: Intermediate - [os.getcwd and os.chdir]**

What do `os.getcwd()` and `os.chdir()` do?

A) Get/set current file
B) Get/change current working directory
C) Get/set command
D) Get/check directory exists

**Answer: B**

**Explanation:**
`getcwd()` returns current directory as string. `chdir('/path')` changes directory. Affects file operations without absolute paths. Generally prefer absolute paths in code.

---

**Q17.32: Intermediate - [shutil.which]**

What does `shutil.which('python')` return?

A) Python version
B) Path to python executable (or None if not found)
C) Which Python
D) True/False

**Answer: B**

**Explanation:**
`which()` finds executable in PATH, like Unix `which` command. Returns path string or None. Useful for checking if programs exist before subprocess calls.

---

**Q17.33: Intermediate - [collections.deque]**

What's the advantage of `deque` over list for queue operations?

A) More memory
B) O(1) append/pop on both ends (list is O(n) for left operations)
C) More features
D) Faster indexing

**Answer: B**

**Explanation:**
`deque` (double-ended queue): O(1) `append`, `appendleft`, `pop`, `popleft`. List `insert(0, x)` is O(n). Use deque for queue/stack patterns. `maxlen` parameter for bounded queue.

---

**Q17.34: Intermediate - [collections.namedtuple]**

What is the output?
```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)
print(p.x, p[0])
```

A) `1, 1`
B) `1, 2`
C) Error
D) `x, 1`

**Answer: A**

**Explanation:**
namedtuple: tuple with named fields. Access by name (`p.x`) or index (`p[0]`). Immutable. Memory-efficient like tuple. `_replace()` returns new instance with changes. Predecessor to dataclasses.

---

**Q17.35: Intermediate - [typing.Optional]**

What does `Optional[str]` mean?

A) String is optional
B) Equivalent to `Union[str, None]` — can be str or None
C) Optional parameter
D) Partial string

**Answer: B**

**Explanation:**
`Optional[str]` = value can be string or None. `Optional[X]` is shorthand for `Union[X, None]`. Use for nullable return values: `def find(id) -> Optional[User]:`. Python 3.10+: `str | None`.

---

**Q17.36: Intermediate - [typing.TypeVar]**

What is `TypeVar` for?

A) Type variables
B) Generic type parameters (like T in List[T])
C) Variable types
D) Type storage

**Answer: B**

**Explanation:**
```python
T = TypeVar('T')
def first(lst: List[T]) -> T: return lst[0]
```
`T` represents "same type throughout". Return type matches input element type. Used for generic functions/classes.

---

**Q17.37: Intermediate - [textwrap Module]**

What does `textwrap.wrap(text, width=40)` do?

A) Word-wraps text into list of lines with max width
B) Removes whitespace
C) Centers text
D) Adds borders

**Answer: A**

**Explanation:**
`wrap()` returns list of lines wrapped at word boundaries. `fill()` returns single string with newlines. `dedent()` removes common leading whitespace. Useful for formatting output.

---

**Q17.38: Intermediate - [secrets Module]**

When use `secrets` instead of `random`?

A) Never
B) For cryptographically secure random data (passwords, tokens)
C) For faster random
D) For testing

**Answer: B**

**Explanation:**
`secrets.token_hex(16)`, `secrets.token_urlsafe()` — cryptographically secure. `random` is predictable (not secure). Use `secrets` for: passwords, tokens, session IDs, anything security-related.

---

**Q17.39: Intermediate - [hashlib Module]**

What is the output?
```python
import hashlib
h = hashlib.sha256(b'hello')
print(len(h.hexdigest()))
```

A) `5`
B) `64`
C) `32`
D) `256`

**Answer: B**

**Explanation:**
SHA-256 produces 256-bit (32 bytes) hash. `hexdigest()` returns hex string = 64 characters (2 per byte). Also: `md5`, `sha1`, `sha512`. Always hash bytes, not strings.

---

**Q17.40: Intermediate - [uuid Module]**

What is the output?
```python
import uuid
u = uuid.uuid4()
print(type(u), len(str(u)))
```

A) `str, 32`
B) `<class 'uuid.UUID'>, 36`
C) `int, 16`
D) Error

**Answer: B**

**Explanation:**
`uuid4()` generates random UUID. Returns UUID object. String form: 36 chars (32 hex + 4 hyphens). Use for unique IDs. `uuid1()` = time-based, `uuid4()` = random (most common).

---

**Q17.41: Intermediate - [itertools.combinations_with_replacement]**

What is the output?
```python
from itertools import combinations_with_replacement
print(list(combinations_with_replacement('AB', 2)))
```

A) `[('A', 'B')]`
B) `[('A', 'A'), ('A', 'B'), ('B', 'B')]`
C) `[('A', 'A'), ('A', 'B'), ('B', 'A'), ('B', 'B')]`
D) `[('A', 'B'), ('B', 'A')]`

**Answer: B**

**Explanation:**
`combinations_with_replacement` allows repeated elements. From 'AB' take 2: AA, AB, BB. Order doesn't matter (no BA — that's same as AB for combinations). With replacement: element can repeat.

---

**Q17.42: Intermediate - [pprint Module]**

What does `pprint.pprint()` do?

A) Just print
B) Pretty-prints data structures with formatting and indentation
C) Prints to printer
D) Debug print

**Answer: B**

**Explanation:**
`pprint.pprint(data)` formats dicts, lists, etc. with proper indentation for readability. `pformat()` returns string. `width` parameter controls line length. Great for debugging complex structures.

---

**Q17.43: Intermediate - [abc Module]**

What does `abc.ABC` provide?

A) Alphabet
B) Base class for abstract base classes — can define abstract methods
C) Basic classes
D) Configuration

**Answer: B**

**Explanation:**
```python
from abc import ABC, abstractmethod
class Shape(ABC):
    @abstractmethod
    def area(self): pass
```
Can't instantiate ABC directly. Subclasses must implement abstract methods. Enforces interface contracts.

---

**Q17.44: Intermediate - [weakref Module]**

What is the output?
```python
import weakref
class Obj: pass

obj = Obj()
ref = weakref.ref(obj)
print(ref() is obj)
del obj
print(ref())
```

A) `True, True`
B) `True, None`
C) `False, None`
D) Error

**Answer: B**

**Explanation:**
`weakref.ref(obj)` creates weak reference. `ref()` returns object (or None if dead). Weak reference doesn't prevent garbage collection. After `del obj`, reference returns None.

---

**Q17.45: Intermediate - [copy.deepcopy]**

What is the output?
```python
import copy
a = [[1, 2], [3, 4]]
b = copy.deepcopy(a)
a[0][0] = 'X'
print(b[0][0])
```

A) `'X'`
B) `1`
C) `[1, 2]`
D) Error

**Answer: B**

**Explanation:**
`deepcopy` recursively copies all nested objects. `b` is completely independent of `a`. Modifying `a` doesn't affect `b`. Compare: `copy.copy()` (shallow) would share nested lists.

---

**Q17.46: Intermediate - [contextlib.suppress]**

What is the output?
```python
from contextlib import suppress

with suppress(FileNotFoundError):
    open('nonexistent.txt')

print("Continued")
```

A) FileNotFoundError
B) `Continued`
C) Nothing
D) Error

**Answer: B**

**Explanation:**
`suppress(ExceptionType)` catches and ignores specified exceptions. Cleaner than try/except/pass. Exception suppressed, execution continues. Use sparingly — hiding errors can mask bugs.

---

**Q17.47: Intermediate - [decimal Module]**

Why use `decimal.Decimal` over `float`?

A) Faster
B) Exact decimal representation (no binary floating point errors)
C) More digits
D) Required for money

**Answer: B**

**Explanation:**
`0.1 + 0.2 != 0.3` with floats (binary representation). `Decimal('0.1') + Decimal('0.2') == Decimal('0.3')`. Essential for financial calculations. Slower but exact. Control precision with `getcontext().prec`.

---

**Q17.48: Intermediate - [fractions Module]**

What is the output?
```python
from fractions import Fraction
f = Fraction(1, 3) + Fraction(1, 6)
print(f)
```

A) `0.5`
B) `1/2`
C) `Fraction(1, 2)`
D) `0.49999...`

**Answer: B**

**Explanation:**
`Fraction` represents rational numbers exactly. `1/3 + 1/6 = 2/6 + 1/6 = 3/6 = 1/2`. Auto-simplifies. `Fraction(0.5)` or `Fraction('1/3')` work. Exact arithmetic for ratios.

---

**Q17.49: Intermediate - [locale Module]**

What does `locale.setlocale()` affect?

A) Location
B) Number formatting, currency, date formatting based on region
C) Language translation
D) Time zone

**Answer: B**

**Explanation:**
`locale.setlocale(locale.LC_ALL, 'en_US.UTF-8')` sets locale. `locale.format_string('%d', 1000, grouping=True)` → "1,000" (US) or "1.000" (Germany). Affects number/date display.

---

**Q17.50: Intermediate - [platform Module]**

What does `platform.system()` return?

A) CPU info
B) OS name: 'Windows', 'Linux', 'Darwin' (macOS)
C) Platform object
D) Version only

**Answer: B**

**Explanation:**
`platform.system()` → 'Windows', 'Linux', 'Darwin'. `platform.python_version()` → Python version. `platform.machine()` → architecture. Useful for platform-specific code paths.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 3 | 6% |
| Intermediate | 47 | 94% |
| Advanced | 0 | 0% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- datetime operations
- math and statistics
- random and secrets
- Regular expressions (re)
- functools and operator
- collections (Counter, defaultdict, deque, namedtuple)
- heapq and bisect
- typing and type hints
- dataclasses and enum
- subprocess and argparse
- Various utility modules
