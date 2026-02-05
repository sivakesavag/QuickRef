# Chapter 21: Pythonic Code & Best Practices

> **Topics Covered**: PEP 8 style, code formatting, naming conventions, documentation, docstrings, type hints, linting, code organization, refactoring, anti-patterns, SOLID principles, design patterns

---

## Questions

---

**Q21.1: Basic - [What is Pythonic]**

What does "Pythonic" mean?

A) Written in Python
B) Code following Python idioms, clear, readable, using language features appropriately
C) Maximum performance
D) Using all features

**Answer: B**

**Explanation:**
Pythonic = idiomatic Python. Uses language features well: comprehensions, context managers, iteration. Clear > clever. The Zen of Python (`import this`) captures philosophy. "There should be one obvious way."

---

**Q21.2: Basic - [PEP 8 Basics]**

What is PEP 8?

A) Python version
B) Style guide for Python code — naming, spacing, formatting
C) Performance guide
D) Security guide

**Answer: B**

**Explanation:**
PEP 8: official style guide. 4-space indent, snake_case for variables/functions, PascalCase for classes, 79-char lines. Consistency matters. Tools: black, autopep8, flake8 enforce/check.

---

**Q21.3: Intermediate - [Naming Conventions]**

Which follows PEP 8?

A) `myVariable = 10`
B) `my_variable = 10`
C) `MyVariable = 10`
D) `MYVARIABLE = 10`

**Answer: B**

**Explanation:**
`snake_case` for variables, functions, modules. `PascalCase` for classes. `UPPER_CASE` for constants. Leading underscore `_private` for internal, double `__name_mangling`. Consistent naming.

---

**Q21.4: Intermediate - [Class Naming]**

Which follows PEP 8?

A) `class user_account:`
B) `class UserAccount:`
C) `class user_Account:`
D) `class USERACCOUNT:`

**Answer: B**

**Explanation:**
PascalCase (CapWords) for classes: `UserAccount`, `HTTPConnection`. Clear word boundaries. Exceptions are rare (e.g., `namedtuple` objects sometimes lowercase). Consistency across codebase.

---

**Q21.5: Intermediate - [Line Length]**

PEP 8 recommends max line length of:

A) 120 characters
B) 79 characters (72 for docstrings)
C) No limit
D) 60 characters

**Answer: B**

**Explanation:**
79 chars enables side-by-side editing, works on all terminals. Many teams allow 100-120 for modern screens. black defaults to 88. Key: consistency in project. Long lines harm readability.

---

**Q21.6: Intermediate - [Import Organization]**

What's the correct import order?

A) Any order
B) Standard library, third-party, local — separated by blank lines
C) Alphabetical only
D) Shortest first

**Answer: B**

**Explanation:**
```python
import os          # stdlib
import sys

import requests    # third-party

from myapp import utils  # local
```
Separated by blank lines. Alphabetical within groups. isort tool auto-sorts.

---

**Q21.7: Intermediate - [Docstring Format]**

What is the output?
```python
def greet(name):
    """Return greeting for name.
    
    Args:
        name: Person's name.
    
    Returns:
        Greeting string.
    """
    return f"Hello, {name}"

print(greet.__doc__.split('\n')[0])
```

A) First line of docstring
B) `Return greeting for name.`
C) Just `greet`
D) Error

**Answer: B**

**Explanation:**
Docstring: first statement in function/class/module. Accessed via `__doc__`. First line is summary. Google, NumPy, Sphinx formats for Args, Returns. Document public APIs.

---

**Q21.8: Intermediate - [Type Hints]**

What do type hints provide?
```python
def greet(name: str) -> str:
    return f"Hello, {name}"
```

A) Runtime enforcement
B) Documentation for readers and static analysis tools
C) Performance improvement
D) Required syntax

**Answer: B**

