# Chapter 5: Functions & Scope

> **Topics Covered**: Function definitions, parameters (positional, keyword, *, *args, **kwargs), default mutable arguments pitfall, LEGB scope resolution, closures, nonlocal, global, lambda functions, function annotations, function attributes, descriptor protocol

---

## Questions

---

**Q5.1: Basic - [Function Definition]**

What is the correct syntax to define a function in Python?

A) `function greet(): pass`
B) `def greet(): pass`
C) `greet() = function: pass`
D) `create greet(): pass`

**Answer: B**

**Explanation:**
Python uses the `def` keyword to define functions. Syntax: `def function_name(parameters): body`. The colon and indentation are required. No `function` keyword like JavaScript, no return type declaration required (but optional with type hints).

---

**Q5.2: Basic - [Return Statement]**

What is the output?
```python
def greet():
    print("Hello")

result = greet()
print(result)
```

A) `Hello` then `Hello`
B) `Hello` then `None`
C) `None` then `Hello`
D) Error

**Answer: B**

**Explanation:**
Functions without an explicit `return` statement return `None`. `greet()` prints "Hello" and implicitly returns `None`. `result` is assigned `None`, so the second print outputs `None`. Every Python function returns something — `None` if not specified.

---

**Q5.3: Basic - [Return Values]**

What is the output?
```python
def add(a, b):
    return a + b

print(add(3, 4))
```

A) `7`
B) `(3, 4)`
C) `34`
D) Error

**Answer: A**

**Explanation:**
The function adds integers a and b, returning 7. `return a + b` computes 3 + 4 = 7. The result is passed to print. Function returns are the primary way to get values out of functions.

---

**Q5.4: Intermediate - [Multiple Return Values]**

What is the output?
```python
def divide(a, b):
    return a // b, a % b

result = divide(17, 5)
print(result, type(result))
```

A) `3, 2, <class 'list'>`
B) `(3, 2), <class 'tuple'>`
C) `3 2, <class 'int'>`
D) Error

**Answer: B**

**Explanation:**
Multiple values after `return` are automatically packed into a tuple. `return a // b, a % b` returns `(3, 2)`. You can unpack: `q, r = divide(17, 5)`. This is a Pythonic way to return multiple values.

---

**Q5.5: Basic - [Positional Arguments]**

What is the output?
```python
def greet(name, greeting):
    print(f"{greeting}, {name}!")

greet("Alice", "Hello")
```

A) `Hello, Alice!`
B) `Alice, Hello!`
C) `greet, name!`
D) Error

**Answer: A**

**Explanation:**
Positional arguments are matched left-to-right. First argument "Alice" → `name`, second "Hello" → `greeting`. The f-string formats as "Hello, Alice!". Order matters for positional arguments.

---

**Q5.6: Basic - [Keyword Arguments]**

What is the output?
```python
def greet(name, greeting):
    print(f"{greeting}, {name}!")

greet(greeting="Hi", name="Bob")
```

A) `Hi, Bob!`
B) `Bob, Hi!`
C) Error: wrong order
D) `name, greeting!`

**Answer: A**

**Explanation:**
Keyword arguments are matched by name, not position. Order doesn't matter when using keyword arguments. `greeting="Hi"` and `name="Bob"` are explicitly assigned. This improves readability and flexibility.

---

**Q5.7: Intermediate - [Mixing Positional and Keyword]**

What is the output?
```python
def func(a, b, c):
    print(a, b, c)

func(1, c=3, b=2)
```

A) `1 2 3`
B) `1 3 2`
C) Error
D) `1 c=3 b=2`

**Answer: A**

**Explanation:**
Positional arguments must come before keyword arguments. `1` is assigned to `a` (positional), then `b=2` and `c=3` are assigned by name. Final values: a=1, b=2, c=3. Output: `1 2 3`.

---

**Q5.8: Intermediate - [Positional After Keyword Error]**

What is wrong with this call?
```python
def func(a, b, c):
    return a + b + c

func(a=1, 2, 3)
```

A) Nothing wrong
B) SyntaxError: positional arguments cannot follow keyword arguments
C) TypeError: too many arguments
D) ValueError

**Answer: B**

