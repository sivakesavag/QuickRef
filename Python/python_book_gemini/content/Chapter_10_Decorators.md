# Chapter 10: Decorators & Metaprogramming

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: Closures, Function Decorators, stacked decorators, `warps`, Class Decorators, Decorators with arguments.

---

**Q10.1: Basic - [Decorator Syntax]**

What is the `@wrapper` syntax syntax equivalent to?

```python
@wrapper
def func(): pass
```

A) `func = wrapper(func)`
B) `wrapper(func)`
C) `func(wrapper)`
D) `wrapper = func(wrapper)`

**Answer: A**

**Explanation:**
The `@decorator` syntax is syntactic sugar. `@wrapper` above `def func` is exactly equivalent to defining `func` and then running `func = wrapper(func)`.

---

**Q10.2: Intermediate - [Closure Definition]**

A closure is a function that:

A) Has no arguments.
B) Is defined inside another function and retains access to the outer function's variables even after the outer function has finished executing.
C) Closes the program.
D) Is private.

**Answer: B**

**Explanation:**
Closures rely on nested scopes. The inner function "closes over" the free variables from the outer scope, keeping them alive.

---

**Q10.3: Advanced - [Order of Execution]**

```python
@d1
@d2
def f(): pass
```
This is equivalent to:

A) `f = d1(d2(f))`
B) `f = d2(d1(f))`
C) `f = d1(f); f = d2(f)`
D) `f = d1(f) + d2(f)`

**Answer: A**

**Explanation:**
Decorators are applied from bottom to top (nearest to function first). `d2` wraps `f`, then `d1` wraps the result of `d2(f)`.

---

**Q10.4: Basic - [Returning Function]**

To create a decorator, the outer function typically returns:

A) `None`.
B) The inner wrapper function.
C) The result of calling the input function.
D) A string.

**Answer: B**

**Explanation:**
A standard decorator accepts a function, defines an inner wrapper that calls the original function (usually adding behavior), and returns that wrapper.

---

**Q10.5: Intermediate - [Functools Wraps]**

Why uses `@functools.wraps(original_func)` inside a decorator?

A) It improves performance.
B) It copies metadata (name, docstring, annotations) from the original function to the wrapper.
C) It prevents recursion.
D) It allows arguments.

**Answer: B**

**Explanation:**
Without `wraps`, the decorated function would look like the wrapper (e.g. `__name__` would be `'wrapper'`). `wraps` fixes this introspection issue.

---

**Q10.6: Advanced - [Decorator with Arguments]**

If you see usage like `@repeat(times=3)`, `repeat` must be:

A) A function returning a decorator.
B) A standard decorator.
C) A class.
D) A generator.

**Answer: A**

**Explanation:**
Decorators with arguments are "factories". `repeat(times=3)` is called first, returning the *actual* decorator, which is then applied to the function. `func = repeat(times=3)(func)`.

---

**Q10.7: Basic - [Argument Passing]**

How does a wrapper function generally accept arbitrary arguments to pass to the original function?

A) `def wrapper(a, b):`
B) `def wrapper(*args, **kwargs):`
C) `def wrapper(args):`
D) `def wrapper():`

**Answer: B**

**Explanation:**
Using `*args` and `**kwargs` allows the wrapper to accept any signature and forward it via `func(*args, **kwargs)`.

---

**Q10.8: Intermediate - [Class Decorator]**

A class decorator takes:

A) An instance.
B) A class object.
C) A string.
D) A method.

**Answer: B**

**Explanation:**
Just like function decorators wrap functions, class decorators receive the `class` object, creating a chance to modify or replace it: `MyClass = decorator(MyClass)`.

---

**Q10.9: Advanced - [Unwrapping]**

Does Python provide a built-in way to "undecorate" a function?

A) No.
B) Yes, `func.__undecorate__()`.
C) Sometimes, if passed through `functools.wraps`, via `func.__wrapped__`.
D) Yes, `del func`.

**Answer: C**

