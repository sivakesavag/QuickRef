# Chapter 23: Interview Preparation & Advanced Topics

> **Topics Covered**: Common interview questions, algorithm thinking, problem-solving patterns, Python internals, CPython details, advanced language features, expert-level concepts, career development

---

## Questions

---

**Q23.1: Basic - [FizzBuzz]**

What is the output?
```python
for i in range(1, 6):
    if i % 3 == 0 and i % 5 == 0:
        print("FizzBuzz")
    elif i % 3 == 0:
        print("Fizz")
    elif i % 5 == 0:
        print("Buzz")
    else:
        print(i)
```

A) 1, 2, Fizz, 4, Buzz
B) FizzBuzz, FizzBuzz, Fizz, FizzBuzz, Buzz
C) 1, 2, 3, 4, 5
D) Error

**Answer: A**

**Explanation:**
Classic interview question. 1: not divisible by 3 or 5, print 1. 2: print 2. 3: divisible by 3, print Fizz. 4: print 4. 5: divisible by 5, print Buzz. Logic order matters.

---

**Q23.2: Intermediate - [Two Sum]**

What's the optimal approach for Two Sum (find two numbers that sum to target)?

A) Nested loops O(n²)
B) Hash map/dict O(n) — store complement, check if exists
C) Sort and binary search
D) Random

**Answer: B**

**Explanation:**
```python
def two_sum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
```
O(n) time, O(n) space. Common pattern: use hash map for O(1) lookup.

---

**Q23.3: Intermediate - [Reverse String]**

Most Pythonic way to reverse a string?

A) `s[::-1]`
B) Loop with concatenation
C) `reversed(s)`
D) `s.reverse()`

**Answer: A**

**Explanation:**
Slicing `s[::-1]` is most Pythonic and efficient. `''.join(reversed(s))` also works. Strings are immutable so no `.reverse()`. Know common string operations.

---

**Q23.4: Intermediate - [Palindrome Check]**

What is the output?
```python
def is_palindrome(s):
    s = s.lower().replace(' ', '')
    return s == s[::-1]

print(is_palindrome("A man a plan a canal Panama"))
```

A) `False`
B) `True`
C) Error
D) `None`

**Answer: B**

**Explanation:**
Normalize: lowercase, remove spaces. "amanaplanacanalpanama" == reversed. Classic string problem. Consider: what chars to remove? How to handle unicode? Edge cases.

---

**Q23.5: Intermediate - [Anagram Check]**

What is the output?
```python
from collections import Counter
def is_anagram(s1, s2):
    return Counter(s1.lower().replace(' ', '')) == Counter(s2.lower().replace(' ', ''))

print(is_anagram("listen", "silent"))
```

A) `False`
B) `True`
C) Error
D) `Counter`

**Answer: B**

**Explanation:**
Anagram: same characters, different order. Counter counts occurrences. Equal counters = anagram. Alternative: sorted(s1) == sorted(s2). Counter is O(n), sorted is O(n log n).

---

**Q23.6: Intermediate - [Find Duplicates]**

Most efficient way to find duplicates in a list?

A) Nested loops O(n²)
B) Use set — seen set, check before adding, O(n)
C) Sort first O(n log n)
D) Counter and filter

**Answer: B**

**Explanation:**
```python
def find_duplicates(items):
    seen = set()
    duplicates = []
    for item in items:
        if item in seen:
            duplicates.append(item)
        seen.add(item)
    return duplicates
```
O(n) time, O(n) space. Set membership is O(1).

---

**Q23.7: Intermediate - [Fibonacci]**

What's the time complexity of naive recursive Fibonacci?

A) O(n)
B) O(2^n) — exponential, recalculates same values
C) O(log n)
D) O(n²)

**Answer: B**

**Explanation:**
```python
def fib(n):
    if n <= 1: return n
    return fib(n-1) + fib(n-2)
```
Exponential: fib(n) calls fib(n-1) and fib(n-2), each branch multiplies. Fix: memoization (@lru_cache) or iterative O(n).

