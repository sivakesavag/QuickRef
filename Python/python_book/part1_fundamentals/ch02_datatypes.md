# Chapter 2: Data Types & Variables

> **Topics Covered**: Primitive types, type hints, type checking, mutability vs immutability, memory management, object identity (id, is vs ==), integer caching, string interning, sys.intern(), small integer optimization, Unicode normalization

---

## Questions

---

**Q2.1: Basic - [Primitive Types]**

Which of the following is NOT a primitive/built-in data type in Python?

A) int
B) str
C) array
D) bool

**Answer: C**

**Explanation:**
`array` is not a built-in type — it requires importing the `array` module. Python's built-in primitive types include `int`, `float`, `str`, `bool`, `bytes`, `None`, `complex`. Lists, tuples, dicts, and sets are also built-in but are collection types, not primitives.

---

**Q2.2: Basic - [Type Checking]**

What is the output of `type(42)`?

A) `int`
B) `<class 'int'>`
C) `'int'`
D) `42`

**Answer: B**

**Explanation:**
`type()` returns the type object of its argument. For an integer, this is `<class 'int'>`. Note that it's not a string — it's an actual type object. You can compare with `type(42) == int` (True). In Python 3, all types are classes.

---

**Q2.3: Basic - [Type Checking]**

How do you check if a variable `x` is an integer?

A) `type(x) == "int"`
B) `isinstance(x, int)`
C) `x.type() == int`
D) `is_int(x)`

**Answer: B**

**Explanation:**
`isinstance(x, int)` is the preferred method because it also returns True for subclasses (e.g., `bool` is a subclass of `int`). `type(x) == int` works but doesn't handle subclasses. Comparing to `"int"` compares type to a string, which won't work. There's no `is_int()` function.

---

**Q2.4: Basic - [None Type]**

What is the type of `None` in Python?

A) `null`
B) `void`
C) `NoneType`
D) `None`

**Answer: C**

**Explanation:**
`None` is a singleton object of type `NoneType`. There's only one `None` object in Python. `type(None)` returns `<class 'NoneType'>`. Python doesn't have `null` (like Java/C) or `void`. `None` is commonly used to represent the absence of a value.

---

**Q2.5: Basic - [Boolean]**

What is the result of `bool("")`?

A) `True`
B) `False`
C) `None`
D) Error

**Answer: B**

**Explanation:**
Empty sequences (strings, lists, tuples, sets, dicts) are falsy in Python. `bool("")` returns `False`. Non-empty strings are truthy. Other falsy values include: `0`, `0.0`, `None`, `False`, and objects that define `__bool__()` or `__len__()` returning False/0.

---

**Q2.6: Intermediate - [Boolean]**

What is the output?
```python
print(bool([]), bool([0]), bool(0))
```

A) `False, False, False`
B) `True, True, False`
C) `False, True, False`
D) `True, False, True`

**Answer: C**

**Explanation:**
- `bool([])` → `False` (empty list)
- `bool([0])` → `True` (non-empty list, content doesn't matter)
- `bool(0)` → `False` (zero is falsy)

A list containing a falsy value is still truthy because the list itself is non-empty.

---

**Q2.7: Basic - [Integer]**

What is the maximum value of an integer in Python 3?

A) 2^31 - 1
B) 2^63 - 1
C) sys.maxsize
D) There is no maximum; integers have arbitrary precision

**Answer: D**

**Explanation:**
Python 3 integers have arbitrary precision — they can be as large as memory allows. There's no `long` type like in Python 2; all integers are of type `int`. `sys.maxsize` is the maximum size of containers (typically 2^63-1 on 64-bit), not the maximum integer value.

---

**Q2.8: Intermediate - [Float]**

What is the output?
```python
print(0.1 + 0.2 == 0.3)
```

A) `True`
B) `False`
C) `0.3`
D) Error

**Answer: B**

**Explanation:**
⚠️ **Common Pitfall**: Floating-point numbers have precision limitations. `0.1 + 0.2` equals `0.30000000000000004` due to binary representation issues. For accurate decimal arithmetic, use the `decimal` module. For approximate comparison, use `math.isclose(0.1 + 0.2, 0.3)`.

