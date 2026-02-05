# Chapter 1: Python Basics & Environment

> **Topics Covered**: Python installation, versions, interpreters (CPython, PyPy, Jython, IronPython), virtual environments (venv, virtualenv, conda), package managers (pip, poetry, uv), Python execution models, bytecode, PVM, PYTHONPATH, sys.path manipulation, startup files, site-packages customization

---

## Questions

---

**Q1.1: Basic - [Python Versions]**

Which statement about Python 2 and Python 3 is correct?

A) Python 2 and Python 3 are fully backward compatible
B) Python 2 reached end-of-life on January 1, 2020
C) Python 3 was released before Python 2
D) Python 2 uses `print()` as a function by default

**Answer: B**

**Explanation:**
Python 2 officially reached end-of-life on January 1, 2020, meaning no more security patches or updates. Python 3 introduced breaking changes, so they are NOT backward compatible. Python 3 was released in 2008, after Python 2. In Python 2, `print` was a statement, not a function (though `from __future__ import print_function` could enable function syntax).

---

**Q1.2: Basic - [Interpreters]**

What is CPython?

A) A Python interpreter written in C++
B) The reference implementation of Python written in C
C) A Python-to-C compiler
D) A C library for embedding Python

**Answer: B**

**Explanation:**
CPython is the reference (default) implementation of Python, written in C. When you download Python from python.org, you get CPython. It compiles Python source code to bytecode and executes it on the Python Virtual Machine (PVM). It's not a compiler that converts Python to C, nor is it written in C++.

---

**Q1.3: Basic - [Interpreters]**

Which Python implementation is designed for high-performance execution using JIT compilation?

A) CPython
B) Jython
C) PyPy
D) IronPython

**Answer: C**

**Explanation:**
PyPy uses Just-In-Time (JIT) compilation to achieve significantly faster execution than CPython for many workloads. Jython runs on the JVM (Java Virtual Machine). IronPython runs on .NET. CPython is the reference implementation using interpretation of bytecode.

---

**Q1.4: Basic - [Interpreters]**

Jython allows Python code to:

A) Compile to native machine code
B) Run on the Java Virtual Machine and use Java libraries
C) Execute faster than any other implementation
D) Run without any interpreter

**Answer: B**

**Explanation:**
Jython is a Python implementation that runs on the Java Virtual Machine (JVM). It allows seamless integration with Java libraries and can import Java classes directly. It doesn't compile to native code and isn't necessarily faster than other implementations.

---

**Q1.5: Intermediate - [Interpreters]**

Which Python implementation would you choose to integrate Python with .NET libraries?

A) CPython
B) PyPy
C) Jython
D) IronPython

**Answer: D**

**Explanation:**
IronPython is designed to run on the .NET framework and allows direct integration with .NET libraries. Jython is for Java integration. CPython and PyPy are general-purpose implementations without built-in .NET integration (though CPython can use libraries like `pythonnet`).

---

**Q1.6: Basic - [Virtual Environments]**

What is the primary purpose of a Python virtual environment?

A) To make Python run faster
B) To isolate project dependencies from the system Python
C) To encrypt Python code
D) To convert Python 2 code to Python 3

**Answer: B**

**Explanation:**
Virtual environments create isolated Python environments with their own installed packages, preventing dependency conflicts between projects. Project A might need Django 3.2 while Project B needs Django 4.0 — virtual environments solve this. They don't affect execution speed, encryption, or version conversion.

---

**Q1.7: Basic - [Virtual Environments]**

Which command creates a virtual environment using Python's built-in `venv` module?

A) `python -m virtualenv myenv`
B) `python -m venv myenv`
C) `pip install venv myenv`
D) `python create venv myenv`

**Answer: B**

**Explanation:**
The correct syntax is `python -m venv myenv`, which uses the built-in `venv` module (available since Python 3.3). `virtualenv` is a third-party tool with slightly different syntax. `pip install venv` is incorrect because `venv` is built-in, not a pip package.

---

**Q1.8: Intermediate - [Virtual Environments]**

After creating a virtual environment on Windows, which command activates it?

