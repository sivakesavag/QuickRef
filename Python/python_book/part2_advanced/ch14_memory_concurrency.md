# Chapter 14: Memory Model & Concurrency

> **Topics Covered**: Memory management, reference counting, GC, GIL, threading, multiprocessing, shared memory, memory views, __slots__, sys.getsizeof, copy vs deepcopy, id(), object identity vs equality

---

## Questions

---

**Q14.1: Basic - [Object Identity]**

What does `id(obj)` return?

A) Object's name
B) Unique integer identifier (memory address in CPython)
C) Object's type
D) Hash value

**Answer: B**

**Explanation:**
`id(obj)` returns a unique integer for the object's lifetime. In CPython, it's the memory address. Two objects with non-overlapping lifetimes may have same id. Compare with `is` operator: `a is b` ≡ `id(a) == id(b)`.

---

**Q14.2: Basic - [is vs ==]**

What is the output?
```python
a = [1, 2, 3]
b = [1, 2, 3]
print(a == b, a is b)
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
`==` compares values (equal lists). `is` compares identity (same object). `a` and `b` are different objects with same contents. Value equal, identity different. Use `is` for None checks, `==` for value comparison.

---

**Q14.3: Intermediate - [Integer Caching]**

What is the output?
```python
a = 256
b = 256
c = 257
d = 257
print(a is b, c is d)
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
CPython caches small integers (-5 to 256). `a` and `b` reference same cached object. 257 is outside cache — `c` and `d` are different objects. Implementation detail — don't rely on it! Use `==` for value comparison.

---

**Q14.4: Intermediate - [String Interning]**

What is the output?
```python
a = "hello"
b = "hello"
c = "hello world"
d = "hello world"
print(a is b, c is d)
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
Python interns short identifier-like strings. "hello" is interned — same object. "hello world" (with space) isn't automatically interned — different objects. Use `sys.intern()` to force interning. Never rely on this; use `==`.

---

**Q14.5: Basic - [Reference Counting]**

What is reference counting?

A) Counting function calls
B) Each object tracks how many references point to it; deleted when count reaches 0
C) Counting lines of code
D) Memory allocation counting

**Answer: B**

**Explanation:**
Every Python object has a reference count. `sys.getrefcount(obj)` returns it (count+1 for the getrefcount argument). When count drops to 0, object is immediately deallocated. Primary memory management in CPython.

---

**Q14.6: Intermediate - [Reference Count Changes]**

What increases reference count?
```python
x = []    # refcount = 1
y = x     # refcount = ?
z = [x]   # refcount = ?
```

A) 1, 1
B) 2, 3
C) 2, 2
D) 3, 4

**Answer: B**

**Explanation:**
`x = []` creates list with refcount 1. `y = x` adds reference → 2. `z = [x]` (x inside z's list) adds reference → 3. Every variable, container element, or argument referencing object increases count.

---

**Q14.7: Intermediate - [Cyclic References]**

What's the problem with cyclic references?

A) Slow performance
B) Reference counting alone can't free them — they keep each other alive
C) Syntax error
D) No problem

**Answer: B**

**Explanation:**
```python
a = []; b = []; a.append(b); b.append(a)
```
Both have refcount > 0 even when nothing else references them. Reference counting fails. Python's garbage collector (generational GC) handles cycles separately.

---

**Q14.8: Intermediate - [Garbage Collection]**

What does Python's garbage collector handle?

A) All memory management
B) Cyclic references that reference counting misses
C) Stack memory only
D) External resources

**Answer: B**

**Explanation:**
Reference counting handles most objects. GC detects and collects unreachable cycles. Runs automatically or manually via `gc.collect()`. `gc.disable()` turns it off (reference counting still works). GC adds overhead for cycle detection.

---

**Q14.9: Intermediate - [gc Module]**

What does `gc.collect()` do?

A) Collects all objects
B) Triggers immediate garbage collection cycle, returns number of objects collected
C) Disables collection
D) Reports memory usage

**Answer: B**

**Explanation:**
`gc.collect()` forces a full GC cycle. Returns count of unreachable objects found. Useful after deleting large structures with potential cycles. Normally GC runs automatically based on allocation thresholds.

---

**Q14.10: basic - [What is GIL]**

What is the GIL (Global Interpreter Lock)?

A) A security feature
B) A mutex that allows only one thread to execute Python bytecode at a time
C) A file lock
D) A garbage collection mechanism

**Answer: B**

**Explanation:**
GIL prevents true parallelism in Python threads. Only one thread runs Python code at a time. Exists because CPython's memory management isn't thread-safe. Threads still useful for I/O-bound work; use multiprocessing for CPU-bound parallelism.

---

**Q14.11: Intermediate - [GIL Implications]**

What is the output?
```python
import threading
counter = 0

