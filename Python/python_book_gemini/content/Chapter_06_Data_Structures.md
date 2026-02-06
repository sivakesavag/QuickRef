# Chapter 6: Data Structures

**Target MCQs**: 60-70
**Current Batch**: 1-30
**Topics Covered**: Lists (internals, complexity), Tuples, Sets, Dictionaries (hashing, collision), Views, Comprehensions (structural details).

---

**Q6.1: Basic - [List Complexity]**

What is the time complexity of `len(my_list)` in Python?

A) O(n) - Linear scan.
B) O(1) - Constant time.
C) O(log n).
D) Depends on list contents.

**Answer: B**

**Explanation:**
Python lists store their length as a metadata field (`ob_size` in C struct). Retrieving it is an instant field lookup.

---

**Q6.2: Intermediate - [List Pop]**

Which operation is strictly slower on a large standard Python list?

A) `list.pop()`
B) `list.pop(0)`
C) `list.append(x)`
D) `list[0]`

**Answer: B**

**Explanation:**
`pop(0)` removes the first element, requiring all subsequent elements (`N-1`) to shift memory addresses by one position to the left. Its complexity is O(N). `pop()` (end) is O(1).

---

**Q6.3: Advanced - [List Internals]**

Under the hood, a Python list is implemented as:

A) A Linked List.
B) A Dynamic Array (contiguous memory of pointers).
C) A Hash Table.
D) A Binary Search Tree.

**Answer: B**

**Explanation:**
Python lists are dynamic arrays of pointers to Python objects. This allows O(1) indexing but requires O(N) for insertions/deletions at the beginning/middle.

---

**Q6.4: Basic - [Tuple Immutability]**

If `t = (1, [2, 3])`, can you assume `t` never changes value?

A) Yes, tuples are immutable.
B) No, the *contents* of mutable elements inside the tuple can change.
C) Only if the list is frozen.
D) Error, tuples cannot contain lists.

**Answer: B**

**Explanation:**
The tuple `t` strictly holds the *reference* to the list. That reference cannot change (you can't swap the list for another object). However, the list object itself remains mutable and can grow/shrink (`t[1].append(4)` works).

---

**Q6.5: Intermediate - [Dict Key Requirement]**

Which object cannot be used as a key in a dictionary?

A) `(1, 2)`
B) `frozenset([1, 2])`
C) `[1, 2]`
D) `1`

**Answer: C**

**Explanation:**
Dictionary keys must be **hashable**. Lists are mutable and unhashable (because if they changed, their hash would change, breaking the lookup). Tuples are hashable only if all their elements are hashable.

---

**Q6.6: Advanced - [Hash Collision]**

What happens if two keys in a dictionary have the same hash value?

A) The second key overwrites the first.
B) `CollisionError` is raised.
C) Python uses Open Addressing (probing) to find the next empty slot.
D) Python uses separate chaining (linked lists) for collisions.

**Answer: C**

**Explanation:**
CPython uses open addressing (specifically a pseudo-random probing sequence) to resolve collisions. It checks the next slot in the probe sequence until it finds an exact match (hash + equality check) or an empty slot.

---

**Q6.7: Basic - [Set Elements]**

`{1, 2, 3, 3, 2, 1}` results in:

A) `{1, 2, 3}`
B) `{1, 2, 3, 3, 2, 1}`
C) Error.
D) A tuple.

**Answer: A**

**Explanation:**
Sets are unordered collections of *unique* elements. Duplicates are automatically removed during construction.

---

**Q6.8: Intermediate - [Set Operations]**

What operator performs symmetric difference (elements in A or B but not both)?

A) `A & B`
B) `A | B`
C) `A ^ B`
D) `A - B`

**Answer: C**

**Explanation:**
`^` (XOR behavior) calculates the symmetric difference.
`&` is intersection. `|` is union. `-` is difference.

---

**Q6.9: Advanced - [Dict Ordering]**

Since Python 3.7+, are dictionary items ordered?

A) No, they are inherently unordered (hashing randomization).
B) Yes, insertion order is guaranteed.
C) Only in `OrderedDict`.
D) Only for string keys.

**Answer: B**

**Explanation:**
Standard `dict` matches insertion order as a language specification guarantee since Python 3.7. (It was an implementation detail in 3.6).

---

**Q6.10: Expert - [Dict View Objects]**

`keys = d.keys()`. If `d` changes size, does `keys` reflect it?

