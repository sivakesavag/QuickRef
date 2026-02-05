# Chapter 6: Data Structures

> **Topics Covered**: Lists, tuples, sets, dictionaries, frozensets, comprehensions, collections module (Counter, defaultdict, OrderedDict, deque, ChainMap, namedtuple), array module, bytearray, hash requirements

---

## Questions

---

**Q6.1: Basic - [Lists]**

Which statement creates an empty list?

A) `lst = {}`
B) `lst = []`
C) `lst = ()`
D) `lst = set()`

**Answer: B**

**Explanation:**
`[]` creates an empty list. `{}` creates an empty dict (not set!). `()` creates an empty tuple. `set()` creates an empty set. Remember: `{}` is dict, not set — this is a common point of confusion.

---

**Q6.2: Basic - [Lists]**

What is the output?
```python
lst = [1, 2, 3]
lst.append([4, 5])
print(len(lst))
```

A) `3`
B) `4`
C) `5`
D) Error

**Answer: B**

**Explanation:**
`append()` adds its argument as a single element. The list `[4, 5]` becomes ONE element in `lst`. Result: `[1, 2, 3, [4, 5]]`, length 4. To add individual elements, use `extend()` or `+=`: `lst.extend([4, 5])` gives length 5.

---

**Q6.3: Basic - [Lists]**

What is the output?
```python
lst = [1, 2, 3]
lst.extend([4, 5])
print(lst)
```

A) `[1, 2, 3, [4, 5]]`
B) `[1, 2, 3, 4, 5]`
C) `[[1, 2, 3], [4, 5]]`
D) Error

**Answer: B**

**Explanation:**
`extend()` adds each element of an iterable individually. `[4, 5]` is unpacked, adding 4 and 5 as separate elements. Result: `[1, 2, 3, 4, 5]`. Compare with `append()` which adds the whole list as one element.

---

**Q6.4: Intermediate - [List Slicing]**

What is the output?
```python
lst = [0, 1, 2, 3, 4, 5]
print(lst[1:4])
```

A) `[1, 2, 3, 4]`
B) `[1, 2, 3]`
C) `[0, 1, 2, 3]`
D) `[2, 3, 4]`

**Answer: B**

**Explanation:**
Slicing `[start:stop]` includes start, excludes stop. `lst[1:4]` gets indices 1, 2, 3. Elements: 1, 2, 3. The stop index is never included — think of it as "up to but not including".

---

**Q6.5: Intermediate - [List Slicing with Step]**

What is the output?
```python
lst = [0, 1, 2, 3, 4, 5]
print(lst[::2])
```

A) `[0, 2, 4]`
B) `[0, 1]`
C) `[2]`
D) `[5, 3, 1]`

**Answer: A**

**Explanation:**
`[::2]` means start to end with step 2. Gets every other element: indices 0, 2, 4. Values: 0, 2, 4. `[::-1]` reverses, `[::-2]` reverses and takes every other.

---

**Q6.6: Intermediate - [List Reversal]**

What is the output?
```python
lst = [1, 2, 3]
print(lst[::-1])
print(lst)
```

A) `[3, 2, 1]` then `[3, 2, 1]`
B) `[3, 2, 1]` then `[1, 2, 3]`
C) `[1, 2, 3]` then `[3, 2, 1]`
D) Error

**Answer: B**

**Explanation:**
`[::-1]` creates a NEW reversed list; original is unchanged. `lst.reverse()` would modify in-place. Slicing always returns a new object for lists. `lst` remains `[1, 2, 3]` after the slice operation.

---

**Q6.7: Basic - [List Methods]**

What does `lst.pop()` return and do?

A) Removes and returns the first element
B) Removes and returns the last element
C) Removes all elements
D) Returns but doesn't remove any element

**Answer: B**

**Explanation:**
`pop()` removes and returns the last element. `pop(0)` removes the first (slower, O(n)). `pop(i)` removes at index i. If list is empty, raises IndexError. Returns the removed value for use.

---

**Q6.8: Basic - [List Methods]**

What is the difference between `remove()` and `pop()`?

A) No difference
B) `remove()` removes by value, `pop()` removes by index
C) `remove()` is faster
D) `pop()` can only remove the first element

**Answer: B**

**Explanation:**
`lst.remove(value)` finds and removes the first occurrence of `value` (raises ValueError if not found). `lst.pop(index)` removes by position and returns the value. `pop()` without argument removes/returns last element.

---

**Q6.9: Intermediate - [List Sorting]**

What is the difference between `lst.sort()` and `sorted(lst)`?

A) No difference
B) `sort()` modifies in-place, `sorted()` returns new list
C) `sorted()` is slower
D) `sort()` returns a new list

**Answer: B**

**Explanation:**
`lst.sort()` sorts in-place and returns `None`. `sorted(lst)` returns a new sorted list, original unchanged. `sorted()` works on any iterable; `.sort()` is list-only. For method chaining, use `sorted()`.

---

**Q6.10: Intermediate - [List Sorting with Key]**

What is the output?
```python
words = ['banana', 'pie', 'Washington', 'book']
print(sorted(words, key=len))
```

