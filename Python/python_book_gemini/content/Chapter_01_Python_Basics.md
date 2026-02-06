# Chapter 1: Python Basics & Environment

**Target MCQs**: 40-50
**Current Batch**: 1-25
**Topics Covered**: Python Versions, Interpreters, Virtual Environments, Package Managers

---

**Q1.1: Basic - [Python Versions]**

Which of the following statements about Python 2 and Python 3 is **true**?

A) Python 3 is backward compatible with Python 2.
B) Python 2.7 is still officially supported with security updates as of 2025.
C) `print` is a statement in Python 2 and a function in Python 3.
D) Integer division `/` behaves identically in both versions.

**Answer: C**

**Explanation:**
In Python 2, `print` is a statement (e.g., `print "hello"`). In Python 3, it is a function (`print("hello")`).
- A is false: Python 3 introduced breaking changes (e.g., Unicode strings).
- B is false: Python 2 reached end-of-life (EOL) on Jan 1, 2020.
- D is false: `3/2` is `1` in Python 2 (floor division for ints) but `1.5` in Python 3.

---

**Q1.2: Basic - [Interpreters]**

What is standard Python (the reference implementation) specifically called?

A) PyPy
B) CPython
C) Jython
D) Cython

**Answer: B**

**Explanation:**
**CPython** is the reference implementation of Python, written in C. It is what you get when you download Python from python.org.
- **PyPy** is a fast, JIT-compiled implementation.
- **Jython** runs on the Java Virtual Machine.
- **Cython** is a superset of Python for writing C extensions, not strictly an interpreter.

---

**Q1.3: Intermediate - [Execution Model]**

When you run a Python script `script.py`, what is the intermediate step before execution by the PVM (Python Virtual Machine)?

A) It is compiled to machine code.
B) It is compiled to bytecode (`.pyc`).
C) It is transpiled to C.
D) It is interpreted line-by-line directly from source.

**Answer: B**

**Explanation:**
Python compiles source code (`.py`) into **bytecode** (platform-independent instructions), often cached as `.pyc` files in `__pycache__`. The PVM then executes this bytecode. Python is not purely interpreted from source, nor is it compiled to native machine code (unlike C++ or Go).

---

**Q1.4: Intermediate - [Virtual Environments]**

Which command creates a lightweight virtual environment using the standard library module in Python 3?

A) `pip install venv`
B) `python -m venv myenv`
C) `virtualenv myenv`
D) `conda create -n myenv`

**Answer: B**

**Explanation:**
`python -m venv myenv` uses the built-in `venv` module (available since Python 3.3).
- `virtualenv` is a third-party tool (pre-dated `venv`).
- `conda` is a separate package/environment manager (Anaconda/Miniconda).
- `pip` is for installing packages, not creating environments.

---

**Q1.5: Advanced - [Package Managers]**

What is the primary difference between `pip` and `poetry` regarding dependency resolution?

A) `pip` does not support installing from git repositories.
B) `poetry` uses a strict deterministic lock file (`poetry.lock`) and resolves dependency conflicts automatically, whereas older `pip` versions could install conflicting dependencies.
C) `pip` only installs binary wheels, while `poetry` only builds from source.
D) `poetry` is built into Python, whereas `pip` requires separate installation.

**Answer: B**

**Explanation:**
`poetry` (and `pipenv`/`uv`) emphasizes deterministic builds using a lock file and a robust dependency resolver. While modern `pip` has a resolver, tools like Poetry provide an entire workflow for project management, packaging, and strict locking suitable for reproducible builds.

---

**Q1.6: Basic - [Python Shell]**

What is the special variable `_` (underscore) used for in the interactive Python shell?

A) It stores the result of the last evaluated expression.
B) It represents the current loop index.
C) It is a placeholder for ignored exceptions.
D) It has no special meaning in the shell.

**Answer: A**

**Explanation:**
In the interactive REPL, `_` holds the result of the last non-None expression.
Example:
```python
>>> 1 + 1
2
>>> _ + 5
7
```
Note: In scripts, `_` is often used by convention for "ignored variable" (e.g., `for _ in range(5)`), but the shell behavior is a specific feature.

---

**Q1.7: Intermediate - [Imports]**