**Explanation:**
`functools.wraps` attaches the original function to the `__wrapped__` attribute of the wrapper. You can access the original function there (though this chain breaks if multiple decorators don't all use `wraps`).

---

**Q10.10: Expert - [Method Decorator vs Function Decorator]**

When decorating a method `def meth(self):`, the standard `def wrapper(*args):` receives `self` as:

A) `args[0]`.
B) It is hidden.
C) A separate argument.
D) It is bound automatically.

**Answer: A**

**Explanation:**
Decorators run at definition time. The wrapper is just a function. When invoked on an instance `obj.meth()`, `obj` is passed as the first argument to the wrapper (`args[0]`).

---

**Q10.11: Basic - [Execution Time]**

When does the decorator code (the part *outside* the wrapper) run?

A) When the function is called.
B) When the Python definition is loaded/executed (import time).
C) When the program exits.
D) Never.

**Answer: B**

**Explanation:**
The decorator expression is evaluated and applied immediately when the `def` statement is processed by the interpreter.

---

**Q10.12: Intermediate - [Global Keyword in Closure]**

Inside a closure, to modify a variable from the *global* scope, use:

A) `nonlocal`
B) `global`
C) `outer`
D) `scope.global`

**Answer: B**

**Explanation:**
`global` targets module-level variables. `nonlocal` targets enclosing function variables.

---

**Q10.13: Advanced - [Nonlocal Keyword]**

To modify a variable from the immediate outer function (closure variable) in Python 3, use:

A) `global`
B) `nonlocal`
C) `super`
D) `outer`

**Answer: B**

**Explanation:**
`nonlocal` allows assignment to variables in the nearest enclosing scope that is not global.

---

**Q10.14: Basic - [Memoization]**

What is "memoization"?

A) Writing memos in code.
B) Caching the results of function calls based on arguments to avoid redundant computation.
C) Encrypting memory.
D) Automatic garbage collection.

**Answer: B**

**Explanation:**
A common use of decorators (like `@lru_cache`) is to cache return values.

---

**Q10.15: Intermediate - [LRU Cache]**

`@functools.lru_cache(maxsize=None)` creates a cache that:

A) Never grows.
B) Grows without bound (can cause memory leak).
C) Keeps only the last item.
D) Is disabled.

**Answer: B**

**Explanation:**
`maxsize=None` disables the LRU eviction logic, allowing the cache to grow indefinitely as new arguments are seen.

---

**Q10.16: Advanced - [Single Dispatch]**

`@functools.singledispatch` transforms a function into:

A) A generic function that dispatches based on the type of the first argument.
B) A singleton.
C) A thread-safe function.
D) A class method.

**Answer: A**

**Explanation:**
It allows function overloading-like behavior in Python, registering different implementations for different types of the first argument.

---

**Q10.17: Expert - [__code__ Object]**

`func.__code__` contains:

A) The source code string.
B) The compiled bytecode and metadata (varnames, constants).
C) The documentation.
D) The return value.

**Answer: B**

**Explanation:**
The code object represents the compiled function body (bytecode operations, stack requirements, variable names) decoupled from a specific function context (closure/globals).

---

**Q10.18: Intermediate - [Chained Decorators]**

If `@timer` prints time, and `@logger` prints "Called", what does:
```python
@timer
@logger
def f(): pass
```
do?
A) Times the logging and execution.
B) Logs the timing.
C) Random order.
D) Error.

**Answer: A**

**Explanation:**
`@timer` wraps `@logger`. So `timer` starts, calls `logger` (which prints "Called", calls `f`), then `timer` finishes and prints time. So it includes the logging overhead in the time.

---

**Q10.19: Basic - [Side Effects]**

Can a decorator completely replace the function with a string or integer?

A) No, must return function.
B) Yes.
C) Only in Python 2.
D) Only if return type matches.

**Answer: B**

**Explanation:**
A decorator is just a function call. It can return *any* object. `f = logic(f)`. If `logic` returns `42`, then `f` becomes `42`. (Though accessing it as a function later will raise TypeError).

---

**Q10.20: Advanced - [Total Ordering]**

`@functools.total_ordering` helps classes by:

A) Sorting instances automatically.
B) Generating missing comparison methods (`__le__`, `__gt__`, etc.) if `__eq__` and one other (`__lt__`) are defined.
C) Optimizing memory.
D) Enforcing types.

**Answer: B**

**Explanation:**
It reduces boilerplate by filling in the remaining rich comparison methods based on the minimum provided set.

---

**Q10.21: Intermediate - [Cached Property]**

`@functools.cached_property` (Py 3.8+) is useful for:

A) Methods that are cheap to calculate.
B) Methods that are expensive, computed once, and then stored as instance attributes.
C) Class variables.
D) Static methods.

**Answer: B**

**Explanation:**
It runs the method once, then replaces the method itself in the instance dict with the result, so subsequent accesses are just attribute lookups.

---

**Q10.22: Expert - [Cell Objects]**

Closures store their free variables in:

A) Global scope.
B) `__dict__`.
C) `__closure__` attribute (tuple of cells).
D) Heap.

**Answer: C**

**Explanation:**
`func.__closure__` holds a tuple of `cell` objects. These cells reference the values of the variables from the outer scope.

---

**Q10.23: Basic - [Calling decorated function]**

Does decorating a function change how you call it?

A) Yes, you must pass extra args.
B) No, ideally the signature remains compatible.
C) Yes, use `.call()`.
D) Yes, use `__wrapped__()`.

**Answer: B**

**Explanation:**
The goal of a well-behaved decorator is to be transparent to the caller, accepting the same arguments.

---

**Q10.24: Intermediate - [Partial]**

`functools.partial(func, 10)` returns:

A) The result of `func(10)`.
B) A new function with the first argument frozen to 10.
C) None.
D) `func` itself.

**Answer: B**

**Explanation:**
`partial` performs partial application, freezing some arguments and returning a callable that takes the remaining arguments.

---

**Q10.25: Advanced - [Register Pattern]**

A decorator that adds the function to a global registry (e.g., list of plugins) but returns the function unchanged is often called:

A) A null decorator.
B) A registration decorator.
C) A void decorator.
D) A wrapper.

**Answer: B**

**Explanation:**
Common pattern: `def register(func): PLUGINS.append(func); return func`.

---

**Q10.26: Expert - [Monkey Patching]**

Monkey patching refers to:

A) Using module `monkey`.
B) Changing code at runtime (e.g. replacing a method on a class dynamically).
C) Writing bad code.
D) Decorating monkeys.

**Answer: B**

**Explanation:**
Dynamic modification of a class or module at runtime (e.g. `Class.method = new_method`) is monkey patching. Useful for testing/hotfixes, but risky.

---

**Q10.27: Intermediate - [Signature Preservation]**

Does `functools.wraps` preserve the *signature* (argument spec) of the wrapped function for inspection tools?

A) No.
B) Yes, by copying `__annotations__` and being compatible with `inspect.signature`.
C) No, you need `decorator` module for that.
D) It only copies docstrings.

**Answer: B**

**Explanation:**
`wraps` copies `__annotations__` and sets `__wrapped__`, allowing `inspect.signature` to follow the chain and find the true signature (in most modern Python versions).

---

**Q10.28: Basic - [Property usage]**

`@property` is a:

A) Built-in class decorator.
B) Built-in descriptor/decorator.
C) Third-party tool.
D) Keyword.

**Answer: B**

**Explanation:**
It's a built-in type that acts as a decorator to define getters/setters.

---

**Q10.29: Advanced - [Stateful Decorator]**

How can a decorator maintain state (e.g., count calls)?

A) Use a global variable.
B) Use a class as a decorator (implementing `__call__`).
C) Use function attributes on the wrapper.
D) All of the above.

**Answer: D**

**Explanation:**
All are valid. A class instance is a common way (`self.count`), or attaching `wrapper.count` works too.

---

**Q10.30: Expert - [Code Object Immutability]**

Can you modify `func.__code__` in place?

A) Yes.
B) No, code objects are immutable. You must assign a new code object.
C) Yes, if using C types.
D) Only `co_consts`.

**Answer: B**