---

**Q2.9: Intermediate - [Float, Special Values]**

What does `float('inf')` represent?

A) An error
B) Positive infinity
C) The string "inf"
D) The largest possible float

**Answer: B**

**Explanation:**
`float('inf')` creates a special floating-point value representing positive infinity. `float('-inf')` is negative infinity. `float('nan')` is "Not a Number". These are valid float values, not errors. Infinity comparisons work: `float('inf') > 10**1000` is True.

---

**Q2.10: Intermediate - [Complex Numbers]**

What is the imaginary part of `3 + 4j`?

A) `4`
B) `4j`
C) `3`
D) `3 + 4j`

**Answer: A**

**Explanation:**
Access complex number parts with `.real` and `.imag` attributes. For `z = 3 + 4j`: `z.real` is `3.0`, `z.imag` is `4.0` (both are floats, not the full complex or just `j`). Python uses `j` instead of `i` for imaginary numbers.

---

**Q2.11: Basic - [Type Hints]**

What is the purpose of type hints in Python?

A) They enforce type checking at runtime
B) They make code run faster
C) They provide documentation and enable static type checking tools
D) They are required in Python 3.10+

**Answer: C**

**Explanation:**
Type hints (PEP 484) are purely for documentation and static analysis tools like mypy, Pyright, or IDE type checkers. Python does NOT enforce types at runtime — you can still pass any type. They don't affect performance. They're optional in all Python versions.

---

**Q2.12: Intermediate - [Type Hints]**

What is the correct type hint for a function that takes a string and returns an integer?

A) `def func(s) -> str: int`
B) `def func(s: str) -> int:`
C) `def func(s: string) -> integer:`
D) `def func(str s) int:`

**Answer: B**

**Explanation:**
Python type hint syntax: `parameter: Type` for parameters, `-> Type` after the closing parenthesis for return type. Use `str`, `int`, `float` (lowercase built-in names), not `string` or `integer`. The syntax is different from C-style declarations.

---

**Q2.13: Intermediate - [Type Hints]**

What does `Optional[str]` mean in type hints?

A) A string that might be empty
B) A string or None
C) An optional parameter
D) A string that can be ignored

**Answer: B**

**Explanation:**
`Optional[str]` is equivalent to `Union[str, None]` or `str | None` (Python 3.10+). It means the value can be a string or `None`. It doesn't mean the parameter is optional (that's determined by having a default value). Empty string and None are different — `Optional` refers to None.

---

**Q2.14: Advanced - [Type Hints, Union]**

🐍 In Python 3.10+, what is the new syntax for `Union[int, str]`?

A) `int & str`
B) `int | str`
C) `int + str`
D) `int or str`

**Answer: B**

**Explanation:**
Python 3.10 introduced the `|` operator for union types (PEP 604). `int | str` is equivalent to `Union[int, str]`. This is cleaner and doesn't require importing from `typing`. It also works in `isinstance()`: `isinstance(x, int | str)`.

---

**Q2.15: Basic - [Mutability]**

Which of these types is mutable?

A) tuple
B) str
C) list
D) int

**Answer: C**

**Explanation:**
Lists are mutable — you can modify their contents after creation. Tuples, strings, integers (and all numbers), and frozensets are immutable. Mutable types: list, dict, set, bytearray. Understanding mutability is crucial for avoiding bugs with shared references.

---

**Q2.16: Intermediate - [Mutability]**

What is the output?
```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)
```

A) `[1, 2, 3]`
B) `[1, 2, 3, 4]`
C) `[4, 1, 2, 3]`
D) Error

**Answer: B**

**Explanation:**
⚠️ `b = a` doesn't create a copy — both `a` and `b` reference the same list object. Modifying `b` modifies `a` as well. To create a copy, use `b = a.copy()`, `b = a[:]`, or `b = list(a)`. This is a common source of bugs when working with mutable objects.

---

**Q2.17: Intermediate - [Mutability]**

What is the output?
```python
a = "hello"
b = a
b = b + " world"
print(a)
```

A) `hello world`
B) `hello`
C) `world`
D) Error

**Answer: B**

