# Chapter 11: Context Managers & Exception Handling

> **Topics Covered**: try/except/else/finally, exception hierarchy, custom exceptions, context managers, __enter__/__exit__, contextlib, with statement, exception chaining, raise from, traceback handling

---

## Questions

---

**Q11.1: Basic - [try/except]**

What is the output?
```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
```

A) Error: ZeroDivisionError
B) `Cannot divide by zero`
C) `None`
D) `0`

**Answer: B**

**Explanation:**
The try block raises ZeroDivisionError. The except clause catches it and executes its block. Without the handler, the program would crash. Exception handling allows graceful error recovery.

---

**Q11.2: Basic - [Multiple except]**

What is the output?
```python
try:
    num = int("abc")
except ZeroDivisionError:
    print("Division error")
except ValueError:
    print("Value error")
```

A) `Division error`
B) `Value error`
C) Both print
D) Error: not caught

**Answer: B**

**Explanation:**
`int("abc")` raises ValueError (not a valid integer). The first except doesn't match; the second does. Only the matching handler executes. Order can matter for exception hierarchy.

---

**Q11.3: Intermediate - [except Tuple]**

What is the output?
```python
try:
    x = 1 / 0
except (ZeroDivisionError, ValueError):
    print("Error caught")
```

A) Error
B) `Error caught`
C) Nothing
D) Both exceptions raised

**Answer: B**

**Explanation:**
`except (ExceptionA, ExceptionB):` catches either exception type. The tuple groups exceptions with same handler. ZeroDivisionError is caught. Useful when handling group of related exceptions identically.

---

**Q11.4: Intermediate - [Catching Exception Object]**

What is the output?
```python
try:
    x = 1 / 0
except ZeroDivisionError as e:
    print(type(e).__name__)
```

A) `ZeroDivisionError`
B) `e`
C) `Error`
D) Nothing

**Answer: A**

**Explanation:**
`as e` binds the exception object to variable `e`. You can inspect it: `str(e)` for message, `type(e)` for class. `type(e).__name__` gives "ZeroDivisionError". Useful for logging or custom error messages.

---

**Q11.5: Basic - [else Clause]**

What is the output?
```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Error")
else:
    print("Success")
```

A) `Error`
B) `Success`
C) `Error Success`
D) Nothing

**Answer: B**

**Explanation:**
`else` runs ONLY if no exception occurred in try block. Here `10/2` succeeds, so else executes. If an exception had been raised and caught, else wouldn't run. Use else for code that should run only on success.

---

**Q11.6: Basic - [finally Clause]**

What is the output?
```python
try:
    x = 1 / 0
except ZeroDivisionError:
    print("Error")
finally:
    print("Done")
```

A) `Error`
B) `Done`
C) `Error Done`
D) Nothing

**Answer: C**

**Explanation:**
`finally` ALWAYS runs — whether exception occurred or not, caught or not. Here: exception caught (prints "Error"), then finally runs (prints "Done"). Use finally for cleanup (closing files, releasing resources).

---

**Q11.7: Intermediate - [finally Always Runs]**

What is the output?
```python
def func():
    try:
        return "try"
    finally:
        print("finally")

result = func()
print(result)
```

A) `try`
B) `finally` then `try`
C) `try` then `finally`
D) Only `finally`

**Answer: B**

**Explanation:**
`finally` runs even when returning from try. Order: finally executes (prints "finally"), THEN return completes. Result is "try". finally is truly guaranteed — even `return` doesn't skip it.

---

**Q11.8: Advanced - [finally Overrides Return]**

What is the output?
```python
def func():
    try:
        return "try"
    finally:
        return "finally"

print(func())
```

A) `try`
B) `finally`
C) `try finally`
D) Error

**Answer: B**

**Explanation:**
⚠️ If finally has a return, it OVERRIDES the try's return. "finally" is returned, not "try". This is generally considered bad practice — avoid returning from finally as it can mask exceptions too.

---

**Q11.9: Basic - [Exception Hierarchy]**