---

**Q23.8: Intermediate - [Binary Search]**

What is the output?
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

print(binary_search([1, 3, 5, 7, 9], 5))
```

A) `5`
B) `2`
C) `1`
D) `-1`

**Answer: B**

**Explanation:**
Binary search: O(log n) for sorted arrays. Target 5 found at index 2. Know this implementation! Common interview question and building block.

---

**Q23.9: Intermediate - [Linked List Concept]**

What's the purpose of using a linked list?

A) Faster random access
B) O(1) insertion/deletion at known position, dynamic size
C) Less memory
D) Sorting

**Answer: B**

**Explanation:**
Linked list: nodes with value + next pointer. Pros: O(1) insert/delete if you have the node. Cons: O(n) access (no indexing). Use: queues, when frequent insertions. Python list handles most cases.

---

**Q23.10: Intermediate - [Stack and Queue]**

Which Python structures for stack and queue?

A) Only list
B) Stack: list (append/pop). Queue: collections.deque (append/popleft O(1))
C) Both use deque
D) Neither exists

**Answer: B**

**Explanation:**
Stack (LIFO): list works great — append(), pop() are O(1). Queue (FIFO): list.pop(0) is O(n)! Use deque: append(), popleft() are O(1). Know when to use which.

---

**Q23.11: Intermediate - [Tree Traversal]**

What's the order for inorder traversal of binary tree?

A) Root, left, right
B) Left, root, right
C) Left, right, root
D) Random

**Answer: B**

**Explanation:**
Inorder: left subtree → root → right subtree. For BST: gives sorted order. Preorder: root → left → right (copying tree). Postorder: left → right → root (deletion). BFS for level-order.

---

**Q23.12: Intermediate - [Graph Representation]**

How to represent a graph in Python?

A) Only matrices
B) Adjacency list (dict of lists) or adjacency matrix (2D list)
C) Linked nodes only
D) Arrays

**Answer: B**

**Explanation:**
```python
# Adjacency list (sparse graphs)
graph = {'A': ['B', 'C'], 'B': ['A', 'D']}
# Adjacency matrix (dense graphs)
matrix = [[0,1,1], [1,0,0], [1,0,0]]
```
List: O(V+E) space. Matrix: O(V²). Choose based on graph density.

---

**Q23.13: Intermediate - [BFS vs DFS]**

When use BFS vs DFS?

A) Same thing
B) BFS: shortest path (unweighted), level-order. DFS: path existence, topological sort
C) BFS always faster
D) DFS always faster

**Answer: B**

**Explanation:**
BFS: explores level by level, finds shortest path first (unweighted). Uses queue. DFS: explores deeply, less memory for narrow graphs. Uses stack/recursion. Choose based on problem.

---

**Q23.14: Intermediate - [Memoization]**

What is memoization?

A) Memory management
B) Caching function results for repeated calls with same arguments
C) Memorizing code
D) Memory allocation

**Answer: B**

**Explanation:**
```python
@lru_cache(maxsize=None)
def fib(n):
    if n <= 1: return n
    return fib(n-1) + fib(n-2)
