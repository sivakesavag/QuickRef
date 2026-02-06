# Chapter 2: Data Types & Variables

**Target MCQs**: 50-60
**Current Batch**: 1-25
**Topics Covered**: Primitives, Mutability, Memory Management, Identity, Type Checking

---

**Q2.1: Basic - [Numeric Types]**

Which of the following is **not** a built-in numeric type in Python 3?

A) `int`
B) `long`
C) `float`
D) `complex`

**Answer: B**

**Explanation:**
Python 2 had `int` and `long`. In Python 3, `int` can explicitly handle arbitrarily large numbers (behaving like `long` in Python 2), so the `long` type was removed. `float` and `complex` are valid numeric types.

---

**Q2.2: Basic - [Strings]**

Which statement correctly defines an f-string (formatted string literal) in Python?

A) `f"Value: {val}"`
B) `format("Value: {val}")`
C) `r"Value: {val}"`
D) `s"Value: {val}"`

**Answer: A**

**Explanation:**
F-strings, introduced in Python 3.6, are prefixed with `f` or `F`. Expressions inside `{}` are evaluated at runtime. `r""` is a raw string (treats backslashes literally).

---

**Q2.3: Intermediate - [Mutability]**

If `a = [1, 2, 3]` and `b = a`, what happens when you evaluate `b.append(4)`?

A) `a` remains `[1, 2, 3]`, `b` becomes `[1, 2, 3, 4]`.
B) Both `a` and `b` become `[1, 2, 3, 4]`.
C) `b` becomes `[1, 2, 3, 4]`, but `a` becomes undefined.
D) Raises a `ReferenceError`.

**Answer: B**

**Explanation:**
Lists are **mutable** objects. `b = a` creates a new reference `b` pointing to the *same object* that `a` points to. Modifying the object via `b` is visible via `a`.

---

**Q2.4: Basic - [Type Checking]**

What is the idiomatic way to check if variable `x` is a string?

A) `type(x) == str`
B) `x.isinstance(str)`
C) `isinstance(x, str)`
D) `typeof(x) == 'str'`

**Answer: C**

**Explanation:**
`isinstance(x, str)` is preferred over `type(x) == str` because it handles inheritance correctly (returns True if `x` is an instance of a subclass of `str`). Code checking specific types should usually allow subclasses (Liskov Substitution Principle).

---

**Q2.5: Advanced - [Complex Numbers]**

How do you instantiate a complex number with real part 3 and imaginary part 4?

A) `3 + 4i`
B) `complex(3, 4)` or `3 + 4j`
C) `3 + 4I`
D) `Complex(3, 4)`

**Answer: B**

**Explanation:**
Python uses `j` or `J` suffix for the imaginary part (`3 + 4j`). Alternatively, the built-in `complex(real, imag)` constructor can be used. `i` is not used in Python syntax for imaginary numbers.

---

**Q2.6: Intermediate - [Integers]**

What is the maximum value of an integer (`int`) in Python 3?

A) `2 ** 31 - 1`
B) `2 ** 63 - 1`
C) It is limited only by available memory.
D) `sys.maxint`

**Answer: C**

**Explanation:**
Python 3 integers have **arbitrary precision**. They automatically grow as large as needed, limited only by the machine's RAM. Python 2 had `sys.maxint` limit for standard integers, but Python 3 merged this with `long`.

---

**Q2.7: Intermediate - [Boolean]**

What is the result of `True + True` in Python?

A) `TrueTrue`
B) `2`
C) `True`
D) `TypeError`

**Answer: B**

**Explanation:**
`bool` is a subclass of `int`. `True` evaluates to `1` and `False` to `0` in numeric contexts. So `1 + 1` is `2`.

---

**Q2.8: Advanced - [Float Precision]**

Why does `0.1 + 0.2 == 0.3` evaluate to `False`?

A) Because of a bug in Python's float implementation.
B) Because `0.3` is an integer in this context.
C) Due to IEEE 754 floating-point representation limitations.
D) It actually evaluates to `True`.

**Answer: C**