A) No, `keys()` returns a static list copy.
B) Yes, `keys()` returns a dynamic View object.
C) It raises `RuntimeError` if accessed after change.
D) Only if re-assigned.

**Answer: B**

**Explanation:**
`d.keys()`, `d.values()`, `d.items()` return **View objects**. They are dynamic windows into the dictionary's current state. If `d` is updated, iterating `keys` yields the new data (or raises RuntimeError if iterating *during* the change).

---

**Q6.11: Basic - [List Remove]**

`x = [1, 2, 3]; x.remove(2)`. What is `x`?

A) `[1, 3]`
B) `[1, 2]`
C) `[1, None, 3]`
D) `[2]`

**Answer: A**

**Explanation:**
`remove(v)` deletes the first occurrence of `v`.

---

**Q6.12: Intermediate - [Sort Stability]**

Python's `sort()` algorithm (Timsort) is "stable". What does this mean?

A) It never crashes.
B) It has guaranteed O(N log N) worst case.
C) It preserves the relative order of elements that compare equal.
D) It uses constant memory.

**Answer: C**

**Explanation:**
Stability means if two items compare equal (e.g., sorting people by age, picking two 25-year-olds), they remain in the same order as they were in the original list.

---

**Q6.13: Advanced - [Hash Implementation]**

For a user-defined class to be usable as a dict key, it must implement:

A) `__key__`
B) `__hash__` AND `__eq__`
C) `__id__`
D) Only `__hash__`

**Answer: B**

**Explanation:**
It needs `__hash__` to determine the slot and `__eq__` to verify identity/equality in case of hash collisions. If two objects are equal (`==`), their hashes *must* be equal.

---

**Q6.14: Basic - [None in Dict]**

Can `None` be a key in a dictionary?

A) Yes.
B) No.
C) Only in `defaultdict`.
D) Only if the value is also None.

**Answer: A**

**Explanation:**
`None` is a singleton, immutable, and hashable object. It is a perfectly valid key.

---

**Q6.15: Intermediate - [Extend vs Append]**

```python
x = [1, 2]
x.append([3, 4])
y = [1, 2]
y.extend([3, 4])
```
What are `x` and `y`?

A) `x`: `[1, 2, 3, 4]`, `y`: `[1, 2, [3, 4]]`
B) `x`: `[1, 2, [3, 4]]`, `y`: `[1, 2, 3, 4]`
C) Both `[1, 2, 3, 4]`
D) Both `[1, 2, [3, 4]]`

**Answer: B**

**Explanation:**
`append` adds the object as a single element. `extend` iterates over the argument and adds each element.

---

**Q6.16: Advanced - [Set Internals]**

A Python `set` is effectively implemented as:

A) A dict with dummy values.
B) A Red-Black tree.
C) A sorted list.
D) A bloom filter.

**Answer: A**

**Explanation:**
A set uses the same hash table probing mechanism as a dictionary, storing only keys (optimization avoids storing values memory-wise, but logic is identical to a dict with no values).

---

**Q6.17: Basic - [Count Method]**

`[1, 2, 1, 3].count(1)` returns:

A) 1
B) 2
C) `True`
D) `[0, 2]`

**Answer: B**

**Explanation:**
`count(x)` returns the number of occurrences of `x`.

---

**Q6.18: Intermediate - [Dict Get Default]**

`d.get("key", 0)` is useful because:

A) It sets the key to 0 if missing.
B) It returns 0 if "key" is missing, preventing KeyError.
C) It is faster than `d["key"]`.
D) It always returns 0.

**Answer: B**

**Explanation:**
`get` handles missing keys gracefully by returning a default (None or specified value) instead of raising an exception.

---

**Q6.19: Expert - [Set Discard vs Remove]**

What is the difference between `set.discard(x)` and `set.remove(x)`?

A) No difference.
B) `discard` raises KeyError if x is missing; `remove` does not.
C) `remove` raises KeyError if x is missing; `discard` does not (no-op).
D) `discard` assumes x is a set.

**Answer: C**

**Explanation:**
`remove(x)` enforces strict presence (raising error if missing). `discard(x)` is safe to call even if element doesn't exist.

---

**Q6.20: Advanced - [Comparison of Tuples]**

`(1, 2, 3) < (1, 2, 4)` is:

A) True
B) False
C) TypeError
D) Valid only in Python 2.

**Answer: A**