Which exception is the base of all built-in exceptions?

A) Exception
B) BaseException
C) Error
D) Object

**Answer: B**

**Explanation:**
`BaseException` is the root. It has children: `Exception` (most exceptions), `KeyboardInterrupt`, `SystemExit`, `GeneratorExit`. Usually catch `Exception`, not `BaseException`, to allow Ctrl+C to work.

---

**Q11.10: Intermediate - [Catch-All Exception]**

What's the issue with `except Exception:`?

A) It's too specific
B) It catches too broadly, potentially hiding unexpected errors
C) It doesn't work
D) No issue

**Answer: B**

**Explanation:**
`except Exception:` catches almost everything, including bugs you should fix. Use specific exceptions when possible. At minimum, log the error. Bare `except:` (catching `BaseException`) is even worse.

---

**Q11.11: Basic - [raise Statement]**

What does `raise ValueError("Bad input")` do?

A) Logs a message
B) Raises a ValueError exception with that message
C) Returns an error
D) Prints the message

**Answer: B**

**Explanation:**
`raise` explicitly throws an exception. The program stops unless caught. The message becomes `str(exception)`. Use raise to signal errors that calling code should handle.

---

**Q11.12: Intermediate - [Re-raising Exceptions]**

What does bare `raise` do inside an except block?

A) Raises RuntimeError
B) Re-raises the current exception unchanged
C) Does nothing
D) Exits the program

**Answer: B**

**Explanation:**
Bare `raise` re-raises the active exception with original traceback preserved. Useful for logging then re-raising: `except Exception: log(error); raise`. Preserves the original error context for debugging.

---

**Q11.13: Advanced - [Exception Chaining - raise from]**

What is the output concept?
```python
try:
    x = int("abc")
except ValueError as e:
    raise TypeError("Failed to convert") from e
```

A) Only TypeError is raised
B) TypeError is raised with ValueError as __cause__
C) Both exceptions print separately
D) ValueError wins

**Answer: B**

**Explanation:**
`raise X from Y` chains exceptions. The new exception has `__cause__` set to original. Traceback shows both: "The above exception was the direct cause..." Explicit chaining for better debugging.

---

**Q11.14: Advanced - [Implicit Exception Chaining]**

What happens when you raise a new exception inside an except block without `from`?

A) Original is lost
B) New exception has __context__ set to original (implicit chaining)
C) Both are raised
D) Error

**Answer: B**

**Explanation:**
Without explicit `from`, Python still chains implicitly via `__context__`. Traceback shows: "During handling of X, another exception occurred: Y". Use `raise X from None` to suppress chaining.

---

**Q11.15: Intermediate - [Custom Exceptions]**

How do you create a custom exception?

A) `class MyError = Exception`
B) `class MyError(Exception): pass`
C) `exception MyError:`
D) `def MyError(Exception):`

**Answer: B**

**Explanation:**
Custom exceptions inherit from `Exception` (or a more specific exception). Minimal definition just needs `pass`. Add `__init__` for custom attributes. Naming convention: end with "Error" or "Exception".

---

**Q11.16: Intermediate - [Custom Exception with Attributes]**

What is the output?
```python
class ValidationError(Exception):
    def __init__(self, field, message):
        self.field = field
        super().__init__(f"{field}: {message}")

try:
    raise ValidationError("age", "must be positive")
except ValidationError as e:
    print(e.field, str(e))
```

A) `age, age: must be positive`
B) `age age: must be positive`
C) Error
D) `ValidationError`

**Answer: B**

**Explanation:**
Custom exception with additional data. `field` stored as attribute. `super().__init__()` sets the message. `e.field` = "age", `str(e)` = "age: must be positive".

---

**Q11.17: Intermediate - [except vs except Exception]**

What's the difference between `except:` and `except Exception:`?

A) No difference
B) `except:` catches BaseException too (KeyboardInterrupt, SystemExit)
C) `except Exception:` is deprecated
D) `except:` is faster

**Answer: B**