**Explanation:**
Floating-point numbers are stored in binary (base 2). Decimal fractions like 0.1 and 0.2 have infinite repeating binary representations. The stored approximation creates small errors: `0.1 + 0.2` results in `0.30000000000000004`, which is not exactly equal to `0.3`.

---

**Q2.9: Expert - [NaN Comparison]**

What is the output of `float('nan') == float('nan')`?

A) `True`
B) `False`
C) `ValueError`
D) `None`

**Answer: B**

**Explanation:**
According to the IEEE 754 standard, **NaN (Not a Number)** is not equal to anything, including itself. To check for NaN, you must use `math.isnan()` or `numpy.isnan()`.

---

**Q2.10: Basic - [String Indexing]**

Given `s = "Python"`, what does `s[-1]` return?

A) "P"
B) "n"
C) "o"
D) `IndexError`

**Answer: B**

**Explanation:**
Negative indexing allows accessing elements from the end. `-1` is the last character, `-2` is the second to last, etc.

---

**Q2.11: Intermediate - [Slicing]**

What is the output of `x = [0, 1, 2, 3, 4, 5]; x[::2]`?

A) `[0, 1, 2]`
B) `[0, 2, 4]`
C) `[1, 3, 5]`
D) `[2]`

**Answer: B**

**Explanation:**
The slice syntax is `start:stop:step`. Omitting start and stop defaults to the whole list. A step of `2` takes every second element starting from index 0 (0, 2, 4).

---

**Q2.12: Advanced - [Bytes]**

What is strict difference between `bytes` and `str` in Python 3?

A) `bytes` are mutable, `str` is immutable.
B) `str` supports Unicode, `bytes` is a sequence of integers (0-255).
C) There is no difference; they are aliases.
D) `str` is for text files, `bytes` is only for network sockets.

**Answer: B**

**Explanation:**
`str` is an immutable sequence of Unicode code points (text). `bytes` is an immutable sequence of bytes (integers 0-255), representing raw binary data. You interpret `bytes` as text by **decoding** and convert `str` to `bytes` by **encoding**.

---

**Q2.13: Intermediate - [Tuple Assignment]**

What is happening in the statement `a, b = b, a`?

A) It causes a race condition.
B) It swaps the values of `a` and `b`.
C) It raises a `SyntaxError`.
D) It creates a tuple `(a, b)` but doesn't assign it.

**Answer: B**

**Explanation:**
This is **tuple unpacking**. The right-hand side `b, a` creates a tuple `(value_of_b, value_of_a)`. The left-hand side unpacks this tuple into variables `a` and `b`. This is the standard, pythonic way to swap variables.

---

**Q2.14: Advanced - [Small Integer Caching]**

For which range of integers does CPython guarantee that `x is y` if `x` and `y` have the same value (singleton objects)?

A) -128 to 127
B) -5 to 256
C) 0 to 255
D) There is no guarantee.

**Answer: B**

**Explanation:**
CPython pre-allocates integer objects for the range [-5, 256] during startup. Any calculation resulting in an integer in this range returns a reference to the existing object.

---

**Q2.15: Expert - [Object Size]**

What is the minimum overhead (in bytes) of a PyObject in CPython 64-bit (e.g., a simple integer like `1`)?

A) 4 bytes
B) 8 bytes
C) 28 bytes
D) 64 bytes

**Answer: C**

**Explanation:**
On a standard 64-bit CPython build, a small integer like `1` requires 28 bytes:
- 8 bytes for reference count (`ob_refcnt`)
- 8 bytes for type pointer (`ob_type`)
- 8 bytes for the size of the variable-length array (`ob_size`) (since int is var-sized)
- 4 bytes (aligned to 8) for the digit value itself.

---

**Q2.16: Intermediate - [String Methods]**

What does `"  python  ".strip()` return?

A) `"python"` (no spaces)
B) `"  python"`
C) `"python  "`
D) `"  p  y  t  h  o  n  "`

**Answer: A**

**Explanation:**
`strip()` removes leading and trailing whitespace characters (spaces, tabs, newlines). `lstrip()` removes leading, `rstrip()` removes trailing.

---