A) `source myenv/bin/activate`
B) `myenv\Scripts\activate`
C) `activate myenv`
D) `python activate myenv`

**Answer: B**

**Explanation:**
On Windows, virtual environments are activated with `myenv\Scripts\activate`. The `source myenv/bin/activate` syntax is for Unix-like systems (Linux, macOS). There's no standalone `activate` command — you must specify the path to the activation script.

---

**Q1.9: Intermediate - [Virtual Environments]**

What is the key difference between `venv` and `virtualenv`?

A) `venv` is faster than `virtualenv`
B) `venv` is built into Python 3.3+, while `virtualenv` is a third-party package
C) `virtualenv` cannot create Python 3 environments
D) `venv` supports conda environments

**Answer: B**

**Explanation:**
`venv` is a built-in module since Python 3.3, requiring no additional installation. `virtualenv` is a third-party package with more features (like supporting Python 2 and creating environments with different Python versions). Both can create Python 3 environments. Neither is related to conda.

---

**Q1.10: Intermediate - [Virtual Environments, Conda]**

How does conda differ from pip + venv?

A) conda can only manage Python packages
B) conda can manage packages from any language and handle non-Python dependencies
C) conda is faster but has fewer packages
D) conda requires root access to install packages

**Answer: B**

**Explanation:**
conda is a cross-platform package and environment manager that can handle packages from any language (Python, R, C++, etc.) and manage non-Python dependencies like system libraries. pip only manages Python packages. conda has a large ecosystem through conda-forge. It doesn't require root access.

---

**Q1.11: Basic - [Package Managers]**

What is the command to install a package using pip?

A) `pip get package_name`
B) `pip install package_name`
C) `pip add package_name`
D) `pip download package_name`

**Answer: B**

**Explanation:**
The correct command is `pip install package_name`. `pip download` downloads without installing. There is no `pip get` or `pip add` command. You can also use `pip install package_name==version` for specific versions.

---

**Q1.12: Intermediate - [Package Managers]**

Which file format does pip use to specify project dependencies?

A) package.json
B) requirements.txt
C) dependencies.yaml
D) install.cfg

**Answer: B**

**Explanation:**
pip traditionally uses `requirements.txt` to list dependencies. Each line contains a package name, optionally with version specifiers (e.g., `django>=4.0,<5.0`). `package.json` is for Node.js. Modern Python projects may also use `pyproject.toml`, but `requirements.txt` remains widely used.

---

**Q1.13: Intermediate - [Package Managers]**

What does `pip freeze > requirements.txt` do?

A) Stops all running pip processes
B) Outputs installed packages with versions to requirements.txt
C) Installs packages from requirements.txt
D) Removes all installed packages

**Answer: B**

**Explanation:**
`pip freeze` outputs all installed packages with their exact versions in a format suitable for `requirements.txt`. The `>` redirects this output to the file. This is useful for creating reproducible environments. To install from this file, use `pip install -r requirements.txt`.

---

**Q1.14: Advanced - [Package Managers, Poetry]**

What advantage does Poetry provide over pip + requirements.txt?

A) Poetry is faster at downloading packages
B) Poetry provides dependency resolution, virtual environment management, and build tools in one package
C) Poetry only works with Python 2
D) Poetry automatically fixes bugs in packages

**Answer: B**

**Explanation:**
Poetry is a modern dependency management tool that combines dependency resolution, lock files (for reproducible builds), virtual environment management, and package building/publishing. It uses `pyproject.toml` and `poetry.lock` files. It works with Python 3 only and handles complex dependency graphs better than pip.

---

**Q1.15: Advanced - [Package Managers, uv]**

What is `uv` in the Python ecosystem?

A) A Python interpreter replacement
B) An extremely fast Python package installer and resolver written in Rust
C) A virtual machine for Python
D) A Unicode validation library

**Answer: B**

**Explanation:**
`uv` is a modern, extremely fast Python package installer and dependency resolver written in Rust. It's designed as a drop-in replacement for pip and pip-tools, offering 10-100x faster package installation. It was created by the Astral team (also behind Ruff linter).

---

**Q1.16: Basic - [Execution Model]**

What happens when you run `python script.py`?

