# Chapter 10: Decorators

> **Topics Covered**: Function decorators, decorator syntax, functools.wraps, decorators with arguments, class decorators, method decorators, stacking decorators, built-in decorators (@property, @classmethod, @staticmethod), decorator factories, advanced patterns

---

## Questions

---

**Q10.1: Basic - [Decorator Concept]**

What is a decorator in Python?

A) A way to decorate output strings
B) A function that modifies or enhances another function
C) A class attribute
D) A comment style

**Answer: B**

**Explanation:**
A decorator is a function that takes another function as input and returns a modified/enhanced version. It "wraps" the original function, adding functionality before/after the call without changing the original code.

---

**Q10.2: Basic - [Decorator Syntax]**

What does `@decorator` syntax do?
```python
@decorator
def func():
    pass
```

A) Nothing, it's a comment
B) Equivalent to `func = decorator(func)`
C) Makes func private
D) Imports decorator

**Answer: B**

**Explanation:**
`@decorator` before a function is syntactic sugar for `func = decorator(func)`. The decorator receives the function, typically wraps it, and returns the wrapped version. The function name now refers to whatever the decorator returned.

---

**Q10.3: Intermediate - [Simple Decorator]**

What is the output?
```python
def loud(func):
    def wrapper():
        print("BEFORE")
        func()
        print("AFTER")
    return wrapper

@loud
def greet():
    print("Hello")

greet()
```

A) `Hello`
B) `BEFORE, Hello, AFTER`
C) `BEFORE, AFTER`
D) Error

**Answer: B**

**Explanation:**
`@loud` wraps `greet`. Calling `greet()` actually calls `wrapper()`, which prints "BEFORE", calls original `func()` (prints "Hello"), then prints "AFTER".

---

**Q10.4: Intermediate - [Decorator with Arguments]**

How do you pass arguments through a decorator?
```python
def decorator(func):
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```

A) The wrapper must accept `*args, **kwargs` to pass any arguments
B) Arguments are passed automatically
C) You can't pass arguments
D) Use special syntax

**Answer: A**

**Explanation:**
`*args, **kwargs` in wrapper captures all positional and keyword arguments. They're passed to the original function with `func(*args, **kwargs)`. This makes the decorator work with any function signature.

---

**Q10.5: Intermediate - [Decorator Return Value]**

What is the output?
```python
def double_result(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        return result * 2
    return wrapper

@double_result
def add(a, b):
    return a + b

print(add(3, 4))
```

A) `7`
B) `14`
C) `(7, 7)`
D) Error

**Answer: B**

**Explanation:**
The decorator doubles the return value. `add(3, 4)` → original returns 7 → wrapper returns 7 * 2 = 14. Decorators can modify both inputs and outputs.

---

**Q10.6: Intermediate - [functools.wraps]**

What is the purpose of `@functools.wraps(func)`?

A) Wraps function in try-except
B) Preserves original function's metadata (__name__, __doc__, etc.)
C) Makes function faster
D) Creates a copy

**Answer: B**

**Explanation:**
Without `@wraps`, the wrapper's name/docstring replace the original's. `@wraps(func)` copies metadata from the wrapped function to the wrapper. Essential for debugging and introspection.

---

**Q10.7: Intermediate - [functools.wraps Example]**

What is the output?
```python
from functools import wraps

def decorator(func):
    @wraps(func)
    def wrapper():
        return func()
    return wrapper

@decorator
def greet():
    """Says hello"""
    return "Hello"

print(greet.__name__, greet.__doc__)
```

A) `wrapper, None`
B) `greet, Says hello`
C) `decorator, None`
D) Error

**Answer: B**

**Explanation:**
`@wraps(func)` copies `__name__`, `__doc__`, and other attributes from `func` to `wrapper`. Without it, `greet.__name__` would be "wrapper" and `__doc__` would be None.

---

**Q10.8: Advanced - [Decorator with Parameters]**

How do you create a decorator that accepts parameters?

A) Add parameters to the wrapper
B) Create a decorator factory — a function that returns the actual decorator
C) Use @decorator(params) syntax directly
D) It's not possible

**Answer: B**

**Explanation:**
A "decorator factory" returns a decorator. Three levels: factory(params) → decorator(func) → wrapper(*args). `@repeat(3)` first calls `repeat(3)` which returns the decorator, which then wraps the function.