**Q2.17: Basic - [None Checking]**

Why is `if x is None:` preferred over `if x == None:`?

A) `==` is slower.
B) `x == None` can trigger `x.__eq__` which might raise an exception or return True incorrectly if overridden. `is` checks identity and is safer/faster.
C) `is` works for all types, `==` only for numbers.
D) There is no difference.

**Answer: B**

**Explanation:**
Classes can override `__eq__` to return arbitrary values (or raise errors). `None` is a singleton, so identity comparison `is` is the most correct, semantically secure, and performant way to check for it.

---

**Q2.18: Advanced - [Copying]**

What is the difference between `copy.copy(x)` and `copy.deepcopy(x)`?

A) `copy()` copies the object, `deepcopy()` copies the type.
B) `copy()` creates a shallow copy (references to nested objects), `deepcopy()` recursively creates copies of nested objects.
C) `copy()` is for lists, `deepcopy()` is for classes.
D) `deepcopy()` saves the object to disk.

**Answer: B**

**Explanation:**
A **shallow copy** constructs a new compound object and inserts *references* into it to the objects found in the original. A **deep copy** constructs a new compound object and then, recursively, inserts *copies* into it of the objects found in the original.

---

**Q2.19: Intermediate - [Type Conversions]**

What happens if you run `int("12.5")`?

A) 12
B) 13
C) 12.5
D) `ValueError`

**Answer: D**

**Explanation:**
`int()` expects a string representing an integer. Passing a string with a decimal point ("12.5") raises `ValueError`. You must convert to float first: `int(float("12.5"))`.

---

**Q2.20: Expert - [String Equivalence]**

If `a = "hello"` and `b = "hel" + "lo"`, is `a is b` True?

A) Always True.
B) Always False.
C) True in CPython (usually) due to constant folding/interning, but implementation dependent.
D) True only if explicitly interned.

**Answer: C**

**Explanation:**
This is an implementation detail. CPython's compiler performs constant folding for short immutable strings. Since `"hel" + "lo"` is calculated at compile time to `"hello"`, it refers to the same interned code object constant as `a`. However, `b = "hel"; b += "lo"` (runtime concatenation) might result in a different object (False), unless the resulting string is short enough and interned implicitly (which CPython sometimes does, but it's not guaranteed).

---

**Q2.21: Basic - [List vs Tuple]**

Why would you use a `tuple` instead of a `list`?

A) Tuples are mutable.
B) Tuples can be used as dictionary keys (if they contain only immutable elements), lists cannot.
C) Tuples support more methods.
D) Lists cannot store mixed data types.

**Answer: B**

**Explanation:**
Dictionary keys must be **hashable**. Mutable types like lists are not hashable (since changing them would change the hash). immutable tuples are hashable (provided their contents are too) and can be used as keys.

---

**Q2.22: Intermediate - [Walrus Operator]**

What is the primary use case for the assignment expression `:=` (Walrus Operator)?

A) To assign variables inside a class definition.
B) To assign values to variables as part of a larger expression (e.g., inside a `while` loop condition).
C) To perform bitwise operations.
D) To test for equality without type coercion.

**Answer: B**

**Explanation:**
Introduced in Python 3.8, `:=` allows assignment within an expression.
Example: `while (line := file.readline()):` reads a line, assigns it to `line`, and checks if it's truthy (not empty) in one step.

---

**Q2.23: Advanced - [FrozenSets]**

What is a `frozenset`?

A) A set that maintains insertion order.
B) An immutable version of a `set`.
C) A set that can store mutable objects.
D) A deprecated data type.

**Answer: B**

**Explanation:**
`frozenset` is an immutable variant of `set`. Because it is immutable and hashable, it can be used as an element of another set or as a dictionary key.

---

**Q2.24: Expert - [Slots]**

What is the effect of defining `__slots__` in a class?

A) It prevents the creation of `__dict__` and `__weakref__` for instances, saving memory.
B) It allows adding arbitrary attributes to instances at runtime.
C) It automatically creates getter and setter methods.
D) It enforces strict type checking for attributes.

**Answer: A**