If you have a file named `math.py` in your current directory and you run `import math`, what happens?

A) Python imports the standard library `math` module.
B) Python imports your local `math.py`, potentially breaking code that relies on the standard library.
C) Python raises an `ImportError`.
D) Python merges both modules.

**Answer: B**

**Explanation:**
This is a common pitfall called **Variable Shadowing/Module Shadowing**. Python looks in the current directory (part of `sys.path`) *before* the standard library paths. Your local `math.py` shadows the standard `math`, causing `AttributeError` if your code expects standard math functions.

---

**Q1.8: Advanced - [GIL]**

Which of the following operations is **thread-safe** in CPython due to the Global Interpreter Lock (GIL)?

A) `n += 1` (where n is an integer)
B) `list.append(item)`
C) `x = x + 1`
D) `dict[key] += 1`

**Answer: B**

**Explanation:**
Operations that map to a single bytecode instruction are generally atomic and thread-safe in CPython. `list.append()` is a single atomic operation.
- `n += 1` involves loading, adding, and storing (3 opcodes), so a thread switch can occur in between, leading to race conditions.

---

**Q1.9: Expert - [Startup Files]**

Which environment variable can be set to a file path that Python executes on startup of an interactive session?

A) `PYTHONSTARTUP`
B) `PYTHONINIT`
C) `PYTHONPATH`
D) `PYTHONHOME`

**Answer: A**

**Explanation:**
`PYTHONSTARTUP` can point to a Python file (e.g., `.pythonrc.py`) that is executed before the interactive reference moves into the prompt. This is useful for importing standard modules (like `os` or `math`) or setting up auto-completion every time you launch the shell.

---

**Q1.10: Basic - [Indentation]**

Which error does Python raise if you mix tabs and spaces for indentation in Python 3?

A) `SyntaxError`
B) `IndentationError`
C) `TabError`
D) It runs fine but warns.

**Answer: C**

**Explanation:**
Python 3 explicitly forbids mixing tabs and spaces for indentation within the same block, raising a `TabError` (a subclass of `IndentationError`). Python 2 was more permissive (but it was bad practice).

---

**Q1.11: Intermediate - [Comparison]**

What is the output of `3 < 4 < 5`?

A) `True`
B) `False`
C) `5`
D) `SyntaxError`

**Answer: A**

**Explanation:**
Python supports **chained comparisons**. `3 < 4 < 5` is evaluated as `(3 < 4) and (4 < 5)`. Both are true, so the result is `True`.

---

**Q1.12: Advanced - [Interning]**

Consider the following code in CPython:
```python
a = 256
b = 256
print(a is b)

x = 257
y = 257
print(x is y)
```
What is the output?

A) True, True
B) False, False
C) True, False
D) False, True

**Answer: C**

**Explanation:**
CPython employs **Small Integer Caching** for integers in the range `[-5, 256]`. Objects in this range are singletons.
- `a` and `b` (256) point to the same object -> `True`.
- `x` and `y` (257) are typically created as new separate objects -> `False`.
*Note: In compiler-optimized contexts (like passing an entire file to the interpreter), 257 might also be cached/reused, but in a standard REPL, this behavior holds.*

---

**Q1.13: Intermediate - [Operators]**

What is the result of `-5 // 2`?

A) `-2`
B) `-3`
C) `-2.5`
D) `2`

**Answer: B**

**Explanation:**
Floor division `//` rounds result down towards negative infinity. `-2.5` rounded down is `-3`.

---

**Q1.14: Basic - [Variables]**

Which of the following is an invalid variable name?

A) `_my_var`
B) `myVar2`
C) `2myVar`
D) `my_var`

**Answer: C**

**Explanation:**
Variable names cannot start with a digit. They must start with a letter (a-z, A-Z) or an underscore.

---

**Q1.15: Advanced - [Bytecode]**

Which module can be used to disassemble Python code to view its bytecode instructions?

A) `inspect`
B) `dis`
C) `sys`
D) `gc`

**Answer: B**

**Explanation:**
The `dis` module (Disassembler) converts compiled Python bytecode into a human-readable format.
Example: `dis.dis(my_func)` shows the opcodes (LOAD_CONST, BINARY_ADD, etc.).

