# Chapter 11: Context Managers

**Target MCQs**: 40-50
**Current Batch**: 1-30
**Topics Covered**: `with` statement, `__enter__`/`__exit__` protocol, `contextlib` utilities (`contextmanager`, `closing`, `suppress`), `ExitStack`, Error handling.

---

**Q11.1: Basic - [With Statement Purpose]**

The primary purpose of the `with` statement in Python is:

A) To create a new thread.
B) To manage resources (setup and teardown) reliably, ensuring cleanup even if errors occur.
C) To import modules locally.
D) To loop over a file.

**Answer: B**

**Explanation:**
The `with` statement simplifies exception handling and finalization by encapsulating standard uses of `try...finally` into context managers (e.g., closing files, releasing locks).

---

**Q11.2: Intermediate - [Context Manager Protocol]**

Which two methods does an object need to implement to be a context manager?

A) `__open__` and `__close__`
B) `__start__` and `__stop__`
C) `__enter__` and `__exit__`
D) `__init__` and `__del__`

**Answer: C**

**Explanation:**
The Context Manager protocol consists of `__enter__` (setup) and `__exit__` (teardown).

---

**Q11.3: Advanced - [Enter Return Value]**

In `with expression as var:`, `var` gets the value returned by:

A) `expression`
B) `expression.__init__()`
C) `expression.__enter__()`
D) `expression.__exit__()`

**Answer: C**

**Explanation:**
The object returned by the `__enter__()` method is bound to the target variable specified after `as`. It is *not* necessarily the context manager object itself (though it often is).

---

**Q11.4: Basic - [Contextlib Decorator]**

`@contextlib.contextmanager` turns a generator function into a context manager. The generator must yield:

A) Exactly once.
B) As many times as needed.
C) Never.
D) Twice (start and end).

**Answer: A**

**Explanation:**
The generator should yield exactly once. The code before the yield is the setup (`__enter__`), the yielded value is bound to the `as` variable, and the code after the yield is the teardown (`__exit__`).

---

**Q11.5: Intermediate - [Exit Arguments]**

The `__exit__` method receives arguments related to:

A) The execution time.
B) The exception type, value, and traceback (if an exception occurred).
C) The file descriptors.
D) The `__enter__` return value.

**Answer: B**

**Explanation:**
`__exit__(self, exc_type, exc_value, traceback)` receives details of any exception raised within the `with` block. If no exception occurred, all are `None`.

---

**Q11.6: Advanced - [Suppressing Exceptions]**

To suppress an exception raised in the `with` block, `__exit__` must return:

A) `False`
B) `None`
C) A Truthy value (e.g., `True`).
D) The exception object.

**Answer: C**

**Explanation:**
If `__exit__` returns a true value, the exception is considered handled and execution resumes after the `with` statement. If it returns `False` or `None`, the exception is re-raised.

---

**Q11.7: Basic - [File Context]**

What happens if an error occurs inside `with open('file.txt') as f:`?

A) The file remains open.
B) The file is closed automatically.
C) `f` becomes None.
D) The error is ignored.

**Answer: B**

**Explanation:**
The built-in file object's `__exit__` method calls `f.close()`, ensuring the file is closed regardless of success or failure.

---

**Q11.8: Intermediate - [Contextlib Suppress]**

`with contextlib.suppress(FileNotFoundError): os.remove('file')` is equivalent to:

A) `try: os.remove('file'); except FileNotFoundError: pass`
B) `if os.exists('file'): os.remove('file')`
C) `os.remove('file', check=False)`
D) A loop until file is removed.

**Answer: A**

**Explanation:**
`suppress` explicitly ignores specified exceptions, providing a readable alternative to `try...expect...pass`.

---

**Q11.9: Advanced - [ExitStack]**

`contextlib.ExitStack` is used for:

A) Tracing program exit.
B) Managing a dynamic number of context managers or stack-based cleanup.
C) Exiting the interpreter securely.
D) Memory stack visualization.

**Answer: B**

