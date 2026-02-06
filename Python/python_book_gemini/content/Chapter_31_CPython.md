# Chapter 31: CPython Internals

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: Bytecode (`dis` module), GIL Mechanics, Memory Allocation (`pymalloc`), Reference Counting, Python Object Structure (`PyObject`), Interpreter Loop, `.pyc` files, Stack Frames, `sys` internals.

---

**Q31.1: Basic - [CPython definition]**

CPython is:

A) The reference implementation of Python, written in C.
B) A python script runner.
C) A C compiler.
D) A database.

**Answer: A**

**Explanation:**
It compiles Python source code into bytecode, which is then executed by the CPython virtual machine.

---

**Q31.2: Intermediate - [Dis Module]**

To view the bytecode instructions of a Python function, you can use:

A) `import dis; dis.dis(func)`
B) `import bytecode; bytecode.show(func)`
C) `func.bytecode`
D) `inspect.code(func)`

**Answer: A**

**Explanation:**
Shows the assembly-like instructions (LOAD_FAST, BINARY_ADD, etc.).

---

**Q31.3: Advanced - [GIL Purpose]**

The Global Interpreter Lock (GIL) exists in CPython to:

A) Protect internal C structures (like reference counts) from race conditions in multi-threaded environments, making the C implementation simpler and thread-safe.
B) Make Python faster.
C) Prevent recursion.
D) Encrypt code.

**Answer: A**

**Explanation:**
It ensures only one thread executes Python bytecode at a time per process.

---

**Q31.4: Expert - [Pymalloc]**

Python's small object allocator ("pymalloc") optimizes memory allocation by:

A) Using "Arenas", "Pools", and "Blocks" to manage small objects (<= 512 bytes) efficiently, reducing fragmentation and system calls (`malloc`).
B) Using a database.
C) Calling the OS for every object.
D) Compressing memory.

**Answer: A**

**Explanation:**
Objects larger than 512 bytes generally go directly to the system's `malloc`.

---

**Q31.5: Basic - [Pyc Files]**

A `.pyc` file contains:

A) Compiled Python Bytecode.
B) Source code.
C) Machine code.
D) C code.

**Answer: A**

**Explanation:**
Stored in `__pycache__` to speed up module loading (not execution) on subsequent runs.

---

**Q31.6: Intermediate - [Reference Counting]**

The primary mechanism for Garbage Collection in CPython is:

A) Reference Counting (deallocating an object immediately when its refcount drops to zero).
B) Mark and Sweep.
C) Generational GC.
D) Manual free.

**Answer: A**

**Explanation:**
The cyclic GC is a secondary system to catch reference cycles.

---

**Q31.7: Advanced - [PyObject Head]**

Every Python object in C (`PyObject`) starts with:

A) `PyObject_HEAD` (containing the reference count and a pointer to the Type object).
B) The value.
C) The name.
D) The size.

**Answer: A**

**Explanation:**
This allows polymorphism; the interpreter knows how to treat any pointer as a `PyObject`.

---

**Q31.8: Expert - [LOAD_FAST]**

The bytecode instruction `LOAD_FAST` is faster than `LOAD_NAME` because:

A) It accesses local variables by index in an array (C array lookup), whereas `LOAD_NAME` searches a dictionary (hash map lookup).
B) It is a shorter instruction.
C) It uses less memory.
D) It runs on GPU.

**Answer: A**

**Explanation:**
Why local variables are faster than globals.

---

**Q31.9: Basic - [Id function]**

In CPython, the `id(obj)` function usually returns:

A) The memory address of the object.
B) A random number.
C) The hash.
D) The value.

**Answer: A**

**Explanation:**
Implementation detail, but reliable in CPython.

---

**Q31.10: Intermediate - [Code Object]**

The compiled bytecode and metadata for a function are stored in:

A) `func.__code__` (a code object).
B) `func.__body__`
C) `func.byte`
D) `func.text`

**Answer: A**

**Explanation:**
Contains `co_code` (raw bytes), `co_varnames`, `co_consts`, etc.

---

**Q31.11: Advanced - [Sys Settrace]**

`sys.settrace(tracefunc)` allows you to:

A) Register a callback function that is executed for every line of code/call/return, enabling debuggers and coverage tools.
B) Draw lines.
C) Trace packets.
D) Stop execution.

**Answer: A**

**Explanation:**
Huge performance overhead, but essential for `pdb`.

---

**Q31.12: Expert - [Frame Object]**

When a function is called, CPython creates a "Frame Object" (`PyFrameObject`) which contains:

A) The execution context: reference to code object, globals dict, locals dict (`f_locals`), logic stack, and instruction pointer.
B) The image frame.
C) The button frame.
D) The return value only.