---

**Q1.16: Intermediate - [Mutability]**

Which of the following types is **immutable**?

A) `list`
B) `set`
C) `tuple`
D) `dict`

**Answer: C**

**Explanation:**
`tuple` is immutable. Once created, its elements cannot be changed. `list`, `set`, and `dict` are mutable. `str`, `int`, `float`, `frozenset` are other immutable types.

---

**Q1.17: Expert - [CPython Optimizations]**

What is "Peephole Optimization" in Python?

A) Optimizing loops by unrolling them.
B) Optimizing small snippets of bytecode during compilation (e.g., constant folding).
C) Removing unused variables.
D) Converting Python directly to C code.

**Answer: B**

**Explanation:**
Peephole optimization acts on the bytecode. It performs simple transformations like **Constant Folding** (evaluating `2 + 3` to `5` at compile time) to improve performance without changing the program's logic.

---

**Q1.18: Intermediate - [Comments]**

How do you create a function documentation string (docstring)?

A) Using `#` at the start of the function.
B) Placing a string literal as the first statement in the function body.
C) Using the `@doc` decorator.
D) Using `//` comments.

**Answer: B**

**Explanation:**
A docstring is a string literal (usually triple-quoted `"""..."""`) that appears as the very first statement in a module, function, class, or method definition. It is accessible via the `__doc__` attribute.

---

**Q1.19: Advanced - [Command Line Arguments]**

In a script `app.py` run via `python app.py arg1`, what is the value of `sys.argv[0]`?

A) `arg1`
B) `python`
C) `app.py`
D) The path to the Python interpreter.

**Answer: C**

**Explanation:**
`sys.argv` is the list of command-line arguments. `sys.argv[0]` is always the name of the script being executed (or an empty string context dependent). The actual user arguments start at `sys.argv[1]`.

---

**Q1.20: Intermediate - [NoneType]**

What is the type of `None`?

A) `null`
B) `int` (0)
C) `False`
D) `NoneType`

**Answer: D**

**Explanation:**
`None` is the sole instance of the `NoneType` class. It represents the absence of a value. It is not 0 or False (though it is falsy).

---

**Q1.21: Basic - [Boolean]**

Which of these values is considered `True` in a boolean context?

A) `[]` (empty list)
B) `0`
C) `"False"` (string)
D) `None`

**Answer: C**

**Explanation:**
Non-empty strings are truthy.
- Empty containers (`[]`, `{}`, `""`, `()`) are falsy.
- Zero (`0`, `0.0`) is falsy.
- `None` is falsy.
The string `"False"` is not empty, so it is `True`.

---

**Q1.22: Advanced - [Type Hinting]**

As of Python 3.5+, how do you annotate a function `add` that takes two integers and returns an integer?

A) `def add(x: int, y: int) -> int:`
B) `def add(int x, int y) returns int:`
C) `def add(x, y) :: int:`
D) `def add(x, y): # type: (int, int) -> int`

**Answer: A**

**Explanation:**
Option A shows standard library syntax for type hints. Option D is an older comment-based syntax used for Python 2 compatibility. Python ignores these hints at runtime; they are for static analysis tools like `mypy`.

---

**Q1.23: Expert - [Memory]**

What does `sys.getrefcount(x)` return?

A) The memory address of x.
B) The size of x in bytes.
C) The number of references to object x.
D) The number of garbage collection cycles x has survived.

**Answer: C**

**Explanation:**
`sys.getrefcount(x)` returns the reference count of the object `x`. Note that the count returned is generally one higher than you might expect because the function call itself (`getrefcount(x)`) creates a temporary reference to `x`.

---

**Q1.24: Intermediate - [Keywords]**

Which of the following is **not** a Python keyword?

A) `pass`
B) `assert`
C) `switch`
D) `yield`

**Answer: C**

**Explanation:**
Python (until 3.10) did not have a `switch` or `match` statement. 3.10 introduced `match` and `case` as "soft keywords". `switch` is not a keyword in Python.

---

**Q1.25: Basic - [Operators]**

What does the `**` operator do?

A) Bitwise XOR
B) Modulo
C) Exponentiation
D) Floor Division