---

**Q10.9: Advanced - [Parameterized Decorator Example]**

What is the output?
```python
def repeat(n):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(n):
                result = func(*args, **kwargs)
            return result
        return wrapper
    return decorator

@repeat(3)
def say(msg):
    print(msg)
    return msg

say("Hi")
```

A) Prints "Hi" once
B) Prints "Hi" three times
C) Returns ["Hi", "Hi", "Hi"]
D) Error

**Answer: B**

**Explanation:**
`@repeat(3)` → `repeat(3)` returns decorator → decorator wraps `say`. Calling `say("Hi")` calls wrapper, which loops 3 times calling original function. Prints "Hi" three times.

---

**Q10.10: Intermediate - [Stacking Decorators]**

What is the output?
```python
def bold(func):
    def wrapper():
        return f"<b>{func()}</b>"
    return wrapper

def italic(func):
    def wrapper():
        return f"<i>{func()}</i>"
    return wrapper

@bold
@italic
def greet():
    return "Hello"

print(greet())
```

A) `<b><i>Hello</i></b>`
B) `<i><b>Hello</b></i>`
C) `<b>Hello</b><i>Hello</i>`
D) Error

**Answer: A**

**Explanation:**
Decorators apply bottom-up but execute top-down. `@italic` wraps `greet` first, then `@bold` wraps that. Order: bold(italic(greet)) → `<b>` then `<i>Hello</i>` then `</b>`.

---

**Q10.11: Intermediate - [Decorator Order Matters]**

If you have `@A @B @C def f(): pass`, what is the equivalent?

A) `f = C(B(A(f)))`
B) `f = A(B(C(f)))`
C) `f = A(f); B(f); C(f)`
D) Order doesn't matter

**Answer: B**

**Explanation:**
Decorators apply bottom-up. First `C(f)`, then `B(result)`, then `A(result)`. So `@A @B @C` equals `f = A(B(C(f)))`. The closest decorator to `def` is applied first.

---

**Q10.12: Intermediate - [@property]**

What does the `@property` decorator do?

A) Makes attribute private
B) Creates a managed attribute with getter (and optionally setter/deleter)
C) Stores properties
D) Documents attributes

**Answer: B**

**Explanation:**
`@property` turns a method into a "getter" accessed like an attribute. `obj.value` calls the method. Add `@value.setter` for write access. Enables validation or computation on attribute access.

---

**Q10.13: Intermediate - [@classmethod]**

What is the output?
```python
class MyClass:
    count = 0
    
    @classmethod
    def increment(cls):
        cls.count += 1
        return cls.count

print(MyClass.increment(), MyClass.increment())
```

A) `1, 2`
B) `0, 0`
C) `1, 1`
D) Error

**Answer: A**

**Explanation:**
`@classmethod` makes the method receive the class (`cls`) instead of instance. `cls.count` modifies the class attribute. First call → 1, second → 2. Works on class or instance.

---

**Q10.14: Intermediate - [@staticmethod]**

What is the output?
```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b

print(Math.add(3, 4))
print(Math().add(3, 4))
```

A) `7, 7`
B) `7, Error`
C) Error, 7
D) Error, Error

**Answer: A**

**Explanation:**
`@staticmethod` creates a method with no implicit first argument (no `self` or `cls`). Works called on class or instance. Essentially a regular function in the class namespace.

---

**Q10.15: Intermediate - [Timing Decorator]**

What does this decorator do?
```python
import time
def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        print(f"Took {time.time() - start:.2f}s")
        return result
    return wrapper
```

A) Limits function runtime
B) Measures and prints function execution time
C) Pauses execution
D) Records timestamps

**Answer: B**

**Explanation:**
This is a common timing decorator. Records start time, calls function, calculates elapsed time, prints it. Useful for profiling. Result is still returned normally.

---

**Q10.16: Intermediate - [Logging Decorator]**

What does this decorator do?
```python
def log_calls(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__} with {args}, {kwargs}")
        return func(*args, **kwargs)
    return wrapper
```

A) Writes to a log file
B) Prints function name and arguments before each call
C) Counts function calls
D) Disables logging

**Answer: B**

**Explanation:**
A logging decorator that prints diagnostic info before each call. Shows function name and arguments. Useful for debugging without modifying the original function.

---