**Answer: A**

**Explanation:**
Frames are linked together to form the call stack (`f_back`).

---

**Q31.13: Basic - [None Singleton]**

In CPython, `None` is:

A) A singleton object (only one instance exists in memory).
B) Not an object.
C) A keyword only.
D) 0.

**Answer: A**

**Explanation:**
`x is None` checks for identity with this single object.

---

**Q31.14: Intermediate - [Interning]**

String "Interning" is a technique where:

A) CPython caches certain immutable strings (like identifiers and small strings) so that only one copy exists, allowing faster identity comparison (`is` instead of `==`).
B) Strings are deleted.
C) Strings are encrypted.
D) Strings are translated.

**Answer: A**

**Explanation:**
Why `'a' is 'a'` is True.

---

**Q31.15: Advanced - [Dict Implementation]**

CPython's `dict` is implemented using:

A) A Hash Table with optimization for sparse arrays (separate keys/values arrays in newer versions to save memory).
B) A Binary Tree.
C) A Linked List.
D) A B-Tree.

**Answer: A**

**Explanation:**
Compact dicts (Python 3.6+) preserve insertion order as a side effect (guaranteed in 3.7+).

---

**Q31.16: Expert - [CEVAL]**

The core evaluation loop of Python (often called `ceval.c`) acts as:

A) A giant `switch` statement (or computed gotos) that iterates over bytecode instructions and performs the corresponding C operation.
B) A compiler.
C) A database.
D) A parser.

**Answer: A**

**Explanation:**
The heart of the Virtual Machine.

---

**Q31.17: Basic - [Bytecode Portable]**

Is Python bytecode compatible across different Python versions (e.g., 3.8 to 3.11)?

A) No, it changes frequently.
B) Yes, always.
C) Only usually.
D) Yes, if compiled on Linux.

**Answer: A**

**Explanation:**
Magic numbers in `.pyc` files prevent loading mismatched versions.

---

**Q31.18: Intermediate - [Sys Getsizeof]**

`sys.getsizeof(obj)` returns:

A) The size of the object in bytes (including overhead like PyObject_HEAD).
B) The length.
C) The value.
D) The type.

**Answer: A**

**Explanation:**
Lists have capacity overhead (`ob_size` vs allocated slots).

---

**Q31.19: Advanced - [Method Resolution Order]**

The C3 Linearization algorithm is used to determine:

A) The Method Resolution Order (MRO) for class inheritance (the order in which base classes are searched).
B) The speed of the method.
C) The memory usage.
D) The function name.

**Answer: A**

**Explanation:**
`Class.mro()`. Solves the diamond problem consistently.

---

**Q31.20: Expert - [List resizing]**

When items are appended to a list and it runs out of allocated space, CPython:

A) Allocates a new, larger array (usually ~1.125x + constant) and copies existing pointers over (amortized O(1)).
B) Adds just one slot.
C) Fails.
D) Compresses the list.

**Answer: A**

**Explanation:**
Over-allocation prevents `realloc` on every append.

---

**Q31.21: Basic - [Interpreted Language]**

Python is technically:

A) A compiled-to-bytecode language, which is then interpreted by a VM.
B) Purely interpreted (reading source line-by-line).
C) Purely compiled (like C++).
D) Hardware code.

**Answer: A**

**Explanation:**
The "Interpretation" happens at the bytecode level.

---

**Q31.22: Intermediate - [Sys Intern]**

You can manually force string interning using:

A) `sys.intern(string)`
B) `sys.cache(string)`
C) `string.intern()`
D) `os.keep(string)`

**Answer: A**

**Explanation:**
Useful for optimizing memory when processing huge numbers of repetitive dictionary keys (e.g., CSV headers).

---

**Q31.23: Advanced - [Python Stack]**

The "Python Stack" (frames) operates:

A) On the heap of the C process (it is a linked list of Frame objects), separate from the C stack (execution stack).
B) On the CPU registers directly.
C) On the disk.
D) On the network.

**Answer: A**

**Explanation:**
This is why recursion depth is limited by a counter, not strictly C stack size (though they are related).

---

**Q31.24: Expert - [Generator Internal]**

Internally, a generator is:

A) A function executing in a stack frame that can be suspended (saving the instruction pointer and locals) and resumed later.
B) A thread.
C) A separate process.
D) A list.

**Answer: A**

**Explanation:**
`yield` preserves the frame state.

---

**Q31.25: Basic - [Magic Number]**

The "Magic Number" at the start of a `.pyc` file identifies:

A) The Python version that compiled it (to prevent incompatibility).
B) The file size.
C) The author.
D) The date.