**Explanation:**
By default, Python objects store attributes in a `__dict__`, which consumes significant memory. Defining `__slots__` (an iterable of attribute names) reserves space for exactly those attributes and prevents the creation of `__dict__`, reducing memory footprint significantly for classes with many instances.

---

**Q2.25: Intermediate - [Id Functionality]**

If `a = [1, 2, 3]` and `b = [1, 2, 3]`, what is the result of `id(a) == id(b)`?

A) True
B) False
C) Random
D) Depends on the OS

**Answer: B**

**Explanation:**
Lists are mutable. Even if they contain the same values, constructing two separate list literals creates two distinct objects in memory. Thus, their identities (addresses) are different.

---

**Q2.26: Basic - [String Immutability]**

Which of the following operations raises a `TypeError` given `s = "hello"`?

A) `s = s + " world"`
B) `s = s.upper()`
C) `s[0] = "H"`
D) `s = "H" + s[1:]`

**Answer: C**

**Explanation:**
Strings are immutable. You cannot resort to item assignment (modifying a character in place). All other options involve creating a *new* string and assigning it back to the variable `s`.

---

**Q2.27: Advanced - [Unicode Normalization]**

What happens when you compare two strings that look identical but use different Unicode compositions (e.g., 'é' as a single code point vs 'e' + combining acute accent)?

A) They compare equal (`==` is True).
B) They compare unequal (`==` is False).
C) It depends on the font.
D) Python raises a `UnicodeError`.

**Answer: B**

**Explanation:**
By default, Python strings compare based on code points. "café" (composed) and "cafe\u0301" (decomposed) are different sequences of code points, so `==` is False. You must use `unicodedata.normalize()` to reliably compare them.

---

**Q2.28: Intermediate - [String Formatting]**

What is the output of `"{:.2f}".format(3.14159)`?

A) `"3.14159"`
B) `"3.14"`
C) `"3.15"` (rounded)
D) `"3.1"`

**Answer: B**

**Explanation:**
The format specifier `.2f` means "fixed-point notation with 2 digits after the decimal point". It rounds the value to 2 decimal places.

---

**Q2.29: Advanced - [Integer Size]**

What determines the size of an `int` object in memory in Python 3?

A) It is always 4 bytes.
B) It is always 8 bytes.
C) It depends on the magnitude of the number (variable length).
D) It depends on the variable name length.

**Answer: C**

**Explanation:**
Python 3 integers are variable-length objects. Small integers take less memory (min 28 bytes), while massive integers grow by allocating more digits (30-bit chunks usually) in the underlying array.

---

**Q2.30: Expert - [Hash]**

Which of the following types is **not** hashable and thus cannot be used as a dictionary key?

A) `str`
B) `tuple` (containing only integers)
C) `frozenset`
D) `bytearray`

**Answer: D**

**Explanation:**
`bytearray` is the mutable version of `bytes`. Mutable objects are generally not hashable because if the object changes, its hash would change, breaking the dictionary lookup invariant. `tuple` and `frozenset` (containing immutable items) are hashable.

---

**Q2.31: Intermediate - [Boolean Int]**

What is the result of `True + 5`?

A) `True5`
B) `6`
C) `TypeError`
D) `5`

**Answer: B**

**Explanation:**
`True` behaves like integer `1` in arithmetic operations. `1 + 5 = 6`.

---

**Q2.32: Advanced - [Variable Scope]**
(Moved to Chapter 5 context, but relevant to variable resolution)
If you assign to a variable inside a function without declaring it global, what happens?

A) It modifies the global variable.
B) It creates a new local variable, shadowing any global one.
C) It raises a `SyntaxError`.
D) It raises an `UnboundLocalError`.

**Answer: B**

**Explanation:**
Assignment to a variable name inside a function makes that variable **local** to the function scope by default, even if a global variable with the same name exists. This is called shadowing.

---

**Q2.33: Basic - [Raw Strings]**

What is the primary purpose of a raw string `r"..."`?

A) To create bytes.
B) To ignore escape characters (like `\n`, `\t`, `\\`).
C) To improve performance.
D) To denote regex patterns automatically.