**Q10.17: Intermediate - [Memoization Decorator]**

What does `@functools.lru_cache` do?

A) Clears cache
B) Caches function results based on arguments
C) Limits function calls
D) Logs return values

**Answer: B**

**Explanation:**
`@lru_cache(maxsize=128)` memoizes results. If called with same arguments again, returns cached result instead of recomputing. "LRU" = Least Recently Used (eviction policy). Arguments must be hashable.

---

**Q10.18: Intermediate - [lru_cache Example]**

What is the output?
```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)

print(fib(10))
print(fib.cache_info())
```

A) `55`, then cache statistics
B) `55`, then Error
C) `89`, then cache statistics
D) Stack overflow

**Answer: A**

**Explanation:**
`fib(10)` returns 55. Without caching, naive recursion is O(2^n). With `@lru_cache`, each value computed once, O(n). `cache_info()` shows hits, misses, size. `maxsize=None` = unlimited cache.

---

**Q10.19: Advanced - [Cache Clear]**

How do you clear an lru_cache?

A) `func.clear()`
B) `func.cache_clear()`
C) `del func.cache`
D) Cannot be cleared

**Answer: B**

**Explanation:**
`func.cache_clear()` empties the cache. Useful when underlying data changes. `func.cache_info()` shows statistics. These methods are added to the decorated function.

---

**Q10.20: Intermediate - [Class Decorator]**

What can a class decorator do?
```python
def decorator(cls):
    cls.new_attr = "added"
    return cls

@decorator
class MyClass:
    pass
```

A) Decorate class methods only
B) Modify or replace the class itself
C) Only add documentation
D) Nothing useful

**Answer: B**

**Explanation:**
Class decorators receive the class and can modify it (add attributes, methods, wrap) or return a different class entirely. `@dataclass` is a famous example that modifies the class extensively.

---

**Q10.21: Intermediate - [@dataclass]**

What does `@dataclass` decorator do?

A) Converts class to data
B) Auto-generates __init__, __repr__, __eq__ based on class annotations
C) Makes class immutable
D) Stores data in database

**Answer: B**

**Explanation:**
`@dataclass` (Python 3.7+) reads class annotations and generates boilerplate methods. Saves writing repetitive code for simple data-holding classes. Options like `frozen=True` add immutability.

---

**Q10.22: Advanced - [Decorator Class]**

Can a class be used as a decorator?

A) No, only functions
B) Yes, by implementing __call__
C) Only with special syntax
D) Only for class decorators

**Answer: B**

**Explanation:**
A class with `__call__` can be used as a decorator. The class instance wraps the function, and calling the instance invokes `__call__`. Useful when decorator needs to maintain state.

---

**Q10.23: Advanced - [Decorator Class Example]**

What is the output?
```python
class Counter:
    def __init__(self, func):
        self.func = func
        self.count = 0
    
    def __call__(self, *args, **kwargs):
        self.count += 1
        return self.func(*args, **kwargs)

@Counter
def greet():
    return "Hello"

greet()
greet()
print(greet.count)
```

A) `0`
B) `1`
C) `2`
D) Error

**Answer: C**

**Explanation:**
The class-based decorator maintains state. Each call increments `count`. After two calls, `greet.count` is 2. `greet` is now a `Counter` instance, not the original function.

---

**Q10.24: Intermediate - [Preserving Signature]**

Why is preserving function signature important in decorators?

A) It's not important
B) For introspection, help(), IDE autocomplete, and debugging
C) For performance
D) Only for type hints

**Answer: B**

**Explanation:**
If signature is lost, `help(func)` shows wrapper's signature, not original's. IDEs can't autocomplete properly. `@wraps` helps, but for complete signature preservation, use `functools.update_wrapper` or libraries like `decorator`.

---

**Q10.25: Advanced - [functools.update_wrapper]**

What does `functools.update_wrapper()` do?

A) Same as @wraps, but as a function call
B) Updates function source code
C) Creates a new function
D) Only updates __name__

**Answer: A**

**Explanation:**
`update_wrapper(wrapper, wrapped)` copies `__name__`, `__doc__`, `__dict__`, etc. from wrapped to wrapper. `@wraps(func)` is shorthand for `@update_wrapper(wrapped=func)`. Also sets `__wrapped__` for accessing original.

---

**Q10.26: Advanced - [__wrapped__ Attribute]**