**Explanation:**
⚠️ Positional arguments must come BEFORE keyword arguments. `func(a=1, 2, 3)` has positional arguments after a keyword argument, which is a syntax error. Correct: `func(1, 2, 3)` or `func(1, b=2, c=3)`.

---

**Q5.9: Basic - [Default Arguments]**

What is the output?
```python
def greet(name, greeting="Hello"):
    print(f"{greeting}, {name}!")

greet("Alice")
greet("Bob", "Hi")
```

A) `Hello, Alice!` then `Hi, Bob!`
B) `Alice, Hello!` then `Bob, Hi!`
C) Error: missing argument
D) `greeting, name!` twice

**Answer: A**

**Explanation:**
Default arguments provide fallback values. `greeting="Hello"` is used when not specified. First call uses default, second overrides it. Parameters with defaults must come after parameters without defaults.

---

**Q5.10: Advanced - [Mutable Default Argument Pitfall]**

What is the output?
```python
def append_to(element, lst=[]):
    lst.append(element)
    return lst

print(append_to(1))
print(append_to(2))
```

A) `[1]` then `[2]`
B) `[1]` then `[1, 2]`
C) `[]` then `[]`
D) Error

**Answer: B**

**Explanation:**
⚠️ **Major pitfall**: Default mutable arguments are evaluated ONCE at function definition, not per call. The same list is reused. Both calls append to the same list. Fix: use `lst=None` and `if lst is None: lst = []` inside the function.

---

**Q5.11: Advanced - [Mutable Default Fix]**

What is the correct way to fix the mutable default argument issue?

A) `def func(lst=list())`
B) `def func(lst=None): if lst is None: lst = []`
C) `def func(lst=new []):`
D) `def func(lst=copy([])):`

**Answer: B**

**Explanation:**
💡 **Best practice**: Use `None` as default, then create a new mutable object inside the function. This ensures each call gets a fresh object. Alternative: use immutable default (tuple) if appropriate. This pattern is essential for lists, dicts, sets as defaults.

---

**Q5.12: Intermediate - [*args]**

What is the output?
```python
def func(*args):
    print(type(args), args)

func(1, 2, 3)
```

A) `<class 'list'> [1, 2, 3]`
B) `<class 'tuple'> (1, 2, 3)`
C) `<class 'args'> (1, 2, 3)`
D) Error

**Answer: B**

**Explanation:**
`*args` collects extra positional arguments into a **tuple** (not list). The name `args` is convention — you could use `*values`. Tuples are immutable, which is appropriate since these are input parameters.

---

**Q5.13: Intermediate - [**kwargs]**

What is the output?
```python
def func(**kwargs):
    print(type(kwargs), kwargs)

func(a=1, b=2)
```

A) `<class 'list'> [(a, 1), (b, 2)]`
B) `<class 'dict'> {'a': 1, 'b': 2}`
C) `<class 'tuple'> (('a', 1), ('b', 2))`
D) Error

**Answer: B**

**Explanation:**
`**kwargs` collects extra keyword arguments into a **dictionary**. Keys are parameter names (strings), values are the arguments. The name `kwargs` is convention. Order is preserved (Python 3.7+).

---

**Q5.14: Intermediate - [Combining *args and **kwargs]**

What is the correct order of parameters in a function definition?

A) `def f(*args, **kwargs, x):`
B) `def f(**kwargs, *args):`
C) `def f(x, *args, **kwargs):`
D) `def f(x, **kwargs, *args):`

**Answer: C**

**Explanation:**
Parameter order: regular parameters, `*args`, keyword-only parameters (after `*`), `**kwargs`. `*args` collects remaining positional args, `**kwargs` collects remaining keyword args. `**kwargs` must be last.

---

**Q5.15: Advanced - [Keyword-Only Arguments]**

What is the output?
```python
def func(a, *, b):
    print(a, b)

func(1, b=2)
```

A) `1 2`
B) Error: b is positional
C) `1, b=2`
D) Error: * is invalid

**Answer: A**

**Explanation:**
Bare `*` indicates that following parameters are keyword-only. `b` cannot be passed positionally — `func(1, 2)` would error. You must use `func(1, b=2)`. This enforces clarity for parameters that should be explicitly named.

---

**Q5.16: Advanced - [Positional-Only Arguments]**

🐍 What does `/` mean in a function signature (Python 3.8+)?