**Explanation:**
Strings are immutable. `b = b + " world"` creates a NEW string object and assigns it to `b`. It doesn't modify the original string that `a` still references. After the concatenation, `a` and `b` point to different objects. This is different from the list example where the same object was modified.

---

**Q2.18: Intermediate - [Object Identity]**

What is the difference between `==` and `is`?

A) No difference, they are interchangeable
B) `==` compares values; `is` compares identity (same object in memory)
C) `is` is faster but less accurate
D) `==` only works for numbers

**Answer: B**

**Explanation:**
`==` checks if values are equal (calls `__eq__`). `is` checks if both operands are the exact same object (same memory address). `a is b` is equivalent to `id(a) == id(b)`. Use `is` for comparing with `None`, `True`, `False`, and singletons. Use `==` for value comparison.

---

**Q2.19: Advanced - [Object Identity, Integer Caching]**

What is the output?
```python
a = 256
b = 256
print(a is b)

c = 257
d = 257
print(c is d)
```

A) `True, True`
B) `False, False`
C) `True, False`
D) `False, True`

**Answer: C**

**Explanation:**
⚠️ **CPython optimization**: Small integers (-5 to 256) are cached and reused. `a` and `b` reference the same cached object. Larger integers like 257 may or may not be the same object (depends on context). **Never rely on this behavior** — always use `==` for value comparison. This is implementation-specific.

---

**Q2.20: Advanced - [Integer Caching]**

Why does Python cache small integers?

A) To save memory and improve performance for commonly used values
B) To make comparison faster
C) It's a bug in Python
D) To prevent integer overflow

**Answer: A**

**Explanation:**
Small integers (-5 to 256 in CPython) are used extremely frequently in typical programs (loop counters, array indices, etc.). Pre-creating and reusing these objects avoids repeated memory allocation/deallocation overhead. This is a memory and performance optimization, not related to comparison or overflow.

---

**Q2.21: Intermediate - [id()]**

What does `id(object)` return?

A) The type of the object
B) A unique integer identifier for the object (memory address in CPython)
C) The hash of the object
D) The reference count of the object

**Answer: B**

**Explanation:**
`id()` returns a unique integer identifier guaranteed to be unique for the object's lifetime. In CPython, this is the memory address. Two objects with non-overlapping lifetimes may have the same `id()`. Note: `id()` is not a hash — unhashable objects still have an id.

---

**Q2.22: Advanced - [String Interning]**

What is string interning?

A) Converting strings to integers
B) Storing strings encrypted internally
C) Reusing identical string objects to save memory
D) Compressing string data

**Answer: C**

**Explanation:**
String interning is an optimization where identical strings share the same memory location. Python automatically interns strings that look like identifiers (alphanumeric, underscore). You can manually intern with `sys.intern()`. Interned strings allow `is` comparison instead of `==` for faster comparison in some cases.

---

**Q2.23: Advanced - [String Interning]**

What is the output?
```python
a = "hello"
b = "hello"
c = "hello world"
d = "hello world"
print(a is b, c is d)
```

A) `True, True`
B) `False, False`
C) `True, False`
D) Depends on Python version and context

**Answer: D**

**Explanation:**
⚠️ String interning behavior varies. Simple strings like `"hello"` are usually interned, so `a is b` is typically True. Strings with spaces may or may not be interned depending on context (compile-time literals vs runtime creation). **Never rely on this for correctness** — use `==` for string comparison.

---

**Q2.24: Expert - [sys.intern()]**

What is the purpose of `sys.intern(string)`?

A) To make the string immutable
B) To force interning of a string, enabling fast identity comparison
C) To convert the string to an internal encoding
D) To store the string in a protected memory region

**Answer: B**

**Explanation:**
`sys.intern()` adds a string to the intern table, ensuring only one copy exists. Returns the interned string. Useful when you have many duplicate strings (e.g., parsing tokens) and want fast `is` comparison or reduced memory. Only works with strings, not bytes.

---

**Q2.25: Intermediate - [Variables]**

In Python, what is a variable?

A) A fixed memory location that holds data
B) A name that refers (binds) to an object
C) A container that stores data permanently
D) A keyword for data declaration

