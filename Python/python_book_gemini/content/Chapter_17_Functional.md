# Chapter 17: Functional Programming

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `lambda` functions, `map`/`filter`/`reduce`, List/Dict/Set Comprehensions, Generator Expressions, Closures, Decorators (functional aspect), `functools` (`partial`, `reduce`, `singledispatch`), Higher-order functions.

---

**Q17.1: Basic - [Lambda Syntax]**

What is the correct syntax for a lambda function adding two numbers?

A) `lambda x, y: return x + y`
B) `lambda x, y: x + y`
C) `def lambda(x, y): x + y`
D) `lambda(x, y) { x + y }`

**Answer: B**

**Explanation:**
Lambda functions are anonymous single-expression functions. They do not use `return` explicitly; the result of the expression is returned automatically.

---

**Q17.2: Intermediate - [Map Function]**

`list(map(lambda x: x*2, [1, 2, 3]))` returns:

A) `[1, 2, 3]`
B) `[2, 4, 6]`
C) `[(1, 2), (2, 4), (3, 6)]`
D) `[3, 6, 9]`

**Answer: B**

**Explanation:**
`map` applies the function to every item in the iterable and returns an iterator (converted to list here).

---

**Q17.3: Advanced - [Closure Definition]**

A closure occurs when:

A) A function captures variables from its enclosing scope (even after the outer function finishes).
B) A function is closed.
C) A class is instantiated.
D) A file is closed.

**Answer: A**

**Explanation:**
Closures allow nested functions to retain access to variables from their parent scope, effectively "closing over" the environment.

---

**Q17.4: Basic - [Filter Function]**

`list(filter(lambda x: x > 1, [1, 2, 3]))` returns:

A) `[1, 2, 3]`
B) `[2, 3]`
C) `[False, True, True]`
D) `[1]`

**Answer: B**

**Explanation:**
`filter` returns only elements for which the function returns True.

---

**Q17.5: Intermediate - [Reduce usage]**

`functools.reduce(lambda x, y: x+y, [1, 2, 3, 4])` calculates:

A) The sum: 10.
B) The product: 24.
C) The average.
D) A list `[1, 2, 3, 4]`.

**Answer: A**

**Explanation:**
It applies the rolling computation: `((1+2)+3)+4`.

---

**Q17.6: Advanced - [List Comprehension vs Map]**

Why is `[f(x) for x in data]` generally preferred over `list(map(f, data))` in modern Python?

A) Ideally, map is deprecated.
B) List comprehensions are more readable and often faster (no function call overhead if expression is inline).
C) Map cannot handle lambdas.
D) Map is memory inefficient.

**Answer: B**

**Explanation:**
While `map` is functionally valid, comprehensions are Pythonic and avoid the overhead of calling the lambda function for every element if the operation can be written as an expression.

---

**Q17.7: Basic - [Generator Expression]**

`(x**2 for x in range(3))` returns:

A) A tuple `(0, 1, 4)`.
B) A list `[0, 1, 4]`.
C) A generator object.
D) An error.

**Answer: C**

**Explanation:**
Parentheses around a comprehension syntax create a generator expression, which yields items lazily.

---

**Q17.8: Intermediate - [Dict Comprehension]**

`{x: x**2 for x in range(3)}` results in:

A) `{0, 1, 4}` (Set)
B) `{0: 0, 1: 1, 2: 4}` (Dict)
C) `[(0,0), (1,1), (2,4)]`
D) Error.

**Answer: B**

**Explanation:**
The `{key: value ...}` syntax creates a dictionary.

---

**Q17.9: Advanced - [Late Binding Closures]**

`funcs = [lambda: i for i in range(3)]`. `funcs[0]()` returns:

A) 0
B) 2
C) 1
D) Error.

**Answer: B**

**Explanation:**
Closures bind variables by *reference*, not value. By the time the lambdas are called, the loop variable `i` has reached its final value (2). Fix: `lambda i=i: i`.

---

**Q17.10: Expert - [Partial Application]**

`functools.partial` is effectively:

A) Currying.
B) Partial application (fixing some arguments).
C) Just a wrapper.
D) A decorator.

**Answer: B**

**Explanation:**
It creates a new function with some arguments pre-filled. Currying is technically transforming `f(a,b,c)` into `f(a)(b)(c)`, whereas partial creates `g(b,c) = f(fixed_a, b, c)`.

---

**Q17.11: Basic - [Pure Function]**

A pure function:

A) Returns `None`.
B) Has no side effects and always returns the same output for same inputs.
C) Is defined with `pure` keyword.
D) Uses no arguments.

**Answer: B**

**Explanation:**
Core concept of functional programming. Makes testing and concurrency easier.

---

**Q17.12: Intermediate - [Single Dispatch]**