A) Division operator
B) Parameters before `/` are positional-only
C) Directory path separator
D) Comment marker

**Answer: B**

**Explanation:**
`def func(a, b, /, c):` means `a` and `b` are positional-only (can't use `a=1`). `c` can be positional or keyword. This matches built-in functions like `len()` where `len(obj=x)` isn't allowed. Improves API stability.

---

**Q5.17: Intermediate - [Unpacking in Function Calls]**

What is the output?
```python
def add(a, b, c):
    return a + b + c

nums = [1, 2, 3]
print(add(*nums))
```

A) `[1, 2, 3]`
B) `6`
C) Error: too many arguments
D) `123`

**Answer: B**

**Explanation:**
`*` unpacks an iterable into positional arguments. `add(*nums)` is equivalent to `add(1, 2, 3)`. This is useful for passing list/tuple elements as separate arguments. `**` similarly unpacks dictionaries into keyword arguments.

---

**Q5.18: Intermediate - [Dict Unpacking in Calls]**

What is the output?
```python
def greet(name, greeting):
    print(f"{greeting}, {name}!")

params = {"name": "Alice", "greeting": "Hello"}
greet(**params)
```

A) `Hello, Alice!`
B) `params, params!`
C) Error
D) `{"name": "Alice", "greeting": "Hello"}`

**Answer: A**

**Explanation:**
`**` unpacks a dictionary into keyword arguments. `greet(**params)` is equivalent to `greet(name="Alice", greeting="Hello")`. Keys must match parameter names. Useful for configuration dictionaries.

---

**Q5.19: Basic - [LEGB Scope]**

What does LEGB stand for in Python scope resolution?

A) Local, Enclosed, Global, Built-in
B) Local, External, General, Base
C) Lowest, Enclosed, Greatest, Built-in
D) Level, Environment, Global, Basic

**Answer: A**

**Explanation:**
LEGB is the scope lookup order: Local (current function), Enclosing (outer functions for nested functions), Global (module level), Built-in (Python built-ins). Python searches these scopes in order until it finds the name or raises NameError.

---

**Q5.20: Intermediate - [Local vs Global]**

What is the output?
```python
x = 10

def func():
    x = 20
    print(x)

func()
print(x)
```

A) `20` then `20`
B) `10` then `10`
C) `20` then `10`
D) `10` then `20`

**Answer: C**

**Explanation:**
`x = 20` inside the function creates a LOCAL variable `x`, shadowing the global. Function prints local x (20). Outside, global x is unchanged (10). Assignment creates a new local variable by default — it doesn't modify the outer scope.

---

**Q5.21: Intermediate - [global Keyword]**

What is the output?
```python
x = 10

def func():
    global x
    x = 20

func()
print(x)
```

A) `10`
B) `20`
C) Error
D) `None`

**Answer: B**

**Explanation:**
`global x` declares that `x` refers to the global variable. Now `x = 20` modifies the global, not creating a local. After calling `func()`, global x is 20. Use `global` sparingly — it creates hidden dependencies and makes code harder to reason about.

---

**Q5.22: Advanced - [UnboundLocalError]**

What is the output?
```python
x = 10

def func():
    print(x)
    x = 20

func()
```

A) `10`
B) `20`
C) UnboundLocalError
D) `None`

**Answer: C**

**Explanation:**
⚠️ **Gotcha**: Python determines scope at compile time. Because `x = 20` exists in the function, `x` is considered local throughout. The `print(x)` tries to read local x before it's assigned → UnboundLocalError. Use `global x` if you intend to use the global.

---

**Q5.23: Intermediate - [Enclosing Scope]**

What is the output?
```python
def outer():
    x = 10
    def inner():
        print(x)
    inner()

outer()
```

A) Error: x not defined
B) `10`
C) `None`
D) Error: can't access outer variable

**Answer: B**

**Explanation:**
Nested functions can READ variables from enclosing scopes. `x` isn't local to `inner`, so Python searches enclosing scope (outer) and finds x=10. This is the "E" in LEGB — enclosing function scope.

---

**Q5.24: Advanced - [nonlocal Keyword]**

What is the output?
```python
def outer():
    x = 10
    def inner():
        nonlocal x
        x = 20
    inner()
    print(x)

outer()
```