**Explanation:**
Type hints are NOT enforced at runtime. They help: IDE autocomplete, mypy static checking, documentation. `typing` module for complex types: `List[int]`, `Optional[str]`, `Dict[str, Any]`.

---

**Q21.9: Intermediate - [Black Formatter]**

What does black do?

A) Checks code
B) Auto-formats Python code with consistent style, no configuration needed
C) Compiles Python
D) Runs tests

**Answer: B**

**Explanation:**
black: opinionated formatter. Run `black file.py` — reformats automatically. Consistent style across team. "You can have any color as long as it's black." Eliminates style debates.

---

**Q21.10: Intermediate - [Linting]**

What do linters like flake8/pylint do?

A) Format code
B) Check for errors, style issues, code smells without running code
C) Run tests
D) Compile Python

**Answer: B**

**Explanation:**
Static analysis: undefined variables, unused imports, style violations, complexity. flake8 = pyflakes + pep8. pylint = comprehensive. ruff = fast modern linter. Catch bugs before running.

---

**Q21.11: Intermediate - [EAFP vs LBYL]**

What is EAFP?

A) Error And Fix Protocol
B) Easier to Ask Forgiveness than Permission — try/except pattern
C) Error Avoidance First Principle
D) Exception Handling

**Answer: B**

**Explanation:**
EAFP: try operation, handle exception if it fails. Pythonic.
```python
try:
    value = d[key]
except KeyError:
    value = default
```
LBYL: `if key in d: value = d[key]`. EAFP often cleaner in Python.

---

**Q21.12: Intermediate - [Explicit is Better]**

Why prefer explicit over implicit?
```python
# Explicit
from math import sqrt
# Implicit 
from math import *
```

A) No difference
B) Explicit shows what's used, * imports can cause naming conflicts
C) * is faster
D) Explicit is required

**Answer: B**

**Explanation:**
`import *` pollutes namespace, unclear origins, may shadow names. Explicit imports: clear dependencies, easier to track. "Explicit is better than implicit" — Zen of Python.

---

**Q21.13: Intermediate - [Comprehension vs Loop]**

Which is more Pythonic?
```python
# A
squares = []
for x in range(10):
    squares.append(x**2)

# B
squares = [x**2 for x in range(10)]
```

A) A is more Pythonic
B) B is more Pythonic
C) Same
D) Depends

**Answer: B**

**Explanation:**
Comprehensions: concise, clear intent, often faster. Use for simple transformations. Complex logic: regular loop is clearer. "Simple is better than complex" — Zen of Python.

---

**Q21.14: Intermediate - [Context Managers]**

Why use context managers?
```python
# Good
with open('file.txt') as f:
    data = f.read()

# Not as good
f = open('file.txt')
data = f.read()
f.close()
```

A) Same behavior
B) with guarantees cleanup even on exception, cleaner code
C) Faster
D) Required syntax

**Answer: B**

**Explanation:**
Context manager (`with`) ensures `__exit__` is called — file closed, lock released, etc. Even if exception occurs. Manual close might be skipped. Pythonic resource management.

---

**Q21.15: Intermediate - [Truthiness]**

Which is more Pythonic?
```python
# A
if len(my_list) > 0:
    ...

# B
if my_list:
    ...
```

A) A is more Pythonic
B) B is more Pythonic
C) Same
D) Neither is correct

**Answer: B**

**Explanation:**
Empty collections are falsy, non-empty are truthy. `if my_list:` is idiomatic. Also: `if count:` vs `if count != 0`. Use truthiness for "is there something?" checks.

---

**Q21.16: Intermediate - [None Comparison]**

Which is correct for None check?
```python
# A
if x == None:
    ...

# B
if x is None:
    ...
```

A) A is correct
B) B is correct (is for None check)
C) Same
D) Neither

**Answer: B**

**Explanation:**
Use `is None` / `is not None`. None is singleton — identity check appropriate. `==` might call `__eq__` method which could have unexpected behavior. PEP 8 recommends `is`.

---

