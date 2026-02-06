# Chapter 12: Exception Handling

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `try...except` blocks, `else`/`finally` clauses, Built-in Exceptions, Custom Exceptions, Exception Chaining (`raise from`), Traceback objects.

---

**Q12.1: Basic - [Try Except Syntax]**

Which keyword catches an exception?

A) `catch`
B) `except`
C) `handle`
D) `error`

**Answer: B**

**Explanation:**
Python uses `try...except` blocks. (`catch` is used in Java/C++).

---

**Q12.2: Intermediate - [Else Clause]**

The `else` block in a `try` statement runs:

A) If an exception is raised.
B) If *no* exception is raised in the `try` block.
C) Always.
D) Instead of `finally`.

**Answer: B**

**Explanation:**
The `else` block executes only if the `try` block completes successfully without raising an exception. It is useful for code that should run only on success but shouldn't be inside the `try` (to avoid accidentally catching exceptions from that code).

---

**Q12.3: Advanced - [Exception Chaining]**

`raise ValueError from e` sets:

A) `__cause__` on the new exception.
B) `__context__` on the new exception.
C) `__parent__`.
D) Nothing.

**Answer: A**

**Explanation:**
`raise ... from ...` (explicit chaining) sets the `__cause__` attribute, indicating the new exception was deliberately raised as a consequence of the original one (which is stored in `e`).

---

**Q12.4: Basic - [Catching All]**

To catch *any* standard runtime error, catch:

A) `BaseException`
B) `Exception`
C) `Error`
D) `RuntimeError`

**Answer: B**

**Explanation:**
`Exception` is the base class for all built-in, non-system-exiting exceptions. `BaseException` includes `SystemExit` and `KeyboardInterrupt`, which you usually shouldn't catch.

---

**Q12.5: Intermediate - [Finally Execution]**

If `return` is executed inside a `try` block, does `finally` run?

A) No.
B) Yes, before the function returns.
C) Yes, after the function returns.
D) Depends on the exception.

**Answer: B**

**Explanation:**
`finally` is guaranteed to run. If there is a return statement, `finally` executes right before the control flow leaves the function.

---

**Q12.6: Advanced - [Reraising]**

How do you re-raise the active exception inside an `except` block?

A) `raise Exception`
B) `raise self`
C) `raise`
D) `raise current`

**Answer: C**

**Explanation:**
A bare `raise` keyword inside an exception handler re-raises the currently active exception, preserving the original traceback.

---

**Q12.7: Basic - [SystemExit]**

Is `SystemExit` caught by `except Exception:`?

A) Yes.
B) No.
C) Only on Linux.
D) Only if explicitly named.

**Answer: B**

**Explanation:**
`SystemExit` inherits from `BaseException`, not `Exception`, so it bypasses standard catch-all blocks. This allows scripts to exit cleanly even inside generic error handlers.

---

**Q12.8: Intermediate - [Argument Exception]**

Exceptions in Python can carry arguments. Where are they stored?

A) `exc.message`
B) `exc.args`
C) `exc.params`
D) `exc.data`

**Answer: B**

**Explanation:**
`exc.args` is a tuple containing arguments passed to the exception constructor.

---

**Q12.9: Advanced - [Context vs Cause]**

If an exception occurs *inside* an `except` block (while handling another exception):

A) The original exception is lost.
B) The new exception has `__context__` set to the original.
C) Python crashes.
D) The new exception has `__cause__` set to the original.

**Answer: B**

**Explanation:**
Implicit chaining sets `__context__`. This shows "During handling of the above exception, another exception occurred" in tracebacks. `__cause__` is for explicit chaining (`from`).

---

**Q12.10: Expert - [Traceback Object]**

To get the current traceback object without an exception variable:

A) `sys.exc_info()[2]`
B) `sys.traceback`
C) `traceback.current()`
D) `Exception.traceback`

**Answer: A**

**Explanation:**
`sys.exc_info()` returns `(type, value, traceback)`.

---

**Q12.11: Basic - [ValueError]**

`int("hello")` raises:

A) `TypeError`
B) `NameError`
C) `ValueError`
D) `SyntaxError`

**Answer: C**

**Explanation:**
It raises `ValueError` because the type is correct (string) but the content (value) is invalid for conversion to integer.

---

**Q12.12: Intermediate - [Custom Exception]**

To create a custom exception, inherit from:

A) `object`
B) `Error`
C) `Exception`
D) `BaseException`

**Answer: C**

**Explanation:**
Custom exceptions should inherit from `Exception` (or a subclass of it) to be compatible with normal error handling practices.

---