A) `10`
B) `20`
C) Error
D) `None`

**Answer: B**

**Explanation:**
`nonlocal x` allows modification of a variable from an enclosing (non-global) scope. Without it, `x = 20` would create a local variable in `inner`. With `nonlocal`, it modifies the `x` in `outer`. Useful for closures that maintain state.

---

**Q5.25: Advanced - [Closure]**

What is a closure?

A) A function that closes the program
B) A function that remembers values from its enclosing scope even after that scope has finished
C) A private function
D) A function that cannot be called

**Answer: B**

**Explanation:**
A closure is a function that captures (closes over) variables from its enclosing scope. Even after the outer function returns, the inner function retains access to those variables. Closures are powerful for creating factory functions and maintaining private state.

---

**Q5.26: Advanced - [Closure Example]**

What is the output?
```python
def make_counter():
    count = 0
    def counter():
        nonlocal count
        count += 1
        return count
    return counter

c = make_counter()
print(c(), c(), c())
```

A) `1 1 1`
B) `1 2 3`
C) `0 0 0`
D) Error

**Answer: B**

**Explanation:**
`make_counter` returns a closure that remembers and modifies `count`. Each call to `c()` increments the captured `count`. The state persists between calls. This is a powerful pattern for stateful functions without using classes.

---

**Q5.27: Basic - [Lambda Functions]**

What is a lambda function?

A) A Greek letter
B) An anonymous (unnamed) function defined with the `lambda` keyword
C) A function that always returns lambda
D) A recursive function

**Answer: B**

**Explanation:**
Lambda functions are small anonymous functions: `lambda arguments: expression`. They can have any number of arguments but only one expression (no statements). Used for short, one-off functions, especially with `map()`, `filter()`, `sorted()`.

---

**Q5.28: Basic - [Lambda Syntax]**

What is the output?
```python
square = lambda x: x ** 2
print(square(5))
```

A) `lambda x: x ** 2`
B) `25`
C) `x ** 2`
D) Error

**Answer: B**

**Explanation:**
`lambda x: x ** 2` creates a function that takes x and returns x squared. Assigned to `square`, it behaves like a regular function. `square(5)` returns 5² = 25. Equivalent to `def square(x): return x ** 2`.

---

**Q5.29: Intermediate - [Lambda with Multiple Args]**

What is the output?
```python
add = lambda a, b: a + b
print(add(3, 4))
```

A) `7`
B) `34`
C) `(3, 4)`
D) Error

**Answer: A**

**Explanation:**
Lambda can take multiple arguments: `lambda a, b: a + b`. It's equivalent to `def add(a, b): return a + b`. The expression after `:` is automatically returned. Result: 3 + 4 = 7.

---

**Q5.30: Intermediate - [Lambda in sorted]**

What is the output?
```python
pairs = [(1, 'b'), (3, 'a'), (2, 'c')]
sorted_pairs = sorted(pairs, key=lambda x: x[1])
print(sorted_pairs)
```

A) `[(1, 'b'), (3, 'a'), (2, 'c')]`
B) `[(3, 'a'), (1, 'b'), (2, 'c')]`
C) `['a', 'b', 'c']`
D) Error

**Answer: B**

**Explanation:**
The `key` function extracts the sort key. `lambda x: x[1]` returns the second element of each tuple. Sorted by second element: 'a' < 'b' < 'c'. Result: `[(3, 'a'), (1, 'b'), (2, 'c')]`. Lambda is perfect for such short extractors.

---

**Q5.31: Intermediate - [map with lambda]**

What is the output?
```python
nums = [1, 2, 3, 4]
result = list(map(lambda x: x * 2, nums))
print(result)
```

A) `[1, 2, 3, 4]`
B) `[2, 4, 6, 8]`
C) `8`
D) `<map object>`

**Answer: B**

**Explanation:**
`map(func, iterable)` applies func to each element. `lambda x: x * 2` doubles each number. `map` returns an iterator, so `list()` converts it. Result: `[2, 4, 6, 8]`. Modern style often prefers list comprehension: `[x * 2 for x in nums]`.

---

**Q5.32: Intermediate - [filter with lambda]**

What is the output?
```python
nums = [1, 2, 3, 4, 5, 6]
result = list(filter(lambda x: x % 2 == 0, nums))
print(result)
```