**Explanation:**
Sequences are compared lexicographically element by element. 1==1, 2==2, 3 < 4 (True).

---

**Q6.21: Intermediate - [Any Hashable]**

Which of these is NOT hashable?

A) `1`
B) `"hello"`
C) `(1, 2)`
D) `({1}, 2)`

**Answer: D**

**Explanation:**
The tuple `({1}, 2)` contains a set `{1}`, which is mutable. Therefore, the tuple itself becomes unhashable. Recursive immutability is required.

---

**Q6.22: Basic - [Empty Check]**

Which is the most "Pythonic" way to check if a list `my_list` is empty?

A) `if len(my_list) == 0:`
B) `if my_list == []:`
C) `if not my_list:`
D) `if my_list.empty():`

**Answer: C**

**Explanation:**
It relies on the Truthiness of the list object (empty list is Falsy), avoiding function calls (`len`) or object creation (`[]`).

---

**Q6.23: Advanced - [Popitem]**

`d.popitem()` on a standard Python 3.7+ dictionary removes:

A) A random item.
B) The last inserted item (LIFO).
C) The first inserted item (FIFO).
D) The smallest key.

**Answer: B**

**Explanation:**
Since dictionaries preserve insertion order, `popitem()` is guaranteed to remove and return the last item inserted (acting like a stack). Before 3.7, it was arbitrary.

---

**Q6.24: Expert - [List Strategy]**

When a list needs to grow (append), Python over-allocates memory. What is the approximate growth factor?

A) 2x (Doubling).
B) 1.5x (roughly).
C) 1.125x (1/8th).
D) Exact size + 1.

**Answer: C**

**Explanation:**
CPython uses a growth pattern: 0, 4, 8, 16, 25, 35, 46... roughly `new_size = size + (size >> 3) + (3 or 6)`. It's roughly ~1.125x (12.5%) for large lists, closer to doubling for very small ones. Choosing ~1.125 or generic "over-allocation" is key; it's not strictly 2x like C++ Vectors often are. *Self-correction: The options might be tricky. Closest general answer often taught is "over-allocates proportionally", usually cited as ~1.125. Option B is common in other languages (Java ArrayList 1.5, C++ Vector 2). Let's stick to C (1.125 / 12.5%) as the CPython specific answer.*

---

**Q6.25: Intermediate - [Set Union Operator]**

Instead of `s1.union(s2)`, you can use:

A) `s1 + s2`
B) `s1 | s2`
C) `s1 or s2`
D) `s1 & s2`

**Answer: B**

**Explanation:**
`|` is the bitwise OR operator overloaded for set union. `+` is not supported for sets (ambiguous meaning).

---

**Q6.26: Basic - [Dict Constructor]**

`dict(a=1, b=2)` creates:

A) `{'a': 1, 'b': 2}`
B) `{a: 1, b: 2}` (using variable values)
C) Error.
D) `[('a', 1), ('b', 2)]`

**Answer: A**

**Explanation:**
When using `dict()` with keyword arguments, the argument names become string keys.

---

**Q6.27: Advanced - [Comprehension Scope leaking]**

`x = 100; [x for x in range(5)]`. In Python 3, what is `x` after this line?

A) 4
B) 100
C) 0
D) 5

**Answer: B**

**Explanation:**
In Python 3, list comprehensions have their own scope. The iteration variable `x` does not leak into or overwrite the enclosing scope variable `x`. (In Python 2, it did leak).

---

**Q6.28: Intermediate - [Tuple Assignment Trick]**

`a = 10; b = 20`. Syntax `a, b = b, a` performs:

A) Swap.
B) Error.
C) `a` becomes `(20, 10)`.
D) No change.

**Answer: A**

**Explanation:**
Standard pythonic swap via tuple packing (RHS creates tuple `(20, 10)`) and unpacking (LHS assigns `a=20, b=10`).

---

**Q6.29: Expert - [`__missing__`]**

Which method should you implement in a `dict` subclass to handle missing keys naturally (like `defaultdict`)?

A) `__getitem__`
B) `__missing__`
C) `__default__`
D) `__error__`

**Answer: B**

**Explanation:**
`__missing__(self, key)` is called by `dict.__getitem__` when a key is not found. Implementing this allows custom default behaviors.

---

**Q6.30: Basic - [Max Function]**

`max([1, 5, 2, 9])` returns:

A) 9
B) 1
C) Index of 9.
D) Error.

**Answer: A**

**Explanation:**
`max` returns the largest item in the iterable.

---

**Q6.31: Intermediate - [Defaultdict]**

`from collections import defaultdict`. What happens when you access a missing key in a `defaultdict(list)`?

A) It returns `None`.
B) It raises `KeyError`.
C) It automatically creates a new empty list `[]` for that key and returns it.
D) It returns `[]` but doesn't store it.

**Answer: C**

**Explanation:**
`defaultdict` calls the factory function (`list`, which produces `[]`) to provide a default value, inserts it into the dictionary, and returns it.

---

**Q6.32: Basic - [Deque vs List]**

`collections.deque` is optimized for:

A) Random access.
B) Fast appends and pops from both ends.
C) Sorting.
D) Hashing.

**Answer: B**

**Explanation:**
`deque` (double-ended queue) is implemented as a doubly linked list of blocks. It provides O(1) complexity for append/pop at both ends, whereas standard `list` is O(N) for operations at the beginning (index 0).

---

**Q6.33: Advanced - [Counter Arithmetic]**

`from collections import Counter`.
`c = Counter(a=3, b=1)`. `d = Counter(a=1, b=2)`.
What is `c - d`?

A) `Counter({'a': 2, 'b': -1})`
B) `Counter({'a': 2})`
C) `Counter({'a': 2, 'b': 0})`
D) Error.

**Answer: B**

**Explanation:**
`Counter` subtraction keeps only positive counts. Elements with zero or negative counts are removed from the result. `a: 3-1=2`. `b: 1-2=-1` (removed).

---

**Q6.34: Expert - [NamedTuple Memory]**

Compared to a regular class or dictionary, does `namedtuple` use less memory?

A) No, it uses more because of metadata.
B) Yes, it's just a tuple with named access properties.
C) Same as a dictionary.
D) Same as a list.

**Answer: B**

**Explanation:**
Instances of named tuples are just tuples (compact C array of pointers) with no per-instance `__dict__`. They are extremely memory efficient. Access is handled via property descriptors generated on the class.

---

**Q6.35: Intermediate - [Heapq]**

`heapq.heappop(h)` returns:

A) The largest element.
B) The random element.
C) The smallest element.
D) The last element.

**Answer: C**

**Explanation:**
Python's `heapq` module implements a **min-heap**. `heappop` returns the smallest item (root of the heap).

---

**Q6.36: Advanced - [Key Error vs Index Error]**

If `d` is a dictionary and `l` is a list, accessing `d[missing]` and `l[out_of_bounds]` raises:

A) KeyError, KeyError.
B) IndexError, IndexError.
C) KeyError, IndexError.
D) ValueError, IndexError.

**Answer: C**

**Explanation:**
Dictionaries raise `KeyError` for missing keys. Sequences (lists, tuples) raise `IndexError` for out-of-range indices.

---

**Q6.37: Basic - [Tuple Concatenation]**

`(1, 2) + (3, 4)` results in:

A) `(1, 2, 3, 4)`
B) `((1, 2), (3, 4))`
C) Error.
D) `[1, 2, 3, 4]`

**Answer: A**

**Explanation:**
`+` operator concatenates two tuples into a new tuple.

---

**Q6.38: Intermediate - [ChainMap]**

`collections.ChainMap` is used to:

A) Merge multiple dictionaries into one new dictionary.
B) Link multiple dictionaries together to check them sequentially as a single unit.
C) Chain function calls.
D) Map a function over a chain of iterables.

**Answer: B**

**Explanation:**
`ChainMap` takes multiple mappings and treats them as a layered unit. Lookups search the first mapping, then the second, etc. It does not copy data; it references the original dicts.

---

**Q6.39: Advanced - [Dict Resize Probability]**

When a Python dictionary resizes (grows), what happens to the internal order of items (pre-3.7)?

A) It stays exactly the same.
B) It changes arbitrarily based on new hash modulus.
C) It reverses.
D) It gets sorted.

**Answer: B**

**Explanation:**
When the table size changes, the index (`hash % new_size`) changes. This re-shuffling is why dictionary iteration order was undefined/random-looking before 3.6/3.7. (Stability in 3.7+ is achieved by a dense array + sparse index array architecture, effectively preserving insertion order even after resize).

---

**Q6.40: Expert - [Bisect]**

