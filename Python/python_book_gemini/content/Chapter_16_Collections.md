# Chapter 16: Advanced Collections & Algorithms

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `collections` (`deque`, `defaultdict`, `Counter`, `namedtuple`), `heapq` (heaps), `bisect` (binary search), `copy` modules, `itertools` recipes, `enum` basics.

---

**Q16.1: Basic - [Deque Definition]**

`collections.deque` is optimized for:

A) Random access (indexing).
B) Fast appends and pops from both ends.
C) Sorting.
D) Matrix operations.

**Answer: B**

**Explanation:**
`deque` (double-ended queue) provides O(1) time complexity for append/pop operations at both ends, whereas lists are O(n) for inserting/popping at the beginning `[0]`.

---

**Q16.2: Intermediate - [Defaultdict]**

`d = defaultdict(list)`: Accessing a missing key `d['k']`:

A) Raises `KeyError`.
B) Returns `None`.
C) Creates a new empty list `[]`, inserts it at `d['k']`, and returns it.
D) Returns `list` type.

**Answer: C**

**Explanation:**
It calls the factory function (`list`) to provide a default value for the missing key, setting it in the dictionary.

---

**Q16.3: Advanced - [Heapq Push]**

`heapq.heappush(h, item)` maintains the heap invariant. Python's `heapq` implements a:

A) Max-Heap.
B) Min-Heap.
C) Binomial Heap.
D) Fibonacci Heap.

**Answer: B**

**Explanation:**
The smallest element is always at index 0 (`h[0]`). To use it as a max-heap, you typically negate values/priorities.

---

**Q16.4: Basic - [Namedtuple Access]**

Given `Point = namedtuple('Point', ['x', 'y'])` and `p = Point(1, 2)`. How can you access `x`?

A) `p[0]` only.
B) `p.x` only.
C) Both `p[0]` and `p.x`.
D) `p('x')`.

**Answer: C**

**Explanation:**
`namedtuple` creates a tuple subclass, so it supports both index-based access (like a regular tuple) and name-based field access (like an object).

---

**Q16.5: Intermediate - [Bisect Module]**

`bisect.bisect(list, item)` assumes the list is:

A) Empty.
B) Sorted.
C) Unique.
D) A set.

**Answer: B**

**Explanation:**
Binary search algorithms rely on the input sequence being sorted. If not sorted, the result is meaningless.

---

**Q16.6: Advanced - [Counter Arithmetic]**

`Counter({'a': 2}) + Counter({'a': 3, 'b': 1})` results in:

A) `Counter({'a': 5, 'b': 1})`
B) `Counter({'a': 6})`
C) Error.
D) `Counter({'a': 2, 'b': 1})`

**Answer: A**

**Explanation:**
Addition of Counters adds the counts of corresponding elements.

---

**Q16.7: Basic - [Copy vs Deepcopy]**

If `L = [[1], [2]]`. `L2 = copy.copy(L)`. If you do `L2[0].append(3)`, what happens to `L`?

A) `L` is unchanged.
B) `L` becomes `[[1, 3], [2]]`.
C) It raises an error.
D) `L` becomes `None`.

**Answer: B**

**Explanation:**
`copy.copy` creates a *shallow* copy. The outer list is new, but the inner lists (references) are shared. Modifying the mutable inner object affects both.

---

**Q16.8: Intermediate - [Deque Maxlen]**

`d = deque(maxlen=3)`. If you append a 4th item:

A) It raises `IndexError`.
B) It expands the deque.
C) The item at the opposite end is automatically discarded.
D) It waits.

**Answer: C**

**Explanation:**
Bounded deques discard items from the other end to maintain the fixed length. Useful for keeping a history of "last N items".

---

**Q16.9: Advanced - [Itertools Chain]**

`itertools.chain([1, 2], [3, 4])`:

A) Creates a new list `[1, 2, 3, 4]`.
B) Returns an iterator that yields 1, 2, 3, 4.
C) Zips them.
D) Returns `[[1, 2], [3, 4]]`.

**Answer: B**

