# Chapter 14: Modules & Packages

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: Import system (`sys.modules`, `sys.path`), `__init__.py`, Relative imports, `__all__`, Namespace packages, `importlib`, Circular imports, Module caching.

---

**Q14.1: Basic - [Import Search Path]**

Which list contains the directories Python searches for modules?

A) `os.path`
B) `sys.path`
C) `sys.modules`
D) `env.PYTHONPATH`

**Answer: B**

**Explanation:**
`sys.path` is a list of strings that specifies the search path for modules. It is initialized from the `PYTHONPATH` environment variable and installation defaults.

---

**Q14.2: Intermediate - [Sys Modules]**

`sys.modules` is:

A) A list of installed modules.
B) A dictionary mapping module names to loaded module objects.
C) A cache of bytecode.
D) A function to load modules.

**Answer: B**

**Explanation:**
It acts as a cache for loaded modules. If a module is found here, `import` returns it immediately without reloading or re-executing.

---

**Q14.3: Advanced - [__all__ usage]**

If `__all__ = ['func']` is defined in a module, `from module import *`:

A) Imports everything.
B) Imports only `func`.
C) Raises SyntaxError.
D) Imports everything except `func`.

**Answer: B**

**Explanation:**
`__all__` restricts what identifiers are exported when the wildcard import (`import *`) is used.

---

**Q14.4: Basic - [Package Definition]**

In standard Python (pre-3.3 namespace packages), what file makes a directory a package?

A) `package.py`
B) `__main__.py`
C) `__init__.py`
D) `config.py`

**Answer: C**

**Explanation:**
The presence of `__init__.py` signals to Python that the directory contains a package.

---

**Q14.5: Intermediate - [Relative Import]**

In `package.submodule`, `from .. import sibling` imports `sibling` from:

A) The same directory.
B) The parent package directory.
C) The root directory.
D) `sys.path`.

**Answer: B**

**Explanation:**
`..` indicates the parent directive in relative imports.

---

**Q14.6: Advanced - [Executed Module Name]**

When a file is run directly (e.g., `python script.py`), its `__name__` is:

A) `'script'`
B) `'__main__'`
C) `'builtins'`
D) `None`

**Answer: B**

**Explanation:**
Python sets the global `__name__` variable to `'__main__'` for the script being executed as the main program.

---

**Q14.7: Basic - [Import As]**

`import numpy as np` does what?

A) Renames the module file on disk.
B) Loads `numpy` but binds it to the name `np` in the current namespace.
C) Creates a copy of numpy.
D) Imports a submodule named `np`.

**Answer: B**

**Explanation:**
Aliasing allows referring to the module by a shorter or different name locally.

---

**Q14.8: Intermediate - [Reloading]**

To reload a module that has already been modified on disk:

A) `import module` again.
B) `importlib.reload(module)`
C) `del sys.modules['module']`
D) `reload(module)` (builtin).

**Answer: B**

**Explanation:**
Standard `import` statements do nothing if the module is in `sys.modules`. `importlib.reload()` forces a reload. (Note: `reload` was a builtin in Python 2, moved to `importlib` (and `imp` deprecated) in Python 3).

---

**Q14.9: Advanced - [Namespace Packages]**

A namespace package (PEP 420):

A) Requires `__init__.py`.
B) Allows a package to be split across multiple directories/locations on `sys.path`.
C) Is a virtual environment.
D) Is static.

**Answer: B**

**Explanation:**
It allows portions of a package to live in different directories (e.g. installed by different `pip` packages), without requiring an `__init__.py` file.

---

**Q14.10: Expert - [RunPy]**

`runpy.run_module('pkg.mod')`:

A) Runs the module as a script (setting `__name__` to `'__main__'`) without importing it in the standard way.
B) Imports the module.
C) Is deprecated.
D) Syntax checks the module.

**Answer: A**

**Explanation:**
It executes the module code. Equivalent to `python -m pkg.mod`.

---

**Q14.11: Basic - [From Import]**

`from math import sqrt`:

A) Imports the whole `math` module and binds `math`.
B) Imports the whole `math` module (into `sys.modules`) but only binds `sqrt` in the local namespace.
C) Reads only the `sqrt` function from disk.
D) Is faster than `import math`.

**Answer: B**

**Explanation:**
The entire module is loaded and executed, but only the specific name `sqrt` is added to the current namespace. `math` itself is not bound.

---

**Q14.12: Intermediate - [__file__ attribute]**

`module.__file__` contains:

A) The source code string.
B) The path to the file from which the module was loaded.
C) The package name.
D) The default export.

**Answer: B**

**Explanation:**
It points to the location of the `.py` (or `.pyc` / `.so`) file.

---