**Explanation:**
`ExitStack` allows you to programmatically enter context managers and ensures their `__exit__` methods are called in reverse order, even if exceptions occur. Useful when you don't know how many contexts you need in advance (e.g. opening a list of files).

---

**Q11.10: Expert - [Reusing Generators]**

A context manager created with `@contextmanager` is:

A) Reusable (can be used in multiple `with` statements).
B) Single-use only.
C) Thread-safe.
D) A singleton.

**Answer: B**

**Explanation:**
Since it relies on a generator which can only be consumed once (yield once), it cannot be reused. You must call the function again to create a fresh context manager.

---

**Q11.11: Basic - [Lock Context]**

`with threading.Lock():` ensures:

A) The lock is created.
B) The lock is acquired at start and released at end.
C) The thread sleeps.
D) Deadlock prevention.

**Answer: B**

**Explanation:**
Locks support the context manager protocol to `acquire()` on enter and `release()` on exit.

---

**Q11.12: Intermediate - [Closing Utility]**

`contextlib.closing(obj)` is useful for objects that:

A) Have a `.close()` method but do not support the context manager protocol.
B) Need to be deleted.
C) Are files.
D) Are generators.

**Answer: A**

**Explanation:**
It wraps the object and calls `obj.close()` in `__exit__`. Example: `urllib.request.urlopen` (in older versions) or custom classes.

---

**Q11.13: Advanced - [Nested Contexts]**

`with A() as a, B() as b:` is equivalent to:

A) `with A() as a: with B() as b:`
B) `with A(B()) as b:`
C) Parallel execution of A and B.
D) `with B() as b: with A() as a:`

**Answer: A**

**Explanation:**
Python 3.1+ supports multiple context managers in a single `with` statement. They are entered left-to-right and exited right-to-left (nested structure).

---

**Q11.14: Basic - [Redirect Stdout]**

`with contextlib.redirect_stdout(f):` effectively changes:

A) `sys.stdin`
B) `sys.stdout`
C) `sys.stderr`
D) System console.

**Answer: B**

**Explanation:**
It temporarily patches `sys.stdout` to point to `f` during the block.

---

**Q11.15: Intermediate - [Exception Propagation]**

If `__enter__` raises an exception:

A) `__exit__` is called immediately.
B) `__exit__` is NOT called.
C) The `with` block runs anyway.
D) The exception is suppressed.

**Answer: B**

**Explanation:**
If an error occurs during setup (`__enter__`), the context is never successfully established, so `__exit__` is not called.

---

**Q11.16: Advanced - [Generator Context Exception]**

In a `@contextmanager` generator, if an exception occurs in the `with` block:

A) The generator is closed immediately.
B) The exception is thrown into the generator at the point of `yield`.
C) The code after `yield` runs normally.
D) The program crashes without cleanup.

**Answer: B**

**Explanation:**
The exception is injected into the generator. You should wrap the `yield` in a `try...finally` (or `except`) block inside the generator to handle cleanup.

---

**Q11.17: Expert - [ContextDecorator Class]**

Inheriting from `contextlib.ContextDecorator`:

A) Automatically generates `__enter__` and `__exit__`.
B) Allows your class to be used as both a context manager (`with my_obj:`) and a function decorator (`@my_obj`).
C) Makes the class abstract.
D) Optimizes context switching.

**Answer: B**

**Explanation:**
It adds `__call__` which wraps the function in the context manager. (Note: The class must still implement `__enter__` and `__exit__`).

---

**Q11.18: Intermediate - [Null Context]**

`contextlib.nullcontext` (Python 3.7+) is a context manager that:

A) Deletes everything.
B) Does nothing (enter returns value, exit does nothing).
C) Raises errors.
D) Checks for nulls.

**Answer: B**

**Explanation:**
Useful for optional context managers (e.g. `cm = optional_cm if condition else nullcontext()`).

---

**Q11.19: Basic - [Variable Scope]**

Variables defined inside a `with` block:

A) Are local to the block.
B) Leak into the enclosing scope.
C) Are deleted after the block.
D) Are constant.

**Answer: B**

**Explanation:**
Python `with` statements (like `if` and `for`) do not create a new scope. Variables behave as if defined in the function/module.