def increment():
    global counter
    for _ in range(1000000):
        counter += 1

t1 = threading.Thread(target=increment)
t2 = threading.Thread(target=increment)
t1.start(); t2.start()
t1.join(); t2.join()
print(counter < 2000000)
```

A) Always `False`
B) Usually `True` (race condition)
C) Always `True`
D) Error

**Answer: B**

**Explanation:**
⚠️ Despite GIL, `counter += 1` is not atomic! It's read-modify-write. GIL releases between bytecode instructions. Race condition causes lost updates. Result is usually less than 2M. Use `Lock` for thread safety.

---

**Q14.12: Intermediate - [Threading Basics]**

What is the output?
```python
import threading

def worker(name):
    print(f"Worker {name}")

threads = [threading.Thread(target=worker, args=(i,)) for i in range(3)]
for t in threads: t.start()
for t in threads: t.join()
print("Done")
```

A) Random order of "Worker 0", "Worker 1", "Worker 2", then "Done"
B) "Worker 0", "Worker 1", "Worker 2", "Done" in order
C) "Done" first
D) Error

**Answer: A**

**Explanation:**
Threads execute concurrently. Print order depends on OS scheduling — could be any order. `join()` waits for threads to complete. "Done" prints after all threads finish. Order of Worker prints is non-deterministic.

---

**Q14.13: Intermediate - [Thread Lock]**

What does `threading.Lock` do?

A) Locks files
B) Provides mutual exclusion — only one thread holds lock at a time
C) Locks memory
D) Prevents deadlocks

**Answer: B**

**Explanation:**
`lock = Lock(); with lock: critical_section()`. If thread A holds lock, thread B's acquire() blocks until A releases. Ensures exclusive access to shared resources. Always use with `with` statement for safety.

---

**Q14.14: Intermediate - [RLock]**

What's the difference between `Lock` and `RLock`?

A) No difference
B) RLock can be acquired multiple times by same thread
C) RLock is faster
D) Lock is deprecated

**Answer: B**

**Explanation:**
`RLock` (Reentrant Lock) allows same thread to acquire multiple times (must release same number). `Lock` deadlocks if same thread tries to acquire twice. Use RLock when locked function calls another locked function.

---

**Q14.15: Intermediate - [Deadlock]**

What causes deadlock?

A) Too many threads
B) Two threads each waiting for a lock the other holds
C) Memory exhaustion
D) GIL

**Answer: B**

**Explanation:**
Classic deadlock: T1 holds Lock A, waits for Lock B. T2 holds Lock B, waits for Lock A. Neither proceeds. Prevention: acquire locks in consistent order, use timeouts, or use `RLock` where appropriate.

---

**Q14.16: Intermediate - [Thread-Safe Queue]**

What is `queue.Queue` for?

A) Data storage
B) Thread-safe communication between threads
C) Priority queuing
D) Database queries

**Answer: B**

**Explanation:**
`queue.Queue` is thread-safe (internally locked). Producer threads `put()`, consumer threads `get()`. Blocks when empty/full. Standard producer-consumer pattern. Also `LifoQueue` (stack) and `PriorityQueue`.

---

**Q14.17: Intermediate - [threading.Event]**

What is `threading.Event` for?

A) Logging events
B) Signaling between threads — one thread waits, another sets the event
C) Event-driven programming
D) UI events

**Answer: B**

**Explanation:**
`event = Event()`. One thread calls `event.wait()` (blocks). Another calls `event.set()` (unblocks waiters). `clear()` resets. Simple coordination mechanism. Unlike Condition, no associated lock.

---

**Q14.18: Basic - [multiprocessing vs threading]**

When use `multiprocessing` instead of `threading`?

A) Always use threading
B) For CPU-bound work — multiprocessing bypasses GIL with separate processes
C) For I/O-bound work
D) Never use multiprocessing

**Answer: B**

**Explanation:**
Threading: limited by GIL for CPU work, good for I/O. Multiprocessing: separate processes, each with own GIL — true parallelism. Higher overhead (process creation, IPC) but utilizes multiple cores for CPU-bound tasks.

---

**Q14.19: Intermediate - [Process Basics]**

What is the output (conceptually)?
```python
from multiprocessing import Process