**Answer: C**

**Explanation:**
`**` is the power operator. `2 ** 3` is 8. `^` is bitwise XOR. `%` is modulo. `//` is floor division.

---

**Q1.26: Intermediate - [Sys Path]**

When Python starts, how is `sys.path` initialized?

A) Only with the directories in the `PYTHONPATH` environment variable.
B) With the current directory, `PYTHONPATH`, and standard library paths.
C) Only with the standard library paths.
D) It is empty until specifically configured.

**Answer: B**

**Explanation:**
`sys.path` is initialized with:
1. The directory containing the input script (or current directory).
2. `PYTHONPATH` (if set).
3. The installation-dependent default strings (standard library).

---

**Q1.27: Advanced - [Path Config files]**

What is the purpose of files ending in `.pth` in the `site-packages` directory?

A) They are backup files.
B) They store Python configuration settings.
C) They add additional directories to `sys.path`.
D) They are C extension headers.

**Answer: C**

**Explanation:**
A path configuration file (`.pth`) is a file containing additional paths (one per line) to be added to `sys.path`. This is a common mechanism used by setuptools and other tools to manage namespaces or editable installs.

---

**Q1.28: Expert - [Site Customization]**

Which module names does Python attempt to import during initialization to allow for site-specific customization?

A) `siteconfig` and `userconfig`
B) `sitecustomize` and `usercustomize`
C) `pythonrc` and `startupscript`
D) It does not import any modules automatically.

**Answer: B**

**Explanation:**
The `site` module (imported automatically at startup) attempts to import `sitecustomize`, and if that is successful (or fails), it attempts to import `usercustomize` (if enabled). These allow arbitrary code execution during Python startup for customization.

---

**Q1.29: Intermediate - [Bytecode Compilation]**

Which tool is used to recursively compile all Python source files in a directory hierarchy to bytecode?

A) `python -m compile`
B) `python -m py_compile`
C) `python -m compileall`
D) `python -O`

**Answer: C**

**Explanation:**
`compileall` is a standard library module that forces the compilation of all `.py` files in a directory tree to `.pyc` files. `py_compile` compiles a single file.

---

**Q1.30: Advanced - [Optimization Flags]**

What is the effect of running Python with the `-O` flag (e.g., `python -O script.py`)?

A) It enables JIT compilation.
B) It removes `assert` statements and sets `__debug__` to False.
C) It removes docstrings.
D) It performs aggressive loop unrolling.

**Answer: B**

**Explanation:**
The `-O` (Optimize) flag generates bytecode where `assert` statements are stripped out, and the built-in constant `__debug__` is set to `False`. It does not perform complex optimizations like JIT or loop unrolling. (Note: `-OO` removes docstrings as well).

---

**Q1.31: Advanced - [String Interning]**

Which function allows you to manually intern a string in Python 3, ensuring that two strings with the same value share the same memory address?

A) `str.intern()`
B) `sys.intern()`
C) `gc.intern()`
D) `intern()` (built-in)

**Answer: B**

**Explanation:**
In Python 3, `intern` was moved to the `sys` module (`sys.intern(string)`). In Python 2, it was a built-in function `intern()`. It is useful for optimizing dictionary lookups for strings that are dynamically created but used frequently as keys.

---

**Q1.32: Basic - [Identity]**

What does the `id()` function return?

A) A unique identifier string for the object.
B) The memory address (integer) of the object in CPython.
C) The type of the object.
D) The reference count of the object.

**Answer: B**

**Explanation:**
`id(obj)` returns an integer representing the identity of the object. In CPython, this is the memory address of the object. It is guaranteed to be unique and constant for this object during its lifetime.

---

**Q1.33: Intermediate - [Eval vs Exec]**

What is the main difference between `eval()` and `exec()`?

A) `eval()` executes declarations/statements, `exec()` evaluates expressions.
B) `eval()` returns the result of an expression, `exec()` executes code (statements) and returns `None`.
C) `exec()` is safer than `eval()`.
D) `eval()` only accepts strings, `exec()` accepts code objects.

**Answer: B**

**Explanation:**
`eval(expression)` evaluates a single expression and returns its value. `exec(code)` executes a block of code (which can contain statements like class definitions, loops, imports) and its return value is always `None`.