---

**Q11.20: Advanced - [Async Context Manager]**

An async context manager uses:

A) `async with`, `__aenter__`, `__aexit__`.
B) `with`, `__enter__`, `__exit__`.
C) `await with`, `__enter__`, `__exit__`.
D) `async with`, `__enter__`, `__exit__`.

**Answer: A**

**Explanation:**
Async context managers are designed for `asyncio` and define async setup/teardown methods (`async def __aenter__`).

---

**Q11.21: Expert - [ExitStack Callbacks]**

`stack.callback(func, *args)` registers a callback that runs:

A) Immediately.
B) When the stack unwinds (at the end of `with`), typically for cleanup that isn't a context manager.
C) If an error occurs.
D) Before `__enter__`.

**Answer: B**

**Explanation:**
`ExitStack` allows registering arbitrary cleanup callbacks which are called when the stack closes (like a `finally` block).

---

**Q11.22: Intermediate - [Typing Context Manager]**

The type hint for a context manager yielding an integer is:

A) `ContextManager[int]`
B) `Generator[int]`
C) `Iterator[int]`
D) `With[int]`

**Answer: A**

**Explanation:**
From `typing` (or `contextlib.AbstractContextManager`).

---

**Q11.23: Basic - [Decimal Context]**

`decimal.localcontext()` allows:

A) Setting global decimal precision permanently.
B) Changing decimal precision/flags only within the block.
C) Defining new numbers.
D) Localizing currency.

**Answer: B**

**Explanation:**
It creates a temporary context with modified settings (like precision) that reverts upon exit.

---

**Q11.24: Advanced - [ExitStack Push]**

`stack.push(cm)` on an `ExitStack`:

A) Enters the context manager `cm` immediately.
B) Schedules `cm.__exit__` to be called at the end, assuming `cm.__enter__` was already called manually.
C) Adds `cm` to a list but does nothing.
D) Pops the last context.

**Answer: B**

**Explanation:**
`push` is for context managers (or callbacks) that are already entered or don't need entry. Use `stack.enter_context(cm)` to enter and push.

---

**Q11.25: Intermediate - [Pathlib Open]**

Does `pathlib.Path.open()` return a context manager?

A) No.
B) Yes, it returns a file object, which is a context manager.
C) Only in Python 3.10+.
D) Yes, but you must close it manually.

**Answer: B**

**Explanation:**
`Path.open()` mimics the built-in `open()`.

---

**Q11.26: Expert - [Reentrant Lock]**

`threading.RLock` is reentrant. This means:

A) It can be acquired multiple times by different threads.
B) It can be acquired multiple times by the *same* thread without blocking.
C) It is recursive.
D) It uses context managers.

**Answer: B**

**Explanation:**
A standard `Lock` would deadlock if the holding thread tried to acquire it again. `RLock` allows nested acquisition by the same thread.

---

**Q11.27: Basic - [With As Optional]**

Is the `as var` part mandatory in a `with` statement?

A) Yes.
B) No.
C) Only if `__enter__` returns something.
D) Only in Python 2.

**Answer: B**

**Explanation:**
You can just use `with lock:` if you don't need the return value.

---

**Q11.28: Advanced - [Handling Multiple Exceptions]**

Can `contextlib.suppress` handle multiple exception types?

A) No.
B) Yes, `suppress(TypeA, TypeB)`.
C) Yes, pass a list.
D) Yes, pass a tuple.

**Answer: B**

**Explanation:**
It accepts variable arguments `*exceptions`.

---

**Q11.29: Intermediate - [Enter No Return]**

If `__enter__` does not have a return statement, `as var` binds `var` to:

A) The context manager instance.
B) `None`.
C) Error.
D) `True`.

**Answer: B**

**Explanation:**
Like any function, implicit return is `None`.

---

**Q11.30: Expert - [Generator Exit Exception]**

What happens if you catch `GeneratorExit` inside a generator context manager and yield a value?

A) It works fine.
B) Python raises `RuntimeError`.
C) The generator restarts.
D) The loop continues.

**Answer: B**