A) `['banana', 'book', 'pie', 'Washington']`
B) `['pie', 'book', 'banana', 'Washington']`
C) `['Washington', 'banana', 'book', 'pie']`
D) `['banana', 'pie', 'Washington', 'book']`

**Answer: B**

**Explanation:**
`key=len` sorts by string length. Lengths: pie(3), book(4), banana(6), Washington(10). Shortest first. The `key` function extracts a comparison value. This is stable: equal-length items maintain original order.

---

**Q6.11: Basic - [Tuples]**

What is the output?
```python
t = (1, 2, 3)
t[0] = 10
```

A) `(10, 2, 3)`
B) TypeError: tuples are immutable
C) `(1, 2, 3, 10)`
D) `10`

**Answer: B**

**Explanation:**
Tuples are immutable — you cannot modify their elements after creation. Attempting to assign to an index raises TypeError. To "modify", create a new tuple: `t = (10,) + t[1:]`. Use lists when you need mutability.

---

**Q6.12: Basic - [Tuple Creation]**

What is the output?
```python
t = (1)
print(type(t))
```

A) `<class 'tuple'>`
B) `<class 'int'>`
C) `<class 'list'>`
D) Error

**Answer: B**

**Explanation:**
⚠️ **Gotcha**: Parentheses don't make a tuple — the comma does. `(1)` is just `1` (parentheses for grouping). For a single-element tuple, use a trailing comma: `(1,)`. `1,` also works but is less clear.

---

**Q6.13: Basic - [Tuple Unpacking]**

What is the output?
```python
a, b, c = (1, 2, 3)
print(b)
```

A) `(1, 2, 3)`
B) `2`
C) `1`
D) Error

**Answer: B**

**Explanation:**
Tuple unpacking assigns each element to a corresponding variable. `a=1, b=2, c=3`. Python unpacks any iterable this way. The number of variables must match the number of elements (unless using `*` for collecting extras).

---

**Q6.14: Intermediate - [Extended Unpacking]**

What is the output?
```python
first, *rest = [1, 2, 3, 4, 5]
print(rest)
```

A) `2, 3, 4, 5`
B) `[2, 3, 4, 5]`
C) `(2, 3, 4, 5)`
D) `1`

**Answer: B**

**Explanation:**
`*rest` collects remaining elements into a list (always a list, even from a tuple). `first=1`, `rest=[2, 3, 4, 5]`. Works at any position: `*start, last = [1,2,3]` gives `start=[1,2], last=3`.

---

**Q6.15: Basic - [Sets]**

What is the output?
```python
s = {1, 2, 2, 3, 3, 3}
print(s)
```

A) `{1, 2, 2, 3, 3, 3}`
B) `{1, 2, 3}`
C) `{3, 2, 1}`
D) Error

**Answer: B**

**Explanation:**
Sets contain only unique elements. Duplicates are automatically removed. The set contains 1, 2, 3 (order may vary in output). Sets are unordered collections — don't rely on element order.

---

**Q6.16: Basic - [Empty Set]**

How do you create an empty set?

A) `s = {}`
B) `s = set()`
C) `s = empty()`
D) `s = []`

**Answer: B**

**Explanation:**
`set()` creates an empty set. `{}` creates an empty **dict**, not a set! This is a common mistake. Once you add elements, `{1, 2}` is a set, but `{}` alone is always a dict.

---

**Q6.17: Intermediate - [Set Operations]**

What is the output?
```python
a = {1, 2, 3}
b = {2, 3, 4}
print(a & b)
```

A) `{1, 2, 3, 4}`
B) `{2, 3}`
C) `{1, 4}`
D) `{}`

**Answer: B**

**Explanation:**
`&` is set intersection — elements in BOTH sets. 2 and 3 appear in both. Also: `a.intersection(b)`. Other operations: `|` (union), `-` (difference), `^` (symmetric difference). Set operations are very efficient.

---

**Q6.18: Intermediate - [Set Operations]**

What is the output?
```python
a = {1, 2, 3}
b = {2, 3, 4}
print(a | b)
```

A) `{1, 2, 3, 4}`
B) `{2, 3}`
C) `{1, 4}`
D) Error

**Answer: A**

**Explanation:**
`|` is set union — elements in EITHER set (or both). Combined unique elements: 1, 2, 3, 4. Also: `a.union(b)`. Union doesn't duplicate common elements — sets always have unique values.

---

**Q6.19: Intermediate - [Set Operations]**

What is the output?
```python
a = {1, 2, 3}
b = {2, 3, 4}
print(a - b)
```

A) `{1}`
B) `{4}`
C) `{1, 4}`
D) `{-1, -1, -1}`

**Answer: A**

**Explanation:**
`-` is set difference — elements in `a` but NOT in `b`. Only 1 is in `a` but not in `b`. Also: `a.difference(b)`. Note: `a - b` ≠ `b - a`. For symmetric difference (in either but not both), use `^`.

---

**Q6.20: Intermediate - [Set Methods]**

What is the difference between `add()` and `update()` for sets?