A) The script is directly executed as machine code
B) The script is compiled to bytecode, then executed by the Python Virtual Machine
C) The script is converted to C and then compiled
D) The script is sent to a server for execution

**Answer: B**

**Explanation:**
Python is an interpreted language with a compilation step. When you run a script, Python first compiles it to bytecode (platform-independent intermediate code), then the Python Virtual Machine (PVM) executes this bytecode. This is different from compiled languages (direct to machine code) or pure interpreters (no bytecode step).

---

**Q1.17: Intermediate - [Bytecode]**

What file extension does Python use for cached bytecode files?

A) .pyc
B) .pyo
C) .pyd
D) .pyb

**Answer: A**

**Explanation:**
Python stores compiled bytecode in `.pyc` files (located in `__pycache__` directories since Python 3). `.pyo` was used in older Python versions for optimized bytecode but is now deprecated. `.pyd` is used for Python extension modules on Windows. There is no `.pyb` extension.

---

**Q1.18: Intermediate - [Bytecode, __pycache__]**

Where does Python 3 store bytecode cache files by default?

A) In the same directory as the source file with .pyc extension
B) In a `__pycache__` subdirectory with version-specific filenames
C) In the system's temp directory
D) In the Python installation directory

**Answer: B**

**Explanation:**
Python 3 stores bytecode in `__pycache__` directories with filenames like `module.cpython-310.pyc` (indicating Python 3.10 on CPython). This prevents conflicts between different Python versions and keeps source directories cleaner. Python 2 stored `.pyc` files alongside source files.

---

**Q1.19: Intermediate - [PVM]**

What is the Python Virtual Machine (PVM)?

A) A hardware device for running Python
B) The runtime engine that executes Python bytecode
C) A cloud service for Python execution
D) A tool for creating virtual environments

**Answer: B**

**Explanation:**
The PVM is the runtime engine (part of the Python interpreter) that executes bytecode. It's a stack-based virtual machine that reads bytecode instructions and performs the corresponding operations. It's not a separate program you install — it's part of the Python interpreter itself.

---

**Q1.20: Advanced - [Bytecode, dis module]**

What does the `dis` module do?

A) Disables Python optimization
B) Disassembles Python bytecode for inspection
C) Distributes Python packages
D) Disconnects from remote debugging

**Answer: B**

**Explanation:**
The `dis` module is a bytecode disassembler. It converts compiled bytecode back into a human-readable format showing the individual bytecode instructions. This is useful for understanding Python's internal execution, debugging, and optimization. Example: `dis.dis(some_function)`.

---

**Q1.21: Advanced - [Bytecode]**

```python
import dis
def add(a, b):
    return a + b
dis.dis(add)
```

What type of output does this produce?

A) The source code of the function
B) Bytecode instructions like LOAD_FAST, BINARY_ADD, RETURN_VALUE
C) Machine code assembly
D) An error because functions cannot be disassembled

**Answer: B**

**Explanation:**
`dis.dis()` shows bytecode instructions. For this function, you'd see something like:
```
LOAD_FAST    0 (a)
LOAD_FAST    1 (b)
BINARY_ADD
RETURN_VALUE
```
These are the stack-based operations the PVM executes. It's not source code, machine code, or an error.

---

**Q1.22: Basic - [PYTHONPATH]**

What is `PYTHONPATH`?

A) The installation directory of Python
B) An environment variable that adds directories to Python's module search path
C) The path to the Python executable
D) A configuration file for Python settings

**Answer: B**

**Explanation:**
`PYTHONPATH` is an environment variable containing a list of directories. Python adds these directories to `sys.path`, allowing modules in these directories to be imported. It's not the installation directory (that might be added separately) or the executable path (that's `PATH`).

---

**Q1.23: Intermediate - [sys.path]**

What is the order of directories Python searches when importing a module?

A) PYTHONPATH, built-in modules, current directory, site-packages
B) Built-in modules, current directory (or script's directory), PYTHONPATH, site-packages
C) site-packages, PYTHONPATH, current directory, built-in modules
D) Current directory, site-packages, PYTHONPATH, built-in modules