A) `[1, 3, 5]`
B) `[2, 4, 6]`
C) `[True, False, True, False, True, False]`
D) `6`

**Answer: B**

**Explanation:**
`filter(func, iterable)` keeps elements where func returns truthy. Lambda checks if x is even. Even numbers 2, 4, 6 pass the filter. Result: `[2, 4, 6]`. List comprehension equivalent: `[x for x in nums if x % 2 == 0]`.

---

**Q5.33: Advanced - [Lambda Closure Pitfall]**

What is the output?
```python
funcs = []
for i in range(3):
    funcs.append(lambda: i)

print([f() for f in funcs])
```

A) `[0, 1, 2]`
B) `[2, 2, 2]`
C) `[0, 0, 0]`
D) Error

**Answer: B**

**Explanation:**
⚠️ **Closure pitfall**: All lambdas capture the same variable `i`, not its value. When called, `i` has its final value (2). All return 2. Fix: `lambda i=i: i` captures current value as default argument, or use a factory function.

---

**Q5.34: Advanced - [Lambda Closure Fix]**

How to fix the lambda closure issue from Q5.33?

A) Use `global i`
B) Use `lambda i=i: i` to capture current value
C) Use `lambda: copy(i)`
D) Not fixable

**Answer: B**

**Explanation:**
Default argument values are evaluated at definition time. `lambda i=i: i` captures the current value of `i` as the default for parameter `i`. Each lambda gets its own captured value. This is a common idiom for the "late binding" closure issue.

---

**Q5.35: Basic - [Function Annotations]**

What is the output?
```python
def greet(name: str) -> str:
    return f"Hello, {name}"

print(greet(123))
```

A) Error: 123 is not a string
B) `Hello, 123`
C) `123`
D) Type mismatch error

**Answer: B**

**Explanation:**
Type annotations are NOT enforced at runtime — they're hints for documentation and type checkers. Passing 123 (int) to a `str`-annotated parameter works fine. f-strings convert it to string. Use mypy/Pyright for static type checking.

---

**Q5.36: Intermediate - [Accessing Annotations]**

How do you access a function's annotations?

A) `func.types`
B) `func.__annotations__`
C) `typing.get_annotations(func)`
D) `func.hints`

**Answer: B**

**Explanation:**
Function annotations are stored in `__annotations__` as a dictionary mapping parameter names to their annotations. `{'name': str, 'return': str}` for the previous example. `typing.get_type_hints()` is more robust for complex cases.

---

**Q5.37: Intermediate - [First-Class Functions]**

What does it mean that functions are "first-class" in Python?

A) Functions are the highest priority
B) Functions can be passed as arguments, returned from functions, assigned to variables
C) Functions are defined before anything else
D) Functions are faster than other objects

**Answer: B**

**Explanation:**
First-class means functions are objects like any other. You can: assign them to variables, pass them as arguments, return them from functions, store them in data structures. This enables functional programming patterns, decorators, callbacks.

---

**Q5.38: Intermediate - [Function as Argument]**

What is the output?
```python
def apply(func, value):
    return func(value)

def double(x):
    return x * 2

print(apply(double, 5))
```

A) `5`
B) `10`
C) `double(5)`
D) Error

**Answer: B**

**Explanation:**
`double` (without parentheses) is the function object itself, passed to `apply`. Inside `apply`, `func(value)` calls it: `double(5)` = 10. This pattern is fundamental to higher-order functions and functional programming.

---

**Q5.39: Advanced - [Function Attributes]**

What is the output?
```python
def greet():
    """Says hello"""
    pass

print(greet.__name__, greet.__doc__)
```

A) `greet, Says hello`
B) `greet Says hello`
C) `__name__ __doc__`
D) Error

**Answer: B**

**Explanation:**
Functions have attributes: `__name__` (function name), `__doc__` (docstring), `__defaults__` (default arg values), `__code__` (code object), etc. These are useful for introspection, decorators, and documentation tools.

---

**Q5.40: Advanced - [Custom Function Attributes]**

Can you add custom attributes to functions?

A) No, functions are immutable
B) Yes, functions are objects with a `__dict__`
C) Only with decorators
D) Only built-in functions

**Answer: B**