A) `add()` adds a single element, `update()` adds elements from an iterable
B) No difference
C) `update()` removes elements
D) `add()` can add multiple elements

**Answer: A**

**Explanation:**
`s.add(elem)` adds one element. `s.update(iterable)` adds all elements from the iterable. `s.add([1,2])` would error (lists are unhashable). `s.update([1,2])` adds 1 and 2 separately.

---

**Q6.21: Intermediate - [Frozenset]**

What is a frozenset?

A) A set that's been frozen for faster access
B) An immutable set
C) A set stored in frozen memory
D) A set that can only contain frozen objects

**Answer: B**

**Explanation:**
`frozenset` is an immutable version of set. Can't add/remove elements after creation. Being immutable makes it hashable, so it can be a dict key or set element. `frozenset([1, 2, 3])` creates one.

---

**Q6.22: Advanced - [Set Hashability]**

Why can't you add a list to a set?

A) Lists are too big
B) Lists are mutable and therefore unhashable
C) Sets only accept numbers
D) It's a Python limitation that might be fixed

**Answer: B**

**Explanation:**
Set elements must be hashable (have consistent `__hash__`). Mutable objects like lists, dicts, sets can change, so their hash could change — breaking set lookup. Tuples (immutable) are hashable if all their elements are.

---

**Q6.23: Basic - [Dictionaries]**

What is the output?
```python
d = {'a': 1, 'b': 2}
print(d['a'])
```

A) `1`
B) `'a'`
C) `{'a': 1}`
D) `0`

**Answer: A**

**Explanation:**
Dictionary access with `d[key]` returns the value associated with the key. `d['a']` returns 1. If key doesn't exist, raises KeyError. Use `d.get('a')` for safe access (returns None if missing).

---

**Q6.24: Basic - [Dictionary get()]**

What is the output?
```python
d = {'a': 1, 'b': 2}
print(d.get('c', 0))
```

A) `Error`
B) `None`
C) `0`
D) `'c'`

**Answer: C**

**Explanation:**
`get(key, default)` returns the value if key exists, otherwise returns default. 'c' isn't in dict, so returns 0. `d.get('c')` without default returns None. Safer than `d['c']` which would raise KeyError.

---

**Q6.25: Intermediate - [Dictionary setdefault()]**

What does `d.setdefault('c', 3)` do?

A) Always sets 'c' to 3
B) Returns d['c'] if exists, otherwise sets d['c']=3 and returns 3
C) Raises error if 'c' exists
D) Deletes 'c' if value is 3

**Answer: B**

**Explanation:**
`setdefault` is like `get` but also sets the key if missing. If 'c' exists, returns existing value (doesn't overwrite). If missing, sets it to 3 and returns 3. Useful for building dicts of lists: `d.setdefault('key', []).append(item)`.

---

**Q6.26: Intermediate - [Dictionary Methods]**

What is the output?
```python
d = {'a': 1, 'b': 2}
print(list(d.keys()), list(d.values()))
```

A) `['a', 'b'], [1, 2]`
B) `[1, 2], ['a', 'b']`
C) `{'a', 'b'}, {1, 2}`
D) Error

**Answer: A**

**Explanation:**
`d.keys()` returns a view of keys. `d.values()` returns a view of values. Converting to lists: `['a', 'b']` and `[1, 2]`. `d.items()` returns key-value pairs as tuples. Views are dynamic — they update when dict changes.

---

**Q6.27: Intermediate - [Dictionary Iteration]**

What is the output?
```python
d = {'x': 10, 'y': 20}
for item in d:
    print(item, end=' ')
```

A) `x 10 y 20`
B) `x y`
C) `10 20`
D) `('x', 10) ('y', 20)`

**Answer: B**

**Explanation:**
Iterating over a dict iterates over its **keys** only. To get values: `for v in d.values()`. For both: `for k, v in d.items()`. This is a common source of confusion — remember: `for x in dict` gives keys.

---

**Q6.28: Intermediate - [Dictionary Update]**

What is the output?
```python
d1 = {'a': 1, 'b': 2}
d2 = {'b': 3, 'c': 4}
d1.update(d2)
print(d1)
```

A) `{'a': 1, 'b': 2, 'c': 4}`
B) `{'a': 1, 'b': 3, 'c': 4}`
C) `{'b': 3, 'c': 4}`
D) Error

**Answer: B**

**Explanation:**
`update()` adds key-value pairs from another dict. Existing keys are overwritten. 'b' was 2, updated to 3. 'c' is added. Result: `{'a': 1, 'b': 3, 'c': 4}`. `update()` modifies in-place, returns None.

---

**Q6.29: Intermediate - [Dict Merge Python 3.9+]**

🐍 What is the output? (Python 3.9+)
```python
d1 = {'a': 1}
d2 = {'b': 2}
d3 = d1 | d2
print(d3)
```

A) `{'a': 1, 'b': 2}`
B) `{1, 2}`
C) Error
D) `{'a': 1} | {'b': 2}`

**Answer: A**

