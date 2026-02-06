# Chapter 33: Edge Cases & Gotchas

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: Floating Point issues, Mutable Default Arguments, Late Binding Closures, `is` vs `==` quirks, `try/finally/return` behavior, `None` comparisons, Boolean short-circuiting, Scope shadowing, `__del__` pitfalls.

---

**Q33.1: Basic - [Floating Point]**

Why does `0.1 + 0.2 == 0.3` return `False` in Python (and most languages)?

A) Floating point standard (IEEE 754) cannot precisely represent 0.1 and 0.2 in binary, leading to a tiny rounding error (`0.30000000000000004`).
B) It's a bug in Python.
C) Python is bad at math.
D) It returns True.

**Answer: A**

**Explanation:**
Use `math.isclose()` or `decimal` module for precision.

---

**Q33.2: Intermediate - [Late Binding]**

What does this code print? `funcs = [lambda: i for i in range(3)]; print([f() for f in funcs])`

A) `[2, 2, 2]`
B) `[0, 1, 2]`
C) `[0, 0, 0]`
D) Error.

**Answer: A**

**Explanation:**
"Late Binding" means the lambda looks up the value of `i` when called (which is 2 at the end of loop), not when defined. Fix: `lambda i=i: i`.

---

**Q33.3: Advanced - [Mutating Loop]**

Iterating over a list while removing items from it (e.g., `for x in mylist: mylist.remove(x)`) is dangerous because:

A) It messes up the internal index iterator, causing it to skip elements.
B) It raises an error.
C) It is infinite.
D) It clears the list perfectly.

**Answer: A**

**Explanation:**
Iterate over a copy instead: `for x in mylist[:]:`.

---

**Q33.4: Expert - [Tuple with Mutable]**

If `t = (1, 2, [3])`, executing `t[2] += [4]`:

A) Raises `TypeError` (because tuple is immutable) BUT also successfully modifies the list in place (the list is mutable).
B) Raises `TypeError` and does nothing.
C) Works fine.
D) Crashes.

**Answer: A**

**Explanation:**
The `+=` operator is not atomic: it modifies the list (success) and then tries to re-assign it to `t[2]` (fail).

---

**Q33.5: Basic - [Is vs Equals]**

`a = [1]; b = [1]`. `a == b` is ____, `a is b` is ____.

A) True; False
B) True; True
C) False; True
D) False; False

**Answer: A**

**Explanation:**
Values are equal, but they are distinct objects in memory.

---

**Q33.6: Intermediate - [Small Int Caching]**

`a = 256; b = 256; a is b` is True. `a = 257; b = 257; a is b` is (usually) False (in standard REPL). Why?

A) CPython caches integer objects from -5 to 256. Larger integers are created as new objects (unless compiler optimized in a file).
B) Random chance.
C) 256 is a byte.
D) Memory error.

**Answer: A**

**Explanation:**
Implementation detail of CPython.

---

**Q33.7: Advanced - [Try Finally Return]**

If a `try` block returns 10, and the `finally` block returns 20, the function returns:

A) 20
B) 10
C) Both.
D) None.

**Answer: A**

**Explanation:**
`finally` always runs and can override the return value.

---

**Q33.8: Expert - [Nan Equality]**

`float('nan') == float('nan')` evaluates to:

A) False
B) True
C) Error
D) None

**Answer: A**

**Explanation:**
By definition (IEEE 754), NaN is not equal to anything, including itself. Use `math.isnan()`.

---

**Q33.9: Basic - [Boolean Short circuit]**

In `x or y`, if `x` is Truthy:

A) `y` is never evaluated (short-circuit), and `x` is returned.
B) `y` is evaluated.
C) True is returned.
D) False is returned.

**Answer: A**

**Explanation:**
Crucial for `if obj is not None and obj.attr...`.

---

**Q33.10: Intermediate - [Chained Comparison]**

`1 < 2 < 3` evaluates to:

A) `(1 < 2) and (2 < 3)` (True).
B) `(1 < 2)` (True, which is 1) `< 3` (True).
C) False.
D) Error.

**Answer: A**

**Explanation:**
Python supports mathematicians' chained comparison syntax.

---

**Q33.11: Advanced - [Dict Iteration]**

Iterating over a dictionary (`for k in d`) iterates over:

A) Keys.
B) Values.
C) Items.
D) Hash.

**Answer: A**

**Explanation:**
Default iterator is `keys()`.

---

**Q33.12: Expert - [Nonlocal]**

The `nonlocal` keyword is used to:

A) Modify a variable in the nearest enclosing scope (excluding globals) - useful in nested functions/closures.
B) Modify global variables.
C) Declare a variable as thread-local.
D) Prevent export.

**Answer: A**

**Explanation:**
Unlike `global`, `nonlocal` requires the variable to already exist.

---

**Q33.13: Basic - [Any All]**

`any([])` returns ____, `all([])` returns ____.

A) False; True
B) False; False
C) True; True
D) True; False

**Answer: A**

**Explanation:**
Vacuous truth: "All elements in an empty list are true" is logically True.

---

**Q33.14: Intermediate - [String strip]**

`"www.example.com".strip("cmowz.")` returns:

A) `'example'` (it removes *all* characters in the set from both ends).
B) `'www.example'`
C) `'example.com'`
D) `'www.example.com'`