**Q12.13: Advanced - [Suppressing Context]**

`raise NewError from None` does what?

A) Raises NewError and hides the original exception (suppresses context).
B) Raises NewError with None as cause.
C) Is invalid syntax.
D) Clears the traceback.

**Answer: A**

**Explanation:**
It explicitly sets `__cause__` to None and `__suppress_context__` to True, telling the traceback display machinery not to show the original exception.

---

**Q12.14: Basic - [AttributeError]**

Accessing `obj.missing_method()` raises:

A) `NameError`
B) `AttributeError`
C) `KeyError`
D) `MethodError`

**Answer: B**

**Explanation:**
Raised when an attribute reference or assignment fails.

---

**Q12.15: Intermediate - [Multiple Except]**

`except (TypeError, ValueError):` catches:

A) Either TypeError or ValueError.
B) Both at the same time (impossible).
C) A tuple of errors.
D) Invalid syntax.

**Answer: A**

**Explanation:**
A tuple matches any of the listed exceptions.

---

**Q12.16: Advanced - [Exception Group]**

(Python 3.11+) `ExceptionGroup` allows:

A) Grouping exceptions in a module.
B) Raising multiple unrelated exceptions simultaneously.
C) Organizing exceptions by priority.
D) Threading exceptions.

**Answer: B**

**Explanation:**
Used (often in `asyncio`) to propagate multiple concurrent errors. Handled via `except*` (exception group filter).

---

**Q12.17: Expert - [Warn vs Raise]**

`warnings.warn("msg")`:

A) Stops execution.
B) Prints a message to stderr (usually) effectively, but execution continues.
C) Raises an exception immediately.
D) Logs to file.

**Answer: B**

**Explanation:**
Warnings are distinct from exceptions. They indicate potential issues but don't halt control flow unless configured to do so (error filter).

---

**Q12.18: Intermediate - [KeyError vs IndexError]**

`lst = [1]; lst[5]` raises `IndexError`. `d = {}; d[5]` raises `KeyError`.
`lst.pop()` on empty list raises:

A) `ValueError`
B) `IndexError`
C) `KeyError`
D) `None`

**Answer: B**

**Explanation:**
`pop` from empty list raises `IndexError`.

---

**Q12.19: Basic - [BaseException]**

Which is NOT a subclass of `Exception`?

A) `ValueError`
B) `KeyboardInterrupt`
C) `OsError`
D) `StopIteration`

**Answer: B**

**Explanation:**
`KeyboardInterrupt` inherits directly from `BaseException` so that a "catch-all" `except Exception` doesn't prevent you from stopping the program with Ctrl+C.

---

**Q12.20: Advanced - [Excepthook]**

`sys.excepthook` allows you to:

A) Hook into every exception raised.
B) Customize the handling of uncaught exceptions (e.g. log to file instead of stderr) just before program exit.
C) Prevent exceptions.
D) Edit exception messages.

**Answer: B**

**Explanation:**
It is the top-level exception handler called when an exception propagates all the way to the top of the interpreter stack.

---

**Q12.21: Intermediate - [Raise Constructor]**

`raise ValueError` (class) vs `raise ValueError()` (instance).

A) First is invalid.
B) Both are valid; Python instantiates the class implicitly with no args.
C) Second is invalid.
D) Different behavior.

**Answer: B**

**Explanation:**
Raising a class `raise TypeError` is shorthand for `raise TypeError()`.

---

**Q12.22: Expert - [Traceback Frames]**

Traceback objects form a linked list of:

A) Frame objects (`tb_frame`).
B) Code objects.
C) Strings.
D) Errors.

**Answer: A**

**Explanation:**
`tb_next` points to the next traceback object, and `tb_frame` points to the execution frame where the exception occurred/passed through.

---

**Q12.23: Basic - [AssertionError]**

`assert False` raises:

A) `AssertionError`
B) `FalseError`
C) `ValueError`
D) Nothing if optimized.

**Answer: A**

**Explanation:**
Usage `assert condition` raises `AssertionError` if condition is false.

---

**Q12.24: Intermediate - [Finally Return]**

If `try` returns 1 and `finally` returns 2. The function returns:

A) 1
B) 2
C) Both.
D) Error.

**Answer: B**

**Explanation:**
The return value from `finally` swallows/overrides any return value (or exception) from the `try` block.

---

**Q12.25: Advanced - [Try-Except-Else-Finally Order]**

The correct order of blocks is:

A) try, except, finally, else
B) try, except, else, finally
C) try, else, except, finally
D) try, finally, except, else

**Answer: B**

**Explanation:**
`try` -> `except` (if error) -> `else` (if no error) -> `finally` (always).

