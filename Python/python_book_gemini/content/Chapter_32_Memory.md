# Chapter 32: Memory Management & Optimization

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `sys.getsizeof`, `slots`, `weakref`, `cProfile`, `timeit`, Generators vs Lists, Deepcopy vs Shallow Copy, String Interning (practical), Memoization (`lru_cache`).

---

**Q32.1: Basic - [Sys Getsizeof]**

To reliably check the memory consumption of a Python object:

A) `sys.getsizeof(obj)`
B) `len(obj)`
C) `obj.size()`
D) `os.size(obj)`

**Answer: A**

**Explanation:**
Does not include referenced objects (shallow size), but gives the size of the container itself.

---

**Q32.2: Intermediate - [Generator Memory]**

Which code snippet is more memory efficient for iterating over a large range?

A) `(x * 2 for x in range(1000000))`
B) `[x * 2 for x in range(1000000)]`
C) `list(range(1000000))`
D) `tuple(range(1000000))`

**Answer: A**

**Explanation:**
The generator expression produces values one by one (O(1) memory), while the list comprehension builds the entire list in memory (O(N)).

---

**Q32.3: Advanced - [Slots Memory]**

Using `__slots__` significantly reduces memory usage of class instances because:

A) It prevents the creation of the `__dict__` dictionary for each instance (which has a large overhead), storing attributes in a fixed-size C array instead.
B) It compresses data.
C) It deletes attributes.
D) It stores data in C++.

**Answer: A**

**Explanation:**
Can reduce memory footprint by 40-50% for classes with millions of instances.

---

**Q32.4: Expert - [Weakref Callback]**

A weak reference (`weakref.ref(obj, callback)`) allows you to:

A) Execute a callback function when the referenced object is garbage collected (about to be destroyed).
B) Prevent garbage collection.
C) Make the object strong.
D) Copy the object.

**Answer: A**

**Explanation:**
Useful for cleaning up external resources associated with an object.

---

**Q32.5: Basic - [Timeit]**

The standard library module for accurately timing small bits of Python code is:

A) `timeit`
B) `time`
C) `clock`
D) `profile`

**Answer: A**

**Explanation:**
`timeit.timeit('code...', number=10000)`. Avoids common pitfalls like system load jitter.

---

**Q32.6: Intermediate - [LRU Cache]**

`@functools.lru_cache(maxsize=128)` helps optimization by:

A) Caching the results of function calls based on arguments (Memoization), returning the cached value for repeated calls instead of re-computing.
B) Deleting old code.
C) Running code faster on GPU.
D) Compressing arguments.

**Answer: A**

**Explanation:**
Great for expensive computations (e.g., recursive Fibonacci).

---

**Q32.7: Advanced - [Copy vs Deepcopy]**

If you have a list of lists `a = [[1], [2]]` and do `b = copy.copy(a)`:

A) `b` is a shallow copy: `b` is a new list, but `b[0]` refers to the *same* inner list as `a[0]`. Modifying `b[0]` changes `a[0]`.
B) `b` is a deep copy: `b[0]` is a completely new list.
C) `b` is the same object as `a`.
D) `b` is empty.

**Answer: A**

**Explanation:**
Use `copy.deepcopy()` to recursively copy everything.

---

**Q32.8: Expert - [CProfile]**

To run the built-in deterministic profiler on a script:

A) `python -m cProfile -s time myscript.py`
B) `python -m timeit myscript.py`
C) `python -m profile myscript.py`
D) `python -m debug myscript.py`

**Answer: A**

**Explanation:**
Shows number of calls (`ncalls`) and time spent (`tottime`, `cumtime`) for every function.

---

**Q32.9: Basic - [Del]**

The `del` statement (`del x`):

A) Deletes the *reference* `x` from the namespace and decrements the reference count of the object it pointed to.
B) Immediately destroys the object from memory.
C) Does nothing.
D) Erases the hard drive.

**Answer: A**

**Explanation:**
The object is only destroyed if the refcount reaches zero.

---

**Q32.10: Intermediate - [Set Membership]**