**Explanation:**
Python 3.9+ supports `|` for dict merging, creating a new dict. `d1 | d2` combines both dicts. `|=` updates in-place. This is cleaner than `{**d1, **d2}` or calling `update()`.

---

**Q6.30: Basic - [Dictionary Comprehension]**

What is the output?
```python
d = {x: x**2 for x in range(4)}
print(d)
```

A) `[0, 1, 4, 9]`
B) `{0: 0, 1: 1, 2: 4, 3: 9}`
C) `{0, 1, 4, 9}`
D) `[(0, 0), (1, 1), (2, 4), (3, 9)]`

**Answer: B**

**Explanation:**
Dict comprehension: `{key_expr: value_expr for item in iterable}`. Creates key-value pairs. x is key, x² is value. Result: mapping of numbers to their squares. Note the `{}` and `:` syntax.

---

**Q6.31: Intermediate - [Dict Comprehension with Condition]**

What is the output?
```python
d = {x: x**2 for x in range(6) if x % 2 == 0}
print(d)
```

A) `{0: 0, 2: 4, 4: 16}`
B) `{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}`
C) `[0, 4, 16]`
D) `{}`

**Answer: A**

**Explanation:**
The `if` clause filters which items are included. Only even numbers (0, 2, 4) pass the condition. Their squares are 0, 4, 16. Odd numbers are excluded entirely.

---

**Q6.32: Intermediate - [Dict from zip]**

What is the output?
```python
keys = ['a', 'b', 'c']
values = [1, 2, 3]
d = dict(zip(keys, values))
print(d)
```

A) `{'a': 1, 'b': 2, 'c': 3}`
B) `[('a', 1), ('b', 2), ('c', 3)]`
C) `{'keys': 'values'}`
D) Error

**Answer: A**

**Explanation:**
`zip()` pairs elements from two iterables. `dict()` converts pairs to a dictionary. This is a clean way to create dicts from parallel lists. Common pattern for processing CSV headers and data.

---

**Q6.33: Basic - [List Comprehension]**

What is the output?
```python
squares = [x**2 for x in range(5)]
print(squares)
```

A) `[0, 1, 4, 9, 16]`
B) `[1, 4, 9, 16, 25]`
C) `(0, 1, 4, 9, 16)`
D) `{0, 1, 4, 9, 16}`

**Answer: A**

**Explanation:**
List comprehension: `[expression for item in iterable]`. Squares of 0,1,2,3,4 are 0,1,4,9,16. Creates a list (square brackets). More readable and often faster than equivalent for loop.

---

**Q6.34: Intermediate - [Set Comprehension]**

What is the output?
```python
s = {x % 3 for x in range(10)}
print(s)
```

A) `{0, 1, 2, 0, 1, 2, 0, 1, 2, 0}`
B) `{0, 1, 2}`
C) `[0, 1, 2]`
D) `{0, 3, 6, 9}`

**Answer: B**

**Explanation:**
Set comprehension uses `{}` without `:`. Like sets, duplicates are removed. Remainders when dividing by 3 are only 0, 1, or 2. Result is `{0, 1, 2}` regardless of input size.

---

**Q6.35: Intermediate - [collections.Counter]**

What is the output?
```python
from collections import Counter
c = Counter('abracadabra')
print(c.most_common(2))
```

A) `[('a', 5), ('b', 2)]`
B) `{'a': 5, 'b': 2}`
C) `['a', 'b']`
D) `5`

**Answer: A**

**Explanation:**
`Counter` counts hashable objects. `'abracadabra'` has: a=5, b=2, r=2, c=1, d=1. `most_common(n)` returns n most frequent as list of (element, count) tuples. Great for frequency analysis.

---

**Q6.36: Intermediate - [Counter Operations]**

What is the output?
```python
from collections import Counter
c1 = Counter(['a', 'b', 'b'])
c2 = Counter(['b', 'c'])
print(c1 + c2)
```

A) `Counter({'b': 3, 'a': 1, 'c': 1})`
B) `{'a', 'b', 'c'}`
C) `Counter({'b': 2})`
D) Error

**Answer: A**

**Explanation:**
Counters support arithmetic. `+` adds counts: a=1, b=2+1=3, c=1. Also: `-` (subtracts, keeps positive), `&` (intersection/min), `|` (union/max). Very useful for combining frequency data.

---

**Q6.37: Intermediate - [collections.defaultdict]**

What is the advantage of defaultdict over regular dict?

A) It's faster
B) It automatically creates a default value for missing keys
C) It can store more keys
D) It preserves insertion order

**Answer: B**

**Explanation:**
`defaultdict(factory)` calls `factory()` for missing keys, avoiding KeyError. `defaultdict(list)` creates empty list for new keys. `defaultdict(int)` defaults to 0. Eliminates `if key not in d: d[key] = []` pattern.

---

**Q6.38: Intermediate - [defaultdict Example]**

What is the output?
```python
from collections import defaultdict
d = defaultdict(list)
d['a'].append(1)
d['a'].append(2)
d['b'].append(3)
print(dict(d))
```