---

**Q12.26: Expert - [RecursionError]**

`RecursionError` inherits from:

A) `RuntimeError`
B) `MemoryError`
C) `SystemError`
D) `OverflowError`

**Answer: A**

**Explanation:**
It indicates the maximum recursion depth has been exceeded, which is a runtime limit invocation.

---

**Q12.27: Basic - [Raising NotImplemented]**

Inside an abstract method or one that child classes must override, you should raise:

A) `NotImplemented`
B) `NotImplementedError`
C) `AbstractError`
D) `None`

**Answer: B**

**Explanation:**
`NotImplemented` is a special singleton value (used in binary ops). `NotImplementedError` is the exception.

---

**Q12.28: Intermediate - [EAFP]**

"EAFP" stands for:

A) Easy Access For Python.
B) Easier to Ask for Forgiveness than Permission.
C) Errors Are For Programmers.
D) Except All Failed Processes.

**Answer: B**

**Explanation:**
Python coding style that assumes valid keys/attributes exist and catches exceptions if the assumption proves false, rather than checking beforehand (`LBYL` - Look Before You Leap).

---

**Q12.29: Advanced - [UnboundLocalError]**

`UnboundLocalError` is a subclass of:

A) `NameError`
B) `ValueError`
C) `AttributeError`
D) `RuntimeError`

**Answer: A**

**Explanation:**
It occurs when a reference is made to a local variable that hasn't been assigned a value yet. Since scoping is name-resolution related, it is a `NameError`.

---

**Q12.30: Expert - [MemoryError Recovery]**

Can you catch `MemoryError` and recover?

A) Never.
B) Yes, sometimes, if you can delete objects to free memory in the handler.
C) Yes, Python automatically expands memory.
D) No, the OS kills the process.

**Answer: B**

**Explanation:**
It is possible to catch `MemoryError`. If the program can release references (e.g. clear a cache) in the `except` block, it may continue running (though tricky in practice).

---

**Q12.31: Intermediate - [Loop Else Exception]**

If the `else` block of a loop raises an exception, is it caught by an `except` block wrapping the loop?

A) No.
B) Yes.
C) Only if `break` was used.
D) Loops don't have `else`.

**Answer: B**

**Explanation:**
The `else` block is part of the loop structure, which is inside the `try` block. Any exception raised there propagates up to the `except` handler.

---

**Q12.32: Advanced - [Yielding in Finally]**

What happens if a generator yields inside a `finally` block?

A) Python 3 forbids it (SyntaxError).
B) It works but swallows exceptions.
C) It works normally (since Python 3.8).
D) It pauses the cleanup.

**Answer: C**

**Explanation:**
Prior to Python 3.8, `yield` in `finally` was not allowed. Now it is permitted, keeping the exception active (suspended) while yielding.

---

**Q12.33: Basic - [ImportError]**

`ModuleNotFoundError` is a subclass of:

A) `ImportError`
B) `NameError`
C) `SystemError`
D) `LoadError`

**Answer: A**

**Explanation:**
It is a more specific error meant to indicate that the module could not be located, whereas `ImportError` can happen for other reasons (e.g. wrapper issues).

---

**Q12.34: Expert - [Exception Args Mutation]**

If you modify `e.args` inside an exception handler:

A) It changes the exception message when printed.
B) It has no effect (immutable).
C) It raises `TypeError`.
D) It changes the type.

**Answer: A**

**Explanation:**
`args` is a tuple, but you can assign a new tuple to `e.args`. The default `__str__` method uses `args` to format the message.

---

**Q12.35: Intermediate - [KeyboardInterrupt Handling]**

To ensure a critical cleanup runs even if user presses Ctrl+C:

A) Use `except Exception`.
B) Use `try...finally`.
C) Use `atexit`.
D) Disable interrupts.

**Answer: B**

**Explanation:**
`finally` blocks execute even on `KeyboardInterrupt` (or any `BaseException`).

---

**Q12.36: Advanced - [Try-Except Scope]**

Variables defined in a `try` block:

A) Are local to the `try` block.
B) Are available in the `except` / `else` / `finally` blocks (if assigned before error).
C) Are deleted if exception occurs.
D) Cannot be accessed outside.

**Answer: B**

**Explanation:**
Blocks (try, if, for) do not define scopes in Python. Variables assigned are visible in the surrounding function scope.

---

**Q12.37: Basic - [ZeroDivisionError]**

`1.0 / 0.0` raises:

A) `ZeroDivisionError`
B) `ValueError`
C) `FloatingPointError`
D) `Infinity`

**Answer: A**