**Explanation:**
`GeneratorExit` indicates the generator is being closed. Yielding a value during close implies the generator is still active/trying to produce data, which is illegal.

---

**Q11.31: Intermediate - [Context Manager Decorator Order]**

When using `@contextmanager` formatted as a decorator `@my_cm` on a function, the context is entered:

A) Before the function call.
B) Inside the function.
C) After the function returns.
D) It doesn't work as a decorator.

**Answer: A**

**Explanation:**
The decorator wraps the function call in a `with` statement. `__enter__` runs before the function body executes, and `__exit__` runs after it returns (or raises).

---

**Q11.32: Advanced - [Multiple Assignments]**

`with A() as (x, y):` works if:

A) `A()` returns a tuple of length 2 from `__enter__`.
B) `A()` is a tuple.
C) Python supports destructuring assignment in `as`.
D) All of the above (A and C).

**Answer: D**

**Explanation:**
The expression `as (x, y)` uses standard tuple unpacking. The object returned by `__enter__` must be iterable with 2 items.

---

**Q11.33: Basic - [File Mode]**

`with open('file.txt', 'w') as f:` opens the file in what mode?

A) Write (truncate).
B) Read.
C) Append.
D) Binary.

**Answer: A**

**Explanation:**
`'w'` mode opens for writing, truncating the file first.

---

**Q11.34: Expert - [ExitStack Enter Context]**

`stack.enter_context(cm)` returns:

A) The `stack` instance.
B) The result of `cm.__enter__()`.
C) `None`.
D) A proxy object.

**Answer: B**

**Explanation:**
It enters the context manager and returns the result of its `__enter__` method which allows `target = stack.enter_context(MyCM())`.

---

**Q11.35: Intermediate - [Custom Exception Class]**

If `__exit__` raises a *new* exception (different from the one passed in arguments):

A) The original exception is suppressed, and the new one propagates.
B) Both are raised (chained).
C) The new exception is ignored.
D) Python crashes.

**Answer: B**

**Explanation:**
In Python 3, the new exception will automatically have `__context__` set to the original exception (implicit chaining).

---

**Q11.36: Advanced - [Argparse]**

Does `argparse.ArgumentParser` support context managers?

A) No.
B) Yes, to suppress output.
C) Yes, mainly for testing/internal cleanup.
D) Only in Python 2.

**Answer: A**

**Explanation:**
Standard `ArgumentParser` is not a context manager. (Though one could wrap it).

---

**Q11.37: Basic - [Tempfile]**

`tempfile.TemporaryFile()` returns:

A) A file-like object that acts as a context manager and deletes itself on close.
B) A string path.
C) A directory.
D) An error.

**Answer: A**

**Explanation:**
It is designed to be used with `with`, ensuring the temporary file is closed and removed automatically.

---

**Q11.38: Intermediate - [Sqlite Transaction]**

`with connection:` where `connection` is a `sqlite3` connection object:

A) Closes the connection.
B) Starts a transaction and commits on success, rolls back on error.
C) Does nothing.
D) Opens a cursor.

**Answer: B**

**Explanation:**
The sqlite3 connection object is a context manager that handles transaction scoping (`COMMIT` / `ROLLBACK`).

---

**Q11.39: Advanced - [Isinstace ContextManager]**

To check if an object is a context manager:

A) `isinstance(obj, contextlib.AbstractContextManager)`
B) `hasattr(obj, '__enter__') and hasattr(obj, '__exit__')`
C) `isinstance(obj, ContextManager)`
D) A or B.

**Answer: D**

**Explanation:**
`B` checks strictly for the protocol (duck typing). `A` checks against the ABC (if registered or inherited).

---

**Q11.40: Expert - [Reentrant vs Reusable]**

A "reentrant" context manager:

A) Can be used in nested `with` statements (e.g. `with cm: with cm: ...`) correctly.
B) Can be reused sequentially.
C) Is thread-safe.
D) Is a generator.

**Answer: A**

**Explanation:**
Reentrancy specifically refers to the ability to re-enter the context while already inside it (like `RLock` or `decimal.localcontext` which pushes a new context on stack).