Checking `if x in my_collection` is fastest (O(1)) if `my_collection` is a:

A) `set` (or `dict`).
B) `list`.
C) `tuple`.
D) `string`.

**Answer: A**

**Explanation:**
Lists and tuples require O(N) linear scan.

---

**Q32.11: Advanced - [String Concatenation]**

For joining a large list of strings, `''.join(list_of_strings)` is much faster than `s = s + new_str` in a loop because:

A) `join` pre-calculates the total size and allocates memory once, whereas `+` creates a new string object for every iteration (quadratic time complexity behavior).
B) `join` uses multiple threads.
C) `+` is broken.
D) `join` compresses strings.

**Answer: A**

**Explanation:**
Classic performance antipattern.

---

**Q32.12: Expert - [Tracemalloc Snapshot]**

`tracemalloc.take_snapshot().compare_to(old_snapshot, 'lineno')` allows you to:

A) See exactly which lines of code increased memory usage (allocated more bytes) between the two snapshots.
B) Compare time.
C) Compare CPU usage.
D) Compare files.

**Answer: A**

**Explanation:**
The modern way to debug memory leaks.

---

**Q32.13: Basic - [Mutable Default]**

Why is using a mutable default argument (like `l=[]`) bad for memory/logic?

A) The object persists between calls. It is never freed until the function is redefined or the module unloaded.
B) It takes too much memory.
C) It raises an error.
D) It is slow.

**Answer: A**

**Explanation:**
Often causes subtle bugs where data "leaks" from one call to the next.

---

**Q32.14: Intermediate - [Map vs List Comp]**

In Python 3, `map(func, iterable)` returns:

A) An iterator (lazy generator), computing values on demand.
B) A list.
C) A dict.
D) A tuple.

**Answer: A**

**Explanation:**
More memory efficient than a list comprehension `[func(x) for x in ...]` if you only iterate once.

---

**Q32.15: Advanced - [Interning Strings]**

If you have millions of dictionaries with the same keys (e.g., from JSON data), explicitly interning keys with `sys.intern(key)` can:

A) Save memory (store 1 string object instead of millions) and speed up dictionary lookups (pointer comparison).
B) Slow down the script.
C) Increase memory usage.
D) Crash the script.

**Answer: A**

**Explanation:**
CPython internals use this heavily.

---

**Q32.16: Basic - [Global Variables]**

Accessing global variables is slower than local variables because:

A) `LOAD_GLOBAL` involves a dictionary lookup, while `LOAD_FAST` (locals) is an array indexing operation.
B) Globals are farther away in RAM.
C) Globals are encrypted.
D) Locals are cached in CPU.

**Answer: A**

**Explanation:**
Optimization tip: assign global functions to a local variable inside a tight loop.

---

**Q32.17: Intermediate - [List Allocation]**

Lists allocate memory in chunks (over-allocation). If a list has size 4 and you append a 5th item, it might resize to hold:

A) 8 items (doubling or growth factor ~1.125), to avoid resizing on every append.
B) 5 items.
C) 100 items.
D) 4 items.

**Answer: A**

**Explanation:**
This gives `append` an amortized O(1) complexity.

---

**Q32.18: Advanced - [WeakKeyDictionary]**

`weakref.WeakKeyDictionary`:

A) A dictionary where keys are weakly referenced. If there are no other references to the key, the entry is automatically removed from the dictionary.
B) A dictionary with weak security.
C) A dictionary that deletes values.
D) A slow dictionary.

**Answer: A**

**Explanation:**
Perfect for associating extra data with objects without keeping them alive (and causing leaks).

---

**Q32.19: Expert - [PyPy]**

PyPy is:

A) An alternative Python implementation with a JIT (Just-In-Time) compiler, often significantly faster than CPython for long-running, pure Python code.
B) A library.
C) A debugger.
D) A linter.

**Answer: A**

**Explanation:**
Does not support all C extensions, but great for CPU-bound Python.

---

**Q32.20: Basic - [Range Object]**

`range(100)` in Python 3 returns:

A) A range object (lazy sequence), not a list of 100 numbers.
B) A list of 100 numbers.
C) A generator.
D) A tuple.

**Answer: A**

**Explanation:**
Uses tiny fixed memory regardless of size.

---

**Q32.21: Intermediate - [List vs Tuple]**

Which is more memory efficient: `[1, 2, 3]` (List) or `(1, 2, 3)` (Tuple)?

A) Tuple.
B) List.
C) About same.
D) Dict.

**Answer: A**

**Explanation:**
Tuples don't need the extra over-allocation for resizing since they are immutable.

---

**Q32.22: Advanced - [Garbage Collection Thresholds]**

`gc.get_threshold()` returns `(700, 10, 10)`. This means:

A) GC runs when allocation count minus deallocation count exceeds 700 (generation 0). The other numbers control promotion to older generations (1 and 2).
B) GC runs every 700 seconds.
C) GC runs when memory is 700MB.
D) GC deletes 700 objects.

**Answer: A**

**Explanation:**
Tuning these can help with latency spikes.

---

**Q32.23: Expert - [Reference Cycle]**

A reference cycle occurs when:

A) Object A references Object B, and Object B references Object A (directly or indirectly), preventing reference counts from hitting zero.
B) A bicycle.
C) A recursive function.
D) A loop.

**Answer: A**

**Explanation:**
Only the Cyclic GC can clean this up.

---

**Q32.24: Basic - [Profiling]**

The first rule of optimization is:

A) Don't optimize without measuring (Profiling). Premature optimization is the root of all evil.
B) Optimize everything.
C) Write in C.
D) Use shorter variable names.

**Answer: A**

**Explanation:**
Guessing where the bottleneck is is usually wrong.

---

**Q32.25: Intermediate - [Array Module]**

For storing large sequences of uniform primitive types (like integers), `array.array('i', [...])` is better than a `list` because:

A) It stores the raw machine values directly (compactly), avoiding the overhead of storing wrapper Python Integer objects for every element.
B) It allows mixed types.
C) It is a list.
D) It is slower.

**Answer: A**

**Explanation:**
Can be 10x more compact.

---

**Q32.26: Advanced - [View Objects]**

Dictionary methods like `.keys()`, `.values()`, `.items()` in Python 3 return:

A) View Objects (dynamic views reflecting changes to the dict), not lists.
B) Static lists.
C) Tuples.
D) Iterators (consume once).

**Answer: A**

**Explanation:**
They are iterable and update if the dict updates.

---

**Q32.27: Expert - [CProfile Tottime vs Cumtime]**

In `cProfile` output, `tottime` is ________, while `cumtime` is ________.

A) Time spent *in* the function itself (excluding subcalls); Time spent in the function *plus* all subcalls.
B) Total time; Cumulative time (same).
C) Time including subcalls; Time excluding subcalls.
D) Time waiting; Time running.

**Answer: A**

**Explanation:**
If `tottime` is high, the bottleneck is inside that function's code.

---

**Q32.28: Intermediate - [FrozenSet]**

A `frozenset` is useful for optimization because:

A) It is immutable and hashable, allowing it to be used as a dictionary key or set element (unlike normal sets).
B) It is faster.
C) It is sorted.
D) It holds more data.

**Answer: A**

**Explanation:**
`s = {frozenset([1,2]): 'value'}`.

---

**Q32.29: Basic - [Big O]**

Searching for an element in a binary search tree (balanced) is:

A) O(log n)
B) O(n) - Linear
C) O(1) - Constant
D) O(n^2)

**Answer: A**

**Explanation:**
Searching a hash map (dict) is O(1). Searching a list is O(n).

---

**Q32.30: Advanced - [Tqdm]**

While not standard library, `tqdm` is widely used for:

A) Wrapping an iterable to show a smart progress bar in the terminal (with loop speed and ETA).
B) Profiling memory.
C) Testing.
D) Linting.

**Answer: A**

**Explanation:**
`for x in tqdm(range(100)): ...` - essential for long-running scripts.

---

**Q32.31: Intermediate - [Dict Comprehension]**