**Explanation:**
It lazily iterates over the first iterable, then the second, without creating a full copy in memory.

---

**Q16.10: Expert - [OrderedDict vs Dict]**

Since Python 3.7, standard `dict` preserves insertion order. What implies `collections.OrderedDict` is still useful?

A) `OrderedDict` is faster.
B) `OrderedDict` supports `move_to_end()` and equality checks trigger based on order.
C) It is not useful anymore.
D) It supports default values.

**Answer: B**

**Explanation:**
`OrderedDict` has order-specific methods (`move_to_end`, `popitem(last=False)`) and `OrderedDict(a=1, b=2) != OrderedDict(b=2, a=1)` (whereas plain dicts would be equal regardless of order).

---

**Q16.11: Basic - [Enum Definition]**

To define an enumeration:

A) `class Color(Enum):`
B) `def Color(Enum):`
C) `enum Color:`
D) `Color = Enum(...)`

**Answer: A**

**Explanation:**
Subclassing `enum.Enum` is the standard way to create enumerations in Python.

---

**Q16.12: Intermediate - [Itertools Cycle]**

`itertools.cycle('AB')` yields:

A) 'A', 'B', 'A', 'B', ... forever.
B) 'A', 'B'.
C) [('A', 'B')].
D) Error.

**Answer: A**

**Explanation:**
Repeats the elements of the iterable indefinitely.

---

**Q16.13: Advanced - [Heapq Nlargest]**

`heapq.nlargest(3, data)` is more efficient than `sorted(data, reverse=True)[:3]` when:

A) `data` is small.
B) `data` is large and N (3) is small compared to len(data).
C) N is close to len(data).
D) Always.

**Answer: B**

**Explanation:**
`nlargest` takes O(N * log(k)) or linear type time, avoiding a full sort O(N * log(N)) of the entire dataset.

---

**Q16.14: Basic - [ChainMap]**

`ChainMap(dict1, dict2)`:

A) Merges dict1 and dict2 into a new dict.
B) Creates a view that searches dict1 then dict2.
C) Links keys.
D) Reverses dicts.

**Answer: B**

**Explanation:**
It logically groups multiple dicts into a single mapping. Lookups search the mappings in order. Writes usually affect only the first mapping.

---

**Q16.15: Intermediate - [Slice Object]**

`s = slice(1, 10, 2)`. You can use it like:

A) `list[s]`
B) `s(list)`
C) `list.slice(s)`
D) `list(s)`

**Answer: A**

**Explanation:**
Slice objects are what `[1:10:2]` syntax compiles to. They can be passed explicitly to `__getitem__`.

---

**Q16.16: Advanced - [WeakRef]**

`weakref.ref(obj)` creates a reference that:

A) Prevents `obj` from being garbage collected.
B) Does not prevent `obj` from being garbage collected.
C) Increments refcount.
D) Copies `obj`.

**Answer: B**

**Explanation:**
Weak references allow you to cache or track objects without keeping them alive (preventing memory leaks).

---

**Q16.17: Expert - [Counter Most Common]**

`Counter(list).most_common(1)` returns:

A) The most common element value.
B) A list of tuples `[(element, count)]` containing the top 1.
C) A dict.
D) The count.

**Answer: B**

**Explanation:**
It returns a list of the n most common elements and their counts from the most common to the least.

---

**Q16.18: Intermediate - [Bisect Insort]**

`bisect.insort(list, item)`:

A) Inserts `item` into `list` keeping it sorted.
B) Checks if `item` is in `list`.
C) Sorts the list.
D) Returns the index.

**Answer: A**

**Explanation:**
Equivalent to finding the insertion point (bisect) and then calling `insert()`.

---

**Q16.19: Basic - [Copy Module]**

`copy.deepcopy(x)` is needed when:

A) `x` is an integer.
B) `x` is a compound object (list of lists) and you want a fully independent copy.
C) `x` is immutable.
D) Performance is critical.

**Answer: B**

**Explanation:**
Deep copy recursively copies all objects found in the original, ensuring no shared references remain.

---

**Q16.20: Advanced - [Deque Rotate]**