A) `{'a': [1, 2], 'b': [3]}`
B) `{'a': 1, 'b': 3}`
C) `[[1, 2], [3]]`
D) Error

**Answer: A**

**Explanation:**
Accessing `d['a']` creates an empty list (default factory). Then `append(1)` and `append(2)` add to it. Same for 'b'. No KeyError, no manual initialization needed. Very clean for grouping data.

---

**Q6.39: Advanced - [OrderedDict]**

In Python 3.7+, when is OrderedDict still useful?

A) Never, regular dicts maintain order now
B) For comparing equality where order matters, and for move_to_end() method
C) Only for Python 2 compatibility
D) For faster lookups

**Answer: B**

**Explanation:**
Since Python 3.7, regular dicts maintain insertion order. But OrderedDict: (1) considers order in `==` comparison (dicts don't), (2) has `move_to_end()` method, (3) makes order-relevant intent explicit. Regular dicts are now usually sufficient.

---

**Q6.40: Intermediate - [collections.deque]**

What is the main advantage of deque over list?

A) deque uses less memory
B) O(1) append/pop on BOTH ends
C) deque can store more elements
D) deque is immutable

**Answer: B**

**Explanation:**
List has O(1) append/pop at end but O(n) at beginning (shifting required). `deque` (double-ended queue) has O(1) for both ends: `append()`, `appendleft()`, `pop()`, `popleft()`. Great for queues and sliding windows.

---

**Q6.41: Intermediate - [deque Operations]**

What is the output?
```python
from collections import deque
d = deque([1, 2, 3])
d.appendleft(0)
d.rotate(1)
print(list(d))
```

A) `[0, 1, 2, 3]`
B) `[3, 0, 1, 2]`
C) `[1, 2, 3, 0]`
D) Error

**Answer: B**

**Explanation:**
After `appendleft(0)`: `[0, 1, 2, 3]`. `rotate(1)` moves each element right by 1, with the last element wrapping to front. Result: `[3, 0, 1, 2]`. Negative rotation rotates left. Great for circular buffers.

---

**Q6.42: Intermediate - [deque maxlen]**

What is the output?
```python
from collections import deque
d = deque([1, 2, 3], maxlen=3)
d.append(4)
print(list(d))
```

A) `[1, 2, 3, 4]`
B) `[2, 3, 4]`
C) `[1, 2, 3]`
D) Error: overflow

**Answer: B**

**Explanation:**
`maxlen` creates a bounded deque. When full, adding to one end removes from the other. Adding 4 removes 1. Result: `[2, 3, 4]`. Perfect for "last N items" tracking, like command history.

---

**Q6.43: Intermediate - [collections.namedtuple]**

What is a namedtuple?

A) A tuple with named elements accessible by attribute or index
B) A dictionary with numeric keys
C) A tuple that can be renamed
D) A class that extends tuple

**Answer: A**

**Explanation:**
`namedtuple` creates a tuple subclass with named fields. `Point = namedtuple('Point', ['x', 'y'])`. Access via `p.x` (readable) or `p[0]` (index). Immutable like tuples. Memory-efficient alternative to classes for simple data.

---

**Q6.44: Intermediate - [namedtuple Example]**

What is the output?
```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(10, 20)
print(p.x, p[1])
```

A) `10, 20`
B) `x, y`
C) `Point(x=10, y=20), Point(x=10, y=20)`
D) Error

**Answer: A**

**Explanation:**
namedtuple supports both attribute access (`p.x` = 10) and index access (`p[1]` = 20). They're interchangeable. This combines tuple efficiency with class-like readability.

---

**Q6.45: Advanced - [ChainMap]**

What is `collections.ChainMap` used for?

A) Creating linked lists
B) Grouping multiple dicts into a single searchable view
C) Encrypting dictionaries
D) Converting dicts to chains

**Answer: B**

**Explanation:**
`ChainMap` groups multiple dicts, searching them in order. First dict with the key wins. Used for layered settings (defaults, user config, command line). `ChainMap(cli_args, user_config, defaults)` searches in that order.

---

**Q6.46: Advanced - [ChainMap Example]**

What is the output?
```python
from collections import ChainMap
defaults = {'color': 'red', 'size': 'medium'}
user = {'color': 'blue'}
cm = ChainMap(user, defaults)
print(cm['color'], cm['size'])
```

A) `blue, medium`
B) `red, medium`
C) Error
D) `blue, None`

**Answer: A**

**Explanation:**
`ChainMap` searches dicts in order. 'color' is found in `user` first → 'blue'. 'size' isn't in `user`, found in `defaults` → 'medium'. No merging — first match wins. Updates go to the first dict only.

---

**Q6.47: Basic - [array module]**

What is the difference between `array.array` and a list?

A) No difference
B) `array.array` stores only one type, using less memory
C) `array.array` is faster for all operations
D) Lists can't store numbers

**Answer: B**

**Explanation:**
`array.array('i', [1, 2, 3])` stores integers in a compact format (like C arrays). All elements must be the same type. Uses less memory than lists. For numeric computing, NumPy arrays are usually preferred.

---