def worker():
    print("Worker")

p = Process(target=worker)
p.start()
p.join()
print("Done")
```

A) `Worker, Done`
B) Error (no main guard)
C) `Done, Worker`
D) Nothing

**Answer: A**

**Explanation:**
Creates new process, runs worker function. `join()` waits for completion. "Worker" prints from child process, "Done" from main. On Windows, needs `if __name__ == '__main__':` guard (implementation detail).

---

**Q14.20: Intermediate - [Sharing Data Between Processes]**

Can processes share Python objects directly?

A) Yes, just like threads
B) No, processes have separate memory — must use IPC mechanisms
C) Only with global variables
D) Only lists

**Answer: B**

**Explanation:**
Each process has isolated memory. Sharing requires: `multiprocessing.Queue`, `Pipe`, `Manager`, `Value`, `Array`, or shared memory (3.8+). Objects are serialized (pickled) for transfer. More complex than threading.

---

**Q14.21: Intermediate - [Process Pool]**

What does `multiprocessing.Pool` do?

A) Creates a swimming pool
B) Maintains pool of worker processes for parallel task execution
C) Memory pooling
D) Connection pooling

**Answer: B**

**Explanation:**
`Pool(4)` creates 4 worker processes. `pool.map(func, items)` distributes work. Reuses processes (avoids creation overhead). `pool.close(); pool.join()` for cleanup. Higher-level than raw Process.

---

**Q14.22: Intermediate - [concurrent.futures]**

What advantage does `concurrent.futures` offer?

A) Faster execution
B) Unified API for threading and multiprocessing via ThreadPoolExecutor/ProcessPoolExecutor
C) Better error handling
D) Lower memory usage

**Answer: B**

**Explanation:**
`ThreadPoolExecutor` and `ProcessPoolExecutor` share same interface. Submit tasks, get futures, wait for results. Switch between threading and multiprocessing by changing executor class. Higher-level, cleaner API.

---

**Q14.23: Intermediate - [Future Objects]**

What is a `Future`?

A) Future version of Python
B) Object representing eventual result of async operation
C) Prediction object
D) Time object

**Answer: B**

**Explanation:**
`future = executor.submit(func, args)`. Future represents pending result. `future.result()` blocks until complete. `future.done()` checks completion. `future.cancel()` attempts cancellation. Pattern for async operation results.

---

**Q14.24: Intermediate - [copy vs deepcopy]**

What is the output?
```python
import copy
original = [[1, 2], [3, 4]]
shallow = copy.copy(original)
deep = copy.deepcopy(original)

original[0][0] = 'X'
print(shallow[0][0], deep[0][0])
```

A) `X, X`
B) `X, 1`
C) `1, 1`
D) `1, X`

**Answer: B**

**Explanation:**
Shallow copy copies outer list but shares inner lists. Deep copy recursively copies everything. Modifying `original[0][0]` affects `shallow` (same inner list) but not `deep` (independent copy).

---

**Q14.25: Intermediate - [Shallow Copy Methods]**

Which creates a shallow copy?

A) `list.copy()`, `list[:]`, `list(original)`, `copy.copy()`
B) Only `copy.deepcopy()`
C) Only slicing
D) None of these

**Answer: A**

**Explanation:**
All of these create shallow copies: `lst.copy()`, `lst[:]`, `list(lst)`, `copy.copy(lst)`, `dict.copy()`, `{**d}`. Only `copy.deepcopy()` creates a deep copy. For nested structures, shallow might be insufficient.

---

**Q14.26: Intermediate - [__slots__]**

What does `__slots__` do?

A) Creates time slots
B) Replaces instance __dict__ with fixed slots — saves memory, slightly faster
C) Limits method access
D) Defines database columns

**Answer: B**

**Explanation:**
```python
class Point:
    __slots__ = ['x', 'y']