**Explanation:**
Standard exception for division by zero.

---

**Q12.38: Intermediate - [Raise Missing]**

`raise` without an active exception:

A) Raises `RuntimeError`.
B) Raises `None`.
C) Does nothing.
D) Raises `SystemError`.

**Answer: A**

**Explanation:**
"No active exception to reraise" is a `RuntimeError`.

---

**Q12.39: Advanced - [Exception Hierarchy]**

`OSError` is the parent of:

A) `FileExistsError`, `FileNotFoundError`, `PermissionError`.
B) `IOError`, `ValueError`.
C) `SystemExit`.
D) `socket.error` only.

**Answer: A**

**Explanation:**
Since Python 3.3, all OS-related errors were unified under `OSError`, with specific subclasses for common scenarios.

---

**Q12.40: Expert - [Traceback Limit]**

`sys.tracebacklimit` controls:

A) The max number of frames printed in a traceback.
B) The recursion depth.
C) The amount of memory for exceptions.
D) Nothing.

**Answer: A**

**Explanation:**
Setting this integer variable affects how many levels of traceback are printed to stderr. Setting it to 0 suppresses tracebacks.

---

**Q12.41: Intermediate - [Assert Tuple]**

`assert (x > 0, "Error")`:

A) Raises AssertionError with message "Error" if x <= 0.
B) Is always True (and thus useless) because non-empty tuples are truthy.
C) is SyntaxError.
D) Checks both conditions.

**Answer: B**

**Explanation:**
Common pitfall! `assert (condition, message)` asserts the *tuple* `(condition, message)`, which is always True. Remove parentheses: `assert condition, message`.

---

**Q12.42: Basic - [IndentationError]**

`IndentationError` inherits from:

A) `SyntaxError`
B) `TabError`
C) `ValueError`
D) `SystemError`

**Answer: A**

**Explanation:**
It is a syntax error regarding whitespace.

---

**Q12.43: Advanced - [Exception Attributes]**

`UnicodeDecodeError` contains attributes like:

A) `object`, `start`, `end`, `reason`.
B) `string`, `index`.
C) `line`, `col`.
D) `code`.

**Answer: A**

**Explanation:**
It provides details to help identify exactly which byte sequence failed and why.

---

**Q12.44: Expert - [Chaining Cycle]**

If `raise e2 from e1` and `e1.__context__` is `e2` (cycle):

A) Python detects it and prints `[Previous line repeated...]`.
B) Python hangs printing traceback.
C) Max recursion error.
D) Traceback ignores one.

**Answer: A**

**Explanation:**
The traceback printing machinery has cycle detection to prevent infinite output loops.

---

**Q12.45: Intermediate - [Catching Multiple specific]**

If `except A:` and `except B:` both match (e.g. B inherits from A), and both are present:

A) The first one defined (`except A`) runs.
B) The most specific one runs.
C) Both run.
D) Error.

**Answer: A**

**Explanation:**
Python checks `except` clauses top-down. Put specific exceptions *before* general ones.

---

**Q12.46: Basic - [Try Finally Return]**

If `try` block raises exception, and `finally` returns a value:

A) The exception activates *after* the return.
B) The exception is swallowed (lost).
C) The exception propagates.
D) Crash.

**Answer: B**

**Explanation:**
A `return` (or `break`/`continue`) in `finally` discards any pending exception.

---

**Q12.47: Advanced - [Warning Filter]**

To turn all warnings into errors:

A) `python -W error`
B) `warnings.simplefilter("error")`
C) Both A and B.
D) `sys.warnings = 'error'`

**Answer: C**

**Explanation:**
Can be set via command line or programmatically.

---

**Q12.48: Expert - [Sys Last Value]**

`sys.last_value` stores:

A) The last value returned.
B) The exception instance of the *last uncaught* exception.
C) The last usage of memory.
D) Last exit code.

**Answer: B**

**Explanation:**
For interactive sessions, `sys.last_type`, `sys.last_value`, and `sys.last_traceback` store info about the last unhandled exception.

---

**Q12.49: Intermediate - [StopAsyncIteration]**

Raised by:

A) `__anext__` to signal end of async iterator.
B) `StopIteration` in async.
C) `await`.
D) `async for` automatically.

**Answer: A**

**Explanation:**
Analogous to `StopIteration` but for asynchronous iterators.

---

**Q12.50: Basic - [Exception String]**

`str(Exception("msg"))` returns:

A) `"msg"`
B) `"Exception: msg"`
C) traceback.
D) `repr`.

**Answer: A**

**Explanation:**
The string representation is typically the message passed to the constructor.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