**Q6.48: Advanced - [Hashability Requirement]**

What makes an object hashable?

A) Being stored in a hash table
B) Having `__hash__` method and consistent equality (if a == b, hash(a) == hash(b))
C) Being a built-in type
D) Having a unique id

**Answer: B**

**Explanation:**
Hashable objects must: (1) implement `__hash__` returning an integer, (2) maintain hash consistency over lifetime, (3) if `a == b`, then `hash(a) == hash(b)`. Mutable objects can't safely guarantee this, so they're typically unhashable.

---

**Q6.49: Intermediate - [List Copy]**

What is the output?
```python
a = [1, 2, [3, 4]]
b = a.copy()
b[2].append(5)
print(a)
```

A) `[1, 2, [3, 4]]`
B) `[1, 2, [3, 4, 5]]`
C) `[1, 2, [3, 4], 5]`
D) Error

**Answer: B**

**Explanation:**
⚠️ `copy()` is shallow — nested objects are still shared. `a[2]` and `b[2]` reference the same inner list. Modifying through `b` affects `a`. Use `copy.deepcopy()` for fully independent copies.

---

**Q6.50: Intermediate - [in Operator Efficiency]**

Which has O(1) average membership test with `in`?

A) list
B) tuple
C) set
D) deque

**Answer: C**

**Explanation:**
Sets use hash tables → O(1) average for `in`. Lists, tuples, deques are O(n) — must scan elements. For frequent membership tests, convert to set first. `x in my_set` is much faster than `x in my_list` for large collections.

---

**Q6.51: Intermediate - [Dict Keys View]**

What is unique about dict `.keys()`, `.values()`, `.items()` views?

A) They're always frozen copies
B) They're dynamic views that reflect dict changes
C) They can only be iterated once
D) They're slower than converting to list

**Answer: B**

**Explanation:**
Dict views are dynamic — they update when the dict changes. If you modify the dict after getting a view, the view reflects the change. This is memory-efficient (no copy), but can cause issues if modifying during iteration.

---

**Q6.52: Advanced - [Dict Ordering]**

Since which Python version are regular dicts guaranteed to maintain insertion order?

A) Python 3.5
B) Python 3.6 (implementation detail), Python 3.7 (language guarantee)
C) Python 2.7
D) Dicts never maintain order

**Answer: B**

**Explanation:**
CPython 3.6 implemented ordered dicts as an internal optimization. Python 3.7 made it a language guarantee. All dicts maintain insertion order. This doesn't mean sorted order — you still need `sorted()` for that.

---

**Q6.53: Basic - [List Multiplication]**

What is the output?
```python
lst = [[0]] * 3
lst[0][0] = 1
print(lst)
```

A) `[[1], [0], [0]]`
B) `[[1], [1], [1]]`
C) `[[0, 1], [0, 1], [0, 1]]`
D) Error

**Answer: B**

**Explanation:**
⚠️ **Major pitfall**: `*` replicates references, not objects. All three inner lists are the same object. Modifying one modifies all. Correct way: `[[0] for _ in range(3)]` creates independent lists.

---

**Q6.54: Intermediate - [List vs Tuple Usage]**

When should you prefer tuples over lists?

A) When you need mutability
B) For heterogeneous collections, as dict keys, or when immutability is desired
C) When you need fast appends
D) Never, lists are always better

**Answer: B**

**Explanation:**
💡 Tuples: (1) for heterogeneous data (like a record: name, age, email), (2) as dict keys or set elements (hashable), (3) when immutability prevents bugs, (4) slightly more memory-efficient. Lists: for homogeneous, mutable collections.

---

**Q6.55: Advanced - [Dict Key Requirements]**

Why can mutable objects not be dict keys?

A) Python limitation
B) If the key changes, its hash changes, making the entry unfindable
C) Mutable objects are too large
D) They can, you just need special syntax

**Answer: B**

**Explanation:**
Dict lookup uses hash to find the bucket. If a key mutates, its hash changes, but it's still in the old bucket. Lookup with the new hash fails to find it. This corrupts the dict. Immutability ensures consistent hashing.

---

**Q6.56: Intermediate - [Tuple as Dict Key]**

What is the output?
```python
d = {(1, 2): 'a', (3, 4): 'b'}
print(d[(1, 2)])
```

A) `'a'`
B) `(1, 2)`
C) Error: tuples can't be keys
D) `None`

**Answer: A**

**Explanation:**
Tuples of hashable elements are hashable, so they can be dict keys. `(1, 2)` is a valid key. Useful for multi-dimensional indexing: `matrix[(row, col)] = value`. Lists can't be keys, but tuples can.

---

**Q6.57: Advanced - [Memory Efficient Alternatives]**

For millions of small objects with fixed attributes, what's more memory-efficient than regular classes?

A) Lists
B) `__slots__` or namedtuple
C) Dictionaries
D) More RAM

**Answer: B**

**Explanation:**
Regular classes have `__dict__` per instance (memory overhead). `__slots__` eliminates `__dict__`, fixing attribute set. namedtuple is even more compact. For large numbers of simple objects, this saves significant memory.