---

**Q1.34: Advanced - [Debug Constant]**

Can you assign a value to `__debug__` in Python code?

A) Yes, it's just a global variable.
B) No, it results in a `SyntaxError` (assignment to keyword/constant).
C) Yes, but only inside a function.
D) No, but it can be changed via `sys.flags`.

**Answer: B**

**Explanation:**
`__debug__` is a true constant in Python. You cannot assign to it. Attempts like `__debug__ = False` raise a `SyntaxError` because the compiler treats it specially to allow dead code elimination when `-O` is used.

---

**Q1.35: Expert - [Builtins]**

Where are the built-in functions like `len()`, `range()`, and `print()` actually located?

A) In the global namespace.
B) In the `sys` module.
C) In the `__builtins__` module (or `builtins` in Python 3).
D) They are keywords, not functions.

**Answer: C**

**Explanation:**
Built-in functions reside in the `builtins` module (Python 3). The interpreter exposes this module as `__builtins__` in the global namespace. When you look up a name, Python checks locals, then enclosing, then globals, and finally the `builtins` namespace.

---

**Q1.36: Advanced - [Sys Modules]**

What does the dictionary `sys.modules` contain?

A) A list of available modules on the system.
B) A cache of already imported modules, mapping module names to module objects.
C) A list of built-in modules only.
D) The dependency graph of the current script.

**Answer: B**

**Explanation:**
`sys.modules` works as a cache. When you import a module, Python first checks `sys.modules`. If present, it returns the existing object. If not, it loads it and adds it to `sys.modules`. This ensures modules are initialized only once.

---

**Q1.37: Intermediate - [Circular Imports]**

What is the most common symptom of a circular import in Python?

A) `SystemError`
B) `RecursionError`
C) `ImportError` or `AttributeError` (partially initialized module).
D) The interpreter crashes.

**Answer: C**

**Explanation:**
When module A imports B, and B imports A, if A attempts to use a name from B that hasn't been defined yet (because B is still executing and waiting on A), it generally raises an `AttributeError` or `ImportError`. The module object exists in `sys.modules` but is empty or incomplete.

---

**Q1.38: Basic - [Main Scope]**

Why is code often encapsulated in `if __name__ == "__main__":`?

A) To prevent it from running when the script is imported as a module.
B) To make it run faster.
C) It is required for the code to run at all.
D) To define the `main` function.

**Answer: A**

**Explanation:**
`__name__` is `"__main__"` when the script is run directly. If the script is imported, `__name__` is the script's filename. This block prevents execution of implementation code (like tests or start commands) when the file is merely imported to usage elsewhere.

---

**Q1.39: Basic - [Interactive Mode]**

What does the `>>>` prompt indicate?

A) Python is installing updates.
B) Python is waiting for input in interactive mode (Primary Prompt).
C) Python is executing a background task.
D) A syntax error occurred.

**Answer: B**

**Explanation:**
The `>>>` is the primary prompt in the interactive shell, indicating it is ready for a new statement. The `...` is the secondary prompt, used for continuation lines (e.g., inside a loop or function definition).

---

**Q1.40: Basic - [Command Line]**

Which command line argument allows you to pass a string of Python code to execute directly without a file?

A) `-x`
B) `-c`
C) `-e`
D) `-r`

**Answer: B**

**Explanation:**
`python -c "print('hello')"` executes the command string key passed after `-c`.

---

**Q1.41: Advanced - [Unbuffered IO]**

Why would you use `python -u` (e.g., in a Docker container)?

A) To run as a specific user.
B) To force stdin, stdout, and stderr to be unbuffered.
C) To use Unicode by default.
D) To update pip packages on start.

**Answer: B**

**Explanation:**
`python -u` forces the standard streams to be unbuffered. This is critical in environments like Docker or when piping output, ensuring that logs (`print` output) appear immediately rather than getting stuck in a buffer until the buffer fills up or the process exits.

---

**Q1.42: Basic - [PYTHONPATH]**

On Windows, what is the separator used in the `PYTHONPATH` environment variable?

A) Colon `:`
B) Semicolon `;`
C) Comma `,`
D) Space ` `