**Answer: B**

**Explanation:**
In Python, variables are names (references) that bind to objects. The object holds the data, not the variable. Multiple names can reference the same object. There's no "variable declaration" — assignment creates the binding. `a = [1,2,3]` binds the name `a` to a list object.

---

**Q2.26: Basic - [Variable Naming]**

Which is a valid variable name in Python?

A) `2nd_value`
B) `_private`
C) `class`
D) `my-variable`

**Answer: B**

**Explanation:**
Valid names: start with letter or underscore, contain letters/digits/underscores. `_private` is valid (leading underscore is a convention for "private"). `2nd_value` is invalid (starts with digit). `class` is invalid (reserved keyword). `my-variable` is invalid (hyphens not allowed).

---

**Q2.27: Intermediate - [Multiple Assignment]**

What is the output?
```python
a, b = 1, 2
a, b = b, a
print(a, b)
```

A) `1 2`
B) `2 1`
C) `2 2`
D) Error

**Answer: B**

**Explanation:**
Python evaluates the right side completely before assignment. `a, b = b, a` swaps values without needing a temporary variable. The right side creates a tuple `(b, a)` which becomes `(2, 1)`, then unpacks to `a=2, b=1`. This is a Pythonic idiom for swapping.

---

**Q2.28: Intermediate - [Unpacking]**

What is the output?
```python
a, *b, c = [1, 2, 3, 4, 5]
print(b)
```

A) `[2, 3, 4]`
B) `2, 3, 4`
C) `[1, 2, 3, 4, 5]`
D) Error

**Answer: A**

**Explanation:**
The `*` in unpacking collects "the rest" into a list. `a` gets first element (1), `c` gets last element (5), `*b` gets everything in between as a list `[2, 3, 4]`. This extended unpacking was introduced in Python 3.0 (PEP 3132).

---

**Q2.29: Intermediate - [Bytes]**

What is the difference between `str` and `bytes`?

A) No difference, they are interchangeable
B) `str` is text (Unicode), `bytes` is binary data (byte sequences)
C) `bytes` is mutable, `str` is immutable
D) `str` is for ASCII only, `bytes` is for all characters

**Answer: B**

**Explanation:**
`str` represents Unicode text (sequence of Unicode code points). `bytes` represents sequences of bytes (integers 0-255). Converting between them requires encoding/decoding: `"hello".encode('utf-8')` → bytes, `b"hello".decode('utf-8')` → str. Both are immutable. This distinction is fundamental in Python 3.

---

**Q2.30: Intermediate - [Bytes]**

What is the output?
```python
s = b"hello"
print(type(s[0]))
```

A) `<class 'bytes'>`
B) `<class 'str'>`
C) `<class 'int'>`
D) `<class 'char'>`

**Answer: C**

**Explanation:**
Indexing a bytes object returns an integer (0-255), not a single-byte bytes object or string. `b"hello"[0]` is `104` (ASCII value of 'h'). This differs from strings where `"hello"[0]` returns `'h'` (a single-character string). There's no `char` type in Python.

---

**Q2.31: Intermediate - [Bytearray]**

What is the difference between `bytes` and `bytearray`?

A) `bytes` is faster
B) `bytes` is immutable, `bytearray` is mutable
C) `bytearray` can only hold ASCII
D) They are identical

**Answer: B**

**Explanation:**
`bytes` is immutable (like str), `bytearray` is mutable (like list). Use `bytearray` when you need to modify binary data in place. `ba = bytearray(b"hello"); ba[0] = 72` works. `b"hello"[0] = 72` raises TypeError. Both store byte values (0-255).

---

**Q2.32: Advanced - [Memory Management]**

What memory management technique does Python primarily use?

A) Manual memory management
B) Garbage collection only
C) Reference counting with cyclic garbage collector
D) Stack-based allocation only

**Answer: C**

**Explanation:**
Python uses reference counting as the primary memory management technique (object deallocated when ref count reaches 0) plus a cyclic garbage collector to handle reference cycles. When you delete a reference or it goes out of scope, the reference count decreases. This is automatic, not manual.

---

**Q2.33: Advanced - [Reference Counting]**