---

**Q11.41: Basic - [With Return]**

The `with` statement itself returns:

A) True/False.
B) The value of the last expression in the block.
C) Nothing (`None`). It is a statement, not an expression.
D) The context manager.

**Answer: C**

**Explanation:**
It is a control flow statement. It does not evaluate to a value.

---

**Q11.42: Intermediate - [Mock Patch]**

`unittest.mock.patch('module.Class')` is:

A) A context manager.
B) A decorator.
C) Both.
D) Neither.

**Answer: C**

**Explanation:**
`patch` returns an object that works as both a context manager (`with patch(...):`) and a decorator (`@patch(...)`).

---

**Q11.43: Advanced - [ExitStack Preservation]**

`stack.pop_all()` does what?

A) Clears the stack without calling exits.
B) Transfers the callbacks/contexts to a new `ExitStack` and returns it, preventing cleanup when the original stack closes.
C) Calls all exits immediately.
D) Pops one item.

**Answer: B**

**Explanation:**
Useful for "initialization" phases where correct completion returns a live stack that shouldn't be closed yet.

---

**Q11.44: Expert - [Async ExitStack]**

`contextlib.AsyncExitStack` supports:

A) Only async context managers.
B) Only sync context managers.
C) Both sync and async context managers.
D) Coroutines only.

**Answer: C**

**Explanation:**
It can manage both. It calls `__exit__` for sync ones and `__aexit__` for async ones.

---

**Q11.45: Intermediate - [Contextmanager Exception]**

If `yield` in a `@contextmanager` raises an exception (because user code raised it), and the generator implementation catches it but *doesn't* stop (e.g. loops back):

A) It's undefined behavior.
B) Python raises `RuntimeError` ("generator didn't stop after throw").
C) It works fine.
D) The loop continues.

**Answer: B**

**Explanation:**
The protocol requires the generator to yield exactly once. If it catches the exception and yields again (or finishes without raising), it violates the one-shot rule. It must either re-raise or exit.

---

**Q11.46: Basic - [Printing to File]**

`print("Hello", file=f)` inside a `with open(...)` block:

A) Prints to screen.
B) Writes to the file `f`.
C) Raises Error.
D) Does nothing.

**Answer: B**

**Explanation:**
Standard print syntax allows redirection to a file object.

---

**Q11.47: Advanced - [Closing Generator]**

`contextlib.closing` on a generator:

A) Calls `close()` on it when exiting.
B) Consumes it.
C) Converts it to a list.
D) Is invalid.

**Answer: A**

**Explanation:**
Generators have a `close()` method. Wrapping a generator in `closing` ensures it is closed (cleaning up any pending `finally` blocks inside it) if iteration is aborted using `break` or error.

---

**Q11.48: Expert - [ExitStack Order]**

Contexts entered in `ExitStack` are exited in:

A) LIFO (Last-In, First-Out) order.
B) FIFO (First-In, First-Out) order.
C) Random order.
D) Explicit order.

**Answer: A**

**Explanation:**
Reverse order of entry, matching nested `with` semantics.

---

**Q11.49: Intermediate - [Subprocess Popen]**

Is `subprocess.Popen` a context manager in Python 3?

A) Yes, it waits for the process to finish on exit.
B) Yes, it closes pipes/handles on exit.
C) No.
D) Only `run`.

**Answer: B**

**Explanation:**
It closes standard file descriptors (stdin/out/err) if they were opened. It does *not* necessarily wait for the process unless you call `.wait()`.

---

**Q11.50: Basic - [With Parentheses]**

Can you use parentheses for multiple context managers? `with (A() as a, B() as b):`

A) No.
B) Yes, since Python 3.10.
C) Yes, in all versions.
D) Only with `\` line continuation.

**Answer: B**

**Explanation:**
Parenthesized context managers were added in Python 3.10 to allow multi-line indentation without backslashes.

---

---

## Review Notes (2026-02-06)

- Q11.24 and Q11.27 each provide only A/B/C options (missing D), inconsistent with the predominant 4-option MCQ format.