Dict comprehensions `{k: v for k, v in iterable}` are generally faster and more memory-efficient than `dict(iterable)` because:

A) They execute at bytecode level (optimized loop), avoiding the `dict()` constructor call and potential generator overhead.
B) They are list comprehensions.
C) They use less disk space.
D) They are slow.

**Answer: A**

**Explanation:**
Syntactic sugar that is also an optimization.

---

**Q32.32: Advanced - [WeakValueDictionary]**

`weakref.WeakValueDictionary` is useful when:

A) You want a cache of objects where the *values* are automatically removed if they are no longer used elsewhere in the program.
B) You want weak keys.
C) You want a persistent DB.
D) You want to sort keys.

**Answer: A**

**Explanation:**
Commonly used for object identity maps.

---

**Q32.33: Basic - [Refcount limit]**

Does Python have a limit on how many references an object can have?

A) Practically no (limited by the size of the `ob_refcnt` field in C, typically `ssize_t`, which is huge on 64-bit systems).
B) Yes, 255.
C) Yes, 1000.
D) Yes, 1.

**Answer: A**

**Explanation:**
You won't hit it in normal usage.

---

**Q32.34: Expert - [Memory Leak in C Extension]**

A common cause of memory leaks in C extensions is:

A) Missing `Py_DECREF()` on temporary objects or return values from C-API calls.
B) Using `malloc`.
C) Using `free`.
D) Using `printf`.

**Answer: A**

**Explanation:**
The internal reference count never drops to zero, so the object lives forever.

---

**Q32.35: Intermediate - [Itertools Chain]**

`itertools.chain(list1, list2)` is more memory efficient than `list1 + list2` because:

A) It yields elements from the first list then the second, without creating a new combined list in memory.
B) It zips them.
C) It sorts them.
D) It deletes them.

**Answer: A**

**Explanation:**
Zero-copy concatenation for iteration.

---

**Q32.36: Advanced - [String Split]**

`s.split()` vs `s.split(' ')`:

A) `s.split()` (no argument) splits by *any* whitespace run and trims empty strings, whereas `split(' ')` splits by strictly single spaces (preserving empty strings).
B) They are identical.
C) `split()` is slower.
D) `split(' ')` removes newlines.

**Answer: A**

**Explanation:**
Important for parsing text files robustly.

---

**Q32.37: Basic - [Garbage Collection Disable]**

You can disable the cyclic garbage collector with:

A) `gc.disable()`
B) `sys.no_gc()`
C) `os.disable_gc()`
D) `gc.stop()`

**Answer: A**

**Explanation:**
Instagram famously did this to save memory on copy-on-write during forking.

---

**Q32.38: Intermediate - [Sort Key]**

For sorting complex objects, `list.sort(key=attrgetter('x'))` is faster than `cmp_to_key` or old `cmp` functions because:

A) The `key` function is called exactly once per element to generate a "Schwartzian transform" (decorate-sort-undecorate) shadow list, which is then sorted efficiently.
B) It calls the key function n*log(n) times.
C) It uses bubble sort.
D) It is slower.

**Answer: A**

**Explanation:**
Minimizes Python function call overhead.

---

**Q32.39: Advanced - [Struct Packing]**

Using `struct` to store data (e.g., 1 million (x, y) coordinates) is more efficient than a list of tuples because:

A) It eliminates the pointer overhead and PyObject overhead for every single integer, storing just the raw packed bytes.
B) It is a list.
C) It is a dict.
D) It is a set.

**Answer: A**

**Explanation:**
Or use `array.array` or NumPy.

---

**Q32.40: Expert - [Objgraph]**

The `objgraph` library is famous for helping debug memory leaks by:

A) Generating visual graphs (using Graphviz) of object references, showing what is keeping a leaked object alive (the "reference chain").
B) Graphing CPU usage.
C) Plotting math functions.
D) Monitoring network.

**Answer: A**

**Explanation:**
`objgraph.show_backrefs(obj, max_depth=10)`.

---

**Q32.41: Basic - [Import Time]**