**Answer: B**

**Explanation:**
On Windows, path variables are separated by semicolons `;`. On Unix/Linux/macOS, they are separated by colons `:`.

---

**Q1.43: Expert - [Hash Randomization]**

What is the purpose of the `PYTHONHASHSEED` environment variable?

A) To set the seed for the `random` module.
B) To control the hash randomization algorithm for dictionary security.
C) To set the initial memory address for objects.
D) To encrypt `.pyc` files.

**Answer: B**

**Explanation:**
It controls the seed used for the hash function (`hash()`) of str, bytes, and datetime objects. Setting it to `random` (default) prevents Hash DoS attacks. Setting it to an integer makes the hash values deterministic, which is needed for repeatable tests involving dictionary iteration order (pre-Python 3.7) or `.pyc` generation stability.

---

**Q1.44: Intermediate - [Executable Path]**

How do you programmatically find the absolute path to the Python interpreter running the current script?

A) `os.python_path`
B) `sys.executable`
C) `platform.python`
D) `env.PYTHON_BIN`

**Answer: B**

**Explanation:**
`sys.executable` contains the absolute path to the Python interpreter binary (e.g., `/usr/bin/python3` or `C:\Python39\python.exe`).

---

**Q1.45: Basic - [Implementation]**

What function would you use to check if you are running on PyPy or CPython?

A) `sys.implementation.name` or `platform.python_implementation()`
B) `sys.version`
C) `os.name`
D) `python.type`

**Answer: A**

**Explanation:**
`platform.python_implementation()` returns a string like "CPython", "PyPy", "Jython". `sys.implementation.name` (Python 3.3+) gives metadata about the implementation.

---

**Q1.46: Basic - [Pip Commands]**

Which `pip` command outputs installed packages in a format suitable for a `requirements.txt` file?

A) `pip list`
B) `pip freeze`
C) `pip show`
D) `pip dump`

**Answer: B**

**Explanation:**
`pip freeze` outputs installed packages with exact versions (e.g., `requests==2.25.1`), which is the standard format for locking dependencies in `requirements.txt`. `pip list` shows a human-readable table.

---

**Q1.47: Intermediate - [User Site]**

What does the command `python -m site --user-site` display?

A) The location of the user-specific site-packages directory.
B) The URL of the official Python website.
C) The configuration of the current virtual environment.
D) The path to the user's home directory.

**Answer: A**

**Explanation:**
This command prints the path to the user site-packages directory (e.g., `~/.local/lib/python3.9/site-packages`), where packages installed with `pip install --user` are stored.

---

**Q1.48: Basic - [Extensions]**

What is the significance of the `.pyw` extension on Windows?

A) It indicates a Python script that should run with `pythonw.exe` (no console window).
B) It is for Python web files.
C) It is a compressed Python file.
D) It is a typo; only `.py` is valid.

**Answer: A**

**Explanation:**
`.pyw` files are associated with `pythonw.exe`, which suppresses the terminal/console window. This is used for GUI applications (like Tkinter apps) where you don't want a command prompt appearing.

---

**Q1.49: Basic - [Shebang]**

In a script on a Unix-like system, what does the first line `#!/usr/bin/env python3` do?

A) It imports the `env` module.
B) It tells the operating system's loader to use the `python3` interpreter found in the user's PATH to execute the script.
C) It is a comment ignored by everyone.
D) It sets the environment variables for Python.

**Answer: B**

**Explanation:**
This is the **shebang** line. Using `/usr/bin/env python3` is more portable than hardcoding `/usr/bin/python3` because it looks up the interpreter in the system's PATH, working correctly in virtual environments.

---

**Q1.50: Intermediate - [Exiting]**

Which function is preferred for exiting a script programmatically in production code?

A) `exit()`
B) `quit()`
C) `sys.exit()`
D) `os._exit()`

**Answer: C**

**Explanation:**
`sys.exit()` is preferred. It raises the `SystemExit` exception, which can be caught and allows cleanups (finally blocks). `exit()` and `quit()` are helper objects added by `site` for the interactive shell and might not exist in some embedded environments. `os._exit()` terminates immediately without cleanup (used in child processes after fork).

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