What is the output?
```python
from functools import wraps

def decorator(func):
    @wraps(func)
    def wrapper():
        return func()
    return wrapper

@decorator
def original():
    """Original docstring"""
    return 42

print(original.__wrapped__.__name__)
```

A) `wrapper`
B) `original`
C) `decorator`
D) Error

**Answer: B**

**Explanation:**
`@wraps` sets `__wrapped__` to the original function, allowing you to access it later. `original.__wrapped__` is the undecorated function. Useful for testing or bypassing decoration.

---

**Q10.27: Intermediate - [Decorator for Methods]**

What extra consideration is needed when decorating methods?

A) None
B) Wrapper must handle `self` as first argument
C) Use @method decorator
D) Methods can't be decorated

**Answer: B**

**Explanation:**
Methods receive `self` as first argument. Wrapper using `*args, **kwargs` handles this automatically — `self` becomes part of `args`. Be careful with `staticmethod`/`classmethod` — decorator order matters.

---

**Q10.28: Intermediate - [Method Decorator Example]**

What is the output?
```python
def log(func):
    def wrapper(self, *args, **kwargs):
        print(f"Called on {self}")
        return func(self, *args, **kwargs)
    return wrapper

class MyClass:
    @log
    def method(self):
        return "done"

obj = MyClass()
obj.method()
```

A) Error: self not defined
B) Prints object representation, returns "done"
C) "done"
D) Error

**Answer: B**

**Explanation:**
The wrapper explicitly accepts `self`. When `obj.method()` is called, `self` is `obj`. This works because decorators are applied at class definition time, not method call time.

---

**Q10.29: Advanced - [staticmethod and classmethod Order]**

What happens here?
```python
def my_decorator(func):
    def wrapper(*args):
        return func(*args)
    return wrapper

class MyClass:
    @staticmethod
    @my_decorator
    def method():
        return "hello"
```

A) Works correctly
B) Error — decorators are in wrong order
C) method becomes instance method
D) Both decorators ignored

**Answer: A**

**Explanation:**
Order matters! `@my_decorator` wraps the function first, then `@staticmethod` makes it static. If reversed (`@my_decorator @staticmethod`), you'd be trying to decorate a staticmethod descriptor object, which won't work as expected.

---

**Q10.30: Intermediate - [Decorator Debugging]**

What helps debug decorated functions?

A) Print statements only
B) @wraps for metadata, __wrapped__ to access original, good IDE support
C) Can't debug decorated functions
D) Use print(func)

**Answer: B**

**Explanation:**
`@wraps` preserves `__name__`, `__doc__`. `__wrapped__` gives access to the original. Debuggers show correct function name. Some IDEs can step through decorators. Logging decorators can show call info.

---

**Q10.31: Advanced - [Optional Parentheses Decorator]**

How do you make a decorator work both as `@dec` and `@dec(args)`?

A) Not possible
B) Check if the first argument is a function or the parameter
C) Use different names
D) Always require parentheses

**Answer: B**

**Explanation:**
```python
def dec(arg=None):
    def decorator(func):
        return wrapper
    if callable(arg):  # used as @dec
        return decorator(arg)
    return decorator  # used as @dec(args)
```
Check if argument is callable to determine usage.

---

**Q10.32: Intermediate - [Decorator Use Cases]**

Which is NOT a common decorator use case?

A) Logging and timing
B) Caching/memoization
C) Access control/authentication
D) Memory allocation

**Answer: D**

**Explanation:**
Common uses: logging, timing, caching, authentication, rate limiting, input validation, retry logic. Memory allocation is typically handled by Python's memory manager, not decorators.

---

**Q10.33: Advanced - [Retry Decorator]**

What does this decorator do?
```python
import time

def retry(max_attempts=3, delay=1):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception:
                    if attempt == max_attempts - 1:
                        raise
                    time.sleep(delay)
        return wrapper
    return decorator
```

A) Makes function faster
B) Retries failed function calls with delay
C) Limits function calls
D) Logs exceptions

**Answer: B**

**Explanation:**
A retry decorator for handling transient failures (network issues, etc.). Attempts function up to max_attempts times, waiting delay seconds between. Raises exception only if all attempts fail. Common in network code.

---

**Q10.34: Intermediate - [Validation Decorator]**