`d.rotate(1)` on `deque([1, 2, 3])` makes it:

A) `[2, 3, 1]`
B) `[3, 1, 2]`
C) `[1, 2, 3]`
D) `[3, 2, 1]`

**Answer: B**

**Explanation:**
Positive rotation moves elements from the right end to the left end. `3` moves to front -> `[3, 1, 2]`.

---

**Q16.21: Expert - [LRU Cache]**

`@functools.lru_cache` decorates a function to:

A) Run it in parallel.
B) Cache its return values based on arguments (Least Recently Used eviction).
C) Log usage.
D) Retry errors.

**Answer: B**

**Explanation:**
Memoization decorator. It keeps recent results.

---

**Q16.22: Intermediate - [Set Default]**

`dict.setdefault(key, default)` returns:

A) `default` always.
B) The value of `key` if it exists, otherwise `default` (and sets `key` to `default`).
C) `None`.
D) `True`.

**Answer: B**

**Explanation:**
Similar to `get()`, but if key is missing, it simultaneously inserts the default value into the dictionary.

---

**Q16.23: Basic - [Itertools Count]**

`itertools.count(10)` yields:

A) 10.
B) 10, 11, 12, ... (infinite).
C) 0 to 9.
D) 10 random numbers.

**Answer: B**

**Explanation:**
Infinite counter starting from the start value.

---

**Q16.24: Advanced - [MappingProxyType]**

`types.MappingProxyType(d)` creates:

A) A read-only view of the dictionary `d`.
B) A copy of `d`.
C) A weak reference.
D) A subclass.

**Answer: A**

**Explanation:**
It allows exposing an internal dictionary (like class `__dict__`) as immutable to the outside.

---

**Q16.25: Intermediate - [Enumerate Start]**

`list(enumerate(['a', 'b'], start=1))` results in:

A) `[(0, 'a'), (1, 'b')]`
B) `[(1, 'a'), (2, 'b')]`
C) `['a', 'b']`
D) `[(1, 'a')]`

**Answer: B**

**Explanation:**
The `start` parameter adjusts the index counting.

---

**Q16.26: Expert - [Itertools Tee]**

`itertools.tee(iterator, n=2)`:

A) Splits an iterator into `n` independent iterators.
B) Copies the iterator `n` times in memory.
C) Takes the top `n` items.
D) Chains them.

**Answer: A**

**Explanation:**
It creates independent iterators from a single iterable. Note: You should not consume the original iterator after calling `tee`. It may buffer large amounts of data if one child iterator advances far ahead of another.

---

**Q16.27: Basic - [Any and All]**

`all([])` returns:

A) `True`.
B) `False`.
C) `None`.
D) Error.

**Answer: A**

**Explanation:**
Vacuously true. Checks if all elements are truthy. (For `any([])`, it is False).

---

**Q16.28: Advanced - [Total Ordering]**

`@functools.total_ordering` decorator:

A) Sorts the class methods.
B) Generates missing comparison methods (`__le__`, `__gt__` etc.) if at least one (`__lt__`) and `__eq__` are defined.
C) Ensures strict types.
D) Total memory usage.

**Answer: B**

**Explanation:**
Reduces boiler-plate by automatically implementing the remaining rich comparison methods based on the provided ones.

---

**Q16.29: Intermediate - [FrozenSet]**

`frozenset` is:

A) A set that is immutable and hashable (can be used as dict key).
B) A set that is frozen in memory (cached).
C) A set of frozen objects.
D) Deprecated.

**Answer: A**

**Explanation:**
Normal sets are mutable and unhashable. Frozensets are immutable.

---

**Q16.30: Expert - [Dict Views]**

`d.keys()`, `d.values()`, `d.items()` return:

A) Lists.
B) View objects (dynamic, reflecting changes to the dict).
C) Iterators.
D) Tuples.

**Answer: B**

**Explanation:**
In Python 3, they return views. If the dict changes, the view reflects the change immediately. They also support set operations (like intersection) for keys/items.

---

**Q16.31: Intermediate - [Itertools Zip Longest]**