**Explanation:**
Functions have `__dict__` for custom attributes. You can add: `func.cache = {}` or `func.call_count = 0`. Useful for function-level caching, counting calls, or attaching metadata. Decorators often use this for wrapper bookkeeping.

---

**Q5.41: Intermediate - [Docstrings]**

What is the recommended way to document a function?

A) Comments above the function
B) Docstring as the first statement in the function body
C) README file
D) Variable named `description`

**Answer: B**

**Explanation:**
💡 **Best practice**: Use a docstring — a string literal as the first statement. Triple quotes for multi-line: `"""Description"""`. Docstrings are accessible via `help()` and `__doc__`. Follow conventions like Google style, NumPy style, or reStructuredText.

---

**Q5.42: Intermediate - [help() function]**

What does `help(func)` display?

A) The source code
B) The docstring and signature
C) Type information only
D) Nothing for user-defined functions

**Answer: B**

**Explanation:**
`help()` shows the function signature and docstring (if any). For built-in functions, it shows detailed documentation. It uses the `pydoc` module. For interactive exploration, `help()` is invaluable. No docstring? It shows just the signature.

---

**Q5.43: Basic - [Return vs Print]**

What is the difference between `return` and `print` in a function?

A) No difference
B) `return` outputs to screen, `print` stores the value
C) `return` gives a value back to the caller, `print` displays to stdout
D) `print` is faster

**Answer: C**

**Explanation:**
`return` exits the function and provides a value to the caller (can be used in expressions, assigned to variables). `print` displays text to stdout and returns `None`. A function that prints but doesn't return gives `None` to its caller. They serve different purposes.

---

**Q5.44: Intermediate - [Early Return]**

What is the output?
```python
def check(x):
    if x < 0:
        return "Negative"
    if x == 0:
        return "Zero"
    return "Positive"

print(check(-5))
```

A) `Negative Zero Positive`
B) `Negative`
C) `Positive`
D) Error

**Answer: B**

**Explanation:**
`return` immediately exits the function. When x=-5, the first condition is True, "Negative" is returned, and execution stops. Subsequent returns are never reached. Early returns improve readability by handling edge cases first.

---

**Q5.45: Advanced - [functools.partial]**

What does `functools.partial` do?

A) Partially executes a function
B) Creates a new function with some arguments pre-filled
C) Returns part of the function's code
D) Divides a function into parts

**Answer: B**

**Explanation:**
`partial(func, *args, **kwargs)` creates a new callable with some arguments "frozen". `from functools import partial; double = partial(multiply, 2)` creates a function that always multiplies by 2. Useful for callbacks and adapting functions to different signatures.

---

**Q5.46: Intermediate - [functools.partial Example]**

What is the output?
```python
from functools import partial

def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)
print(square(5))
```

A) `25`
B) `10`
C) `2`
D) Error

**Answer: A**

**Explanation:**
`partial(power, exponent=2)` creates a function where `exponent` is fixed at 2. Calling `square(5)` is like `power(5, exponent=2)` = 5² = 25. Useful for creating specialized versions of general functions.

---

**Q5.47: Advanced - [Recursion]**

What is the output?
```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))
```

A) `5`
B) `120`
C) `15`
D) Error: RecursionError

**Answer: B**

**Explanation:**
Factorial via recursion: 5! = 5 × 4 × 3 × 2 × 1 = 120. Base case: n ≤ 1 returns 1. Recursive case: n × factorial(n-1). Python has a default recursion limit (~1000), so deep recursion may fail.

---

**Q5.48: Advanced - [Recursion Limit]**

What happens with very deep recursion in Python?

A) Python handles it automatically
B) RecursionError is raised when the limit is exceeded
C) The program silently fails
D) Memory automatically expands

**Answer: B**

**Explanation:**
Python has a recursion limit (default ~1000) to prevent stack overflow. `sys.getrecursionlimit()` returns it, `sys.setrecursionlimit(n)` changes it. For deep recursion, use iteration or tail-call optimization libraries. Python doesn't optimize tail recursion.

---

**Q5.49: Advanced - [Generator vs Regular Function]**

What makes a function a generator?

A) Returning a list
B) Using the `yield` keyword
C) Having `generator` in the name
D) Returning multiple values

**Answer: B**