`@functools.singledispatch` allows:

A) Disabling a function.
B) Function overloading based on the type of the first argument.
C) Single threading.
D) Dispatching events.

**Answer: B**

**Explanation:**
It transforms a function into a generic function, allowing you to register different implementations for different types.

---

**Q17.13: Advanced - [Nested Comprehension]**

`[x for sublist in [[1,2], [3]] for x in sublist]` results in:

A) `[[1,2], [3]]`
B) `[1, 2, 3]` (Flattened)
C) `[1, 3]`
D) Error.

**Answer: B**

**Explanation:**
The order of `for` clauses matches nested loops: `for sublist ... for x ...`. It flattens the list of lists.

---

**Q17.14: Basic - [Lambda Limit]**

Lambdas are limited because:

A) They cannot take arguments.
B) They can only contain a single expression (no statements like `if/else` block, `assignment`, `while`).
C) They are slow.
D) They cannot return values.

**Answer: B**

**Explanation:**
By design, intended for simple, throwaway functions.

---

**Q17.15: Intermediate - [Filter None]**

`filter(None, [0, 1, 2, ''])` filters out:

A) `None`.
B) Falsy values (`0`, `''`, `None`, `False`).
C) Truthy values.
D) Nothing.

**Answer: B**

**Explanation:**
If the function argument is `None`, `filter` uses the identity function, keeping only elements that evaluate to True.

---

**Q17.16: Advanced - [Nonlocal Keyword]**

To modify a variable in an outer (enclosing) scope from an inner function, use:

A) `global`
B) `nonlocal`
C) `outer`
D) `super`

**Answer: B**

**Explanation:**
`nonlocal` allows assignment to variables in the nearest enclosing scope (excluding globals).

---

**Q17.17: Expert - [Y Combinator equivalent]**

Is it possible to implement recursion with anonymous lambdas in Python (without assigning to a name)?

A) No.
B) Yes, using the Y combinator pattern (fixed-point combinator).
C) Yes, using `self`.
D) Only in Python 2.

**Answer: B**

**Explanation:**
Technically possible via functional concepts, though extremely un-Pythonic. E.g. `(lambda f: (lambda x: f(lambda v: x(x)(v)))(lambda x: f(lambda v: x(x)(v))))`.

---

**Q17.18: Intermediate - [Wraps Decorator]**

`@functools.wraps(wrapped_func)` is used to:

A) Wrap the function in a try-catch.
B) Copy metadata (`__name__`, `__doc__`, etc.) from the original function to the wrapper.
C) Make it faster.
D) Wrap text.

**Answer: B**

**Explanation:**
Without it, decorated functions lose their original identity (name/docstring), confusing introspection tools.

---

**Q17.19: Basic - [First Class Objects]**

"Functions are first-class objects" means:

A) They are the most important.
B) They can be passed as arguments, returned from functions, and assigned to variables.
C) They are classes.
D) They run first.

**Answer: B**

**Explanation:**
Enables higher-order functions and functional paradigms.

---

**Q17.20: Advanced - [Reduce Initializer]**

If `reduce` is called without an `initializer`, and the list has 1 element:

A) It calls the function once.
B) It returns that element without calling the function.
C) Error.
D) Returns None.

**Answer: B**

**Explanation:**
With 1 element, no reduction is needed; the element itself is the result.

---

**Q17.21: Expert - [Lru Cache Typed]**

`@lru_cache(typed=True)` treats `3` and `3.0` as:

A) The same argument (cache hit).
B) Different arguments (cache miss).
C) Error.
D) Strings.

**Answer: B**

**Explanation:**
With `typed=True`, arguments of different types map to different cache entries even if they compare equal.

---

**Q17.22: Intermediate - [Set Comprehension]**

`{x%2 for x in range(10)}` returns:

A) `{0, 1}`
B) `[0, 1, 0, 1...]`
C) `{0, 1, 2, 3...}`
D) Error.

**Answer: A**

**Explanation:**
Set comprehension builds a set, automatically removing duplicates. Results are `0` and `1`.

---

**Q17.23: Basic - [Any Usage]**

`any([False, 0, ''])` returns:

A) True.
B) False.
C) None.
D) Error.

**Answer: B**

**Explanation:**
All elements are falsy, so `any` returns False.

---

**Q17.24: Advanced - [Key Argument]**

Functions like `max()`, `min()`, `sort()` take a `key` argument. `key` expects:

A) A dictionary.
B) A single-argument function that transforms each element before comparison.
C) A boolean.
D) An index.

**Answer: B**

**Explanation:**
Allows custom sorting logic (e.g. `key=len` to sort strings by length).

---

**Q17.25: Intermediate - [Decorator Basic]**

A decorator is conceptually:

A) A function that takes a function and returns a modified function (or callable).
B) A keyword `decorator`.
C) A comment.
D) A class method.