What is the output?
```python
import sys
a = [1, 2, 3]
print(sys.getrefcount(a))
```

A) `1`
B) `2`
C) `3`
D) Error

**Answer: B**

**Explanation:**
`sys.getrefcount()` returns the reference count of an object. The count is 2 because: (1) the variable `a` references the list, (2) the parameter to `getrefcount()` creates a temporary reference. The actual reference count when not being inspected is 1 in this case.

---

**Q2.34: Advanced - [Weak References]**

What is the purpose of weak references?

A) To create faster references
B) To reference objects without increasing their reference count
C) To reference deleted objects
D) To create encrypted references

**Answer: B**

**Explanation:**
Weak references (via `weakref` module) allow you to reference an object without preventing garbage collection. Useful for caches, observer patterns. When the only remaining references are weak, the object can be garbage collected. Access the object via `ref()` (returns None if collected).

---

**Q2.35: Intermediate - [Type Conversion]**

What is the output?
```python
print(int("42"), int(42.9), int("42.9"))
```

A) `42, 42, 42`
B) `42, 42, Error`
C) `42, 43, 42`
D) `42, 42, 43`

**Answer: B**

**Explanation:**
`int("42")` → `42` (string with integer parses fine). `int(42.9)` → `42` (truncates toward zero, not rounding). `int("42.9")` → **ValueError** (can't parse float string directly to int). Use `int(float("42.9"))` for two-step conversion.

---

**Q2.36: Intermediate - [Type Conversion]**

What is the output?
```python
print(list("abc"))
```

A) `['abc']`
B) `['a', 'b', 'c']`
C) `['a,b,c']`
D) Error

**Answer: B**

**Explanation:**
`list()` on a string iterates through the characters, creating a list of individual character strings. Strings are iterable sequences of characters. Similarly, `tuple("abc")` returns `('a', 'b', 'c')`. This is useful for character manipulation.

---

**Q2.37: Basic - [Type Conversion]**

What is the output of `str(42) + str(8)`?

A) `50`
B) `"50"`
C) `"428"`
D) Error

**Answer: C**

**Explanation:**
`str(42)` creates `"42"`, `str(8)` creates `"8"`. The `+` operator concatenates strings, resulting in `"428"`. It does NOT add them numerically. String concatenation is different from numeric addition. Compare with `42 + 8 = 50`.

---

**Q2.38: Advanced - [Unicode]**

What is the output?
```python
print(len("café"), len("café".encode('utf-8')))
```

A) `4, 4`
B) `4, 5`
C) `5, 5`
D) `5, 4`

**Answer: B**

**Explanation:**
`len("café")` returns 4 (number of Unicode characters). `"café".encode('utf-8')` converts to bytes, where `é` requires 2 bytes in UTF-8, giving 5 bytes total. Character count ≠ byte count for non-ASCII. This distinction is crucial for internationalized applications.

---

**Q2.39: Expert - [Unicode Normalization]**

What is Unicode normalization?

A) Converting Unicode to ASCII
B) Different ways of representing equivalent Unicode strings
C) Encrypting Unicode data
D) Compressing Unicode strings

**Answer: B**

**Explanation:**
Unicode normalization addresses the fact that some characters can be represented multiple ways (e.g., `é` can be one character U+00E9 or `e` + combining accent). Use `unicodedata.normalize()` with forms NFC, NFD, NFKC, NFKD. Important for string comparison and database storage.

---

**Q2.40: Expert - [Unicode]**

What is the output?
```python
a = "café"  # é as single character
b = "cafe\u0301"  # e + combining acute accent
print(a == b, len(a), len(b))
```

A) `True, 4, 4`
B) `False, 4, 5`
C) `True, 4, 5`
D) `False, 5, 5`

**Answer: B**

**Explanation:**
⚠️ **Unicode gotcha**: `a` uses precomposed é (1 char), `b` uses decomposed e+accent (2 chars). They look identical but are different strings. `len(a)` is 4, `len(b)` is 5. Use `unicodedata.normalize('NFC', s)` before comparing to handle this.

---

**Q2.41: Intermediate - [Boolean as Integer]**