**Explanation:**
Bare `except:` catches EVERYTHING including KeyboardInterrupt (Ctrl+C) and SystemExit. `except Exception:` lets these through. Generally, never use bare `except:` — it prevents normal program termination.

---

**Q11.18: Basic - [Context Manager Purpose]**

What problem do context managers solve?

A) Managing configuration
B) Ensuring cleanup code runs even if exceptions occur
C) Managing memory
D) Context switching

**Answer: B**

**Explanation:**
Context managers guarantee cleanup. Files get closed, locks get released, connections terminate — even if exceptions occur. The `with` statement enforces this pattern. Before context managers, try/finally was needed everywhere.

---

**Q11.19: Basic - [with Statement]**

What is the output?
```python
with open('test.txt', 'w') as f:
    f.write('hello')
print(f.closed)
```

A) `True`
B) `False`
C) Error
D) `None`

**Answer: A**

**Explanation:**
`with` calls `__exit__` when block ends (normally or via exception). For files, `__exit__` closes the file. After the block, `f.closed` is True. No explicit `f.close()` needed.

---

**Q11.20: Intermediate - [Context Manager Protocol]**

What methods define a context manager?

A) `__start__` and `__stop__`
B) `__enter__` and `__exit__`
C) `__open__` and `__close__`
D) `__with__` and `__end__`

**Answer: B**

**Explanation:**
`__enter__(self)` is called at `with` start, returns value for `as` clause. `__exit__(self, exc_type, exc_val, exc_tb)` is called at end. Receives exception info if one occurred.

---

**Q11.21: Intermediate - [__enter__ and __exit__]**

What is the output?
```python
class Manager:
    def __enter__(self):
        print("Enter")
        return self
    
    def __exit__(self, *args):
        print("Exit")
        return False

with Manager() as m:
    print("Inside")
```

A) `Enter, Inside, Exit`
B) `Inside, Enter, Exit`
C) `Enter, Exit, Inside`
D) `Inside` only

**Answer: A**

**Explanation:**
`with` calls `__enter__` first (prints "Enter"), returns self assigned to `m`. Block runs (prints "Inside"). Then `__exit__` (prints "Exit"). Order: Enter → Inside → Exit.

---

**Q11.22: Intermediate - [__exit__ Parameters]**

What do the parameters of `__exit__` represent?

A) Random information
B) Exception type, value, and traceback (None if no exception)
C) Context information
D) User data

**Answer: B**

**Explanation:**
`__exit__(self, exc_type, exc_val, exc_tb)`: `exc_type` = exception class, `exc_val` = exception instance, `exc_tb` = traceback. All None if block completed normally. Allows handling/suppressing exceptions.

---

**Q11.23: Advanced - [Suppressing Exceptions]**

What is the output?
```python
class Suppress:
    def __enter__(self):
        return self
    
    def __exit__(self, exc_type, exc_val, exc_tb):
        return True  # Suppress exception

with Suppress():
    raise ValueError("Test")

print("Continued")
```

A) ValueError raised
B) `Continued`
C) Nothing
D) Error

**Answer: B**

**Explanation:**
If `__exit__` returns True, the exception is suppressed (not re-raised). The program continues after the `with` block. Return False or None to let exception propagate. Use carefully — suppressing exceptions can hide bugs.

---

**Q11.24: Intermediate - [contextlib.contextmanager]**

What does `@contextmanager` do?

A) Manages contexts automatically
B) Converts a generator function into a context manager
C) Creates manager classes
D) Documents context

**Answer: B**

**Explanation:**
`@contextmanager` lets you write context managers as generators — simpler than classes. Code before `yield` is `__enter__`, code after is `__exit__`. The yielded value becomes the `as` variable.

---

**Q11.25: Intermediate - [@contextmanager Example]**

What is the output?
```python
from contextlib import contextmanager

@contextmanager
def tag(name):
    print(f"<{name}>")
    yield
    print(f"</{name}>")

with tag("p"):
    print("Content")
```

A) `<p>, Content, </p>`
B) `Content, <p>, </p>`
C) `<p>, </p>, Content`
D) Error