**Answer: A**

**Explanation:**
Basic definition of the `@decorator` syntax sugar.

---

**Q17.26: Expert - [Function Attributes]**

Since functions are objects, can you attach arbitrary attributes to them? `func.count = 0`.

A) No.
B) Yes.
C) Only inside the function.
D) Only if defined as a class.

**Answer: B**

**Explanation:**
User-defined functions allow arbitrary attribute assignment, often used for caching or state (though closures or classes are usually cleaner).

---

**Q17.27: Basic - [Zip Function]**

`zip([1,2], [3,4])` helps to:

A) Compress files.
B) Combine two iterables element-wise into tuples `(1, 3), (2, 4)`.
C) Concatenate lists.
D) Encrypt data.

**Answer: B**

**Explanation:**
Standard tool for parallel iteration.

---

**Q17.28: Advanced - [Cmp to Key]**

If you have an old-style comparison function `cmp(a, b)` returning -1/0/1, how do you use it with `sorted(key=...)`?

A) `key=cmp`
B) `key=functools.cmp_to_key(cmp)`
C) You can't.
D) `key=cmp(a,b)`

**Answer: B**

**Explanation:**
Python 3 removed the `cmp` argument from sort. `cmp_to_key` wraps the comparison function into a class that implements comparison dunder methods (`__lt__`, etc.) usable as a key.

---

**Q17.29: Intermediate - [Operator Module]**

The `operator` module (e.g., `operator.add`) is useful when:

A) You want to avoid using `+`.
B) You need to pass arithmetic/logical operators as functions (e.g., to `reduce` or `map`).
C) You want faster math.
D) You are using classes.

**Answer: B**

**Explanation:**
Instead of writing `lambda x, y: x+y`, you can use `operator.add`, which is faster and cleaner.

---

**Q17.30: Expert - [MethodCaller]**

`operator.methodcaller('split', ' ')(string)` is equivalent to:

A) `string.split(' ')`
B) `split(string, ' ')`
C) `string('split', ' ')`
D) Error.

**Answer: A**

**Explanation:**
`methodcaller` creates a function that calls a method on its object argument. Useful in functional pipelines (like map).

---

**Q17.31: Intermediate - [Generator Expression Memory]**

Compared to `[x*2 for x in range(1000000)]`, `(x*2 for x in range(1000000))` uses:

A) Same memory.
B) Significantly less memory.
C) More memory.
D) Depends on OS.

**Answer: B**

**Explanation:**
Generators yield items one by one and do not store the entire sequence in memory, making them ideal for large datasets.

---

**Q17.32: Advanced - [Functools Reduce Args]**

`functools.reduce` requires a function that accepts how many arguments?

A) 1
B) 2
C) 3
D) Variable.

**Answer: B**

**Explanation:**
It applies a binary function (taking two arguments) cumulatively to the items of the iterable. `val = func(accumulator, current_item)`.

---

**Q17.33: Basic - [Lambda Closure]**

Can a lambda function access variables defined in its outer scope?

A) Yes.
B) No.
C) Only if declared global.
D) Only constants.

**Answer: A**

**Explanation:**
Lambdas support full lexical scoping (closures) just like `def` functions.

---

**Q17.34: Expert - [Recursive Lambda]**

Assigning a lambda to a variable allows recursion: `fact = lambda x: 1 if x == 0 else x * fact(x-1)`.
Is this considered "anonymous" recursion?

A) Yes.
B) No, because it relies on the name `fact` being bound in the closure.
C) It is invalid syntax.
D) It causes a stack overflow immediately.

**Answer: B**

**Explanation:**
True anonymous recursion requires combinators (like Y combinator) because the lambda itself has no name to refer to itself. Relying on `fact` works only if `fact` is not reassigned.

---

**Q17.35: Intermediate - [Filter usage]**

`filter(lambda x: x % 2 == 0, range(5))` returns an iterator yielding:

A) `1, 3`
B) `0, 2, 4`
C) `0, 1, 2, 3, 4`
D) `False, True, False, True, False`

**Answer: B**

**Explanation:**
 Keeps elements where `x % 2 == 0` is True.

---

**Q17.36: Advanced - [Cell Objects]**

Closures in Python are implemented using:

A) Cell objects (`__closure__` attribute).
B) Global variables.
C) Hidden classes.
D) Copying the function code.

**Answer: A**

**Explanation:**
Variables captured by a closure are stored in special "cell" objects referenced by the `__closure__` tuple of the function object.

---

**Q17.37: Basic - [Map Multiple Iterables]**

`map(lambda x, y: x+y, [1, 2], [10, 20])` yields:

A) `11, 22`
B) `1, 2, 10, 20`
C) `Error`.
D) `(1, 10), (2, 20)`