What is the output?
```python
print(True + True + False)
```

A) `Error`
B) `True`
C) `2`
D) `TrueTrueFalse`

**Answer: C**

**Explanation:**
In Python, `bool` is a subclass of `int`. `True == 1` and `False == 0`. So `True + True + False` is `1 + 1 + 0 = 2`. This allows booleans in arithmetic expressions, which is used in patterns like `sum(x > 5 for x in items)` to count True values.

---

**Q2.42: Intermediate - [Float Precision]**

Which module should you use for exact decimal arithmetic?

A) math
B) decimal
C) float_precision
D) numbers

**Answer: B**

**Explanation:**
The `decimal` module provides arbitrary-precision decimal arithmetic. Unlike floats (binary representation with precision issues), decimals represent numbers exactly. Essential for financial calculations: `Decimal('0.1') + Decimal('0.2') == Decimal('0.3')` is True. Configure precision with `getcontext().prec`.

---

**Q2.43: Advanced - [Fraction]**

What module provides exact rational number arithmetic?

A) rational
B) fractions
C) ratio
D) numbers

**Answer: B**

**Explanation:**
The `fractions` module provides the `Fraction` class for exact rational arithmetic. `Fraction(1, 3) + Fraction(1, 3) + Fraction(1, 3) == 1` is True. Fractions maintain exact representation with numerator/denominator. Useful when you need mathematical precision without floating-point errors.

---

**Q2.44: Intermediate - [Dynamic Typing]**

What is dynamic typing in Python?

A) Variables must be declared with types
B) Types are checked and associated with values at runtime, not compile time
C) Python automatically converts between types
D) Types cannot change during execution

**Answer: B**

**Explanation:**
Python is dynamically typed: type information is associated with values (objects), not variables. A variable can reference objects of different types at different times. Type checking happens at runtime, not compile time. This allows flexibility but means type errors are caught during execution.

---

**Q2.45: Intermediate - [Duck Typing]**

What is "duck typing" in Python?

A) A type for waterproof variables
B) If an object behaves like a type (has expected methods), it can be used as that type
C) A special type for games
D) A typographical error checking system

**Answer: B**

**Explanation:**
"If it walks like a duck and quacks like a duck, it's a duck." Python cares about what an object can DO (methods it has), not what it IS (its class). A function expecting a "file-like object" works with anything having `read()` and `write()` methods, not just actual files.

---

**Q2.46: Advanced - [Type Annotations at Runtime]**

How can you access type hints at runtime?

A) `type(func).__hints__`
B) `func.__annotations__`
C) `typing.get_hints(func)`
D) Type hints are not accessible at runtime

**Answer: B**

**Explanation:**
Function annotations are stored in `__annotations__` (a dict mapping parameter names to their annotations). `typing.get_type_hints()` is better for complex cases (resolves forward references, handles string annotations). Class annotations are in `ClassName.__annotations__`.

---

**Q2.47: Expert - [Small Integer Pool Range]**

What is the range of integers cached by CPython?

A) 0 to 100
B) 0 to 256
C) -5 to 256
D) -128 to 127

**Answer: C**

**Explanation:**
CPython caches integers from -5 to 256 inclusive (262 objects). This range was chosen based on common usage patterns. Note: this is an implementation detail of CPython specifically, not part of the Python language specification. Other implementations may differ.

---

**Q2.48: Intermediate - [Immutable Containers]**

What is the output?
```python
t = (1, 2, [3, 4])
t[2].append(5)
print(t)
```

A) `Error: tuples are immutable`
B) `(1, 2, [3, 4])`
C) `(1, 2, [3, 4, 5])`
D) `(1, 2, (3, 4, 5))`

**Answer: C**

**Explanation:**
⚠️ **Gotcha**: Tuples are immutable (can't add/remove elements or change references), but they can contain mutable objects. The tuple's reference to the list doesn't change — we're modifying the list object itself. This is a subtle distinction between container immutability and object immutability.

---

**Q2.49: Advanced - [Hash Requirement]**

Why is this an error?
```python
d = {[1, 2]: "value"}
```

A) Dictionaries can't have string values
B) Lists can't be dictionary keys because they're unhashable
C) The syntax is wrong
D) Numbers can't be in lists that are keys