---

**Q6.58: Intermediate - [Sorting Stability]**

Python's sort is "stable". What does this mean?

A) It never crashes
B) Equal elements maintain their original relative order
C) It always produces the same result
D) It's numerically stable

**Answer: B**

**Explanation:**
Stable sorting preserves original order for equal elements. If items with same sort key were at positions 3 and 7, they stay in that relative order after sorting. This is useful for multi-key sorting: sort by secondary key, then primary.

---

**Q6.59: Advanced - [heapq]**

What does `heapq` provide?

A) A heap data structure class
B) Functions to use a list as a min-heap
C) Priority queue implementation
D) Memory heap management

**Answer: B**

**Explanation:**
`heapq` provides heap operations on regular lists: `heappush`, `heappop`, `heapify`. It's a min-heap — smallest element is always at index 0. For max-heap, negate values. Used for priority queues and finding top-k elements efficiently.

---

**Q6.60: Intermediate - [bisect]**

What does the `bisect` module do?

A) Splits lists in half
B) Maintains sorted lists by providing binary search insertion points
C) Sorts lists faster
D) Compares two lists

**Answer: B**

**Explanation:**
`bisect.bisect_left(lst, x)` finds insertion point to keep list sorted. `bisect.insort(lst, x)` inserts while maintaining order. Binary search is O(log n); inserting is still O(n) due to shifting. Useful for maintaining sorted sequences.

---

**Q6.61: Intermediate - [Nested List Comprehension]**

What is the output?
```python
matrix = [[1, 2], [3, 4], [5, 6]]
flat = [x for row in matrix for x in row]
print(flat)
```

A) `[[1, 2], [3, 4], [5, 6]]`
B) `[1, 2, 3, 4, 5, 6]`
C) `[[1, 3, 5], [2, 4, 6]]`
D) Error

**Answer: B**

**Explanation:**
Nested comprehension reads left-to-right like nested for loops. Outer: `for row in matrix`. Inner: `for x in row`. Flattens the 2D list to 1D. For the transpose (columns), you'd use `[[row[i] for row in matrix] for i in range(len(matrix[0]))]`.

---

**Q6.62: Basic - [Dict pop()]**

What is the output?
```python
d = {'a': 1, 'b': 2}
val = d.pop('b')
print(val, d)
```

A) `2, {'a': 1}`
B) `{'a': 1}, 2`
C) `None, {'a': 1, 'b': 2}`
D) Error

**Answer: A**

**Explanation:**
`pop(key)` removes the key-value pair and returns the value. 'b' is removed, 2 is returned. `pop(key, default)` avoids KeyError if missing. Compare with `del d['b']` which removes but doesn't return the value.

---

**Q6.63: Intermediate - [Dict popitem()]**

What does `d.popitem()` do in Python 3.7+?

A) Removes a random item
B) Removes and returns the last inserted key-value pair (LIFO)
C) Removes the first item
D) Pops only if dict is non-empty

**Answer: B**

**Explanation:**
In Python 3.7+, dicts are ordered. `popitem()` removes and returns the last inserted item as a (key, value) tuple (LIFO order). In older versions, it was arbitrary. Useful for processing dicts in stack-like manner.

---

**Q6.64: Advanced - [Dict Comparison]**

What is the output?
```python
d1 = {'a': 1, 'b': 2}
d2 = {'b': 2, 'a': 1}
print(d1 == d2)
```

A) `True`
B) `False`
C) Error
D) Depends on Python version

**Answer: A**

**Explanation:**
Dict equality compares only content (keys and values), not insertion order. `d1` and `d2` have the same key-value pairs, so they're equal. For order-sensitive comparison, use `OrderedDict` or compare `list(d.items())`.

---

**Q6.65: Expert - [Dict Subclass Detection]**

How can you check if an object is dict-like?

A) `type(obj) == dict`
B) `isinstance(obj, dict)`
C) `isinstance(obj, collections.abc.Mapping)`
D) `hasattr(obj, 'keys')`

**Answer: C**

**Explanation:**
💡 `collections.abc.Mapping` is the abstract base class for dict-like objects. This catches regular dicts, OrderedDict, ChainMap, defaultdict, and other dict-like objects. `isinstance(obj, dict)` misses subclasses and dict-like non-dicts. ABC check is most Pythonic.

---

**Q6.66: Intermediate - [List Index]**

What is the output?
```python
lst = [10, 20, 30, 20, 40]
print(lst.index(20))
```

A) `1`
B) `3`
C) `[1, 3]`
D) `20`

**Answer: A**

**Explanation:**
`index(value)` returns the index of the FIRST occurrence. 20 first appears at index 1. To find all occurrences, use comprehension: `[i for i, x in enumerate(lst) if x == 20]`. Raises ValueError if not found.

---

**Q6.67: Basic - [List Count]**

What is the output?
```python
lst = [1, 2, 2, 3, 2, 4]
print(lst.count(2))
```

A) `2`
B) `3`
C) `1`
D) `[1, 3, 4]`

**Answer: B**