**Answer: B**

**Explanation:**
Python's import search order is:
1. Built-in modules (like `sys`, `os`)
2. Current directory or the directory containing the script
3. Directories in `PYTHONPATH`
4. Installation-dependent defaults (including `site-packages`)

This can be viewed with `import sys; print(sys.path)`.

---

**Q1.24: Intermediate - [sys.path]**

How can you programmatically add a directory to Python's import path at runtime?

A) `os.path.add('/new/path')`
B) `sys.path.append('/new/path')`
C) `import.path.add('/new/path')`
D) `python.path.append('/new/path')`

**Answer: B**

**Explanation:**
`sys.path` is a list of strings that Python searches for modules. You can modify it at runtime with standard list methods: `sys.path.append('/new/path')` or `sys.path.insert(0, '/new/path')` to add at the beginning. Changes affect subsequent imports in that session only.

---

**Q1.25: Advanced - [sys.path, .pth files]**

What is the purpose of `.pth` files in site-packages?

A) They contain Python bytecode
B) They contain paths that are automatically added to sys.path
C) They encrypt Python modules
D) They define package dependencies

**Answer: B**

**Explanation:**
`.pth` (path configuration) files in site-packages contain paths (one per line) that Python automatically adds to `sys.path` at startup. This is how some packages (like development installs) add themselves to the import path without modifying `PYTHONPATH`. They can also contain Python code that runs at startup if prefixed with `import`.

---

**Q1.26: Expert - [Startup Files, PYTHONSTARTUP]**

What is the `PYTHONSTARTUP` environment variable used for?

A) Defining which Python version to use
B) Specifying a script that runs before the interactive interpreter starts
C) Setting the startup timeout for Python scripts
D) Configuring the Python installer

**Answer: B**

**Explanation:**
`PYTHONSTARTUP` points to a Python file that executes automatically when you start the interactive interpreter (not when running scripts). It's commonly used to set up convenience imports, configure readline history, or define helper functions for interactive sessions.

---

**Q1.27: Expert - [site module]**

What does `python -S` do?

A) Runs Python in safe mode
B) Skips importing the site module at startup
C) Starts Python in server mode
D) Enables strict mode

**Answer: B**

**Explanation:**
The `-S` flag prevents Python from importing the `site` module at startup. The `site` module normally adds site-packages to `sys.path` and processes `.pth` files. Using `-S` results in a minimal `sys.path`, useful for debugging import issues or creating minimal environments.

---

**Q1.28: Intermediate - [Python Versions]**

Which Python version introduced f-strings (formatted string literals)?

A) Python 3.4
B) Python 3.5
C) Python 3.6
D) Python 3.7

**Answer: C**

**Explanation:**
F-strings (f"Hello, {name}!") were introduced in Python 3.6 (PEP 498). They provide a concise and readable way to embed expressions inside string literals. Python 3.5 introduced type hints, 3.7 introduced dataclasses, and 3.4 introduced `asyncio`.

---

**Q1.29: Intermediate - [Python Versions]**

🐍 Which Python version introduced the match-case (pattern matching) statement?

A) Python 3.8
B) Python 3.9
C) Python 3.10
D) Python 3.11

**Answer: C**

**Explanation:**
Pattern matching with `match-case` (PEP 634-636) was introduced in Python 3.10. It provides structural pattern matching similar to switch statements in other languages but with powerful destructuring capabilities. Python 3.8 introduced the walrus operator, 3.9 introduced dict union operators.

---

**Q1.30: Basic - [Execution]**

What is the correct shebang line for a Python 3 script on Unix-like systems?

A) `#!/python3`
B) `#!/usr/bin/env python3`
C) `#!python3`
D) `//usr/bin/python3`

**Answer: B**

**Explanation:**
`#!/usr/bin/env python3` is the preferred shebang. Using `env` searches the PATH for Python, making the script more portable across different systems where Python might be installed in different locations. The shebang must start with `#!` (not `//`), and needs a complete path or `env` command.

---

**Q1.31: Intermediate - [Execution Modes]**

What is the difference between running `python script.py` and `python -m module_name`?