`bisect.bisect_left(sorted_list, x)` returns an insertion point `i`. What property holds for `i`?

A) `all(val < x for val in sorted_list[:i])` and `all(val >= x for val in sorted_list[i:])`
B) `sorted_list[i] == x`
C) `sorted_list[i] > x`
D) `i` is the midpoint.

**Answer: A**

**Explanation:**
`bisect_left` finds the first index where `x` could be inserted while maintaining order. All elements to the left are `< x`. All elements to the right (including `i`) are `>= x`.

---

**Q6.41: Basic - [Immutable Set]**

Which built-in type represents an immutable set?

A) `iset`
B) `immutable_set`
C) `frozenset`
D) `tupleset`

**Answer: C**

**Explanation:**
`frozenset` is the immutable version of a set. It is hashable and can be used as a dictionary key or an element of another set.

---

**Q6.42: Intermediate - [List Copy]**

`new_list = old_list[:]` creates:

A) A shallow copy.
B) A deep copy.
C) A reference (alias).
D) A view.

**Answer: A**

**Explanation:**
Slicing `[:]` creates a new list object containing references to the same items as the original list (Shallow Copy).

---

**Q6.43: Advanced - [Refcount list]**

If `a = [1]`, `b = a`, `c = [a]`. How many references to the list object `[1]` exist?

A) 1
B) 2
C) 3
D) 4

**Answer: C**

**Explanation:**
1 (variable `a`) + 1 (variable `b`) + 1 (inside list `c`). Total 3 strong references.

---

**Q6.44: Expert - [Dict Key Coercion]**

If you have a dict `{1: 'a', True: 'b'}`. What is the content of the dict?

A) `{1: 'a', True: 'b'}` (both keys exist)
B) `{1: 'b'}` (keys collided and overwrote)
C) `{True: 'b'}`
D) Error.

**Answer: B**

**Explanation:**
`True` equals `1` and `hash(True) == hash(1)`. Python processes the dict literal left-to-right. `1` is inserted. Then `True` is processed: matches `1`. The key is **not** updated (it remains `1`), but the value is updated to `'b'`. Result is `{1: 'b'}`.

---

**Q6.45: Basic - [Range Type]**

Is `range` a data structure?

A) No, it's a function.
B) No, it's a generator.
C) Yes, it's an immutable sequence type.
D) Yes, it's a list.

**Answer: C**

**Explanation:**
`range` is a class (type) in Python 3. It creates an immutable sequence object that supports indexing `r[0]`, hashing (in 3.x), and iteration.

---

**Q6.46: Intermediate - [Set Difference]**

`{1, 2, 3} - {2, 3, 4}` results in:

A) `{1}`
B) `{1, 4}`
C) `{1, 2, 3}`
D) Error.

**Answer: A**

**Explanation:**
Set difference (`-`) returns elements in the first set that are NOT in the second. (`4` is ignored as it wasn't in the first).

---

**Q6.47: Advanced - [Queue Module]**

`queue.Queue` is designed for:

A) Fast data processing in single threads.
B) Thread-safe multi-producer, multi-consumer FIFO queues.
C) Networking buffers only.
D) Inter-process communication.

**Answer: B**

**Explanation:**
The `queue` module provides synchronized (locking) queue classes suitable for threading. For simple non-threaded FIFO, `collections.deque` is faster.

---

**Q6.48: Basic - [Tuple Packing]**

`val = 1, 2, 3`. What type is `val`?

A) Integer
B) Tuple
C) List
D) String

**Answer: B**

**Explanation:**
Comma separation without brackets implicitly packs values into a tuple.

---

**Q6.49: Intermediate - [Dictionary Comprehension]**

`{x: x**2 for x in (2, 3)}` returns:

A) `{(2, 4), (3, 9)}`
B) `[2: 4, 3: 9]`
C) `{2: 4, 3: 9}`
D) `(2: 4, 3: 9)`

**Answer: C**

**Explanation:**
This is the syntax for a dictionary comprehension, creating key-value pairs.

---

**Q6.50: Advanced - [WeakRef]**

Which module allows creating references to objects that do not increase the reference count (allowing garbage collection)?

A) `sys`
B) `gc`
C) `weakref`
D) `pointers`

**Answer: C**

**Explanation:**
`weakref` module allows creating weak references. If the only references to an object are weak, the garbage collector can destroy it.

---

**Q6.51: Expert - [OrderedDict vs Dict]**