What does this decorator pattern do?
```python
def validate_positive(func):
    def wrapper(x):
        if x < 0:
            raise ValueError("Must be positive")
        return func(x)
    return wrapper
```

A) Makes x positive
B) Validates input before calling function
C) Validates output
D) Does nothing

**Answer: B**

**Explanation:**
Input validation decorator. Checks argument before calling function. Raises exception on invalid input. Keeps validation logic separate from business logic. Common for API parameter checking.

---

**Q10.35: Advanced - [Singleton Decorator]**

What does this decorator create?
```python
def singleton(cls):
    instances = {}
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance
```

A) A class factory
B) A singleton pattern — only one instance ever created
C) Multiple instances
D) A cached class

**Answer: B**

**Explanation:**
Singleton decorator ensures only one instance of the class exists. First call creates instance, subsequent calls return the same one. `instances` dict stores the single instance per class.

---

**Q10.36: Intermediate - [Deprecated Decorator]**

What is the purpose of a deprecation decorator?

A) Removes old code
B) Warns users that a function is deprecated and may be removed
C) Makes functions slower
D) Updates function code

**Answer: B**

**Explanation:**
```python
def deprecated(func):
    def wrapper(*args, **kwargs):
        warnings.warn(f"{func.__name__} is deprecated", DeprecationWarning)
        return func(*args, **kwargs)
    return wrapper
```
Emits warning when deprecated function is called. Helps with gradual API changes.

---

**Q10.37: Advanced - [functools.singledispatch]**

What does `@functools.singledispatch` do?

A) Dispatches to a single function
B) Enables function overloading based on first argument's type
C) Limits function calls to one
D) Creates single instances

**Answer: B**

**Explanation:**
Single dispatch enables different implementations based on the first argument's type. Register implementations for different types. Provides a form of function overloading. Python 3.4+.

---

**Q10.38: Advanced - [singledispatch Example]**

What is the output?
```python
from functools import singledispatch

@singledispatch
def process(arg):
    return f"Default: {arg}"

@process.register(int)
def _(arg):
    return f"Int: {arg}"

@process.register(list)
def _(arg):
    return f"List: {len(arg)} items"

print(process(42), process([1, 2]))
```

A) `Default: 42, Default: [1, 2]`
B) `Int: 42, List: 2 items`
C) Error
D) `42, [1, 2]`

**Answer: B**

**Explanation:**
`singledispatch` routes to implementation based on type. 42 is int → "Int: 42". [1, 2] is list → "List: 2 items". Unregistered types get the default (base) implementation.

---

**Q10.39: Intermediate - [Decorator vs Inheritance]**

When is a decorator better than inheritance?

A) Always
B) When you want to add behavior to existing functions/classes without modifying them
C) Never
D) Only for classes

**Answer: B**

**Explanation:**
Decorators add behavior non-invasively. You can decorate third-party functions. More flexible than inheritance — can combine multiple decorators. Follows "composition over inheritance" principle.

---

**Q10.40: Advanced - [Decorator Drawbacks]**

What are potential drawbacks of decorators?

A) No drawbacks
B) Can hide behavior, complicate debugging, add overhead, change signature
C) Only performance issues
D) Only readable code issues

**Answer: B**

**Explanation:**
Drawbacks: hidden behavior (need to check decorators), debugging complexity (stack traces include wrappers), small performance overhead, can lose signature info. Use wisely and document.

---

**Q10.41: Intermediate - [contextlib Decorators]**

What does `@contextlib.contextmanager` do?

A) Manages contexts
B) Converts a generator function into a context manager
C) Creates managers
D) Documents context

**Answer: B**

**Explanation:**
Allows writing context managers as generators instead of classes. Code before `yield` = `__enter__`, code after = `__exit__`. Simpler syntax for many context manager use cases.

---

**Q10.42: Advanced - [Decorator Composition]**

What's a "decorator factory"?

A) A factory that builds objects
B) A function that returns decorators, allowing parameterization
C) A class-based decorator
D) A design pattern for factories

**Answer: B**

**Explanation:**
Decorator factory = function that returns a decorator. Enables parameterized decorators like `@retry(3)` where `retry(3)` returns the actual decorator. Three-level nesting: factory → decorator → wrapper.

---

**Q10.43: Intermediate - [nonlocal in Decorators]**

Why might you need `nonlocal` in a decorator?