**Explanation:**
Any function with `yield` becomes a generator function. When called, it returns a generator object (iterator) instead of executing immediately. `yield` produces values one at a time, remembering state between calls. Covered in detail in Chapter 9.

---

**Q5.50: Intermediate - [Function as Object]**

What is the output?
```python
def greet():
    return "Hello"

funcs = [greet, greet, greet]
print(funcs[0]())
```

A) `[greet, greet, greet]`
B) `Hello`
C) `greet`
D) Error

**Answer: B**

**Explanation:**
Functions can be stored in lists. `funcs[0]` retrieves the function object, `()` calls it. `funcs[0]()` is equivalent to `greet()`, returning "Hello". This enables function dispatch tables and other patterns.

---

**Q5.51: Expert - [Function Code Object]**

What does `func.__code__` contain?

A) The function's source code as a string
B) A code object with bytecode, variable names, and other metadata
C) Encrypted code
D) C code

**Answer: B**

**Explanation:**
`__code__` is a code object containing compiled bytecode, local variable names, constants, argument count, etc. Useful for introspection: `func.__code__.co_varnames` (local vars), `co_argcount` (argument count). Not the source code itself.

---

**Q5.52: Expert - [Descriptor Protocol in Functions]**

Why does accessing a function as a class attribute return a method?

A) Python magic
B) Functions implement the descriptor protocol (__get__)
C) Classes convert functions automatically
D) It doesn't — they're the same

**Answer: B**

**Explanation:**
Functions implement `__get__`, making them non-data descriptors. When accessed through an instance, `__get__` binds the function to the instance, creating a bound method. This is how `self` gets passed automatically. `func.__get__(obj, type)` returns a method.

---

**Q5.53: Intermediate - [Callable Objects]**

How can you make a class instance callable?

A) Add a `call` method
B) Implement `__call__`
C) Inherit from `callable`
D) Add `@callable` decorator

**Answer: B**

**Explanation:**
Implementing `__call__(self, ...)` makes an instance callable like a function. `obj()` invokes `obj.__call__()`. Useful for stateful functions (closure alternative), function objects with configuration, or callable factory objects.

---

**Q5.54: Intermediate - [Callable Check]**

How do you check if something is callable?

A) `type(x) == function`
B) `callable(x)`
C) `x.is_callable()`
D) `hasattr(x, 'call')`

**Answer: B**

**Explanation:**
`callable(obj)` returns True if `obj` appears callable (has `__call__` or is a function/class). Classes are callable (return instances). Don't use `hasattr(x, '__call__')` alone — it's less reliable. `callable()` handles edge cases correctly.

---

**Q5.55: Advanced - [Type Hints Complex Types]**

What type hint represents a function that takes a string and returns an int?

A) `Function[str, int]`
B) `Callable[[str], int]`
C) `(str) -> int`
D) `def(str): int`

**Answer: B**

**Explanation:**
`Callable[[arg_types], return_type]` from the `typing` module represents callable signatures. `Callable[[str], int]` = function taking str, returning int. Python 3.10+ allows `(str) -> int` in some contexts. `Callable[..., int]` = any args, returns int.

---

**Q5.56: Expert - [Introspection with inspect]**

Which module provides tools for introspecting functions?

A) reflection
B) introspect
C) inspect
D) meta

**Answer: C**

**Explanation:**
The `inspect` module provides functions for examining live objects: `inspect.signature(func)` (signature details), `inspect.getsource(func)` (source code), `inspect.getmembers()` (all attributes), `inspect.isfunction()`, etc. Essential for metaprogramming.

---

**Q5.57: Intermediate - [Function Purity]**

What is a "pure" function?

A) A function with no bugs
B) A function that only returns value without side effects and returns same output for same input
C) A function without parameters
D) A function that only uses built-ins

**Answer: B**

**Explanation:**
Pure functions: (1) no side effects (don't modify external state), (2) deterministic (same input → same output). `len()` is pure; `random.random()` is not. Pure functions are easier to test, reason about, and parallelize. Important in functional programming.

---

**Q5.58: Intermediate - [Side Effects]**

Which function has a side effect?
```python
def f1(x): return x * 2
def f2(x): print(x); return x
def f3(x): return x + 1
def f4(x): return x ** 2
```

A) f1
B) f2
C) f3
D) f4

**Answer: B**