```
Fibonacci O(2^n) → O(n) with memoization. Trade memory for time. Dynamic programming technique.

---

**Q23.15: Advanced - [CPython Internals]**

What is CPython?

A) Compiled Python
B) Reference implementation of Python, written in C
C) C extension
D) Cython

**Answer: B**

**Explanation:**
CPython: official Python interpreter. Compiles to bytecode, interprets on VM. Other implementations: PyPy (JIT), Jython (JVM), IronPython (.NET). CPython-specific: GIL, C API.

---

**Q23.16: Advanced - [Python Bytecode]**

What is Python bytecode?

A) Binary executable
B) Intermediate representation compiled from source, executed by VM
C) Machine code
D) Assembly

**Answer: B**

**Explanation:**
`dis.dis(func)` shows bytecode. Instructions like LOAD_FAST, CALL_FUNCTION. `.pyc` files store bytecode. Python VM interprets bytecode. Not machine code — interpreted.

---

**Q23.17: Advanced - [Object Model]**

In CPython, what is a PyObject?

A) Python class
B) Base C struct for all Python objects — contains refcount and type
C) Object file
D) Interface

**Answer: B**

**Explanation:**
Every Python object in CPython: PyObject struct with `ob_refcnt` (reference count) and `ob_type` (type pointer). Everything is object. Understanding helps with C extensions, performance.

---

**Q23.18: Advanced - [Small Integer Cache]**

Why does this happen?
```python
a = 256; b = 256; print(a is b)  # True
c = 257; d = 257; print(c is d)  # False (usually)
```

A) Bug
B) CPython caches integers -5 to 256 — same object reused
C) Random
D) Integer overflow

**Answer: B**

**Explanation:**
Implementation detail: small integers are cached at startup. 256 is cached, same object. 257 created fresh each time. Never rely on this — use `==` for value comparison, `is` only for None/explicit checks.

---

**Q23.19: Advanced - [String Interning]**

When are strings interned?

A) Never
B) Identifier-like strings (alphanumeric) often interned automatically
C) All strings
D) Only ASCII

**Answer: B**

**Explanation:**
`"hello"` may be interned (one copy shared). `"hello world"` (space) typically not. `sys.intern()` forces interning. Optimization for known identifiers. Don't rely on it for logic.

---

**Q23.20: Advanced - [__dict__ vs __slots__]**

What is the output?
```python
class A:
    pass

class B:
    __slots__ = ['x']

print(hasattr(A(), '__dict__'), hasattr(B(), '__dict__'))
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
Regular class: each instance has `__dict__` for attributes. `__slots__`: fixed attributes, no dict. Memory savings. Slot instances don't have `__dict__` unless explicitly included in slots.

---

**Q23.21: Intermediate - [Sliding Window]**

When use sliding window pattern?

A) GUI windows
B) Contiguous subarray/substring problems — maintain window, slide through data
C) Sorting
D) Graph problems

**Answer: B**

**Explanation:**
```python
# Max sum of k consecutive elements
window_sum = sum(arr[:k])
max_sum = window_sum
for i in range(k, len(arr)):
    window_sum += arr[i] - arr[i-k]  # Slide window
    max_sum = max(max_sum, window_sum)
```
O(n) instead of O(n*k). Common pattern for substring, subarray problems.

---

**Q23.22: Intermediate - [Two Pointers]**

When use two pointers pattern?

A) Pointer management
B) Sorted arrays, pair finding, partitioning — two indices moving inward/outward
C) Linked lists only
D) Binary trees

**Answer: B**

**Explanation:**
Two Sum (sorted): one pointer at start, one at end, move based on sum. Palindrome: compare from both ends. O(n) vs O(n²) for many problems. Know this pattern.

---

**Q23.23: Intermediate - [Hash Map Uses]**

Common interview uses for hash maps:

A) Sorting only
B) Counting, caching, lookup tables, deduplication, anagram grouping
C) Graph traversal
D) Tree operations

**Answer: B**

**Explanation:**
Hash maps everywhere: frequency counts (Counter), seen sets, complement lookup (Two Sum), grouping by key, caching. O(1) average operations. Master this data structure.

---

**Q23.24: Advanced - [Descriptor Protocol]**

What makes something a descriptor?

A) Decorator
B) Object with __get__, __set__, or __delete__ methods
C) Description attribute
D) Docstring

**Answer: B**

**Explanation:**
Descriptors: customize attribute access. `property` is a descriptor. Define `__get__(self, obj, type)`, etc. When accessed on instance, descriptor protocol invoked. Powerful but advanced.

---

**Q23.25: Advanced - [Import System]**

What happens during `import module`?