A) For global variables
B) To modify variables from enclosing scope (like counters)
C) For nested functions
D) Never needed

**Answer: B**

**Explanation:**
If wrapper needs to modify a variable from the decorator's scope (e.g., call counter), use `nonlocal`. Without it, assignment creates a local variable instead of modifying the closure variable.

---

**Q10.44: Advanced - [Type Checking Decorator]**

What does this decorator enforce?
```python
def enforce_types(func):
    def wrapper(*args, **kwargs):
        hints = func.__annotations__
        # Check each arg against type hints
        return func(*args, **kwargs)
    return wrapper
```

A) Documentation
B) Runtime type checking based on annotations
C) Type hints
D) Nothing by itself

**Answer: B**

**Explanation:**
A runtime type checker decorator. Reads `__annotations__` and validates arguments match type hints. Python doesn't enforce types normally, but decorators can add runtime checking.

---

**Q10.45: Advanced - [Descriptor Protocol in Decorators]**

How does `@property` work internally?

A) Magic
B) It's a descriptor implementing __get__, __set__, __delete__
C) Special Python syntax
D) Modifies the class

**Answer: B**

**Explanation:**
`property` is a descriptor class. The decorated method becomes `__get__`. When accessing as attribute, `__get__` is called. `@prop.setter` adds `__set__`. This is the descriptor protocol in action.

---

**Q10.46: Intermediate - [Multiple Decorators Same Function]**

What is the output?
```python
def add_one(func):
    def wrapper(x):
        return func(x) + 1
    return wrapper

def double(func):
    def wrapper(x):
        return func(x) * 2
    return wrapper

@add_one
@double
def identity(x):
    return x

print(identity(3))
```

A) `6`
B) `7`
C) `8`
D) `4`

**Answer: B**

**Explanation:**
Order: `add_one(double(identity))`. First `identity(3)` → 3. Then `double` → 3 * 2 = 6. Then `add_one` → 6 + 1 = 7. Bottom decorator applies first, but outer runs on its result.

---

**Q10.47: Advanced - [functools.cache vs lru_cache]**

What's the difference between `@cache` and `@lru_cache`?

A) No difference
B) `@cache` is `@lru_cache(maxsize=None)` — unbounded cache
C) `@cache` is faster
D) `@lru_cache` is deprecated

**Answer: B**

**Explanation:**
`@functools.cache` (Python 3.9+) is shorthand for `@lru_cache(maxsize=None)`. No size limit, no LRU eviction. Simpler for cases where you want infinite caching.

---

**Q10.48: Intermediate - [Decorator Best Practices]**

Which is a best practice for decorators?

A) Never use @wraps
B) Always use @functools.wraps for preserving metadata
C) Make decorators complex
D) Avoid using decorators

**Answer: B**

**Explanation:**
💡 Best practices: use `@wraps`, keep decorators focused (single responsibility), document what they do, consider making them optional for testing, handle both sync and async if needed.

---

**Q10.49: Advanced - [Async Decorator]**

How do you decorate an async function?

A) Same as regular functions
B) Wrapper must be async and await the original
C) Can't decorate async functions
D) Use @async_decorator

**Answer: B**

**Explanation:**
```python
def decorator(func):
    async def wrapper(*args, **kwargs):
        # before
        result = await func(*args, **kwargs)
        # after
        return result
    return wrapper
```
Wrapper must be `async` if decorating async functions.

---

**Q10.50: Advanced - [inspect.signature Preservation]**

How can you fully preserve a function's signature in a decorator?

A) Use @wraps only
B) Use inspect.signature and recreate wrapper with same signature
C) Not possible
D) Use *args, **kwargs

**Answer: B**

**Explanation:**
`@wraps` doesn't fully preserve signature for introspection. Libraries like `wrapt` or `decorator` properly preserve signatures. Or use `inspect.signature` to copy/apply the signature to the wrapper.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 4 | 8% |
| Intermediate | 30 | 60% |
| Advanced | 16 | 32% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- Function decorator syntax and mechanics
- functools.wraps for metadata preservation
- Decorators with/without parameters
- Stacking decorators
- Built-in decorators (@property, @classmethod, @staticmethod)
- @lru_cache for memoization
- Class decorators
- Decorator factories
- Common patterns (logging, timing, retry, validation)
- @singledispatch for function overloading