**Q14.13: Advanced - [Circular Import]**

If module A imports B, and B imports A:

A) Python deadlocks.
B) It works if the imports are placed inside functions or if names are not accessed immediately at top-level.
C) It never works (RecursionError).
D) It creates two copies of modules.

**Answer: B**

**Explanation:**
If the import is at the top level, one module will see the other as partially initialized (potentially empty). Moving the import inside a function delays execution until both are fully initialized.

---

**Q14.14: Basic - [Dir() Module]**

`dir(module)` returns:

A) List of files in the module's folder.
B) List of names (attributes, functions, classes) defined in the module.
C) The path.
D) Documentation.

**Answer: B**

**Explanation:**
Introspection tool to see what symbols are available in the module.

---

**Q14.15: Intermediate - [ImportError vs ModuleNotFoundError]**

A) They are unrelated.
B) `ModuleNotFoundError` is a subclass of `ImportError`.
C) `ImportError` is a subclass of `ModuleNotFoundError`.
D) `ImportError` is deprecated.

**Answer: B**

**Explanation:**
Added in Python 3.6. `ModuleNotFoundError` is raised when the module isn't found. `ImportError` can be raised if the module is found but fails to load (e.g. missing dependency or bad syntax).

---

**Q14.16: Advanced - [__main__.py]**

The `__main__.py` file is executed when:

A) `import package` is called.
B) The package is executed via `python -m package`.
C) The package is installed.
D) `__init__.py` finishes.

**Answer: B**

**Explanation:**
It serves as the entry point for executable packages.

---

**Q14.17: Expert - [Meta Path Finder]**

`sys.meta_path` contains:

A) List of finder objects to locate modules *before* looking at `sys.path`.
B) Metadata about paths.
C) Strings of URL paths.
D) Cached bytecodes.

**Answer: A**

**Explanation:**
Part of the import machinery (PEP 302). Objects in `sys.meta_path` (Finders) are queried to see if they know how to handle the module.

---

**Q14.18: Intermediate - [Deleting Module]**

If you `del sys.modules['math']`:

A) It uninstalls math.
B) Formatting happens.
C) The next `import math` will reload it from disk/source.
D) It crashes.

**Answer: C**

**Explanation:**
Removing it from the cache forces the import system to look for and execute the module again.

---

**Q14.19: Basic - [Standard Library]**

Which module is NOT in the standard library?

A) `os`
B) `sys`
C) `requests`
D) `json`

**Answer: C**

**Explanation:**
`requests` is a popular third-party package. `urllib` is the standard library equivalent (though less ergonomic).

---

**Q14.20: Advanced - [Importlib Resources]**

To read a data file inside a package in a zip-safe way (modern Python):

A) `open('pkg/data.txt')`
B) `pkgutil.get_data()`
C) `importlib.resources.files('pkg').joinpath('data.txt').read_text()`
D) `os.path.dirname(__file__)`

**Answer: C**

**Explanation:**
`importlib.resources` (Python 3.7+) abstracts resource access, working even if the package is in a zip file/egg.

---

**Q14.21: Expert - [Loader Execmodule]**

In the import protocol, `loader.exec_module(module)`:

A) Finds the module.
B) Executes the module's body (filling its `__dict__`).
C) Returns the source.
D) Compiles the bytes.

**Answer: B**

**Explanation:**
After the Finder locates the module and creates a ModuleSpec, the Loader executes the module.

---

**Q14.22: Intermediate - [Module Docstring]**

The docstring of a module is stored in:

A) `__doc_string__`
B) `__doc__`
C) `__help__`
D) `__info__`

**Answer: B**

**Explanation:**
The first string literal in the file is assigned to `__doc__`.

---

**Q14.23: Basic - [Init Exec]**

When you `import package`, does `package/__init__.py` run?

A) Yes, immediately.
B) No, only when initializing submodules.
C) No.
D) Only if you run `import package.__init__`.

**Answer: A**

**Explanation:**
Importing the package executes its initialization script.

---

**Q14.24: Advanced - [Relative Import Main]**

Can you use relative imports `from . import utils` in a script run directly (`__name__ == '__main__'`)?

A) Yes.
B) No.
C) Only if `__init__.py` exists.
D) Only in Python 2.

**Answer: B**

**Explanation:**
Relative imports rely on `__package__` metadata. A top-level script (main module) has no known parent package context, so relative imports fail with "ImportError: attempted relative import with no known parent package".

---

**Q14.25: Intermediate - [Star Import Limit]**

`from module import *` is allowed:

A) Anywhere.
B) Only at module level (top level).
C) Inside functions.
D) Inside classes.

**Answer: B**