A) Just reads file
B) Find module → load → create module object → execute code → cache in sys.modules
C) Only finds module
D) Compiles to binary

**Answer: B**

**Explanation:**
Import: search sys.path, find .py or package, compile to bytecode, execute (running top-level code), cache in sys.modules. Re-import uses cache. `importlib` for programmatic control.

---

**Q23.26: Advanced - [Circular Imports]**

How to fix circular import errors?

A) Can't fix
B) Import inside function, restructure modules, use TYPE_CHECKING guard
C) Delete one import
D) Use * imports

**Answer: B**

**Explanation:**
A imports B which imports A. During A's import, B tries to access not-yet-defined names. Fixes: import inside function (lazy), restructure to remove cycle, `if TYPE_CHECKING:` for type hints only.

---

**Q23.27: Advanced - [MRO (Method Resolution Order)]**

What is MRO?

A) Memory Release Order
B) Order Python searches for methods in class hierarchy — C3 linearization
C) Method Return Order
D) Module Read Order

**Answer: B**

**Explanation:**
With multiple inheritance, which parent's method wins? `ClassName.__mro__` shows order. C3 linearization algorithm. Respects: children before parents, preserve order. Diamond problem solved.

---

**Q23.28: Advanced - [Metaclass __new__ vs __init__]**

When is metaclass `__new__` called?

A) Instance creation
B) Class creation — when class statement is executed
C) Never
D) Import time

**Answer: B**

**Explanation:**
`class Foo(metaclass=Meta):` executes `Meta.__new__` to create class Foo itself. Metaclass controls class behavior, not instance. `__call__` on metaclass is called when Foo() is called.

---

**Q23.29: Intermediate - [Time Complexity Analysis]**

What's the time complexity?
```python
for i in range(n):
    for j in range(i, n):
        print(i, j)
```

A) O(n)
B) O(n²)
C) O(n log n)
D) O(2^n)

**Answer: B**

**Explanation:**
Outer: n iterations. Inner: n, n-1, n-2, ... 1 iterations. Total: n(n+1)/2 ≈ n²/2 = O(n²). Common analysis. Nested loops usually multiply complexities.

---

**Q23.30: Intermediate - [Space Complexity]**

What's the space complexity?
```python
def func(n):
    result = []
    for i in range(n):
        result.append(i * 2)
    return result
```

A) O(1)
B) O(n) — result list grows with n
C) O(log n)
D) O(n²)

**Answer: B**

**Explanation:**
Space for result list = O(n). Also consider: recursion stack, temporary variables. Here: O(n) for output. Sometimes output space isn't counted; clarify in interviews.

---

**Q23.31: Intermediate - [Recursion Stack]**

What's the space complexity due to recursion?
```python
def factorial(n):
    if n <= 1: return 1
    return n * factorial(n - 1)
```

A) O(1)
B) O(n) — call stack depth is n
C) O(log n)
D) O(n!)

**Answer: B**

**Explanation:**
Each recursive call adds stack frame. n calls deep = O(n) stack space. Python default limit ~1000. Tail recursion optimization doesn't exist in Python. Consider iterative for deep recursion.

---

**Q23.32: Advanced - [Generator Internals]**

What state does a generator maintain?

A) Nothing
B) Local variables, bytecode position — freezes and resumes
C) Only yield value
D) Full function copy

**Answer: B**

**Explanation:**
Generator frame: local variables, instruction pointer, exception state. `next()` resumes from where it yielded. `gen.gi_frame.f_locals` shows current state. Coroutine-like suspension.

---

**Q23.33: Advanced - [async/await Internals]**

What is a coroutine at implementation level?

A) Thread
B) Generator-based state machine — async/await are syntax over generators
C) Process
D) Callback

**Answer: B**

**Explanation:**
`async def` creates coroutine function. Coroutine is generator-like: suspends at await, resumes when awaited value ready. Event loop schedules. Not threads — cooperative multitasking.