**Explanation:**
`count(value)` returns the number of occurrences. 2 appears at indices 1, 2, 4 — three times. O(n) operation — scans entire list. For frequent counting, use `collections.Counter`.

---

**Q6.68: Intermediate - [Tuple Methods]**

Which methods do tuples have?

A) `append`, `extend`, `pop`
B) `count`, `index`
C) `sort`, `reverse`
D) No methods at all

**Answer: B**

**Explanation:**
Tuples are immutable, so no modifying methods. They only have `count()` (occurrences) and `index()` (position of value). Same behavior as list equivalents. No `sort()`/`reverse()` — use `sorted(t)`/`reversed(t)` to get new sequences.

---

**Q6.69: Advanced - [Slot List Gotcha]**

What is the issue with `[[]] * n` for creating a 2D grid?

A) Too slow
B) Creates references to the same inner list, not n independent lists
C) Uses too much memory
D) Nothing wrong

**Answer: B**

**Explanation:**
`[[]] * n` creates `n` references to the SAME empty list. Modifying any "row" affects all of them. Correct: `[[] for _ in range(n)]` creates n independent lists. This is one of Python's most common gotchas for beginners.

---

**Q6.70: Intermediate - [Deque vs List]**

When is list better than deque?

A) For queue operations
B) For random access by index (O(1) list vs O(n) deque)
C) For stack operations
D) Never, deque is always better

**Answer: B**

**Explanation:**
Lists have O(1) random access (`lst[i]`). Deques have O(n) for accessing middle elements (must traverse from an end). deque is for queue/stack operations at ends. For random access patterns, use lists.

---

**Q6.71: Basic - [in Operator]**

What is the output?
```python
print(3 in [1, 2, 3])
print('a' in 'abc')
print('x' in {'x': 1})
```

A) `True, True, True`
B) `True, True, False`
C) `True, False, True`
D) `False, True, True`

**Answer: A**

**Explanation:**
`in` works for: lists (element check), strings (substring check), dicts (key check, not value). 3 is in the list, 'a' is in the string, 'x' is a key in the dict. All three are True.

---

**Q6.72: Intermediate - [Sorted with Multiple Keys]**

What is the output?
```python
data = [('a', 2), ('b', 1), ('a', 1)]
sorted_data = sorted(data, key=lambda x: (x[0], x[1]))
print(sorted_data)
```

A) `[('a', 1), ('a', 2), ('b', 1)]`
B) `[('a', 2), ('a', 1), ('b', 1)]`
C) `[('b', 1), ('a', 1), ('a', 2)]`
D) `[('a', 2), ('b', 1), ('a', 1)]`

**Answer: A**

**Explanation:**
Sorting by tuple compares element-by-element. First by `x[0]` (letter), then by `x[1]` (number) for ties. 'a' before 'b'. Among 'a' items, 1 before 2. Result: `('a', 1), ('a', 2), ('b', 1)`.

---

**Q6.73: Advanced - [__contains__ Method]**

What method does `in` operator call?

A) `__in__`
B) `__contains__`
C) `__has__`
D) `__member__`

**Answer: B**

**Explanation:**
`x in obj` calls `obj.__contains__(x)`. If not defined, Python falls back to iteration (`__iter__`). Custom classes can implement `__contains__` for efficient membership testing. Sets' fast `in` is due to their `__contains__` using hash lookup.

---

**Q6.74: Intermediate - [Reversing Sequences]**

What are three ways to reverse a list `lst`?

A) `lst.reverse()`, `reversed(lst)`, `lst[::-1]`
B) `reverse(lst)`, `lst.flip()`, `lst[-1:0:-1]`
C) `lst.reverse()`, `sorted(lst, reverse=True)`, `lst[::-1]`
D) There's only one way

**Answer: A**

**Explanation:**
(1) `lst.reverse()` reverses in-place, returns None. (2) `reversed(lst)` returns an iterator (lazy). (3) `lst[::-1]` creates a new reversed list. Note: `sorted(lst, reverse=True)` sorts in reverse order, which is different from reversing.

---

**Q6.75: Expert - [Dict Internals]**

What data structure does Python's dict use internally?

A) Linked list
B) Hash table with open addressing
C) Binary search tree
D) Array of arrays

**Answer: B**

**Explanation:**
Python dicts use hash tables. Keys are hashed to find buckets. Open addressing (specifically, a variant of it) handles collisions. This gives O(1) average for lookup/insert/delete. The implementation changed in Python 3.6 for better memory efficiency and ordering.

---

## Chapter Summary

**Total MCQs: 75**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 22 | 29% |
| Intermediate | 40 | 53% |
| Advanced | 11 | 15% |
| Expert | 2 | 3% |

**Key Topics Covered:**
- Lists: methods, slicing, copying, comprehensions
- Tuples: creation, unpacking, immutability
- Sets: operations, frozenset, hashability
- Dictionaries: methods, views, comprehensions
- collections module: Counter, defaultdict, OrderedDict, deque, ChainMap, namedtuple
- Shallow vs deep copy
- Membership testing efficiency
- Sorting with keys