**Q21.17: Intermediate - [Avoid Global State]**

Why avoid global variables?

A) Slower
B) Hard to test, unexpected modifications, implicit dependencies, coupling
C) Not allowed
D) Use more memory

**Answer: B**

**Explanation:**
Globals: hidden state, functions depend on external changes, hard to test/debug. Prefer: pass as arguments, return values, classes. Necessary sometimes (configuration) but minimize.

---

**Q21.18: Intermediate - [Function Size]**

Why keep functions small?

A) Performance
B) Single responsibility, easier to test, understand, reuse
C) Required
D) No reason

**Answer: B**

**Explanation:**
"Do one thing well." Small functions: clear purpose, easier to name, test, reuse. If function does X and Y, split. Refactor when functions grow. Improves maintainability.

---

**Q21.19: Intermediate - [DRY Principle]**

What is DRY?

A) Debugging Really Yields
B) Don't Repeat Yourself — avoid duplicate code
C) Dynamic Resource Yield
D) Data Representation

**Answer: B**

**Explanation:**
Duplicate code: harder to maintain, bugs fix in one place not another. Extract to functions/classes. But: don't over-abstract for two uses. "WET" (Write Everything Twice) as counter-argument.

---

**Q21.20: Intermediate - [Magic Numbers]**

What's wrong with this code?
```python
if status == 7:
    process_complete()
```

A) Nothing
B) Magic number — use named constant: STATUS_COMPLETE = 7
C) Wrong comparison
D) Syntax error

**Answer: B**

**Explanation:**
Magic numbers: unclear meaning. What's 7? Use constants: `STATUS_COMPLETE = 7`. Better: Enum. Self-documenting code. Same for magic strings, repeated values.

---

**Q21.21: Intermediate - [SOLID - Single Responsibility]**

What is Single Responsibility Principle?

A) One file per class
B) Class/function should have one reason to change
C) One line functions
D) Single return statement

**Answer: B**

**Explanation:**
Class does one thing: User class handles user data, not email sending. Easier to maintain, test, understand. If class has AND in description ("does X and Y"), might need splitting.

---

**Q21.22: Intermediate - [SOLID - Open/Closed]**

What is Open/Closed Principle?

A) Open source
B) Open for extension, closed for modification — add new behavior without changing existing code
C) Open files
D) Closing connections

**Answer: B**

**Explanation:**
Add functionality by extending (inheritance, composition, plugins), not modifying existing tested code. Strategy pattern, decorators enable this. Reduces risk of breaking existing features.

---

**Q21.23: Intermediate - [Composition over Inheritance]**

Why prefer composition over inheritance?

A) Inheritance is bad
B) More flexible, avoids deep hierarchies, can combine behaviors
C) Faster
D) No difference

**Answer: B**

**Explanation:**
Inheritance: rigid hierarchy, superclass changes ripple. Composition: class HAS-A another class, delegate. Duck typing makes composition natural in Python. Use inheritance for IS-A, composition for HAS-A.

---

**Q21.24: Intermediate - [Code Comments]**

When are comments valuable?

A) Every line
B) Explain WHY, not WHAT — non-obvious decisions, complex algorithms
C) Never
D) Only for functions

**Answer: B**

**Explanation:**
Code shows what. Comments explain why: "# Cache expires in 1 hour to match external API refresh". Avoid: `x += 1 # increment x`. Good naming reduces need for comments.

---

**Q21.25: Intermediate - [Docstrings vs Comments]**

What's the difference between docstrings and comments?

A) Same thing
B) Docstrings document APIs (accessible via __doc__); comments explain implementation
C) Docstrings are faster
D) Comments are for functions

**Answer: B**

**Explanation:**
Docstring: first string in function/class/module. Describes what it does for users. Appears in help(), documentation. Comments: internal explanations for maintainers. Different audiences.

---

**Q21.26: Intermediate - [Unpacking]**

