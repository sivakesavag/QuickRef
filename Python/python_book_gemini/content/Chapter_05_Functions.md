# Chapter 5: Functions & Scope

**Target MCQs**: 60-70
**Current Batch**: 1-30
**Topics Covered**: Parameters, Arguments, Defaults, *args/**kwargs, Positional/Keyword only, Scope (LEGB), Global/Nonlocal, Lambdas.

---

**Q5.1: Basic - [Function Definition]**

What is the return value of a function that does not have a `return` statement?

A) `0`
B) `False`
C) `None`
D) `undefined`

**Answer: C**

**Explanation:**
In Python, if a function body ends without hitting a `return` statement, it implicitly returns `None`.

---

**Q5.2: Basic - [Mutable Default Argument]**

What is the output of the following code?
```python
def append_item(item, list=[]):
    list.append(item)
    return list

print(append_item(1))
print(append_item(2))
```

A) `[1]` then `[2]`
B) `[1]` then `[1, 2]`
C) `[1]` then `Error`
D) `[1]` then `[2]` (if lists are local)

**Answer: B**

**Explanation:**
Default argument values are evaluated **only once** at function definition time, not at call time. The list `[]` is created once and stored in `func.__defaults__`. Subsequent calls reuse the *same* list object.

---

**Q5.3: Intermediate - [Keyword Arguments]**

Given `def func(a, b, c): ...`, which call is valid?

A) `func(a=1, 2, 3)`
B) `func(1, b=2, 3)`
C) `func(1, 2, c=3)`
D) `func(a=1, b=2, 3)`

**Answer: C**

**Explanation:**
Positional arguments must come *before* keyword arguments. Options A, B, and D violate this rule.

---

**Q5.4: Basic - [Arbitrary Arguments]**

How do you define a function that accepts any number of positional arguments?

A) `def func(args):`
B) `def func(*args):`
C) `def func(**args):`
D) `def func(...args):`

**Answer: B**

**Explanation:**
The `*` prefix acts as a collector, gathering extra positional arguments into a tuple named `args`.

---

**Q5.5: Intermediate - [Arbitrary Keyword Arguments]**

What is the type of `kwargs` in `def func(**kwargs):`?

A) Tuple
B) List
C) Set
D) Dictionary

**Answer: D**

**Explanation:**
`**kwargs` collects extra keyword arguments into a standard Python dictionary.

---

**Q5.6: Advanced - [Argument Unpacking]**

Given `args = [1, 2]` and `def func(a, b): ...`, how do you call `func` using `args`?

A) `func(args)`
B) `func(*args)`
C) `func(**args)`
D) `func(&args)`

**Answer: B**

**Explanation:**
`*` unpacks the iterable `args` into individual positional arguments: `func(1, 2)`.

---

**Q5.7: Basic - [Scope LEGB]**

What does LEGB stand for in Python scope resolution?

A) Local, Enclosing, Global, Built-in
B) Local, External, Global, Binary
C) Level, Entry, Global, Base
D) Loop, Exception, Global, Built-in

**Answer: A**

**Explanation:**
Python searches names in this order: **L**ocal (function), **E**nclosing (nested function), **G**lobal (module), **B**uilt-in (Python core).

---

**Q5.8: Intermediate - [Global Keyword]**

What does the `global` keyword do?

A) Declares a variable available to all modules.
B) Allows a function to modify a variable in the global (module) scope.
C) Imports a variable from another file.
D) Makes a variable constant.

**Answer: B**

**Explanation:**
By default, assigning to a name inside a function creates a local variable. `global x` tells Python that assignments to `x` should target the global variable `x`, not create a local one.

---

**Q5.9: Advanced - [Nonlocal Keyword]**

The `nonlocal` keyword is used to:

A) Access global variables.
B) Modify variables in the nearest enclosing scope (excluding global).
C) Declare variables that cannot be local.
D) Access built-ins.

**Answer: B**

**Explanation:**
`nonlocal` allows a nested function to modify a variable defined in an outer (enclosing) function. It does not look in the global scope.

---

**Q5.10: Expert - [Late Binding Closures]**

What is printed?
```python
funcs = [lambda: i for i in range(3)]
print([f() for f in funcs])
```

A) `[0, 1, 2]`
B) `[2, 2, 2]`
C) `[0, 0, 0]`
D) `[3, 3, 3]`

**Answer: B**

**Explanation:**
Closures in Python capture variables by **reference**, not by value (late binding). By the time the lambdas are executed, the loop has finished, and `i` holds the final value `2`. All lambdas refer to this same `i`. Fix: `lambda i=i: i`.

---

**Q5.11: Basic - [Lambda Syntax]**

What is a correct lambda function to add 5 to inputs?

A) `def x: x + 5`
B) `lambda x: x + 5`
C) `lambda x -> x + 5`
D) `function(x) { return x + 5 }`

**Answer: B**

**Explanation:**
Standard syntax: `lambda arguments: expression`.

---

**Q5.12: Advanced - [Lambda Limitations]**

Which of the following is NOT allowed in a Python lambda?

A) Conditional expressions (`x if y else z`)
B) Function calls
C) Statements (like `x = 5`, `print`, `return`)
D) Multiple arguments

**Answer: C**

**Explanation:**
Lambdas are restricted to a **single expression**. Statements (assignment, `return`, `assert`, `while`) are not expressions and are illegal inside a lambda. (Note: `print()` is a function in Py3, so it is allowed, but `return` keyword is not).

---

**Q5.13: Intermediate - [Keyword-Only Arguments]**

How do you define a function where `c` must be passed as a keyword argument?

A) `def f(a, b, keyword c):`
B) `def f(a, b, *, c):`
C) `def f(a, b, &c):`
D) `def f(a, b, / c):`

**Answer: B**

**Explanation:**
The bare asterisk `*` in the parameter list indicates the end of positional arguments. Parameters following it (`c`) must be keyword-only.

---

**Q5.14: Advanced - [Positional-Only Arguments]**

Introduced in Python 3.8, what does `/` signify in `def f(a, b, /, c):`?

A) Division operator.
B) `a` and `b` are positional-only.
C) `c` is keyword-only.
D) `a` and `b` are optional.

**Answer: B**

**Explanation:**
The `/` allows defining positional-only parameters. Arguments before `/` cannot be passed by keyword. `f(a=1, ...)` would fail.

---

**Q5.15: Expert - [Function Introspection]**

Where are a function's default argument values stored?

A) `func.__args__`
B) `func.__defaults__`
C) `func.__closure__`
D) They are re-calculated every call.

**Answer: B**

**Explanation:**
`__defaults__` is a tuple containing the default values for positional arguments. (Keyword-only defaults are in `__kwdefaults__`).

---

**Q5.16: Intermediate - [Docstrings]**

How do you access the docstring of a function `my_func`?

A) `my_func.doc`
B) `my_func.__doc__`
C) `help(string)`
D) `my_func.__string__`

**Answer: B**

**Explanation:**
The docstring is stored in the `__doc__` attribute. `help()` displays it, but `__doc__` accesses the raw string.

---

**Q5.17: Advanced - [Unpacking in Calls 2]**

Combining list and dict unpacking:
`func(1, *[2], a=3, **{'b': 4})` is equivalent to:

A) `func(1, [2], a=3, {'b': 4})`
B) `func(1, 2, a=3, b=4)`
C) Syntax Error
D) `func(1, 2, 3, 4)`

**Answer: B**

**Explanation:**
Python unpacks `*[2]` to `2`, and `**{'b': 4}` to `b=4`. Result: `func(1, 2, a=3, b=4)`.

---

**Q5.18: Basic - [Recursion]**

What creates a default recursion depth limit in Python?

A) Memory only (stack overflow).
B) `sys.getrecursionlimit()` (typically 1000).
C) There is no limit.
D) The `@recursion` decorator.

**Answer: B**

**Explanation:**
Python prevents C stack overflows by enforcing a recursion limit, adjustable via `sys.setrecursionlimit()`. Default is usually 1000.

---

**Q5.19: Intermediate - [Annotations]**

What does `def f(x: int) -> str:` do at runtime?

A) Enforces types (raises Error if x is not int).
B) Converts x to int automatically.
C) Nothing (ignored by interpreter, stored in `__annotations__`).
D) Optimizes compiled code.

**Answer: C**

**Explanation:**
Type hints in strict Python are invalidation-free metadata. They are stored in `__annotations__` but are not enforced at runtime (unless using a separate tool like Pydantic or typeguard).

---

**Q5.20: Expert - [Scope Shadowing]**

```python
x = 10
def f():
    print(x)
    x = 20
f()
```
What happens?

A) Prints 10, then sets local x to 20.
B) Prints 10, sets global x to 20.
C) `UnboundLocalError`.
D) Syntax Error.

**Answer: C**

**Explanation:**
If a variable is assigned to (`x = 20`) anywhere inside a function, Python treats it as **local** for the entire function. The `print(x)` tries to access this local variable before it is initialized, causing `UnboundLocalError`.

---

**Q5.21: Advanced - [Closure Cell]**

Which attribute on a function object stores the remote variables captured by a closure?

A) `__globals__`
B) `__closure__`
C) `__enclosing__`
D) `__environment__`

**Answer: B**

**Explanation:**
`__closure__` is a tuple of cell objects containing the variables captured from the enclosing scope.

---

**Q5.22: Intermediate - [Parameter Ordering]**

What is the correct order of parameters in a definition?

A) `def f(args, standard, kwargs):`
B) `def f(standard, *args, kwonly, **kwargs):`
C) `def f(standard, **kwargs, *args):`
D) `def f(*args, standard):`

**Answer: B**

**Explanation:**
Correct order:
1. Positional/Standard
2. `*args`
3. Keyword-only arguments
4. `**kwargs`

---

**Q5.23: Basic - [First Class Objects]**

"Functions are first-class objects" means:

A) They are declared at the top of the file.
B) They can be assigned to variables, passed as arguments, and returned.
C) They are immutable.
D) They have higher priority than classes.

**Answer: B**

**Explanation:**
In Python, functions are objects like integers or strings. You can store them in data structures, pass them around, etc.

---

**Q5.24: Advanced - [Safe Defaults]**

What is the standard idiom to avoid the mutable default argument problem?

A) Use a tuple `val=()`.
B) Use `val=None` and check `if val is None: val = []`.
C) Use `val=list()`.
D) Use `copy.deepcopy`.

**Answer: B**

**Explanation:**
Using `None` as the sentinel value allows creating a new list *inside* the function call, ensuring each call gets a fresh list.

---

**Q5.25: Expert - [Deleting Global]**

If you delete a global variable inside a function using `global x; del x`, what happens?

A) Only the local reference is removed.
B) The global variable `x` is removed from the module namespace.
C) `SyntaxError`.
D) `PermissionError`.

**Answer: B**

**Explanation:**
`global x` binds the name `x` to the module scope. `del x` removes that name from the module's `__dict__`.

---

**Q5.26: Intermediate - [Inner Functions]**

Why are inner (nested) functions used?

A) To create closures/factories.
B) Hiding helper functions (encapsulation).
C) Decorator implementation.
D) All of the above.

**Answer: D**

**Explanation:**
All are valid use cases. Closures need nesting; hiding helpers keeps global namespace clean; decorators rely on nested wrapper functions.

---

**Q5.27: Advanced - [KWArgs Collision]**

`def f(a, **kwargs): pass`.
Call `f(a=1, a=2)`. What happens?

A) `kwargs` gets `{'a': 2}`.
B) `a` is 1.
C) `TypeError`: multiple values for argument 'a'.
D) `a` is 2.

**Answer: C**

**Explanation:**
`a` is a named parameter. Passing `a=2` attempts to pass it again (once as keyword `a=1` via position or name, then essentially colliding). Even `f(1, a=2)` fails. Python detects the collision.

---

**Q5.28: Basic - [Return Multiple]**

`def f(): return 1, 2`. What is the type of the return value?

A) List
B) Two integers (stack unpacking).
C) Tuple
D) Set

**Answer: C**

**Explanation:**
Code separated by commas returns a tuple. Parentheses are optional. `(1, 2)`.

---

**Q5.29: Advanced - [Method vs Function]**

When a function is accessed as an attribute of an instance, it becomes:

A) A static method.
B) A bound method.
C) A class method.
D) A closure.

**Answer: B**

**Explanation:**
Accessing `obj.func` creates a **bound method**. It wraps the function and automatically inserts `obj` as the first argument (`self`) when called.

---

**Q5.30: Intermediate - [Map Function]**

What does `map(func, iterable)` return in Python 3?

A) A list.
B) An iterator (map object).
C) A tuple.
D) None (applies in-place).

**Answer: B**

**Explanation:**
`map` is lazy in Python 3. It returns an iterator that computes values on demand. In Python 2, it returned a list.

---

**Q5.31: Intermediate - [Filter Function]**

What is the result of `list(filter(None, [0, 1, False, 2, ""]))`?

A) `[0, 1, 2]`
B) `[1, 2]`
C) `[0, 1, False, 2, ""]`
D) `[1, False, 2]`

**Answer: B**

**Explanation:**
When the function argument to `filter()` is `None`, it filters out elements that are Falsy (`0`, `False`, `""`). Only `1` and `2` remain.

---

**Q5.32: Advanced - [Partial Functions]**

Which module allows you to "freeze" some arguments of a function, creating a new callable?

A) `itertools`
B) `operations`
C) `functools`
D) `collections`

**Answer: C**

**Explanation:**
`functools.partial(func, *args, **kwargs)` creates a new partial object which behaves like `func` called with the supplied params.

---

**Q5.33: Expert - [Function Attributes]**

Can you attach arbitrary attributes to a Python function instance?
```python
def func(): pass
func.data = 42
```

A) No, functions are immutable.
B) Yes, functions are objects with a `__dict__`.
C) Only if using a decorator.
D) No, `AttributeError`.

**Answer: B**

**Explanation:**
Functions are full objects. You can assign arbitrary attributes to them, which is often used by web frameworks (like Flask/Django) or decorators to store metadata.

---

**Q5.34: Intermediate - [Star Operator in Call]**

What error occurs if you pass too many arguments via `*args` to a fixed-parameter function?
`def f(a, b): pass`
`f(*[1, 2, 3])`

A) `ValueError`
B) `IndexError`
C) `TypeError`
D) It ignores extra arguments.

**Answer: C**

**Explanation:**
`TypeError`: f() takes 2 positional arguments but 3 were given.

---

**Q5.35: Basic - [Variables in If block]**

Does a variable defined inside an `if` block persist after the block ends?
```python
if True:
    x = 10
print(x)
```

A) Yes
B) No, `NameError`.
C) Only if `else` is present.
D) Only in functions.

**Answer: A**

**Explanation:**
Python does not have block scope (variables are scoped to Function, Module, or Class). Variables defined in `if`, `for`, `while`, `with`, `try` blocks leak into the surrounding scope.

---

**Q5.36: Advanced - [Nonlocal vs Global]**

If you use `nonlocal x` when `x` exists only in the global scope (not the enclosing function), what happens?

A) It binds to the global variable.
B) It creates a new local variable.
C) `SyntaxError` (no binding for nonlocal 'x' found).
D) It imports `x`.

**Answer: C**

**Explanation:**
`nonlocal` strictly requires the variable to exist in a bound (enclosing) scope that is *not* global. If not found, it raises SyntaxError.

---

**Q5.37: Intermediate - [Recursive Lambda]**

How can a lambda function call itself recursively?

A) It cannot (it has no name).
B) By assigning it to a variable name first.
C) Using `self`.
D) Using `__func__`.

**Answer: B**

**Explanation:**
`fact = lambda n: 1 if n == 0 else n * fact(n-1)`. The lambda accesses the variable `fact` from the outer scope.

---

**Q5.38: Advanced - [Yield Statement]**

If a function contains the `yield` keyword, what does it return when called?

A) The yielded value.
B) `None`.
C) A generator object.
D) A list of values.

**Answer: C**

**Explanation:**
The presence of `yield` makes the function a generator factory. Calling it returns a generator iterator; the code body is not executed until `next()` is called on that iterator.

---

**Q5.39: Expert - [Yield From]**

What does `yield from iterator` do?

A) Needs a `for` loop to yield items one by one.
B) Delegates to the sub-generator, yielding all its values and handling `send`/`throw` transparently.
C) Imports values from another file.
D) Yields the iterator itself.

**Answer: B**

**Explanation:**
`yield from` is syntax for delegating to a sub-generator. It enables two-way communication (values out, data in via `.send()`) between the caller and the sub-generator.

---

**Q5.40: Intermediate - [Local Variable Trap]**

```python
x = 10
def f():
    print(x)
```
This prints 10.
```python
x = 10
def f():
    print(x)
    x = 20
```
This raises UnboundLocalError. Why?

A) Python is single-pass compiler.
B) Variable scope is determined statically at compile time.
C) `print` is asynchronous.
D) `x` is deleted.

**Answer: B**

**Explanation:**
Scope is determined statically. Because `x = 20` exists in the body, `x` is flagged as local for the *entire* function. The print statement tries to load this local `x` before assignment.

---

**Q5.41: Advanced - [Closure Reference]**

Does a closure keep the enclosing function's stack frame alive?

A) Yes, the whole frame is kept in memory.
B) No, only the referenced "cell" variables are kept alive.
C) No, it copies the values.
D) Only if the inner function is returned.

**Answer: B**

**Explanation:**
Python's closure mechanism uses "cells" (`PyCellObject`). Only the specific variables referred to by the inner function are stored in cells and kept alive. The rest of the enclosing frame can be reclaimed.

---

**Q5.42: Basic - [Type Hinting Return]**

The syntax `-> None` in a definition usually indicates:

A) The function does not return anything (returns `None`).
B) The function must return an empty string.
C) The function loops forever.
D) The function throws an error.

**Answer: A**

**Explanation:**
`def func() -> None:` is the standard type hint for void-like functions.

---

**Q5.43: Intermediate - [Call by Object Reference]**

If you pass a list to a function and the function does `lst.append(1)`, does the caller see the change?

A) Yes.
B) No.
C) Only if using `global`.
D) Only in Python 2.

**Answer: A**

**Explanation:**
Python uses "Call by Object Reference" (or "Call by Sharing"). Mutable objects passed as arguments can be modified in-place by the function.

---

**Q5.44: Advanced - [Rebinding Argument]**

If you pass a list to a function and the function does `lst = [1]`, does the caller see the change?

A) Yes.
B) No.
C) Only if `lst` was global.
D) Yes, but only in strict mode.

**Answer: B**

**Explanation:**
`lst = [1]` simply rebinds the local parameter name `lst` to a new list object. It breaks the link to the original object passed by the caller. The original list remains untouched.

---

**Q5.45: Expert - [UnboundLocalError vs NameError]**

What is the difference between `NameError` and `UnboundLocalError`?

A) They are unrelated.
B) `UnboundLocalError` is a subclass of `NameError`, specific to unassigned local variables.
C) `NameError` is for functions, `UnboundLocalError` for classes.
D) `UnboundLocalError` occurs at compile time.

**Answer: B**

**Explanation:**
`UnboundLocalError` inherits from `NameError`. It specifically occurs when a variable referenced is logically local (due to assignment elsewhere in the scope) but has not been bound a value yet in execution.

---

**Q5.46: Intermediate - [Dir Scoping]**

What does `dir()` return when called without arguments inside a function?

A) The list of global names.
B) The list of built-in names.
C) The list of names in the current local scope.
D) An empty list.

**Answer: C**

**Explanation:**
`dir()` without args returns the names in the current local symbol table.

---

**Q5.47: Advanced - [Function Decorator @]**

Applying a decorator `@wrap` to `func` is equivalent to:

A) `func = wrap(func)`
B) `wrap(func)`
C) `func = wrap`
D) `func(wrap)`

**Answer: A**

**Explanation:**
The `@decorator` syntax is syntactic sugar for passing the function definition to the decorator and assigning the result back to the function name.

---

**Q5.48: Basic - [Built-in Scope]**

Where does Python look if a name is not found in Local, Enclosing, or Global scopes?

A) It stops and raises NameError.
B) It checks the `builtins` module.
C) It checks the file system.
D) It checks `sys.path`.

**Answer: B**

**Explanation:**
The "B" in LEGB stands for Built-ins (e.g., `len`, `range`, `ValueError`), which live in the `builtins` module.

---

**Q5.49: Intermediate - [Help Function]**

Which function starts the interactive help utility?

A) `doc()`
B) `info()`
C) `help()`
D) `man()`

**Answer: C**

**Explanation:**
`help()` invokes the built-in help system.

---

**Q5.50: Advanced - [Method vs Function Type]**

Is `type(obj.method)` the same as `type(Class.method)`?

A) Yes, both are `function`.
B) No, `obj.method` is `method`, `Class.method` is `function` (in Python 3).
C) Yes, both are `method`.
D) No, `obj.method` is `closure`.

**Answer: B**

**Explanation:**
In Python 3, accessing a method on a class returns the raw function. Accessing it on an instance returns a bound method object.

---

**Q5.51: Expert - [Code Object Free Vars]**

Which attribute of a function's code object lists the names of variables captured from closure?

A) `co_varnames`
B) `co_freevars`
C) `co_names`
D) `co_closure`

**Answer: B**

**Explanation:**
`func.__code__.co_freevars` is a tuple containing the names of free variables (variables used in the function but defined in an enclosing scope).

---

**Q5.52: Intermediate - [Max Arguments]**

Is there a hard limit on the number of arguments a Python function can accept?

A) 255 (byte limit).
B) 65535.
C) No hard limit (memory dependent).
D) 20.

**Answer: C**

**Explanation:**
Historically (CPython < 3.7), explicit argument count was limited by byte code (`XX_ARG` opcodes being 1 byte/255). In modern Python (3.7+), the `EXTENDED_ARG` opcode allows for much higher limits, effectively removing the 255 barrier. Ideally, one should not use so many arguments, but the hard limit is gone.

---

**Q5.53: Advanced - [Recursive Lambdas 2]**

Can you write a recursive lambda without assigning it to a name? (e.g., essentially anonymous recursion).

A) No.
B) Yes, using the Y-combinator technique.
C) Yes, using `self`.
D) Only in Python 4.

**Answer: B**

**Explanation:**
It is possible using functional programming concepts (Y Combinator), though extremely unpythonic and unreadable. e.g., `(lambda f: (lambda x: f(lambda v: x(x)(v)))(lambda x: f(lambda v: x(x)(v))))(lambda f: lambda n: 1 if n == 0 else n * f(n-1))(5)`.

---

**Q5.54: Intermediate - [Return Tuple Unpacking]**

`x, y = f()` works because:

A) `f` returns two values.
B) `f` returns a tuple (or iterable) of length 2.
C) Python supports multiple return values natively without containers.
D) Magic.

**Answer: B**

**Explanation:**
Functions return a single object. If that object is a tuple (created by `return a, b`), the assignment side `x, y = ...` performs standard iterable unpacking.

---

**Q5.55: Advanced - [Function Annotation Access]**

If `def f(x: int): pass`, what is `f.__annotations__`?

A) `{'x': int}`
B) `{'x': 'int'}`
C) `[int]`
D) Empty dict (annotations are stripped).

**Answer: A**

**Explanation:**
It returns a dictionary mapping parameter names to the evaluated annotation values (the class `int`).

---

**Q5.56: Expert - [Exec Scope]**

When using `exec(code, globs, locs)`, if `locs` is usually a dictionary, do variable changes inside `exec` update `locs`?

A) Yes, always.
B) No, never.
C) Yes, but if `locs` is the actual local scope of a function, updates might be lost due to "fast locals" optimization.
D) `exec` is read-only.

**Answer: C**

**Explanation:**
Inside functions, Python uses optimized local variable access (via array slots, not a dict). `locals()` returns a *copy* or proxy of this state. Modifying the dict returned by `locals()` (passed to exec) does not reliably write back to the actual local frame variables.

---

**Q5.57: Basic - [Keyword Argument Order]**

In a function call `f(a=1, b=2)`, does the order of keyword arguments matter?

A) Yes, must match definition.
B) No, they are matched by name.
C) Yes, must be alphabetical.
D) Only if `*args` is used.

**Answer: B**

**Explanation:**
Keyword arguments are matched by name, so `f(b=2, a=1)` is identical to `f(a=1, b=2)`.

---

**Q5.58: Intermediate - [Call operator]**

To make an instance of a class callable like a function `obj()`, which method must be implemented?

A) `__init__`
B) `__call__`
C) `__run__`
D) `__func__`

**Answer: B**

**Explanation:**
`__call__` allows class instances to behave like functions.

---

**Q5.59: Advanced - [Nested Scope Variable]**

If an inner function reads a variable `x` from the outer function, and the outer function finishes returning the inner function. How does the inner function still access `x`?

A) It keeps a copy of `x` value.
B) It has a reference to the `x` object via a closure cell.
C) It accesses global `x`.
D) It converts `x` to a constant.

**Answer: B**

**Explanation:**
The variable `x` is stored in a `cell` object referenced by the inner function's `__closure__`. This cell keeps the object alive even after the outer function's frame is gone.

---

**Q5.60: Basic - [Pass by value/reference]**

Strictly speaking, Python's argument passing strategy is named:

A) Call by Value.
B) Call by Reference.
C) Call by Sharing (or Object Reference).
D) Call by Constant.

**Answer: C**

**Explanation:**
"Call by Sharing" means the *reference* (memory address) of the object is passed by value. We share the object. If mutable, changes show up. References can't be reseated (like Pointers in C++).

---

---

## Review Notes (2026-02-06)

- Q5.52 has an answer-key conflict: `**Answer: A**` but the explanation revises the answer to C and discusses modern behavior differently.
- Q5.52 also includes drafting text ("Self-correction", "Revised Answer") that should be cleaned for production content.
- Q5.43 and Q5.44 use only A/B options, which is inconsistent with the predominant 4-option MCQ format.