```
No `__dict__` per instance — fixed attributes only. Saves ~40% memory for small objects. Prevents adding arbitrary attributes. Slight attribute access speedup. Trade-off: less flexibility.

---

**Q14.27: Intermediate - [sys.getsizeof]**

What does `sys.getsizeof(obj)` return?

A) Total memory including referenced objects
B) Direct memory of object only (shallow size)
C) Disk size
D) Reference count

**Answer: B**

**Explanation:**
`getsizeof` returns bytes for object itself, NOT including objects it references. For `[1, 2, 3]`, returns list overhead, not int objects. For deep size, use libraries like `pympler` or recursively sum sizes.

---

**Q14.28: Intermediate - [Memory View]**

What is `memoryview()`?

A) Debugger view
B) Zero-copy access to memory of bytes-like objects
C) Memory dump
D) Visualization tool

**Answer: B**

**Explanation:**
`memoryview(buffer)` creates view without copying data. Slicing a memoryview doesn't copy. Efficient for large binary data processing. `mv = memoryview(bytes); mv[0:10]` references same memory. Works with bytes, bytearray, array.array.

---

**Q14.29: Intermediate - [Shared Memory]**

What is `multiprocessing.shared_memory` (Python 3.8+)?

A) Normal memory
B) Memory block accessible by multiple processes without copying
C) Virtual memory
D) Cached memory

**Answer: B**

**Explanation:**
True shared memory between processes — no serialization overhead. Create: `shm = SharedMemory(create=True, size=1000)`. Access: `shm.buf`. Much faster for large data than Queue/Pipe. Must manage cleanup manually.

---

**Q14.30: Intermediate - [Object Lifetime]**

When is a Python object destroyed?

A) When function returns
B) When reference count reaches 0 (or GC collects cyclic garbage)
C) When program ends
D) Never automatically

**Answer: B**

**Explanation:**
Object is destroyed when: refcount → 0 (immediate in CPython) OR unreachable cycle detected by GC. `__del__` is called (if defined). Don't rely on `__del__` timing — use context managers for cleanup.

---

**Q14.31: Advanced - [Weak References]**

What are weak references?

A) Slow references
B) References that don't prevent garbage collection
C) Optional references
D) Compressed references

**Answer: B**

**Explanation:**
`weakref.ref(obj)` creates reference that doesn't increment refcount. If obj is deleted, weak ref returns None. Use `weakref.WeakValueDictionary` for caches. Prevents memory leaks from circular references.

---

**Q14.32: Advanced - [__del__ Problems]**

Why is `__del__` problematic?

A) It's slow
B) Unpredictable timing, resurrection issues, can prevent GC of cycles
C) It doesn't work
D) Only works in Python 2

**Answer: B**

**Explanation:**
`__del__` timing is unpredictable (especially with cycles). Object can resurrect itself. Cycles with `__del__` objects cause issues. Exceptions in `__del__` are swallowed. Prefer context managers and explicit cleanup.

---

**Q14.33: Intermediate - [Thread Local Storage]**

What is `threading.local()`?

A) Local variables
B) Per-thread storage — each thread sees its own values
C) Local network
D) Temporary variables

**Answer: B**

**Explanation:**
```python
local = threading.local()
local.value = 10  # Each thread has own 'value'
```
Access same attribute name but each thread gets own storage. Useful for thread-specific context (database connections, user sessions).

---

**Q14.34: Intermediate - [Atomic Operations]**

Which operations are atomic (thread-safe without locks)?

A) All operations
B) Some, like reading/writing single bytecode — but increments are NOT atomic
C) None
D) Only locks

**Answer: B**

**Explanation:**
Simple loads/stores of built-in types are atomic due to GIL. But `x += 1` is NOT atomic (read-modify-write = multiple bytecode). Never assume thread safety without verification. Use locks or atomic types.

---

**Q14.35: Intermediate - [Thread Daemon]**

What is a daemon thread?

A) Background process
B) Thread that doesn't prevent program exit — killed when main thread ends
C) Malicious thread
D) System thread

**Answer: B**

**Explanation:**
`thread.daemon = True` before start. Daemon threads are abruptly killed when main thread exits — no cleanup. Use for background tasks that can be safely abandoned. Non-daemon threads block program exit.

---

**Q14.36: Advanced - [Memory Profiling]**

How do you profile memory usage?

A) Only with debugger
B) Tools like memory_profiler, tracemalloc (stdlib), objgraph
C) Not possible
D) Only CPU profiling exists

**Answer: B**

**Explanation:**
`tracemalloc` (stdlib): tracks allocations. `memory_profiler`: line-by-line usage. `objgraph`: object graphs. `sys.getsizeof()` for individual objects. `gc.get_objects()` lists all tracked objects. Essential for finding leaks.

---

**Q14.37: Intermediate - [tracemalloc]**

What does `tracemalloc` do?

A) Traces function calls
B) Tracks memory allocations with traceback to source
C) Traces garbage collection
D) Traces file access

**Answer: B**

**Explanation:**
```python
tracemalloc.start()
# ... code ...
snapshot = tracemalloc.take_snapshot()
```
Shows where memory was allocated, with stack traces. `snapshot.statistics()` groups by file/line. Essential for finding memory growth causes.

---

**Q14.38: Intermediate - [Mutable Default Arguments]**

What is the output?
```python
def append_to(element, lst=[]):
    lst.append(element)
    return lst