A) No difference, they are identical
B) `-m` runs a module as a script and properly sets `__package__`
C) `-m` is faster
D) `-m` can only run built-in modules

**Answer: B**

**Explanation:**
`python -m module_name` runs a module as a script while properly setting `__package__` and handling relative imports correctly. It searches `sys.path` for the module. This is important for packages with `__main__.py`. Running `python script.py` uses the file path directly and may not handle package context properly.

---

**Q1.32: Advanced - [__main__.py]**

What is the purpose of `__main__.py` in a package?

A) It contains the main class of the package
B) It defines what happens when the package is run with `python -m package`
C) It must contain the word "main" in its content
D) It's required for all packages

**Answer: B**

**Explanation:**
`__main__.py` allows a package to be executed as a script using `python -m package_name`. The code in `__main__.py` runs when the package is invoked this way. It's optional — only needed if you want your package to be runnable. It doesn't need to contain "main" in its actual code.

---

**Q1.33: Intermediate - [__name__]**

What is the value of `__name__` when a Python file is run directly?

A) The filename
B) `"__main__"`
C) `"__name__"`
D) `None`

**Answer: B**

**Explanation:**
When a Python file is executed directly (`python script.py`), `__name__` is set to `"__main__"`. When the same file is imported as a module, `__name__` is set to the module name. This allows the common pattern: `if __name__ == "__main__":` to run code only when executed directly.

---

**Q1.34: Basic - [Interactive Mode]**

How do you start Python in interactive mode?

A) `python --interactive`
B) `python -i` or just `python` with no arguments
C) `python --shell`
D) `python -r`

**Answer: B**

**Explanation:**
Running `python` without arguments starts the interactive interpreter (REPL). The `-i` flag forces interactive mode even after running a script (`python -i script.py`), which is useful for debugging. There's no `--interactive`, `--shell`, or `-r` flag for this purpose.

---

**Q1.35: Intermediate - [pip]**

What does `pip install -e .` do?

A) Installs packages from the current directory in editable mode
B) Installs all packages ending with 'e'
C) Exports the current environment
D) Installs packages with elevated privileges

**Answer: A**

**Explanation:**
`pip install -e .` (editable install, aka development mode) installs the package in the current directory in a way that changes to the source code are immediately reflected without reinstalling. It creates a `.egg-link` file in site-packages pointing to your source directory. Essential for package development.

---

**Q1.36: Advanced - [pip, wheel]**

What is a wheel file in Python packaging?

A) A circular dependency detector
B) A built distribution format (.whl) that installs faster than source distributions
C) A GUI tool for package management
D) A testing framework

**Answer: B**

**Explanation:**
Wheel (`.whl`) is a built package format (PEP 427) that installs much faster than source distributions because it doesn't require a build step. Wheels contain pre-compiled bytecode and any platform-specific binaries. Installing from wheel: just unzip and copy. Installing from source: may need to compile C extensions.

---

**Q1.37: Intermediate - [Virtual Environments]**

What files/directories does `venv` create in a virtual environment?

A) Only a `lib` folder
B) `Scripts` (Windows) or `bin` (Unix), `lib`, `include`, and `pyvenv.cfg`
C) Only `requirements.txt`
D) A copy of the entire Python installation

**Answer: B**

**Explanation:**
A virtual environment contains:
- `Scripts/` (Windows) or `bin/` (Unix): activation scripts and Python executable
- `lib/`: installed packages
- `include/`: C header files
- `pyvenv.cfg`: configuration file pointing to base Python

It uses symlinks or copies of essential files, not the entire Python installation.

---

**Q1.38: Advanced - [site-packages]**

What is the difference between user site-packages and system site-packages?

A) There is no difference
B) User site-packages is writable without admin rights and per-user; system site-packages is shared
C) User site-packages is faster
D) System site-packages is deprecated

**Answer: B**

**Explanation:**
User site-packages (`~/.local/lib/python3.x/site-packages` on Unix, `%APPDATA%\Python` on Windows) allows installing packages without admin rights. System site-packages requires elevated privileges and affects all users. `pip install --user package` installs to user site-packages. Check locations with `python -m site`.

---