Which is more Pythonic?
```python
# A
first = my_list[0]
second = my_list[1]

# B
first, second, *rest = my_list
```

A) A is more Pythonic
B) B is more Pythonic (for appropriate use cases)
C) Same
D) Neither

**Answer: B**

**Explanation:**
Unpacking is Pythonic: tuple return `a, b = func()`, swap `a, b = b, a`, extended `first, *middle, last = list`. Cleaner than indexing when you need multiple values.

---

**Q21.27: Intermediate - [enumerate]**

Which is more Pythonic?
```python
# A
for i in range(len(items)):
    print(i, items[i])

# B
for i, item in enumerate(items):
    print(i, item)
```

A) A is more Pythonic
B) B is more Pythonic
C) Same
D) Depends

**Answer: B**

**Explanation:**
`enumerate` provides index and item cleanly. `range(len(...))` is anti-pattern. Also: `enumerate(items, start=1)` for 1-indexed. Pythonic iteration pattern.

---

**Q21.28: Intermediate - [zip]**

Which is more Pythonic?
```python
# A
for i in range(len(names)):
    print(names[i], ages[i])

# B
for name, age in zip(names, ages):
    print(name, age)
```

A) A is more Pythonic
B) B is more Pythonic
C) Same
D) Neither works

**Answer: B**

**Explanation:**
`zip` pairs elements from multiple iterables. Cleaner than index gymnastics. `zip_longest` for different lengths. Pythonic parallel iteration.

---

**Q21.29: Intermediate - [any() and all()]**

Which is more Pythonic?
```python
# A
has_positive = False
for x in numbers:
    if x > 0:
        has_positive = True
        break

# B
has_positive = any(x > 0 for x in numbers)
```

A) A is more Pythonic
B) B is more Pythonic
C) Same
D) Neither

**Answer: B**

**Explanation:**
`any()` returns True if any element is truthy. `all()` returns True if all are truthy. Short-circuit evaluation. Generator expression is lazy. Expressive, Pythonic.

---

**Q21.30: Intermediate - [defaultdict Pattern]**

Which is more Pythonic?
```python
# A
d = {}
if key not in d:
    d[key] = []
d[key].append(value)

# B
from collections import defaultdict
d = defaultdict(list)
d[key].append(value)
```

A) A is more Pythonic
B) B is more Pythonic for this pattern
C) Same
D) Neither

**Answer: B**

**Explanation:**
`defaultdict` eliminates boilerplate for default values. Also: `dict.setdefault(key, []).append(value)`. Or `Counter` for counting. Use right tool for pattern.

---

**Q21.31: Intermediate - [Anti-Pattern: Mutable Default]**

What's wrong here?
```python
def add_item(item, items=[]):
    items.append(item)
    return items
```

A) Nothing
B) Mutable default argument shared across calls — items accumulates
C) Syntax error
D) Type error

**Answer: B**

**Explanation:**
Default list created once at definition. All calls share it: `add_item(1)` → [1], `add_item(2)` → [1, 2]. Fix: `items=None; if items is None: items = []`. Common bug.

---

**Q21.32: Intermediate - [Anti-Pattern: Bare Except]**

What's wrong here?
```python
try:
    risky_operation()
except:
    pass
```

A) Nothing
B) Bare except catches everything including KeyboardInterrupt, SystemExit; silently ignores
C) Syntax
D) Performance

**Answer: B**

**Explanation:**
⚠️ Catches `KeyboardInterrupt` (Ctrl+C), `SystemExit`, actual bugs. Silently swallowing errors hides problems. Catch specific exceptions: `except ValueError:`. At minimum: `except Exception:`.

---

**Q21.33: Intermediate - [Anti-Pattern: == True/False]**

What's wrong here?
```python
if is_valid == True:
    ...
```

A) Nothing
B) Redundant — just use `if is_valid:`
C) Wrong syntax
D) Performance issue

**Answer: B**