print(append_to(1))
print(append_to(2))
```

A) `[1], [2]`
B) `[1], [1, 2]`
C) `[1, 2], [1, 2]`
D) Error

**Answer: B**

**Explanation:**
⚠️ Default mutable argument is shared across calls! The default list is created ONCE at function definition, not per call. Second call appends to same list. Fix: `lst=None; if lst is None: lst = []`.

---

**Q14.39: Intermediate - [Interned Objects]**

What is interning?

A) Internal variables
B) Reusing existing immutable objects instead of creating duplicates
C) Internet access
D) Variable naming

**Answer: B**

**Explanation:**
Python interns small integers (-5 to 256) and some strings. `a = 256; b = 256` → same object (interned). Saves memory. `sys.intern(string)` forces interning. Implementation detail — don't rely on it for logic.

---

**Q14.40: Intermediate - [Object Creation Overhead]**

Which is more memory efficient for many instances?
```python
# A: Regular class
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

# B: With __slots__
class SlotPoint:
    __slots__ = ['x', 'y']
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

A) A is more efficient
B) B is more efficient (no __dict__)
C) Same efficiency
D) Depends on x, y values

**Answer: B**

**Explanation:**
Regular class: each instance has `__dict__` (hashtable overhead). `__slots__`: fixed struct-like layout, no dict. For millions of Point objects, slots saves significant memory. Trade-off: can't add arbitrary attributes.

---

**Q14.41: Advanced - [__sizeof__]**

What is `__sizeof__()` method?

A) Same as sys.getsizeof
B) Returns internal size of object; getsizeof adds GC overhead
C) File size
D) Class size

**Answer: B**

**Explanation:**
`obj.__sizeof__()` returns object's own memory use. `sys.getsizeof(obj)` calls `__sizeof__` and adds garbage collector overhead (typically 16 bytes for tracked objects). For exact bytes, use `__sizeof__`.

---

**Q14.42: Intermediate - [Process vs Thread Memory]**

Which uses more memory: 10 threads or 10 processes?

A) 10 threads
B) 10 processes (each has separate memory space)
C) Same
D) Depends on GIL

**Answer: B**

**Explanation:**
Threads share memory — only thread stack is separate (default ~1MB each). Processes have complete memory isolation — entire Python interpreter replicated. 10 processes use much more memory than 10 threads.