---

**Q23.34: Intermediate - [Behavioral Questions]**

What to emphasize in "Tell me about yourself"?

A) Personal life
B) Relevant experience, skills for the role, career goals aligned with position
C) Full resume recitation
D) Salary expectations

**Answer: B**

**Explanation:**
2-minute pitch: current role/background, key achievements, relevant skills, interest in this role. Practice but don't memorize. Tailor to position. Show enthusiasm.

---

**Q23.35: Intermediate - [Problem Solving Approach]**

How to approach interview coding problems?

A) Start coding immediately
B) Clarify problem → examples → approach → code → test → optimize
C) Ask for hints
D) Use memorized solutions

**Answer: B**

**Explanation:**
1) Clarify inputs/outputs/constraints. 2) Work through examples. 3) Explain approach before coding. 4) Code cleanly. 5) Test with examples. 6) Discuss optimization. Communicate throughout.

---

**Q23.36: Intermediate - [System Design Basics]**

What's covered in system design interviews?

A) Coding only
B) High-level architecture — scalability, databases, caching, load balancing
C) Low-level code
D) Testing

**Answer: B**

**Explanation:**
Design: URL shortener, Twitter feed, etc. Discuss: requirements, scale, components, database schema, APIs, scalability (sharding, caching, CDN). Show breadth. Senior roles especially.

---

**Q23.37: Advanced - [Context Switching Cost]**

What is context switch overhead?

A) No overhead
B) CPU state save/restore when switching between processes/threads — impacts performance
C) Memory cost
D) Network latency

**Answer: B**

**Explanation:**
Switching: save registers, stack pointer, restore other process's state. Thousands per second okay, millions = overhead. Async: no context switch for I/O wait. Understand tradeoffs.

---

**Q23.38: Expert - [Memory Layout]**

How is Python dict implemented?

A) Array only
B) Hash table with open addressing — keys hashed, collisions handled
C) Tree
D) Linked list

**Answer: B**

**Explanation:**
Dict: hash table. Key → hash → index. Collision: probe for next slot (open addressing in CPython 3.6+). O(1) average, O(n) worst case. Compact dict preserves insertion order (3.7+).

---

**Q23.39: Advanced - [GIL Alternatives]**

Ways to work around GIL for CPU-bound work?

A) None
B) multiprocessing, C extensions releasing GIL, subinterpreters (3.12+), free-threading (3.13+)
C) Threading
D) Async

**Answer: B**

**Explanation:**
multiprocessing: separate processes, each has GIL. NumPy/C: release GIL during compute. Subinterpreters: multiple interpreters in one process. PEP 703: optional GIL-free mode. Evolving area.

---

**Q23.40: Intermediate - [Code Quality Metrics]**

What metrics indicate code quality?

A) Lines of code
B) Test coverage, cyclomatic complexity, maintainability index, lint issues
C) File count
D) Comments ratio

**Answer: B**

**Explanation:**
Coverage: how much tested. Complexity: branching paths (lower better). Maintainability: combined metric. Lint issues: style/error counts. Metrics are indicators, not absolute measures.

---

**Q23.41: Intermediate - [Technical Debt]**

What is technical debt?

A) Money owed
B) Shortcuts taken that create future work — "quick fix" now, problems later
C) Infrastructure cost
D) Training cost

**Answer: B**

**Explanation:**
Debt: ship fast with suboptimal code. Interest: bugs, slow features, hard maintenance. Pay down: refactoring. Some debt okay intentionally; untracked debt is dangerous. Balance shipping vs quality.

---

**Q23.42: Intermediate - [Code Review Skills]**

What makes a good code reviewer?

A) Finding all bugs
B) Constructive feedback, teaching, understanding constraints, focusing on important issues
C) Speed only
D) Nitpicking style

**Answer: B**

**Explanation:**
Good reviews: catch real issues, suggest improvements, teach patterns, understand context. Not: blocking on style (use formatters), being harsh, reviewing too slowly. Both sides learn.