**Answer: A**

**Explanation:**
Common mistake: expecting it to remove a *substring*. Use `removeprefix/removesuffix` (Py 3.9+).

---

**Q33.15: Advanced - [Init return]**

The `__init__` method must return:

A) `None`
B) The new instance.
C) True.
D) Nothing (void).

**Answer: A**

**Explanation:**
Returning anything else raises a `TypeError`.

---

**Q33.16: Expert - [Del behavior]**

Does `__del__` guaranteed to run when the script exits?

A) No, CPython does not guarantee finding all objects and calling `__del__` on interpreter shutdown (especially if there are cycles).
B) Yes, always.
C) Only on Windows.
D) Only on Linux.

**Answer: A**

**Explanation:**
Use Context Managers (`with`) for cleanup instead of `__del__`.

---

**Q33.17: Basic - [Round Half to Even]**

`round(2.5)` in Python 3 returns:

A) 2 (Banker's Rounding / Round Half To Even).
B) 3
C) 2.5
D) 0

**Answer: A**

**Explanation:**
Python 2 returned 3. `round(3.5)` -> 4. Reduces bias in sums.

---

**Q33.18: Intermediate - [Bool inheritance]**

Can you inherit from `bool`?

A) No, `bool` is final.
B) Yes.
C) Only in Python 2.
D) If you force it.

**Answer: A**

**Explanation:**
`class MyBool(bool):` raises TypeError.

---

**Q33.19: Advanced - [Augmented Assignment]**

`a = [1, 2]; b = a; a += [3]` results in `b` being:

A) `[1, 2, 3]` (Mutates in place).
B) `[1, 2]` (Creates new list).
C) Error.
D) Empty.

**Answer: A**

**Explanation:**
`+=` calls `__iadd__`. Compare `a = a + [3]` which creates a NEW list.

---

**Q33.20: Expert - [Eval evil]**

`eval()` is considered dangerous because:

A) It executes arbitrary code string (can delete files, steal secrets).
B) It is slow.
C) It relies on C.
D) It is deprecated.

**Answer: A**

**Explanation:**
Use `ast.literal_eval()` for safely parsing literals.

---

**Q33.21: Basic - [Zip unknown]**

`zip([1, 2], [3, 4, 5])` produces:

A) `(1, 3), (2, 4)` (Truncates to shortest).
B) `(1, 3), (2, 4), (None, 5)`
C) Error.
D) `(1, 3, 5)`

**Answer: A**

**Explanation:**
Use `itertools.zip_longest` if you want None padding, or `strict=True` (Py 3.10+) to error.

---

**Q33.22: Intermediate - [Dict Key Collision]**

If `hash(a) == hash(b)`, are `a` and `b` necessarily equal?

A) No, this is a hash collision. Python then checks equality `a == b`.
B) Yes.
C) Only for strings.
D) Only for ints.

**Answer: A**

**Explanation:**
The hash is just a quick bin lookup.

---

**Q33.23: Advanced - [Multiline String]**

Implicit string concatenation happens when:

A) Two string literals are placed next to each other: `"Hello " "World"`.
B) Using `+`.
C) Using `join`.
D) Using `,`.

**Answer: A**

**Explanation:**
`("a" "b")` -> `"ab"`. Easy to create bugs in lists `["a", "b" "c"]`.

---

**Q33.24: Expert - [Function Default Introspection]**

Where are default argument values stored?

A) `func.__defaults__` (tuple).
B) `func.defaults`
C) `sys.defaults`
D) Nowhere.

**Answer: A**

**Explanation:**
This is why they persist.

---

**Q33.25: Basic - [Not operator]**

`not True` is:

A) False
B) True
C) None
D) 0

**Answer: A**

**Explanation:**
Standard boolean logic.

---

**Q33.26: Intermediate - [Enumerate Start]**

To start numbering from 1 in `enumerate(items)`:

A) `enumerate(items, start=1)`
B) `enumerate(items, 1)` (also works).
C) `enumerate(items) + 1`
D) `enumerate(items, index=1)`

**Answer: A**

**Explanation:**
Clean pythonic way.

---

**Q33.27: Advanced - [Generator Exhaustion]**

Re-iterating a generator object a second time:

A) Yields nothing (it is exhausted).
B) Restarts from beginning.
C) Raises Error.
D) Reverses it.

**Answer: A**

**Explanation:**
Generators are one-time use.

---

**Q33.28: Expert - [Hash Randomization]**

By default, string hashes are randomized per process in Python 3 to:

A) Prevent Hash DoS attacks (where an attacker feeds keys that collide to slow down dict lookups).
B) Make it faster.
C) Make it random.
D) Save memory.

**Answer: A**

**Explanation:**
`PYTHONHASHSEED=0` disables this (for deterministic testing).

---

**Q33.29: Intermediate - [F-string vs Format]**

F-strings `f"{value}"` are evaluated:

A) At runtime (eagerly).
B) At compile time.
C) When printed.
D) Never.

**Answer: A**

**Explanation:**
Unlike `.format()` which is a method call.

---

**Q33.30: Basic - [Empty Set]**

`{}` creates a:

A) Dictionary (empty).
B) Set (empty).
C) Tuple.
D) List.

**Answer: A**

**Explanation:**
Use `set()` to create an empty set.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