In Python 3.7+, `dict` preserves insertion order. What feature does `collections.OrderedDict` still have that `dict` does NOT?

A) `popitem()`
B) Reversibility (`reversed(d)`) - (Actually dict supports this now too).
C) Equality check considers order.
D) `update()`.

**Answer: C**

**Explanation:**
For standard dicts, order is ignored during equality checks (`{'a':1, 'b':2} == {'b':2, 'a':1}` is True). For `OrderedDict`, order matters (`OrderedDict([('a',1), ('b',2)]) != OrderedDict([('b',2), ('a',1)])`). Also `OrderedDict` has `move_to_end()`.

---

**Q6.52: Intermediate - [List Index]**

`[1, 2, 3].index(4)` raises:

A) `ValueError`
B) `IndexError`
C) `KeyError`
D) Returns -1

**Answer: A**

**Explanation:**
`list.index(x)` searches for x and returns its index. If not found, it raises `ValueError`.

---

**Q6.53: Advanced - [Struct Module]**

The `struct` module is primarily used for:

A) Creating C-struct-like objects in Python.
B) Packing/unpacking binary data to/from Python values (e.g. for network/files).
C) Organizing code structure.
D) Creating immutable classes.

**Answer: B**

**Explanation:**
`struct` converts between Python values and C structs represented as Python `bytes` objects. Used for handling binary file formats or network packets.

---

**Q6.54: Basic - [Mutable Types]**

Which of the following is MUTABLE?

A) `str`
B) `int`
C) `tuple`
D) `bytearray`

**Answer: D**

**Explanation:**
`str`, `int`, `tuple` are immutable. `bytearray` is a mutable sequence of bytes.

---

**Q6.55: Intermediate - [Deque Maxlen]**

`d = deque(maxlen=3)`. If you append a 4th item, what happens?

A) `IndexError`.
B) The deque grows to size 4.
C) The oldest item is automatically discarded.
D) `BufferError`.

**Answer: C**

**Explanation:**
A `deque` with a fixed `maxlen` acts as a circular buffer. Pushing a new item discards the item from the opposite end.

---

**Q6.56: Advanced - [Key Sort]**

To sort a list of strings by their length, use:

A) `list.sort(key=len)`
B) `list.sort(cmp=len)`
C) `list.sort(by=len)`
D) `list.sort(reverse=len)`

**Answer: A**

**Explanation:**
The `key` parameter accepts a callable that transforms each element before comparison.

---

**Q6.57: Expert - [Dict Size Iteration]**

Why does `len(d)` work in O(1) for a dictionary?

A) It counts keys on demand.
B) It stores the size in the `PyDictObject` struct.
C) It computes lookup table utilization.
D) It sums the linked lists.

**Answer: B**

**Explanation:**
Like lists, dictionaries maintain a `ma_used` field in their C struct that tracks the number of active items.

---

**Q6.58: Intermediate - [Generator Space]**

Which uses less memory to represent the numbers 0 to 1,000,000?

A) `[x for x in range(1000000)]`
B) `(x for x in range(1000000))`
C) `list(range(1000000))`
D) A tuple of 1M items.

**Answer: B**

**Explanation:**
B is a generator expression. It produces values one by one and (mostly) occupies constant memory size. A creates a full list in memory.

---

**Q6.59: Advanced - [Set Update]**

`s = {1, 2}`. `s.update([2, 3, 4])`. What is `s`?

A) `{1, 2, [2, 3, 4]}`
B) `{1, 2, 2, 3, 4}`
C) `{1, 2, 3, 4}`
D) Error.

**Answer: C**

**Explanation:**
`update()` takes an iterable and adds its elements to the set (union-inplace).

---

**Q6.60: Basic - [Del]**

To remove an item from a list by index:

A) `del my_list[i]`
B) `my_list.delete(i)`
C) `my_list.erase(i)`
D) `my_list.remove(i)`

**Answer: A**

**Explanation:**
`del` is a statement that removes the binding or the item at the index. `remove(v)` removes by value. (You can also use `pop(i)`).

---

---

## Review Notes (2026-02-06)

- Q6.44 has an answer-key conflict: `**Answer: C**` but the explanation concludes "So answer is B."
- Q6.44 includes drafting/self-correction text that should be cleaned for production content.
- Q6.14 and Q6.58 use only A/B options, which is inconsistent with the predominant 4-option MCQ format.