**Explanation:**
In Python 3, wildcard imports are syntax errors inside functions because they make local variable optimization impossible (the compiler can't know what names exist).

---

**Q14.26: Expert - [__import__ function]**

The built-in `__import__()` is:

A) The function called by the `import` statement.
B) A private function.
C) A fast version.
D) For internal use only.

**Answer: A**

**Explanation:**
The `import` statement is syntactic sugar that effectively calls `__import__`. You can override it to customize import behavior (though using import hooks is cleaner).

---

**Q14.27: Basic - [Sys Path Append]**

If you want to import a module from a specific custom folder:

A) Move the file to C:.
B) `sys.path.append('/path/to/folder')`
C) `import '/path/to/folder'`
D) config.json.

**Answer: B**

**Explanation:**
Modifying `sys.path` dynamically adds the folder to the search locations.

---

**Q14.28: Advanced - [Lazy Import]**

Are imports lazy by default in Python?

A) Yes.
B) No.
C) Only in packages.
D) Only with `importlib`.

**Answer: B**

**Explanation:**
Standard imports act immediately. Lazy importing (loading only when accessed) requires third-party tools or specific `importlib` recipes (mostly available in newer Python versions/libraries like `lazy_loader`).

---

**Q14.29: Intermediate - [__package__ attribute]**

If `__package__` is `None` or empty, it means:

A) The module is a top-level module (not part of a package).
B) The package is broken.
C) It is `__main__`.
D) A or C.

**Answer: D**

**Explanation:**
It indicates the module structure. Top level modules have no package.

---

**Q14.30: Expert - [Submodule Caching]**

If you `import pkg.mod`, and `pkg` is already imported:

A) `pkg.mod` is reloaded.
B) Python adds `mod` as an attribute to the `pkg` object (i.e. `pkg.mod`).
C) `pkg` is overwritten.
D) Error.

**Answer: B**

**Explanation:**
Importing a submodule injects that submodule object into the parent package's namespace.

---

**Q14.31: Intermediate - [Importing from Parent in Script]**

If you run `python pkg/script.py` (not as a module), and `script.py` tries `import pkg`:

A) It works.
B) It fails (ImportError) unless `.` is in `PYTHONPATH` or the script does `sys.path.append('..')`.
C) It works because siblings are visible.
D) It crashes.

**Answer: B**

**Explanation:**
When running a script inside a package directory directly, the parent directory (root of package) is *not* added to `sys.path`. Python adds the script's directory. Thus `pkg` is not visible.

---

**Q14.32: Advanced - [Zipimport]**

`zipimport` allows Python to:

A) Zip files.
B) Import modules directly from ZIP archives added to `sys.path`.
C) Compress modules.
D) Encrypt code.

**Answer: B**

**Explanation:**
Built-in support for treating ZIP files as directories of modules.

---

**Q14.33: Basic - [Import Side Effect]**

Does `import module` run the code inside `module.py` every time it is called?

A) Yes.
B) No, only the first time per process.
C) Only if explicitly requested.
D) Randomly.

**Answer: B**

**Explanation:**
Python checks `sys.modules`. If present, it returns the cached object. It executes the body only on the first import.

---

**Q14.34: Expert - [pth Files]**

`.pth` files in `site-packages` are used to:

A) Add additional directories to `sys.path` automatically on startup.
B) Define paths to executables.
C) Store python configuration.
D) List installed packages.

**Answer: A**

**Explanation:**
Any `.pth` file in the site-packages directory is parsed, and listed paths are added to `sys.path`. Commonly used by editable installs (`pip install -e .`).

---

**Q14.35: Intermediate - [Import Error Name]**

`from A import B`. If `B` cannot be found in `A`, it raises:

A) `ModuleNotFoundError`
B) `ImportError`
C) `AttributeError`
D) `NameError`

**Answer: B**

**Explanation:**
Or `ImportError: cannot import name 'B' from 'A'`. (It might raise `AttributeError` if accessed as `A.B`, but generic `from` import failure is `ImportError`).

---

**Q14.36: Advanced - [Package Init Variable]**

If `pkg/__init__.py` defines `x = 1`, and you do `import pkg`:

A) `pkg.x` is 1.
B) `x` is in the global namespace.
C) `pkg.x` is undefined.
D) `x` is private.

**Answer: A**

**Explanation:**
The `__init__.py` file *is* the body of the package module. Variables defined there become attributes of the package.

---

**Q14.37: Basic - [Pip Install Target]**

`pip install package` typically installs to:

A) `site-packages`
B) `dist-packages` (on some Debian systems)
C) Global libs.
D) A or B.

**Answer: D**

**Explanation:**
Standard location for third-party packages.

---

**Q14.38: Intermediate - [Importlib Import Module]**