**Explanation:**
Boolean variable is already True/False. `== True` is redundant, less clear. Just `if is_valid:`. Similarly: `if not is_valid:` instead of `if is_valid == False:`.

---

**Q21.34: Intermediate - [Design Patterns - Factory]**

What is Factory pattern?

A) Manufacturing
B) Function/method that creates and returns objects, hiding instantiation logic
C) File creation
D) Testing pattern

**Answer: B**

**Explanation:**
```python
def create_user(user_type):
    if user_type == 'admin':
        return Admin()
    return RegularUser()
```
Centralizes object creation. Can return different subclasses based on conditions. Decouples code from specific classes.

---

**Q21.35: Intermediate - [Design Patterns - Singleton]**

What is Singleton pattern?

A) Single file
B) Ensure only one instance of class exists
C) Single function
D) One-line code

**Answer: B**

**Explanation:**
Sometimes needed: configuration, connection pool. Python approaches: module-level variable, `__new__` override, decorator. Often overused — prefer dependency injection. Global state concerns apply.

---

**Q21.36: Intermediate - [Design Patterns - Strategy]**

What is Strategy pattern?

A) Planning
B) Encapsulate algorithms in classes, switch at runtime
C) Game strategy
D) Error strategy

**Answer: B**

**Explanation:**
```python
class SortStrategy: ...
class QuickSort(SortStrategy): ...
class MergeSort(SortStrategy): ...
sorter.strategy = QuickSort()
```
Swap algorithm without changing client. In Python: often just pass function (duck typing makes this natural).

---

**Q21.37: Intermediate - [Code Smell - Long Parameter List]**

What's the problem with many function parameters?

A) Slower
B) Hard to remember order/meaning, sign of doing too much
C) No problem
D) Required

**Answer: B**

**Explanation:**
`func(a, b, c, d, e, f, g)` — unclear. Solutions: dataclass/namedtuple for related params, split function, builder pattern. If >3-4 params, reconsider design.

---

**Q21.38: Intermediate - [Code Smell - Nested Conditions]**

How to fix deeply nested conditions?
```python
if a:
    if b:
        if c:
            do_thing()
```

A) Can't fix
B) Guard clauses (early returns), extract functions
C) More nesting
D) Remove conditions

**Answer: B**

**Explanation:**
```python
if not a: return
if not b: return
if not c: return
do_thing()
```
Guard clauses flatten code. Extract complex conditions to well-named functions. Max 2-3 levels of nesting.

---

**Q21.39: Intermediate - [Testing Mindset]**

Why write tests alongside code?

A) Slows development
B) Catches bugs early, documents behavior, enables safe refactoring
C) Optional extra
D) Only for production

**Answer: B**

**Explanation:**
Tests: executable documentation, catch regressions, enable confident changes. TDD: test first, then code. Tests aren't overhead — they're investment. Untested code is liability.

---

**Q21.40: Intermediate - [Refactoring]**

What is refactoring?

A) Rewriting from scratch
B) Improving code structure without changing behavior
C) Debugging
D) Adding features

**Answer: B**

**Explanation:**
Refactoring: cleaner code, same functionality. Rename variables, extract methods, simplify logic. Tests ensure behavior preserved. Continuous improvement. Technical debt reduction.

---

**Q21.41: Intermediate - [Virtual Environments]**

Why use virtual environments?

A) Security
B) Isolate project dependencies — different projects can use different package versions
C) Faster
D) Required

**Answer: B**

**Explanation:**
`python -m venv venv` creates isolated environment. Project A uses Django 3, Project B uses Django 4. Reproducible: `pip freeze > requirements.txt`. Always use venvs.

---

**Q21.42: Intermediate - [requirements.txt]**

What should be in requirements.txt?

A) All installed packages
B) Direct dependencies with versions: package==1.2.3
C) System packages
D) Python version

**Answer: B**