**Answer: A**

**Explanation:**
Before yield: print `<p>`. yield pauses. Block runs: print "Content". After yield: print `</p>`. The generator-based context manager is much cleaner than writing a class.

---

**Q11.26: Advanced - [@contextmanager with Exception]**

What happens if an exception occurs inside a `@contextmanager` block?

A) Post-yield code doesn't run
B) Exception is raised at yield point, must handle with try/except around yield
C) Exception is lost
D) Python handles it automatically

**Answer: B**

**Explanation:**
If exception occurs, it's raised at the `yield` point. Use try/finally around yield for guaranteed cleanup:
```python
try:
    yield
finally:
    cleanup()
```
Without this, cleanup might not happen on exception.

---

**Q11.27: Intermediate - [contextlib.suppress]**

What does `contextlib.suppress(Exception)` do?

A) Raises Exception
B) Suppresses (ignores) specified exceptions that occur in the block
C) Logs exceptions
D) Converts exceptions

**Answer: B**

**Explanation:**
`with suppress(FileNotFoundError): os.remove(file)` — if file doesn't exist, no error. Cleaner than try/except/pass for ignored exceptions. Multiple types: `suppress(A, B)`.

---

**Q11.28: Intermediate - [contextlib.redirect_stdout]**

What does `contextlib.redirect_stdout` do?

A) Redirects print output to a different file or buffer
B) Stops stdout
C) Creates new stdout
D) Logs stdout

**Answer: A**

**Explanation:**
```python
with redirect_stdout(file):
    print("Goes to file")
```
Temporarily redirects stdout. Useful for capturing print output in tests or redirecting to files. `redirect_stderr` does the same for stderr.

---

**Q11.29: Intermediate - [ExitStack]**

What is `contextlib.ExitStack` for?

A) Stack data structure
B) Managing dynamic number of context managers programmatically
C) Exit handling
D) Stack traces

**Answer: B**

**Explanation:**
`ExitStack` manages contexts dynamically. Useful when the number of context managers isn't known at write-time:
```python
with ExitStack() as stack:
    files = [stack.enter_context(open(f)) for f in filenames]
```
All get cleaned up properly.

---

**Q11.30: Basic - [File Context Manager]**

What's the advantage of `with open()` over manual `f.close()`?

A) Faster
B) File is guaranteed to close even if exception occurs
C) Uses less memory
D) No advantage

**Answer: B**

**Explanation:**
`with open()` uses context manager. If exception occurs in the block, file still closes. Manual approach requires try/finally. `with` is cleaner and safer — always use it for files.

---

**Q11.31: Intermediate - [Multiple Context Managers]**

What is the output?
```python
with open('a.txt', 'w') as a, open('b.txt', 'w') as b:
    a.write('A')
    b.write('B')
```

A) Error: can't have two
B) Both files opened and closed properly
C) Only first file handled
D) Need nested with statements

**Answer: B**

**Explanation:**
Multiple context managers in one `with` — comma-separated. Both are managed. If one fails during setup, already-entered ones exit. Cleaner than nested `with` statements.

---

**Q11.32: Intermediate - [Lock as Context Manager]**

Why is `threading.Lock` a context manager?

A) It isn't
B) Ensures lock is released even if exception occurs in critical section
C) For locking files
D) For security

**Answer: B**

**Explanation:**
```python
with lock:
    critical_section()
```
Lock is acquired on enter, released on exit — even with exceptions. Prevents deadlocks from forgotten releases. Most synchronization primitives are context managers.

---

**Q11.33: Intermediate - [traceback Module]**

What does `traceback.print_exc()` do?

A) Raises an exception
B) Prints current exception's traceback to stderr
C) Creates a traceback
D) Exits the program

**Answer: B**

**Explanation:**
Inside an except block, `traceback.print_exc()` prints the full traceback. Useful for logging while continuing execution. `traceback.format_exc()` returns it as a string instead.

---

**Q11.34: Advanced - [sys.exc_info()]**