**Answer: A**

**Explanation:**
First 4 bytes.

---

**Q31.26: Intermediate - [Mutable Default arg]**

Why is `def f(l=[]):` dangerous in CPython implementation?

A) The list `[]` is created *once* at definition time (when the `def` opcode is executed) and stored in the function object's `__defaults__` tuple, so it persists across calls.
B) It creates a new list every time.
C) It is a syntax error.
D) It is slow.

**Answer: A**

**Explanation:**
Function defaults are evaluated once.

---

**Q31.27: Advanced - [Type vs Object]**

In Python 3, `type` is:

A) An object itself (an instance of `type`), and the metaclass of all classes.
B) A function only.
C) A string.
D) A keyword only.

**Answer: A**

**Explanation:**
"Everything is an object" - even classes.

---

**Q31.28: Expert - [Buffer Interface C]**

The `Py_buffer` C struct is central to:

A) The Buffer Protocol (sharing raw memory regions between objects like bytes, memoryview, and numpy arrays).
B) String formatting.
C) File buffering.
D) Network buffering.

**Answer: A**

**Explanation:**
Allows zero-copy operations at the C level.

---

**Q31.29: Intermediate - [Slot Wrapper]**

When you define `__slots__`, CPython:

A) Does not create a `__dict__` for instances, instead accessing attributes via array offsets in memory (descriptors).
B) Creates a bigger dict.
C) Makes it slower.
D) Hides attributes.

**Answer: A**

**Explanation:**
Memory optimization.

---

**Q31.30: Basic - [Global Keyword]**

The `global` keyword affects bytecode generation by:

A) Changing a variable access from `STORE_FAST` (local) to `STORE_GLOBAL`.
B) Making it faster.
C) Making it public.
D) Exporting it.

**Answer: A**

**Explanation:**
Tells the compiler scope logic where to look.

---

**Q31.31: Intermediate - [Python Memory Allocator]**

When a small object (<= 512 bytes) is freed, CPython:

A) Does not return the memory to the OS immediately; it keeps it in its pools for future allocations of the same size class (to avoid fragmentation and syscall overhead).
B) Returns it to the OS.
C) Deletes the pool.
D) Crashes.

**Answer: A**

**Explanation:**
This is why Python process memory usage rarely goes down, even after deleting objects.

---

**Q31.32: Advanced - [Co_freevars]**

In a closure, the variables from the outer scope that are captured are stored in the code object's:

A) `co_freevars`
B) `co_names`
C) `co_vars`
D) `co_locals`

**Answer: A**

**Explanation:**
And the values are stored in the `__closure__` cell objects.

---

**Q31.33: Basic - [Hashability]**

For an object to be used as a dictionary key, it must be "Hashable", which usually implies:

A) It has a `__hash__` method that (ideally) returns the same value for the object's lifetime, and an `__eq__` method.
B) It is a list.
C) It is a dict.
D) It is mutable.

**Answer: A**

**Explanation:**
Mutable objects (lists) are not hashable.

---

**Q31.34: Expert - [Traceback Object]**

A "Traceback Object" (`sys.last_traceback`) is a linked list of:

A) Stack Frames (snapshots of the execution stack at the moment the exception occurred).
B) Errors.
C) Files.
D) Strings.

**Answer: A**

**Explanation:**
Holding onto a traceback can keep all those frames (and their locals) alive, causing memory leaks.

---

**Q31.35: Intermediate - [Ellipsis]**

The `...` literal in Python is:

A) The `Ellipsis` singleton object (often used in NumPy slicing or as a placeholder).
B) A syntax error.
C) A comment.
D) Used for ranges.

**Answer: A**

**Explanation:**
`type(...)` is `EllipsisType`.

---

**Q31.36: Advanced - [PyLong Implementation]**

How does CPython implement integers (`int`)?

A) As arbitrary-precision integers (essentially an array of digits/digits in base 2^30), allowing them to grow as large as memory permits.
B) As 64-bit C integers.
C) As floats.
D) As strings.

**Answer: A**

**Explanation:**
No overflow (but slower than native C ints).

---

**Q31.37: Basic - [Disasm]**

The output of `dis.dis()` typically shows columns for:

A) Line Number, Byte Offset, Opcode Name, Argument (if any), and Human-readable argument interpretation.
B) Binary code only.
C) Source code only.
D) C code.

**Answer: A**

**Explanation:**
Helpful for understanding what the interpreter is actually doing.

---

**Q31.38: Intermediate - [Function Attributes]**

Since functions are objects, you can:

A) Attach arbitrary attributes to them (e.g., `func.my_attr = 10`) at runtime.
B) Cannot change them.
C) Convert them to classes.
D) Delete them.

**Answer: A**

**Explanation:**
Useful for caching or metadata (like Flask's route decorators do).

---

**Q31.39: Advanced - [Cell Object]**

A "Cell Object" is used to:

A) Implement closures; it holds the value of a variable referenced by nested functions, allowing updates to be seen across scopes.
B) Store Excel data.
C) Run biological simulations.
D) Store global variables.

**Answer: A**

**Explanation:**
`LOAD_DEREF` / `STORE_DEREF` opcodes use cells.

---

**Q31.40: Expert - [Py_INCREF]**

In C extension modules, `Py_INCREF(obj)`:

A) Increments the reference count of `obj` (ensuring it is not collected while C code is using it).
B) Increases the value.
C) Increases the size.
D) Crashes the interpreter.

**Answer: A**

**Explanation:**
Forgetting this (or `Py_DECREF`) is the #1 cause of memory leaks/crashes in C extensions.

---

**Q31.41: Basic - [Builtins]**

The `__builtins__` module contains:

A) References to all built-in functions and exceptions (print, len, Exception, etc.) available in the global scope.
B) User functions.
C) Hidden files.
D) OS commands.

**Answer: A**

**Explanation:**
Technically accessible as `builtins` (standard library).

---

**Q31.42: Intermediate - [Bytecode Optimization]**

CPython's peephole optimizer performs simple optimizations like:

A) Constant Folding (e.g., converting `2 + 3` to `5` at compile time).
B) JIT compilation.
C) Removing loops.
D) Parallelizing code.

**Answer: A**

**Explanation:**
It works on the bytecode before saving to `.pyc`.

---

**Q31.43: Advanced - [Sys Modules]**

`sys.modules` is:

A) A dictionary mapping module names to loaded module objects (a cache), ensuring modules are initialized only once per process.
B) A list of installed modules.
C) A function.
D) A file.

**Answer: A**

**Explanation:**
Modifying this can trick Python into reloading or hotswapping code.

---

**Q31.44: Expert - [PyTypeObject]**

The `PyTypeObject` struct in C determines:

A) The behavior of a Python type (its name, size, and pointers to C functions implementing standard operations like `tp_new`, `tp_call`, `tp_repr`).
B) The type of a file.
C) The keyboard output.
D) The variable name.

**Answer: A**

**Explanation:**
Writing a C extension type involves filling out this struct.

---

**Q31.45: Intermediate - [Immutability Internal]**

Why are tuples immutable?

A) To allow them to be hashable (and thus dictionary keys) and to allow optimization (storing in fixed-size memory blocks without over-allocation).
B) To be annoying.
C) To save disk space.
D) They are mutable.

**Answer: A**

**Explanation:**
`tuple` is leaner than `list`.

---

**Q31.46: Basic - [Dir function]**

`dir(obj)` generally inspects:

A) The object's `__dict__` and its class's (and bases') `__dict__` to list valid attributes.
B) The directory on disk.
C) The documentation.
D) The type.

**Answer: A**

**Explanation:**
Does not show everything (can be customized via `__dir__`).

---

**Q31.47: Advanced - [Compare Opcode]**

The opcode `COMPARE_OP` (e.g., `a < b`):

A) Calls the rich comparison function `PyObject_RichCompare` (which in turn invokes `__lt__`, `__gt__`, etc.).
B) Compares memory addresses.
C) Subtracts values.
D) Errors.

**Answer: A**

**Explanation:**
Handling the 6 comparison operators (<, <=, ==, !=, >, >=).

---

**Q31.48: Expert - [Arena]**

In pymalloc, an "Arena" is:

A) A large chunk of memory (e.g., 256KB) allocated from the OS via `mmap`, which is then carved up into Pools.
B) A fighting ring.
C) A small object.
D) A list.

**Answer: A**

**Explanation:**
The highest level of the memory hierarchy. Arenas can be returned to the OS if empty.

---

**Q31.49: Intermediate - [Bound Method]**

A "Bound Method" is an object that wraps:

A) A function and an instance (self), so when called, it automatically passes the instance as the first argument.
B) A class.
C) A static method.
D) A lambda.

**Answer: A**

**Explanation:**
`instance.method` vs `Class.method`.

---

**Q31.50: Basic - [Import mechanism]**

When you `import foo`, Python first checks:

A) `sys.modules` to see if it's already loaded.
B) The current directory only.
C) The internet.
D) `pip`.

**Answer: A**

**Explanation:**
The import system is complex (`sys.meta_path`, `sys.path_hooks`), but caching is step 1.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