**Answer: A**

**Explanation:**
If multiple iterables are passed, the function must accept that many arguments. `map` consumes them in parallel.

---

**Q17.38: Intermediate - [Partial vs Default Args]**

Difference between `partial(func, a=1)` and defining `def func(a=1, ...)`:

A) `partial` creates a new function object; default args are stored in the original function.
B) `partial` is faster.
C) Default args are mutable.
D) No difference.

**Answer: A**

**Explanation:**
`partial` dynamically wraps the function. Default arguments are evaluated once at definition time.

---

**Q17.39: Advanced - [Callable Class]**

A class instance can behave like a function (closure) if the class defines:

A) `__init__`
B) `__call__`
C) `__func__`
D) `__closure__`

**Answer: B**

**Explanation:**
Implementing `__call__` allows instances to be invoked using `()` syntax, often used to create stateful functions (an OOP alternative to closures).

---

**Q17.40: Expert - [Function Attributes vs Closures]**

When maintaining state in a function, which is generally thread-safe for independent calls?

A) Function attributes (`func.state = 1`).
B) Closures (using `nonlocal` state created per call).
C) Global variables.
D) None.

**Answer: B**

**Explanation:**
Function attributes are stored on the function object (singleton), so they are shared across all threads/calls (not thread-safe without locks). A closure created by a factory function has independent state for each instance.

---

**Q17.41: Intermediate - [Sorted Key Lambda]**

Sorting a list of strings by their last character:

A) `sorted(L, key=lambda s: s[-1])`
B) `sorted(L, key=lambda s: s[0])`
C) `sorted(L, reverse=True)`
D) `sorted(L, key=-1)`

**Answer: A**

**Explanation:**
The key function extracts the sort criterion.

---

**Q17.42: Basic - [Immutability]**

Functional programming heavily relies on:

A) Global state.
B) Mutable data structures.
C) Immutable data and pure functions.
D) For loops.

**Answer: C**

**Explanation:**
Avoids side-effects by not modifying state in place.

---

**Q17.43: Advanced - [Yield From]**

`yield from iterator` is equivalent to:

A) `yield iterator`
B) `for x in iterator: yield x` (plus handling return values/exceptions).
C) `return iterator`
D) `yield next(iterator)`

**Answer: B**

**Explanation:**
It delegates the generator responsibility to a sub-generator, transparantly passing values out and sent values/exceptions in.

---

**Q17.44: Expert - [Reduce Empty Error]**

`functools.reduce(lambda x,y: x+y, [])` raises:

A) `TypeError: reduce() of empty sequence with no initial value`
B) `ValueError`
C) Returns `None`
D) Returns `0`

**Answer: A**

**Explanation:**
Without an initial value, reduction is impossible on an empty sequence.

---

**Q17.45: Intermediate - [Generator Exhaustion]**

`g = (x for x in range(3))`. After running `sum(g)`, running `list(g)` returns:

A) `[0, 1, 2]`
B) `[]` (Empty list)
C) `[0, 1, 2]` again.
D) Error.

**Answer: B**

**Explanation:**
Generators are single-use iterators. Once consumed (by `sum`), they are empty.

---

**Q17.46: Basic - [Filter Truthy]**

`filter(bool, [0, 1, False, True])`:

A) Returns `[1, True]`
B) Returns `[0, False]`
C) Error.
D) Returns everything.

**Answer: A**

**Explanation:**
Filters keeping only items where `bool(item)` is True.

---

**Q17.47: Advanced - [Currying]**

Currying transforms `f(x, y)` into:

A) `f(x, y)`
B) `g(x)(y)`
C) `g(y, x)`
D) `f(x)`

**Answer: B**

**Explanation:**
Decomposing a multi-argument function into a sequence of single-argument functions.

---

**Q17.48: Expert - [Decorator Stacking]**

If you stack decorators:
```python
@d1
@d2
def f(): pass
```
It is equivalent to:

A) `f = d1(d2(f))`
B) `f = d2(d1(f))`
C) `f = d1(f) + d2(f)`
D) Parallel execution.

**Answer: A**

**Explanation:**
Decorators are applied bottom-up (d2 first, then d1 on the result of d2).

---

**Q17.49: Intermediate - [List Comp Condition]**

`[x for x in range(10) if x % 2 == 0]` is equivalent to:

A) `map`
B) `filter` followed by `list`.
C) `reduce`
D) `zip`

**Answer: B**

**Explanation:**
The `if` clause acts as a filter.

---

**Q17.50: Basic - [Lambda Return]**

The return type of a lambda function:

A) `None` (implicit).
B) Depends on the expression result.
C) Is always a function.
D) Is a tuple.

**Answer: B**

**Explanation:**
It returns whatever the evaluation of the body expression returns.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