What does `sys.exc_info()` return?

A) Exception message
B) Tuple of (type, value, traceback) for current exception
C) All exceptions
D) Exception count

**Answer: B**

**Explanation:**
`sys.exc_info()` returns `(exc_type, exc_value, exc_traceback)` for the exception being handled. Returns `(None, None, None)` if no exception. Used for introspection and passing exception info.

---

**Q11.35: Intermediate - [Exception Args]**

What is the output?
```python
try:
    raise ValueError("error", 42)
except ValueError as e:
    print(e.args)
```

A) `('error', 42)`
B) `error`
C) `42`
D) Error

**Answer: A**

**Explanation:**
`Exception.args` is a tuple of arguments passed to the exception. Here: `("error", 42)`. `str(e)` concatenates them. Access individual: `e.args[0]`, `e.args[1]`.

---

**Q11.36: Intermediate - [Assert Statement]**

What is the output?
```python
x = 5
assert x > 0, "x must be positive"
print("Passed")
```

A) `AssertionError: x must be positive`
B) `Passed`
C) `True`
D) Nothing

**Answer: B**

**Explanation:**
`assert condition, message` raises AssertionError if condition is False. Here x > 0 is True, so no exception. "Passed" prints. Asserts are for debugging, can be disabled with `-O` flag.

---

**Q11.37: Intermediate - [Assert AssertionError]**

What is the output?
```python
assert False, "This failed"
```

A) Nothing
B) `AssertionError: This failed`
C) `False`
D) `This failed`

**Answer: B**

**Explanation:**
`assert False` always raises AssertionError. The message becomes the exception's argument. Uses: verifying invariants, preconditions, postconditions during development. Disabled with `python -O`.

---

**Q11.38: Advanced - [Warning vs Exception]**

What's the difference between warnings and exceptions?

A) Same thing
B) Warnings don't stop execution by default; exceptions do
C) Exceptions are for development only
D) Warnings are silent

**Answer: B**

**Explanation:**
`warnings.warn("message")` issues a warning — logs but continues. Exceptions halt unless caught. Use warnings for deprecation, non-fatal issues. Configure warning handling with `warnings.filterwarnings()`.

---

**Q11.39: Intermediate - [asyncio and Exceptions]**

How should exceptions be handled in async code?

A) Same as sync code
B) Use try/except, but be aware of where exceptions propagate from tasks
C) Different syntax
D) Exceptions don't occur in async

**Answer: B**

**Explanation:**
Async try/except works normally. But: exceptions in `asyncio.create_task()` don't propagate until task is awaited. Use `asyncio.gather(return_exceptions=True)` to collect exceptions without stopping.

---

**Q11.40: Basic - [Common Exceptions]**

Match exception to cause: accessing dict with missing key.

A) IndexError
B) KeyError
C) ValueError
D) TypeError

**Answer: B**

**Explanation:**
`dict['missing_key']` raises KeyError. IndexError is for sequences (lists). ValueError is for wrong value (right type). TypeError is for wrong type. Knowing common exceptions helps debugging.

---

**Q11.41: Basic - [IndexError]**

What causes IndexError?

A) Missing dictionary key
B) Index out of range for a sequence
C) Wrong type of index
D) Divide by zero

**Answer: B**

**Explanation:**
`list[100]` when list has fewer items raises IndexError. Negative indices also raise it if too negative. Check `len()` or use try/except or `.get()` equivalent patterns.

---

**Q11.42: Basic - [TypeError]**

What causes TypeError?

A) Type conversion failure
B) Operation on incompatible types or wrong argument count
C) Type doesn't exist
D) Memory error

**Answer: B**

**Explanation:**
`"a" + 1` (can't add str and int), `func(x, y)` when func takes one arg, calling non-callable. TypeError = wrong types being used together or wrong number of arguments.

---

**Q11.43: Basic - [ValueError]**

What causes ValueError?

A) Value doesn't exist
B) Function receives argument of right type but wrong value
C) Missing value
D) Value is None

**Answer: B**