**Q1.39: Expert - [Import Hooks]**

What are import hooks in Python?

A) Error messages during import
B) Custom finders and loaders that extend Python's import system
C) Keyboard shortcuts for importing
D) Tools for importing legacy code

**Answer: B**

**Explanation:**
Import hooks (PEP 302) allow customizing how Python finds and loads modules. You can create custom finders (added to `sys.meta_path` or `sys.path_hooks`) that locate modules in custom ways, and loaders that load them. Used for importing from databases, encrypted files, or remote sources.

---

**Q1.40: Expert - [importlib]**

How can you programmatically import a module by name string?

A) `eval("import " + module_name)`
B) `importlib.import_module(module_name)`
C) `import(module_name)`
D) `__import__(module_name)` only

**Answer: B**

**Explanation:**
`importlib.import_module(module_name)` is the recommended way to dynamically import modules. While `__import__()` works, it's lower-level and returns the top-level package for dotted names. `eval("import ...")` works but is a security risk and bad practice. There's no `import()` function.

---

**Q1.41: Intermediate - [pip]**

What does `pip install package[extra]` syntax do?

A) Installs an extra version of the package
B) Installs the package with optional dependencies specified by the extra
C) Downloads extra documentation
D) Installs the package with debugging symbols

**Answer: B**

**Explanation:**
Extras are optional dependency groups defined by package authors. `pip install requests[security]` installs `requests` plus its security-related optional dependencies (like `cryptography`). This allows packages to have optional features without requiring all dependencies for every user.

---

**Q1.42: Advanced - [pyproject.toml]**

What is `pyproject.toml` used for?

A) Configuring the Python interpreter
B) Defining project metadata, dependencies, and build system configuration
C) Storing Python bytecode
D) Configuring the operating system for Python

**Answer: B**

**Explanation:**
`pyproject.toml` (PEP 517, 518, 621) is the modern standard for Python project configuration. It defines project metadata (name, version, dependencies), build system requirements, and tool configurations (for pytest, black, mypy, etc.). It's replacing `setup.py`, `setup.cfg`, and per-tool config files.

---

**Q1.43: Basic - [help()]**

What does `help(object)` display in the Python interpreter?

A) The source code of the object
B) Documentation and usage information about the object
C) The memory address of the object
D) A list of all Python objects

**Answer: B**

**Explanation:**
`help(object)` displays the docstring and documentation for any object (module, function, class, etc.). It uses the built-in pydoc module to format the help text nicely. For functions, it shows parameters, docstrings, and method resolution order for classes.

---

**Q1.44: Intermediate - [dir()]**

What does `dir(object)` return?

A) The directory containing the object
B) A list of valid attributes and methods of the object
C) The object's documentation
D) The object's memory size

**Answer: B**

**Explanation:**
`dir(object)` returns a sorted list of names (strings) comprising the attributes, methods, and other names defined for that object. Without arguments, `dir()` lists names in the current scope. It's useful for exploration and introspection. It includes special methods like `__init__`.

---

**Q1.45: Expert - [Optimization Flags]**

What is the difference between `python -O` and `python -OO`?

A) `-O` is faster than `-OO`
B) `-O` removes assert statements; `-OO` also removes docstrings
C) `-OO` enables double optimization
D) `-O` is for output and `-OO` is for object-oriented mode

**Answer: B**

**Explanation:**
`-O` sets `__debug__` to False, removing `assert` statements and `if __debug__:` blocks. `-OO` does the same plus removes docstrings (`__doc__`), further reducing bytecode size. These optimizations produce `.opt-1.pyc` and `.opt-2.pyc` files respectively. Rarely used in practice due to limited benefits.

---

## Chapter Summary

**Total MCQs: 45**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 14 | 31% |
| Intermediate | 20 | 44% |
| Advanced | 8 | 18% |
| Expert | 3 | 7% |

**Key Topics Covered:**
- Python interpreters (CPython, PyPy, Jython, IronPython)
- Virtual environments (venv, virtualenv, conda)
- Package managers (pip, Poetry, uv)
- Python execution model and bytecode
- sys.path and PYTHONPATH
- Import system and startup configuration