`itertools.zip_longest('ABCD', 'xy', fillvalue='-')` yields:

A) `('A', 'x'), ('B', 'y'), ('C', '-'), ('D', '-')`
B) `('A', 'x'), ('B', 'y')`
C) `('A', 'x'), ('B', 'y'), ('C', None), ('D', None)`
D) Error.

**Answer: A**

**Explanation:**
Unlike `zip()` which stops at the shortest iterable, `zip_longest` continues until the longest one is exhausted, filling missing values with `fillvalue`.

---

**Q16.32: Advanced - [Enum Auto]**

`enum.auto()` is used to:

A) Automatically format strings.
B) Automatically assign values to Enum members (usually 1, 2, 3...) so you don't have to pick them manually.
C) Automatically import enums.
D) Create a dynamic enum.

**Answer: B**

**Explanation:**
Useful when the exact value doesn't matter, only the distinction between members.

---

**Q16.33: Basic - [Sorted vs Sort]**

Difference between `list.sort()` and `sorted(list)`:

A) No difference.
B) `list.sort()` modifies the list in-place and returns `None`; `sorted()` creates a new list.
C) `sorted()` is faster.
D) `list.sort()` works on any iterable.

**Answer: B**

**Explanation:**
`list.sort` is a method of list objects (in-place). `sorted()` is a builtin function that accepts any iterable and returns a new list.

---

**Q16.34: Expert - [Heapq PushPop]**

`heapq.heappushpop(h, item)` is equivalent to:

A) `heappush(h, item); return heappop(h)`
B) `heappop(h); return heappush(h, item)`
C) `push(item)`
D) `pop()`

**Answer: A**

**Explanation:**
It pushes the new item onto the heap, then returns the smallest item. It is more efficient than calling push and pop separately. Note: if the pushed item is smaller than everything else, it is immediately returned.

---

**Q16.35: Intermediate - [Bisect Left vs Right]**

For list `[1, 2, 2, 3]`, `bisect.bisect_left(L, 2)` returns:

A) 1
B) 2 (same as `bisect`)
C) 0
D) 3

**Answer: A**

**Explanation:**
`bisect_left` returns the insertion point *before* any existing entries of the same value (index 1). `bisect` (alias for `bisect_right`) returns the point *after* (index 3).

---

**Q16.36: Advanced - [UserDict]**

Why inherit from `collections.UserDict` instead of `dict`?

A) No reason.
B) `dict` allows easier customization.
C) Subclassing built-in `dict` can be tricky because internal methods (like `update`, `__getitem__`) might bypass overridden methods. `UserDict` solves this.
D) `UserDict` is faster.

**Answer: C**

**Explanation:**
Built-in types like `dict` and `list` are optimized in C and don't always call their own methods (e.g., `update` might not call `__setitem__`). `UserDict` is a pure Python wrapper designed for inheritance.

---

**Q16.37: Basic - [Itertools Product]**

`itertools.product('AB', repeat=2)` yields:

A) `AA`, `AB`, `BA`, `BB`
B) `AB`
C) `A`, `B`
D) `AA`, `BB`

**Answer: A**

**Explanation:**
 Cartesian product. Equivalent to nested for-loops.

---

**Q16.38: Intermediate - [ChainMap Write]**

If `cm = ChainMap(d1, d2)` and you do `cm['k'] = v`:

A) It writes to `d1` and `d2`.
B) It writes only to `d1` (the first mapping).
C) It writes to `d2`.
D) It creates a new dict.

**Answer: B**

**Explanation:**
Updates/writes to a ChainMap always affect the first mapping in the chain.

---

**Q16.39: Advanced - [Functools Partial]**

`p = functools.partial(func, 10)`:

A) Runs `func(10)` immediately.
B) Returns a new callable that behaves like `func` but with the first argument frozen as 10.
C) Partially runs the function.
D) Is a decorator.

**Answer: B**

**Explanation:**
Used to "freeze" some portion of a function's arguments and/or keywords, resulting in a new object with a simplified signature.

---

**Q16.40: Expert - [WeakKeyDictionary]**

`weakref.WeakKeyDictionary`:

A) Keys are weak references. If the key object is garbage collected, the entry is automatically removed.
B) Values are weak references.
C) Both are weak.
D) is deprecated.

**Answer: A**

**Explanation:**
Useful for associating additional data with an object without extending it or keeping it alive (e.g., caching, or attaching state to objects you don't own).

---

**Q16.41: Intermediate - [Enum Unique]**

`@enum.unique` decorator:

A) Ensures all members have unique names.
B) Ensures all members have unique values (raises ValueError if aliases exist).
C) Makes the enum a singleton.
D) Optimizes access.

**Answer: B**

**Explanation:**
By default, Enums allow aliases (two names for same value). `@unique` enforces one-to-one mapping.

---

**Q16.42: Basic - [Reverse Iterator]**

`reversed(list)`:

A) Returns a new list in reverse order.
B) Returns an iterator that yields items in reverse.
C) Modifies list in-place.
D) Is slow.

**Answer: B**

**Explanation:**
It returns an iterator, avoiding memory allocation for a full copy.

---

**Q16.43: Advanced - [Dataclasses vs Namedtuple]**

Data classes (Python 3.7+) vs `namedtuple`:

A) Data classes are mutable by default; namedtuples are immutable.
B) Namedtuples are classes.
C) Data classes are slower.
D) They are identical.

**Answer: A**

**Explanation:**
`dataclasses` are generated classes with mutable fields (by default) and support type hints. `namedtuple` creates tuple subclasses (immutable, index-accessible).

---

**Q16.44: Expert - [Operator Itemgetter]**

`sorted(data, key=operator.itemgetter(1))` is often preferred over `key=lambda x: x[1]` because:

A) It allows multiple indices.
B) It is slightly faster (implemented in C) and pickles better.
C) It is less readable.
D) Lambda cannot handle tuples.

**Answer: B**

**Explanation:**
`operator` functions are efficient C implementations.

---

**Q16.45: Intermediate - [Itertools Groupby]**

`itertools.groupby(iterable)` works correctly only if:

A) The iterable is already sorted by the grouping key.
B) The iterable is a list.
C) The iterable has unique elements.
D) The key is None.

**Answer: A**

**Explanation:**
`groupby` only groups *consecutive* elements. If the underlying data isn't sorted, identical keys separated by other values will form separate groups.

---

**Q16.46: Basic - [Array Module]**

`array.array('i', [1, 2, 3])`:

A) Creates a list of integers.
B) Creates a compact, typed array of signed integers (like logical C array).
C) Creates a NumPy array.
D) Is deprecated.

**Answer: B**

**Explanation:**
More memory efficient than a list for large amounts of uniform numerical data.

---

**Q16.47: Advanced - [SimpleNamespace]**

`types.SimpleNamespace(a=1, b=2)`:

A) Is a dictionary.
B) Is a simple object wrapper allowing attribute access (`obj.a`).
C) Is a named tuple.
D) Is immutable.

**Answer: B**

**Explanation:**
A simple object subclass that provides attribute access to its namespace. Mutable.

---

**Q16.48: Expert - [Reduce Default]**

`functools.reduce(func, seq, initial)`: If `seq` is empty:

A) Raises TypeError.
B) Returns `initial`.
C) Returns None.
D) Raises ValueError.

**Answer: B**

**Explanation:**
The `initial` value serves as the starting accumulator. If the sequence is empty, the initial value is returned.

---

**Q16.49: Intermediate - [Set Discard vs Remove]**

Difference between `set.discard(x)` and `set.remove(x)`:

A) `remove` raises KeyError if x is missing; `discard` does not.
B) `discard` raises KeyError.
C) `remove` is faster.
D) No difference.

**Answer: A**

**Explanation:**
`discard` is safe if you don't know if the element exists.

---

**Q16.50: Basic - [Identity Check]**

To check if two variables refer to the exact same object in memory:

A) `a == b`
B) `a.equals(b)`
C) `a is b`
D) `id(a) == b`

**Answer: C**

**Explanation:**
`is` checks for object identity (address), whereas `==` checks for value equality.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