**Explanation:**
`int("abc")` — string is right type, but "abc" isn't a valid integer value. `math.sqrt(-1)` — float but negative. Right type, inappropriate value.

---

**Q11.44: Intermediate - [AttributeError]**

What causes AttributeError?

A) Missing class
B) Accessing attribute that doesn't exist on object
C) Wrong attribute type
D) Attribute is private

**Answer: B**

**Explanation:**
`obj.nonexistent_method()` or `obj.missing_attr`. The object doesn't have that attribute. Check with `hasattr(obj, 'attr')` or use `getattr(obj, 'attr', default)`.

---

**Q11.45: Intermediate - [ImportError/ModuleNotFoundError]**

What's the difference between ImportError and ModuleNotFoundError?

A) Same thing
B) ModuleNotFoundError is subclass of ImportError for when module doesn't exist
C) ImportError is deprecated
D) ModuleNotFoundError is for packages

**Answer: B**

**Explanation:**
`ModuleNotFoundError` (Python 3.6+) inherits from `ImportError`. It's raised when module isn't found. `ImportError` covers broader import problems (including module not found). Catching `ImportError` catches both.

---

**Q11.46: Advanced - [Exception Groups]**

What are exception groups (Python 3.11+)?

A) Groups of related exception classes
B) A way to raise and handle multiple unrelated exceptions simultaneously
C) Exception categories
D) Testing feature

**Answer: B**

**Explanation:**
`ExceptionGroup` bundles multiple exceptions together. Raised when multiple tasks fail (async). Handle with `except* SomeError:` which handles matching exceptions from the group. New in Python 3.11.

---

**Q11.47: Advanced - [Exception Notes]**

What is `exception.add_note()` (Python 3.11+)?

A) Documentation
B) Adds contextual information to an exception after creation
C) Logs the exception
D) Creates a notebook

**Answer: B**

**Explanation:**
`e.add_note("Additional context")` adds notes displayed in traceback. Useful when catching and re-raising: add context about what was being attempted. Notes appear after the exception message.

---

**Q11.48: Intermediate - [Context Manager for Timing]**

Which is a valid timing context manager?
```python
# A
class Timer:
    def __enter__(self):
        self.start = time.time()
    def __exit__(self, *args):
        print(time.time() - self.start)

# B
@contextmanager
def timer():
    start = time.time()
    yield
    print(time.time() - start)
```

A) Only A
B) Only B
C) Both work
D) Neither works

**Answer: C**

**Explanation:**
Both are valid approaches. Class-based (A) stores start in self. Generator-based (B) uses local variable. Generator is more concise. Both print elapsed time after block completes.

---

**Q11.49: Intermediate - [Context Manager Returning Value]**

What is the output?
```python
from contextlib import contextmanager

@contextmanager
def provide_value():
    yield 42

with provide_value() as value:
    print(value)
```

A) `None`
B) `42`
C) `provide_value`
D) Error

**Answer: B**

**Explanation:**
The yielded value becomes the `as` variable. `yield 42` → `value = 42`. The context manager can provide resources, connections, configuration, or just values.

---

**Q11.50: Advanced - [Async Context Managers]**

What methods define an async context manager?

A) `__enter__` and `__exit__`
B) `__aenter__` and `__aexit__`
C) `async_enter` and `async_exit`
D) Same as sync with await

**Answer: B**

**Explanation:**
Async context managers use `__aenter__` and `__aexit__` (returning awaitables). Used with `async with`. For I/O operations that need async setup/teardown. Example: `async with aiohttp.ClientSession()`.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 15 | 30% |
| Intermediate | 28 | 56% |
| Advanced | 7 | 14% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- try/except/else/finally mechanics
- Exception hierarchy (BaseException, Exception)
- Re-raising and exception chaining
- Custom exceptions
- Context manager protocol (__enter__, __exit__)
- contextlib module (@contextmanager, suppress, ExitStack)
- Common built-in exceptions
- traceback handling
- Python 3.11+ features (exception groups, notes)