---

**Q23.43: Advanced - [Python Enhancement Proposals]**

What are PEPs?

A) Python libraries
B) Python Enhancement Proposals — design documents for features, standards
C) Error reports
D) Packages

**Answer: B**

**Explanation:**
PEP 8: style guide. PEP 20: Zen of Python. PEP 484: type hints. PEP 703: free-threading. PEPs document language changes. Reading relevant PEPs shows language design understanding.

---

**Q23.44: Intermediate - [Common Mistakes]**

Common Python interview mistakes:

A) None exist
B) Modifying list while iterating, mutable defaults, ignoring edge cases, not testing
C) Using built-ins
D) Type hints

**Answer: B**

**Explanation:**
Watch for: mutable default arguments, off-by-one errors, not handling empty input, forgetting return statements, infinite loops. Test your code with examples before saying done.

---

**Q23.45: Intermediate - [Growth Mindset]**

What is growth mindset for developers?

A) Salary focus
B) Belief that skills can be developed through effort, learning from failure
C) Fixed talent
D) Rapid promotion

**Answer: B**

**Explanation:**
"I can't do this YET." Failures are learning. Feedback is growth opportunity. Continuous learning: new languages, tools, domains. Career longevity requires adaptation.

---

**Q23.46: Advanced - [Type Narrowing]**

What is type narrowing?

A) Reducing types
B) Type checker inferring more specific type after condition
C) Type casting
D) Generics

**Answer: B**

**Explanation:**
```python
x: str | None = get_value()
if x is not None:
    # Type checker knows x is str here
    print(x.upper())
```
mypy/pyright narrow type based on conditionals. Enables type-safe code without casts.

---

**Q23.47: Expert - [Walrus Operator Internals]**

What scope does `:=` (walrus operator) use?

A) Always local
B) Enclosing scope for comprehensions, otherwise local — special scoping rules
C) Global
D) No scope

**Answer: B**

**Explanation:**
```python
[y := x for x in range(3)]  # y available after
```
In comprehensions, `:=` target is in enclosing scope (not comprehension's hidden scope). Subtle but intentional for practical use.

---

**Q23.48: Intermediate - [Career Development]**

How to grow as a Python developer?

A) Only work experience
B) Read code, contribute to open source, learn new areas, teach others, build projects
C) Certifications only
D) Stay in comfort zone

**Answer: B**

**Explanation:**
Growth: read quality code (stdlib, popular packages). Contribute: issues, PRs. Expand: web, ML, systems. Teach: blog, mentor. Build: personal projects. Diversify while deepening core.

---

**Q23.49: Advanced - [Pattern Matching (3.10+)]**

What is structural pattern matching?

A) Regex
B) match/case statements for matching structure of data and destructuring
C) String patterns
D) Design patterns

**Answer: B**

**Explanation:**
```python
match point:
    case (0, 0):
        print("Origin")
    case (x, 0):
        print(f"On x-axis at {x}")
```
Match type + structure, capture values. Powerful for handling different shapes of data. Python 3.10+.

---

**Q23.50: Expert - [Future of Python]**

Recent/upcoming Python developments:

A) No changes
B) Faster CPython (3.11+), optional GIL removal (3.13+), pattern matching, improved typing
C) Python 4.0
D) Deprecating Python

**Answer: B**

**Explanation:**
3.11: 25% faster on average. 3.13: experimental free-threading (no GIL build). JIT exploration. Better typing (TypedDict, Protocol). Pattern matching. Active development continuing.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 1 | 2% |
| Intermediate | 30 | 60% |
| Advanced | 15 | 30% |
| Expert | 4 | 8% |

**Key Topics Covered:**
- Classic interview problems
- Algorithm patterns (two pointers, sliding window)
- Data structures (hash maps, trees, graphs)
- CPython internals
- Time/space complexity analysis
- System design basics
- Career development
- Python language evolution