**Explanation:**
`print()` is a side effect — it outputs to stdout, changing the external state. f1, f3, f4 are pure: they only compute and return values without affecting anything outside. Side effects make functions harder to test and reason about.

---

**Q5.59: Advanced - [Function Composition]**

What is function composition?

A) Writing functions inside functions
B) Combining functions where output of one becomes input of another
C) Naming functions with related names
D) Creating composite data types

**Answer: B**

**Explanation:**
Composition: `(f ∘ g)(x) = f(g(x))`. In Python: `result = f(g(x))`. Libraries like `toolz` provide `compose`. Common pattern: `sorted(set(map(str.lower, words)))`. Each function transforms the data, feeding into the next.

---

**Q5.60: Expert - [Higher-Order Functions]**

What is a higher-order function?

A) A function with many parameters
B) A function that takes functions as arguments or returns functions
C) A function defined at the top of a file
D) An optimized function

**Answer: B**

**Explanation:**
Higher-order functions either: take functions as arguments (like `map`, `filter`, `sorted`), or return functions (like decorators, closures). They enable powerful abstractions and functional programming patterns. Python's support for higher-order functions is fundamental to its expressiveness.

---

**Q5.61: Intermediate - [Default Parameter Evaluation]**

When are default parameter values evaluated?

A) Each time the function is called
B) Once, when the function is defined
C) When the module is imported
D) When the parameter is used

**Answer: B**

**Explanation:**
Default values are evaluated ONCE at function definition time, not at call time. That's why mutable defaults are problematic — the same object is reused. Expressions like `def f(x=datetime.now())` capture the definition-time value, not call-time.

---

**Q5.62: Advanced - [Late Binding Defaults]**

How can you have a default that's evaluated at call time?

A) Use `dynamic = True`
B) Use `None` as default and compute inside the function
C) Use `@late_binding` decorator
D) Not possible

**Answer: B**

**Explanation:**
💡 Pattern: `def func(x=None): if x is None: x = compute_default()`. This evaluates `compute_default()` each call. Common for mutable defaults, timestamps, or configuration that might change. Sentinel objects (`_MISSING = object()`) allow `None` as a valid input.

---

**Q5.63: Intermediate - [Order of Argument Types]**

What is the correct order of parameter types in a function signature?

A) `*args, regular, **kwargs`
B) `regular, *args, keyword-only, **kwargs`
C) `**kwargs, *args, regular`
D) Any order

**Answer: B**

**Explanation:**
Complete order: positional-only (before `/`), regular positional/keyword, `*args`, keyword-only (after `*` or `*args`), `**kwargs`. Example: `def f(a, /, b, *args, c, **kwargs)`. This structure provides maximum flexibility.

---

**Q5.64: Expert - [functools.wraps]**

What is the purpose of `@functools.wraps(func)` in decorators?

A) Wraps the function in error handling
B) Preserves the original function's metadata (__name__, __doc__, etc.)
C) Makes the function run faster
D) Adds type checking

**Answer: B**

**Explanation:**
When creating a wrapper function in a decorator, the wrapper's `__name__`, `__doc__`, etc. replace the original's. `@wraps(func)` copies these attributes from the wrapped function to the wrapper, preserving introspection capabilities. Essential for well-behaved decorators.

---

**Q5.65: Advanced - [Function Caching]**

What does `@functools.lru_cache` do?

A) Limits function execution time
B) Caches function results based on arguments for reuse
C) Logs function calls
D) Rate-limits function calls

**Answer: B**

**Explanation:**
`@lru_cache(maxsize=128)` memoizes function results. If called with the same arguments, returns cached result instead of recomputing. "LRU" = Least Recently Used (eviction policy). Arguments must be hashable. Great for expensive, pure functions.

---

## Chapter Summary

**Total MCQs: 65**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 16 | 25% |
| Intermediate | 31 | 48% |
| Advanced | 15 | 23% |
| Expert | 3 | 4% |

**Key Topics Covered:**
- Function definitions and return values
- Parameters: positional, keyword, *args, **kwargs
- Mutable default argument pitfall
- LEGB scope resolution
- global and nonlocal keywords
- Closures
- Lambda functions
- Higher-order functions (map, filter)
- Function annotations and type hints
- Function attributes and introspection
- functools (partial, wraps, lru_cache)