---

**Q14.43: Advanced - [GIL Release during I/O]**

When does Python release the GIL?

A) Never
B) During I/O operations and C extensions that release it
C) Every 100 instructions
D) Only in multiprocessing

**Answer: B**

**Explanation:**
GIL releases during: blocking I/O (file, network), time.sleep(), many C extensions (NumPy operations). That's why threading helps I/O-bound code despite GIL — threads can run while one waits on I/O.

---

**Q14.44: Advanced - [Free-Threading Python]**

What is free-threading/no-GIL Python?

A) Python without threading
B) Experimental builds without GIL for true parallelism (PEP 703)
C) Faster Python
D) Python 4

**Answer: B**

**Explanation:**
PEP 703 proposes optional GIL-free mode. Python 3.13+ has experimental `--disable-gil` build. True thread parallelism but requires thread-safe code. Trade-off: single-thread performance may decrease. Evolving feature.

---

**Q14.45: Intermediate - [Condition Variable]**

What is `threading.Condition`?

A) If statement
B) Allows threads to wait for a condition and be notified when it changes
C) Health check
D) Error condition

**Answer: B**

**Explanation:**
`cond = Condition(); with cond: cond.wait()` — releases lock, waits. `cond.notify()` wakes one waiter. `notify_all()` wakes all. For producer-consumer, bounded buffers. More flexible than Event.

---

**Q14.46: Advanced - [Memory-Mapped Files]**

What is `mmap.mmap()`?

A) Memory map visualization
B) Maps file to memory — access file like bytearray, OS handles paging
C) Memory manager
D) Map data structure

**Answer: B**

**Explanation:**
Memory-mapped file: file appears as memory buffer. OS pages data in/out. Efficient for large files — no explicit read/write. Can share between processes. Random access without loading entire file.

---

**Q14.47: Intermediate - [Barrier]**

What is `threading.Barrier(n)`?

A) Thread limit
B) Synchronization point — all n threads must reach it before any proceeds
C) Memory barrier
D) Error barrier

**Answer: B**

**Explanation:**
`barrier = Barrier(3)` — 3 threads must call `barrier.wait()` before any continues. All wait at barrier until all arrive, then all proceed. Use for phased computation where all threads must complete a phase together.

---

**Q14.48: Advanced - [ctypes Memory]**

What is `ctypes.create_string_buffer()`?

A) String object
B) Mutable C-compatible character buffer
C) File buffer
D) Hash buffer

**Answer: B**

**Explanation:**
Creates mutable buffer for C interop. Unlike Python strings (immutable), this buffer can be modified. Used when calling C functions that write to memory. Direct memory manipulation without Python object overhead.

---

**Q14.49: Intermediate - [copy.copy with Custom Classes]**

How do you customize copying behavior?

A) Override copy()
B) Implement __copy__ and/or __deepcopy__ methods
C) Use decorators
D) Not possible

**Answer: B**

**Explanation:**
`def __copy__(self): return MyClass(...)` for shallow copy. `def __deepcopy__(self, memo): ...` for deep. `memo` dict prevents infinite loops for cyclic structures. `copy.copy()` and `copy.deepcopy()` call these methods.

---

**Q14.50: Advanced - [Object Equality and Hashing]**

What is the relationship between `__eq__` and `__hash__`?

A) Unrelated
B) If a == b, then hash(a) must equal hash(b) for dict/set use
C) hash must be unique
D) eq implies different hash

**Answer: B**

**Explanation:**
Objects that compare equal MUST have same hash for dict/set correctness. Defining `__eq__` without `__hash__` makes class unhashable. Immutable objects use immutable attributes for hash. Mutable objects shouldn't be hashable.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 6 | 12% |
| Intermediate | 35 | 70% |
| Advanced | 9 | 18% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- Object identity (id, is vs ==)
- Reference counting and garbage collection
- GIL (Global Interpreter Lock)
- threading module basics
- multiprocessing for parallelism
- concurrent.futures
- copy vs deepcopy
- __slots__ for memory efficiency
- Memory profiling tools
- Weak references
- Thread synchronization primitives