**Explanation:**
Code objects are immutable. To change a function's behavior at bytecode level, you must create a new code object and assign it to `func.__code__`.

---

**Q10.31: Intermediate - [Wrapped Attribute]**

To access the original function underneath `@functools.wraps`, access:

A) `__func__`
B) `__origin__`
C) `__wrapped__`
D) `__inner__`

**Answer: C**

**Explanation:**
`functools.wraps` helps inspection by assigning the original function to `__wrapped__`.

---

**Q10.32: Basic - [StaticMethod Decorator]**

`@staticmethod`:

A) Makes the method private.
B) Allows calling the method without an instance (just via Class).
C) Compiles to C.
D) Makes the method immutable.

**Answer: B**

**Explanation:**
It removes the requirement to pass the instance (`self`) or class (`cls`) automatically.

---

**Q10.33: Advanced - [Class Creation Hook]**

Which dictionary is passed to `__new__` of a metaclass during class creation?

A) `self.__dict__`
B) The class namespace dictionary (containing methods and attributes defined in the class body).
C) `globals()`
D) Empty dict.

**Answer: B**

**Explanation:**
Metaclass `__new__(mcls, name, bases, namespace)` receives the namespace populated by executing the class body.

---

**Q10.34: Expert - [Metaclass Inheritance]**

If `A` has metaclass `MetaA`, and `B(A)` is defined, what is `B`'s metaclass?

A) `type` (default).
B) `MetaA`.
C) `None`.
D) Error.

**Answer: B**

**Explanation:**
Metaclasses are inherited. The type of the class `B` will be `MetaA`.

---

**Q10.35: Intermediate - [Late Binding Closures]**

```python
funcs = [lambda: i for i in range(3)]
print([f() for f in funcs])
```
Output?

A) `[0, 1, 2]`
B) `[2, 2, 2]`
C) `[0, 0, 0]`
D) Error.

**Answer: B**

**Explanation:**
Closures bind to variables by *reference* (late binding), not by value. When the lambdas run, the loop has finished, and `i` is 2. (Fix: `lambda i=i: i`).

---

**Q10.36: Advanced - [Result Unpacking Decorator]**

A decorator that automatically unpacks a tuple return value into multiple arguments for the next function is:

A) Impossible.
B) Common in pipeline frameworks.
C) Built-in `unpack`.
D) Only via `yield from`.

**Answer: B**

**Explanation:**
It is possible and common to write decorators/wrappers that adapt signatures (e.g. converting a tuple return into `*args`).

---

**Q10.37: Basic - [Documentation]**

If you don't use `wraps`, `help(decorated_func)` shows:

A) The original docstring.
B) The wrapper's docstring (or None).
C) Error.
D) Both.

**Answer: B**

**Explanation:**
Without copying metadata, the help system sees the wrapper function's attributes.

---

**Q10.38: Intermediate - [Functools Update Wrapper]**

`functools.update_wrapper` is:

A) The underlying function called by `@wraps`.
B) A deprecated function.
C) Used for updating libraries.
D) For GUI wrappers.

**Answer: A**

**Explanation:**
`@wraps` is a convenience factory that returns a partial of `update_wrapper`. You can call `update_wrapper(wrapper, wrapped)` manually.

---

**Q10.39: Expert - [Prepare Metaclass]**

`__prepare__` in a metaclass allows you to:

A) Print a message before creation.
B) Customize the mapping object (namespace) used during class body execution (e.g., to use an `OrderedDict`).
C) Initialize `__slots__`.
D) Prepare the compiler.

**Answer: B**

**Explanation:**
`__prepare__` returns the dictionary-like object that will process the class body statements. This allows tracking order of definition (pre-Python 3.6 implementation detail, now default order is preserved, but still useful for other custom namespaces).

---

**Q10.40: Advanced - [Nested Decorators Order]**

For `@A @B def f`: `f` is passed to:

A) A first, then B.
B) B first, then the result to A.
C) Parallel execution.
D) A wrapper around B.

**Answer: B**

**Explanation:**
It matches `f = A(B(f))`. B takes f. A takes result of B.