**Answer: B**

**Explanation:**
Raw strings treat backslashes as literal characters. `r"\n"` is a string of two characters (`\` and `n`), not a newline. This is heavily used in Regular Expressions and file paths on Windows.

---

**Q2.34: Expert - [Interning]**

Does Python automatically intern all strings?

A) Yes, all strings are interned.
B) No, only short strings that look like identifiers (letters, digits, underscores) are usually interned automatically.
C) No, strings are never interned unless you use `sys.intern()`.
D) Yes, but only in Python 3.

**Answer: B**

**Explanation:**
CPython automatically interns string literals that look like identifiers (and some others) to speed up dictionary lookups (variables, attributes). Strings created at runtime or containing special characters are usually not interned unless explicitly requested via `sys.intern()`.

---

**Q2.35: Intermediate - [Augmented Assignment]**

What is the difference between `x = x + y` and `x += y` for a list `x`?

A) No difference.
B) `x += y` modifies the list in-place (like `extend`), `x = x + y` creates a new list.
C) `x += y` is slower.
D) `x = x + y` raises an error.

**Answer: B**

**Explanation:**
For mutable objects like lists, `+=` calls `__iadd__` (in-place add). `x.extend(y)` is effectively called, modifying the original object. `x + y` calls `__add__`, creating a new list object containing elements from both.

---

**Q2.36: Advanced - [Complex Constructor]**

What is the result of `complex('1+2j')`?

A) `1+2j`
B) `ValueError`
C) `TypeError`
D) `(1+2j)`

**Answer: A**

**Explanation:**
The `complex()` constructor can parse a string. However, **no spaces** are allowed around the `+` or `-` operator in the string. `complex('1 + 2j')` would raise `ValueError`. `complex('1+2j')` works.

---

**Q2.37: Intermediate - [None Return]**

If a function does not explicitly return a value, what does it return?

A) `0`
B) `False`
C) `None`
D) It returns nothing (void).

**Answer: C**

**Explanation:**
In Python, all functions return a value. If no `return` statement is executed, the function implicitly returns `None`.

---

**Q2.38: Advanced - [Chained Assignment]**

In `x = y = []`, are `x` and `y` the same object?

A) Yes.
B) No.
C) Depends on optimization levels.
D) Syntax Error.

**Answer: A**

**Explanation:**
The expression creates a single list object `[]` and assigns its reference to both variables `x` and `y`. Modifying one will affect the other.

---

**Q2.39: Basic - [Del]**

What does the `del` statement do?

A) Destroys the object immediately (frees memory).
B) Removes the reference (name binding) to the object.
C) Sets the variable to `None`.
D) Deletes the file on disk.

**Answer: B**

**Explanation:**
`del x` removes the name `x` from the namespace. It decrements the reference count of the object `x` pointed to. The object is only destroyed (garbage collected) if its reference count drops to zero.

---

**Q2.40: Intermediate - [String Encode]**

Which method converts a `str` to `bytes`?

A) `decode()`
B) `encode()`
C) `bytes()`
D) `to_bytes()`

**Answer: B**

**Explanation:**
Strings are encoded into bytes (e.g., using UTF-8). Bytes are decoded into strings. mnemonic: "You encode text into secret code (bytes), and decode it back".

---

**Q2.41: Expert - [Ellipsis]**

What is the `...` literal in Python?

A) A syntax error.
B) The Ellipsis object (singleton).
C) A placeholder for future code (pass).
D) A valid variable name.

**Answer: B**

**Explanation:**
`...` is the literal for the `Ellipsis` object (a singleton). It is used in extended slicing (NumPy), type hints (Callable[..., int]), and as a placeholder for unwritten code (similar to `pass`).

---

**Q2.42: Basic - [Casting]**

What is the result of `bool("False")`?

A) `False`
B) `True`
C) `None`
D) `0`

**Answer: B**

**Explanation:**
`bool(x)` creates `True` for any non-empty string. Only empty string `""` becomes `False`. The content "False" is irrelevant; it's a non-empty string.

---

**Q2.43: Intermediate - [Literals]**

Which literal represents the decimal value 10?

A) `0b1010`
B) `0o12`
C) `0xA`
D) All of the above.

**Answer: D**

**Explanation:**
- `0b1010` is binary for 10 ($$1*8 + 0*4 + 1*2 + 0*1$$).
- `0o12` is octal for 10 ($$1*8 + 2*1$$).
- `0xA` is hex for 10.
All are valid integer literals for the value 10.

---

**Q2.44: Advanced - [Type vs Isinstance]**

Why doesn't `isinstance(True, int)` return `False`?

A) Because `bool` is a subclass of `int` in Python.
B) It's a bug in Python.
C) `isinstance` checks the value, not the type.
D) It typically returns False, unless `ABC` is used.

**Answer: A**

**Explanation:**
In Python, `bool` inherits from `int`. `True` is effectively `1` and `False` is `0`. Thus `isinstance(True, int)` is `True`.

---

**Q2.45: Expert - [String Formatting Attack]**

What is a potential security risk of using `str.format()` with user-supplied format strings?

A) Code injection.
B) Accessing internal object attributes/globals.
C) Buffer overflow.
D) SQL Injection.

**Answer: B**

**Explanation:**
If an attacker controls the format string, they can access attributes of the arguments. E.g., `"{0.__class__.__init__.__globals__}".format(user_input)` could leak global variables or secrets. This is why f-strings (evaluated in code scope) or explicit templates are safer than formatting untrusted strings.

---

**Q2.46: Intermediate - [Float Infinity]**

How do you represent positive infinity as a float?

A) `float('inf')`
B) `math.infinity` (not in standard, `math.inf` exists)
C) `Infinity`
D) `1e999` (overflows to inf)

**Answer: A**

**Explanation:**
`float('inf')` creates an infinite float. `math.inf` is also available in Python 3.5+.

---

**Q2.47: Advanced - [Bytearray]**

What is the key difference between `bytes` and `bytearray`?

A) `bytearray` can contain unicode.
B) `bytearray` is mutable.
C) `bytes` takes less memory per element.
D) `bytes` is not iterable.

**Answer: B**

**Explanation:**
`bytearray` is a mutable sequence of integers (0-255). You can modify elements in place: `b[0] = 255`. `bytes` is immutable.

---

**Q2.48: Basic - [None comparison]**

Is `None == 0` True or False?

A) True
B) False
C) It raises SyntaxError.
D) Only in Python 2.

**Answer: B**

**Explanation:**
`None` is its own type and is not equal to 0, False, or empty string.

---

**Q2.49: Intermediate - [Identity conservation]**

Which of the following creates a new object (new id)?

A) `x = 100; y = 100` (in REPL)
B) `s1 = "hello"; s2 = s1`
C) `L1 = [1, 2]; L2 = list(L1)`
D) `t1 = (1, 2); t2 = tuple(t1)`

**Answer: C**

**Explanation:**
- A refers to small int caching (same id).
- B refers to simple alias binding (same id).
- D `tuple()` on a tuple returns the original object (optimization since immutable).
- C `list()` on a list creates a shallow copy (new object).

---

**Q2.50: Expert - [Subclassing Primitives]**

Can you extend the built-in `str` class?

A) No, built-in types are final.
B) Yes, by inheriting from `str`.
C) Only via C extensions.
D) Yes, but you cannot add new methods.

**Answer: B**

**Explanation:**
You can subclass built-in types like `str`, `int`, `list`. For immutable types like `str` and `int`, you often need to override `__new__` instead of `__init__` to customize instance creation.

---

---

## Review Notes (2026-02-06)

- Q2.15 contains drafting artifacts and a revised question embedded in the option/explanation text; the original premise is also misleading for typical CPython builds.
- Q2.43 appears twice (duplicate question ID). The first Q2.43 includes an incorrect literal note (`0x10`) and inline answer-drafting text ("Answer check", "Let's refine").
- Q2.50 option D has a typo ("Ye" -> "Yes").
- Q2.48 uses only A/B choices, which is inconsistent with the predominant 4-option MCQ format.