**Answer: B**

**Explanation:**
Dictionary keys must be hashable (immutable, consistent hash value). Lists are mutable, so they're unhashable. If a key could change after insertion, the dict couldn't find it. Use tuples instead: `{(1, 2): "value"}` works. This applies to set members too.

---

**Q2.50: Expert - [Copy vs Deepcopy]**

What is the difference between `copy.copy()` and `copy.deepcopy()`?

A) `copy()` is faster but less accurate
B) `copy()` is shallow (copies object, not nested objects); `deepcopy()` copies everything recursively
C) `deepcopy()` encrypts the copy
D) No difference for mutable objects

**Answer: B**

**Explanation:**
`copy.copy()` creates a new object but references to nested objects remain shared. `copy.deepcopy()` recursively copies all nested objects. For `[[1,2], [3,4]]`: shallow copy shares inner lists, deep copy creates new inner lists. Deep copying handles circular references.

---

**Q2.51: Intermediate - [Copy]**

What is the output?
```python
import copy
a = [[1, 2], [3, 4]]
b = copy.copy(a)
a[0].append(5)
print(b[0])
```

A) `[1, 2]`
B) `[1, 2, 5]`
C) `[5]`
D) Error

**Answer: B**

**Explanation:**
Shallow copy `copy.copy()` creates a new outer list, but the inner lists are still references to the same objects. `a[0]` and `b[0]` point to the same list. Modifying `a[0]` affects `b[0]`. Use `copy.deepcopy()` if you need fully independent copies.

---

**Q2.52: Basic - [None Comparison]**

What is the recommended way to check if a variable is None?

A) `if x == None:`
B) `if x is None:`
C) `if not x:`
D) `if x.isNone():`

**Answer: B**

**Explanation:**
💡 **Best Practice**: Use `is None` or `is not None` for None comparison. `None` is a singleton, so identity comparison is faster and correct. `== None` works but is slower and could be overridden by `__eq__`. `not x` catches other falsy values too (0, "", []), not just None.

---

**Q2.53: Advanced - [Type vs isinstance]**

When should you use `type()` instead of `isinstance()`?

A) Always use `type()`, it's better
B) When you need to check for an exact type, not subclasses
C) When working with built-in types only
D) Never, `isinstance()` is always preferred

**Answer: B**

**Explanation:**
`isinstance(True, int)` returns True (bool is subclass of int). `type(True) == int` returns False. Use `type()` when you need exact type matching without subclass consideration. Generally `isinstance()` is preferred for polymorphism, but sometimes exact type matters.

---

**Q2.54: Intermediate - [Numeric Tower]**

What is the result of `3 + 4.5`?

A) `7` (int)
B) `7.5` (float)
C) Error: can't add int and float
D) `"34.5"` (string)

**Answer: B**

**Explanation:**
Python automatically converts int to float when needed (numeric coercion). `3 + 4.5` produces `7.5` (float). The numeric tower is: int < float < complex. Operations between different numeric types produce the "wider" type. No explicit casting needed.

---

**Q2.55: Expert - [__slots__]**

What is the purpose of `__slots__` in a class?

A) To define methods available in the class
B) To restrict attributes and reduce memory usage by avoiding __dict__
C) To create additional memory space
D) To define slot-based method dispatch

**Answer: B**

**Explanation:**
`__slots__` declares a fixed set of attributes, replacing the per-instance `__dict__` with a more memory-efficient structure. Useful for classes with many instances. Constraints: can't add new attributes, no `__dict__` (unless explicitly included), affects inheritance. Example: `__slots__ = ['x', 'y']`.

---

## Chapter Summary

**Total MCQs: 55**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 14 | 25% |
| Intermediate | 27 | 49% |
| Advanced | 11 | 20% |
| Expert | 3 | 6% |

**Key Topics Covered:**
- Primitive types and type checking
- Mutability vs immutability
- Object identity (is vs ==)
- Integer caching and string interning
- Memory management and reference counting
- Type hints and annotations
- Unicode and encoding
- Copy vs deepcopy