`importlib.import_module('a.b')` returns:

A) The module `a`.
B) The module `a.b` (the leaf).
C) `None`.
D) The source code.

**Answer: B**

**Explanation:**
Unlike `__import__` (which might return the top-level package), `import_module` always returns the specified module.

---

**Q14.39: Advanced - [Module Spec]**

`ModuleSpec` (PEP 451) contains:

A) Information used to load the module (name, loader, origin/location).
B) The source code only.
C) The bytecode.
D) Documentation.

**Answer: A**

**Explanation:**
The encapsulation of import-related information used during the loading process.

---

**Q14.40: Expert - [Sys Meta Path Insert]**

If you insert a custom Finder at `sys.meta_path[0]`:

A) It works for all imports, intercepting everything.
B) It breaks Python.
C) It is ignored.
D) It only works for builtins.

**Answer: A**

**Explanation:**
`sys.meta_path` is searched in order. Placing a finder first gives it priority over built-in finders (allowing you to hook standard imports).

---

**Q14.41: Intermediate - [Relative Import Error]**

`from . import x` inside `pkg/mod.py` works if:

A) `pkg` is in `sys.path` and imported as `import pkg.mod`.
B) `pkg/mod.py` is run directly.
C) `pkg` is not a package.
D) `x` does not exist.

**Answer: A**

**Explanation:**
Relative imports require the module to have been loaded as part of a package (i.e., `__package__` is set).

---

**Q14.42: Basic - [Attributes of Module]**

Accessing `sys.modules['math']` returns:

A) String "math".
B) The module object `math`.
C) The file path.
D) Error.

**Answer: B**

**Explanation:**
The cache stores the actual module objects.

---

**Q14.43: Advanced - [Importing by File Path]**

To import a Python file from an arbitrary path (without adding to `sys.path`), use:

A) `importlib.util.spec_from_file_location` and `module_from_spec`.
B) `imp.load_source` (Deprecated).
C) `exec(open(path).read())` (Risky/Limited).
D) A (Preferred Modern Way) or B (Old).

**Answer: D**

**Explanation:**
`importlib` recipes permit loading a module from a specific file path directly.

---

**Q14.44: Expert - [Namespace Package Priority]**

If both a regular package (with `__init__.py`) and a namespace package (without) exist for `pkg` in different `sys.path` entries:

A) The regular package takes precedence.
B) The namespace package takes precedence.
C) They merge.
D) Error.

**Answer: A**

**Explanation:**
Regular packages are found first. Namespace packages are a fallback if no `__init__.py` is found.

---

**Q14.45: Intermediate - [Name Shadowing]**

If you have `email.py` in your script's folder and do `import email`:

A) Python imports the standard library `email`.
B) Python imports your local `email.py`, potentially breaking other libraries.
C) Error.
D) Both.

**Answer: B**

**Explanation:**
Since the script's directory is usually first in `sys.path`, local files shadow standard library modules. Common beginner mistake.

---

**Q14.46: Basic - [Wildcard All]**

If `__all__` is NOT defined, `from module import *`:

A) Imports all names that do not start with `_`.
B) Imports nothing.
C) Imports only classes.
D) Imports private members too.

**Answer: A**

**Explanation:**
Default behavior is to export all public names (no leading underscore).

---

**Q14.47: Advanced - [Lazy Loader]**

`sys.modules` entry that is `None` usually means:

A) The module failed to import.
B) The module is explicitly disabled or blacklisted (often done by security sandboxes or packagers).
C) The module is loading.
D) It is empty.

**Answer: B**

**Explanation:**
Setting `sys.modules['mod'] = None` forces subsequent imports of `mod` to raise `ModuleNotFoundError`.

---

**Q14.48: Expert - [Import Hook]**

An "Import Hook" allows you to:

A) Run code when a specific module is imported.
B) Change the syntax of Python.
C) Delete modules.
D) Modify bytecode on disk.

**Answer: A**

**Explanation:**
Using `sys.meta_path` or `sys.path_hooks` to intercept import requests and dynamically load/modify code.

---

**Q14.49: Intermediate - [Reload Issues]**

When `reload(mod)` is called, existing instances of classes defined in `mod`:

A) Are updated to the new class definition automatically.
B) Keep referring to the *old* class definition.
C) Are deleted.
D) Raise Error.

**Answer: B**

**Explanation:**
Reloading re-executes the module and updates the names in the module namespace to point to new objects. However, existing objects in memory (instances) still hold references to the old class types.

---

**Q14.50: Basic - [Sys Meta Path Type]**

`sys.meta_path` is a:

A) List.
B) Dict.
C) Set.
D) String.

**Answer: A**

**Explanation:**
A list of finder objects associated with the import system.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