To debug slow import times, you can use the environment variable:

A) `PYTHONPROFILEIMPORTTIME=1`
B) `PYTHONDEBUG=1`
C) `PYTHONPATH=1`
D) `PYTHONFAST=1`

**Answer: A**

**Explanation:**
Shows a cumulative tree of import duration.

---

**Q32.42: Intermediate - [Set Difference]**

To efficiently find items in list A but not in list B:

A) `set(A) - set(B)` (set difference).
B) `[x for x in A if x not in B]` (O(N*M)).
C) `list(A) - list(B)`.
D) `A.remove(B)`.

**Answer: A**

**Explanation:**
O(N) vs O(N*M). Huge difference for large lists.

---

**Q32.43: Advanced - [Multiple Inheritance MRO]**

Memory layout in multiple inheritance is handled such that:

A) The instance `__dict__` holds all attributes, and method resolution follows the MRO in the class hierarchy, with no duplication of parent classes (thanks to C3 linearization).
B) Parent classes are duplicated.
C) It uses more memory significantly.
D) It fails.

**Answer: A**

**Explanation:**
Efficient reuse.

---

**Q32.44: Expert - [Pymalloc Arenas]**

Since Python 3.3, if an Arena (256KB chunk) becomes completely empty (all pools inside it are freed), CPython:

A) Returns the memory to the OS (via `munmap` or equivalent), allowing the process size to actually shrink.
B) Keeps it forever.
C) Crashes.
D) Converts it to a list.

**Answer: A**

**Explanation:**
Before 3.3, Python memory would almost never be returned to OS until exit.

---

**Q32.45: Intermediate - [Bisect]**

To maintain a sorted list and insert a new item in the correct position (O(n)), use:

A) `bisect.insort(list, item)`
B) `list.append(item); list.sort()` (O(n log n)).
C) `list.insert(0, item)`.
D) `list.add(item)`.

**Answer: A**

**Explanation:**
`bisect` module is efficient for maintaining sorted sequences.

---

**Q32.46: Basic - [Sys Getsizeof Recursive]**

Does `sys.getsizeof(list_obj)` calculate the size of the objects *inside* the list?

A) No, only the size of the list structure (pointers array). You need a recursive function (like Pympler's `asizeof`) for deep size.
B) Yes, always.
C) Yes, if integers.
D) No, it returns 0.

**Answer: A**

**Explanation:**
Common misconception. A list of 1000 huge objects has a small `getsizeof`.

---

**Q32.47: Advanced - [Pandas vs List]**

For working with tabular data (rows/cols), Pandas DataFrame is preferred over List of Dicts because:

A) It uses NumPy arrays internally (contiguous C memory blocks) and vectorized operations, often 100x faster and 10x more memory efficient.
B) It is slower.
C) It is built-in.
D) It is a database.

**Answer: A**

**Explanation:**
List of Dicts has massive metadata overhead for every single cell.

---

**Q32.48: Expert - [Gil release]**

For CPU-bound tasks, using `multiprocessing` is better than `threading` because:

A) Each process has its own GIL and Python interpreter, allowing true parallelism on multi-core CPUs.
B) Threads have no GIL.
C) Processes share memory.
D) Processes are lighter.

**Answer: A**

**Explanation:**
The overhead of pickling data between processes is the tradeoff.

---

**Q32.49: Intermediate - [Fastest Loop]**

Which loop is generally fastest in Python?

A) Built-in functions implemented in C (e.g., `sum(list)`, `map`), avoiding the Python bytecode interpreter loop overhead entirely.
B) `for` loop.
C) `while` loop.
D) Recursive loop.

**Answer: A**

**Explanation:**
"Push loops into C" is the optimization mantra (Vectorization).

---

**Q32.50: Basic - [MemoryError]**

A `MemoryError` is raised when:

A) An operation runs out of memory (malloc fails).
B) The disk is full.
C) You forget a variable.
D) Syntactic error.

**Answer: A**

**Explanation:**
Usually indicates a need to optimize data structures or switch to streaming/generators.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