---

**Q10.41: Intermediate - [Context Manager as Decorator]**

Can `contextlib.ContextDecorator` let you use a context manager as a decorator?

A) Yes.
B) No.
C) Only in async.
D) Only if it is a class.

**Answer: A**

**Explanation:**
Inheriting from `ContextDecorator` allows a class to act as both a `with` statement manager and a function decorator.

---

**Q10.42: Basic - [Metaclass Default]**

The default metaclass for a standard class in Python 3 is:

A) `object`
B) `class`
C) `type`
D) `meta`

**Answer: C**

**Explanation:**
`type` is the class that creates classes.

---

**Q10.43: Advanced - [Dynamic Attribute Access]**

`__getattr__` is called when:

A) Any attribute is accessed.
B) An attribute is NOT found by normal lookup.
C) An attribute is set.
D) An attribute is deleted.

**Answer: B**

**Explanation:**
`__getattr__` is a fallback. `__getattribute__` is unconditional.

---

**Q10.44: Expert - [New vs Init in Metaclass]**

In a metaclass, `__new__` creates the **class object**, while `__init__` initializes it. To alter the generated class list of bases *before* creation, you must use:

A) `__new__`
B) `__init__`
C) `__call__`
D) `__create__`

**Answer: A**

**Explanation:**
`__new__` receives `bases` as an argument and passes them to `super().__new__`. Once the class object is created (returned from new), `__init__` is called, but the bases are already set (mostly immutable internal structure).

---

**Q10.45: Intermediate - [Inspect Signature]**

`inspect.signature(f).bind(*args, **kwargs)` is useful in decorators to:

A) Call the function.
B) Map execution arguments to parameter names (handling defaults, kwargs, etc.) uniformly.
C) Bind the function to an object.
D) Check types.

**Answer: B**

**Explanation:**
It creates a `BoundArguments` object, mapping the provided args to the function's signature. This allows a decorator to read specific arguments (like `request` or `user`) regardless of whether passed positionally or by keyword.

---

**Q10.46: Basic - [Calling Original]**

If a decorator does NOT call the original function:

A) The program crashes.
B) The original function never runs (it is effectively replaced/suppressed).
C) It runs automatically at the end.
D) Python raises a warning.

**Answer: B**

**Explanation:**
The decorator has full control. It can strip the logic entirely.

---

**Q10.47: Advanced - [Function Annotations Access]**

Decorators can read type hints via:

A) `func.__types__`
B) `func.__annotations__`
C) `func.hints`
D) `func.doc`

**Answer: B**

**Explanation:**
`__annotations__` is a dictionary containing the type hints.

---

**Q10.48: Expert - [Function inside Class]**

Defining a function inside a class body (during definition) but decorating it with a custom decorator returns an object. Does that object automatically become a bound method when accessed on an instance?

A) Yes, always.
B) No, only if the object is a function or implements `__get__` (Descriptor protocol).
C) No, never.
D) Yes, if it is callable.

**Answer: B**

**Explanation:**
The "binding" magic happens because functions are descriptors. If your decorator returns a plain object (not a function/descriptor), `obj.method` returns that object directly, without binding `self`.

---

**Q10.49: Intermediate - [Abstract Property]**

Can you combine `@property` and `@abstractmethod`?

A) Yes, `@property` then `@abstractmethod`.
B) No.
C) Yes, `@abstractmethod` then `@property`.
D) Order doesn't matter.

**Answer: A**

**Explanation:**
Syntax:
```python
@property
@abstractmethod
def foo(self): ...
```
This defines an abstract property getter.

---

**Q10.50: Basic - [Function Name]**

`def my_func(): pass`. `my_func.__name__` is:

A) `"my_func"`
B) `"function"`
C) `None`
D) Address.

**Answer: A**

**Explanation:**
The `__name__` attribute holds the name of the function as string.

---

---

## Review Notes (2026-02-06)

- Q10.18, Q10.40, and Q10.41 each provide only A/B/C options (missing D), inconsistent with the predominant 4-option MCQ format.