**Explanation:**
List direct dependencies (not sub-dependencies). Pin versions for reproducibility: `requests==2.28.1`. `pip freeze` includes everything — cleanup. Modern: use poetry, pipenv for lock files.

---

**Q21.43: Intermediate - [Project Structure]**

Standard Python project structure:

A) All in one file
B) project/src/package/, tests/, docs/, pyproject.toml
C) No standard
D) Flat structure

**Answer: B**

**Explanation:**
```
myproject/
  src/mypackage/
    __init__.py
    module.py
  tests/
  pyproject.toml
  README.md
```
Separation: source, tests, docs. `pyproject.toml` for build config. Consistent structure aids navigation.

---

**Q21.44: Intermediate - [pyproject.toml]**

What is pyproject.toml?

A) Project documentation
B) Unified configuration for Python project metadata, dependencies, tools
C) Test config
D) Django settings

**Answer: B**

**Explanation:**
Modern replacement for setup.py + setup.cfg. Project metadata, dependencies, build system. Tool configs (black, pytest) can go here. PEP 517/518 standard. Single source of truth.

---

**Q21.45: Intermediate - [Code Review]**

What makes good code reviews?

A) Finding all bugs
B) Constructive feedback on design, clarity, correctness; learning opportunity
C) Speed
D) Approval only

**Answer: B**

**Explanation:**
Reviews: catch bugs, share knowledge, maintain standards. Focus: correctness, clarity, design. Not: style (use formatters). Be kind, specific, explain why. Learning for both parties.

---

**Q21.46: Intermediate - [Pre-commit Hooks]**

What are pre-commit hooks?

A) Git commits
B) Automated checks that run before committing — format, lint, test
C) Comments before code
D) Version control

**Answer: B**

**Explanation:**
pre-commit framework: run black, flake8, isort automatically on commit. Catch issues before they enter codebase. Consistent enforcement. `.pre-commit-config.yaml` configuration.

---

**Q21.47: Intermediate - [CI/CD]**

What is CI/CD for Python projects?

A) Compiler
B) Continuous Integration/Deployment — automated testing and deployment on code changes
C) Code import
D) Configuration

**Answer: B**

**Explanation:**
Push code → CI runs tests, linting. Pass → CD deploys. GitHub Actions, GitLab CI, Circle CI. Catch issues early, automate deployment. Essential for team development.

---

**Q21.48: Intermediate - [Logging over Print]**

Why use logging instead of print?

A) Same thing
B) Logging: levels, formatting, multiple outputs, can be configured, disabled
C) Faster
D) Required

**Answer: B**

**Explanation:**
`print`: development only. `logging`: levels (DEBUG/INFO/WARNING), configurable output, timestamps, can disable in production. `logging.info("msg")` vs `print("msg")`. Professional approach.

---

**Q21.49: Intermediate - [Error Messages]**

What makes good error messages?

A) "Error occurred"
B) What happened, context, how to fix: "Invalid email format 'abc'. Expected: user@domain.com"
C) Stack trace only
D) Error code

**Answer: B**

**Explanation:**
Good errors: what went wrong, what was expected, how to fix. Include problematic value (sanitized). User-facing: friendly. Developer-facing: technical. Reduce debugging time.

---

**Q21.50: Intermediate - [Documentation]**

What documentation should projects have?

A) None needed
B) README, API docs (docstrings), examples, changelog
C) Only code comments
D) Only README

**Answer: B**

**Explanation:**
README: what, why, quick start. API docs: from docstrings (Sphinx). Examples: common use cases. Changelog: what changed per version. Contributing guide. Documentation as important as code.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 2 | 4% |
| Intermediate | 48 | 96% |
| Advanced | 0 | 0% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- PEP 8 and style guides
- Pythonic idioms
- Type hints and documentation
- Code formatting tools
- Design principles (SOLID, DRY)
- Common anti-patterns
- Design patterns
- Project structure
- Testing and refactoring
- CI/CD and best practices
