# Chapter 3: Operators & Expressions

**Target MCQs**: 40-50
**Current Batch**: 1-25
**Topics Covered**: Arithmetic, Bitwise, Logical, Comparison, Precedence, Short-circuiting

---

**Q3.1: Basic - [Arithmetic Operators]**

What is the result of `10 % 3`?

A) `1`
B) `3`
C) `0`
D) `3.33`

**Answer: A**

**Explanation:**
The modulus operator `%` returns the remainder of the division. `10 // 3` is `3`, and the remainder is `1` ($$10 - 3 \times 3 = 1$$).

---

**Q3.2: Basic - [Power Operator]**

Which operator is used for exponentiation in Python?

A) `^`
B) `**`
C) `exp()`
D) `^^`

**Answer: B**

**Explanation:**
`**` is the exponentiation operator. `2 ** 3` is `8`. The `^` operator is the Bitwise XOR operator in Python.

---

**Q3.3: Intermediate - [Operator Precedence]**

What is the result of `2 + 3 * 4`?

A) `20`
B) `14`
C) `24`
D) `10`

**Answer: B**

**Explanation:**
Multiplication `*` has higher precedence than addition `+`. `3 * 4` is evaluated first (12), then `2 + 12` results in `14`.

---

**Q3.4: Basic - [Comparison]**

What is the result of `10 != 10`?

A) `True`
B) `False`
C) `None`
D) `Error`

**Answer: B**

**Explanation:**
`!=` checks for inequality. Since `10` is equal to `10`, the statement "10 is not equal to 10" is False.

---

**Q3.5: Advanced - [Chained Comparison]**

What is the result of `1 < 2 < 3`?

A) `True`
B) `False`
C) `3`
D) `1`

**Answer: A**

**Explanation:**
Python chains comparisons. `1 < 2 < 3` is equivalent to `(1 < 2) and (2 < 3)`. Both are true, so the result is True. This is unlike many C-like languages where `(1 < 2)` evaluates to `1` (true), and then `1 < 3` is checked.

---

**Q3.6: Intermediate - [Bitwise Operators]**

What is the result of `5 & 3`?

A) `7`
B) `1`
C) `5`
D) `8`

**Answer: B**

**Explanation:**
`&` is the Bitwise AND operator.
5 in binary: `101`
3 in binary: `011`
Result:      `001` (which is decimal 1).

---

**Q3.7: Intermediate - [Bitwise shift]**

What is the result of `8 >> 2`?

A) `4`
B) `2`
C) `1`
D) `32`

**Answer: B**

**Explanation:**
`>>` is the right shift operator. Shifting 8 (`1000`) right by 2 bits results in `0010`, which is 2. Effectively, it divides by $$2^n$$ (integer division). $$8 // 2^2 = 2$$.

---

**Q3.8: Advanced - [Boolean Logic]**

What is the result of `True or False and False`?

A) `False`
B) `True`
C) `None`
D) `SyntaxError`

**Answer: B**

**Explanation:**
`and` has higher precedence than `or`.
1. `False and False` -> `False`
2. `True or False` -> `True`
If read left-to-right without precedence, it would be `(True or False) -> True`, then `True and False -> False`, which is incorrect.

---

**Q3.9: Expert - [Short Circuiting]**

Consider the function:
```python
def check():
    print("Checked")
    return True
```
What is printed when running `True or check()`?

A) "Checked"
B) Nothing
C) "True"
D) Error

**Answer: B**

**Explanation:**
The `or` operator **short-circuits**. If the first operand is Truthy (`True`), it returns it immediately without evaluating the second operand. Thus, `check()` is never called.

---

**Q3.10: Intermediate - [Walrus Operator]**

What does the following equality check evaluate to?
`(x := 10) == 10`

A) `True` (and `x` is 10)
B) `False`
C) `None`
D) SyntaxError

**Answer: A**

**Explanation:**
The assignment expression `x := 10` assigns `10` to `x` and *returns* the value `10`. Then `10 == 10` is evaluated, which is `True`.

---

**Q3.11: Basic - [Identity vs Equality]**

Which operator checks if two variables point to the same object in memory?

A) `==`
B) `eq`
C) `is`
D) `===`

**Answer: C**

**Explanation:**
`is` checks for object identity (memory address). `==` checks for value equality. Python does not have `===`.

---

**Q3.12: Advanced - [Unary Operators]**

What is the result of `~5`?

A) `-5`
B) `-6`
C) `4`
D) `-4`

**Answer: B**

**Explanation:**
`~` is the bitwise NOT operator. The result of `~x` is arithmetic $$-(x+1)$$. `~5` -> $$-(5+1) = -6$$. In two's complement binary: `0...0101` becomes `1...1010` (which represents -6).

---

**Q3.13: Intermediate - [In Operator]**

Which of the following raises a `TypeError`?

A) `"a" in "apple"`
B) `1 in [1, 2, 3]`
C) `1 in "123"`
D) `"key" in {"key": 1}`

**Answer: C**

**Explanation:**
The `in` operator for strings expects the left operand to also be a string. `1` is an integer. Correct usage: `"1" in "123"`.

---

**Q3.14: Advanced - [Ternary Operator]**

What is the correct syntax for a conditional expression (ternary operator) in Python?

A) `condition ? true_val : false_val`
B) `true_val if condition else false_val`
C) `if condition then true_val else false_val`
D) `condition and true_val or false_val`

**Answer: B**

**Explanation:**
Python's syntax is `value_if_true if condition else value_if_false`.
Option D is an old trick that works partially but fails if `true_val` is Falsy.

---

**Q3.15: Expert - [Tuple Unpacking Star]**

What is the value of `b` after `a, *b, c = [1, 2, 3, 4, 5]`?

A) `2`
B) `[2, 3, 4]`
C) `(2, 3, 4)`
D) `[2, 3, 4, 5]`

**Answer: B**

**Explanation:**
The `*` operator in unpacking captures "the rest" of the items as a list. `a` gets `1` (first), `c` gets `5` (last), and `b` captures everything in between as a `list`: `[2, 3, 4]`.

---

**Q3.16: Intermediate - [String Concatenation]**

What is the result of `"Ha" * 3`?

A) `"HaHaHa"`
B) `"Ha3"`
C) Error
D) `["Ha", "Ha", "Ha"]`

**Answer: A**

**Explanation:**
The `*` operator on a string and an integer performs repetition.

---

**Q3.17: Basic - [Logic]**

What is the result of `not True`?

A) `False`
B) `True`
C) `None`
D) `-1`

**Answer: A**

**Explanation:**
`not` is the logical negation operator.

---

**Q3.18: Advanced - [List Addition]**

What happens if you do `[1, 2] + (3, 4)`?

A) `[1, 2, 3, 4]`
B) `TypeError`
C) `(1, 2, 3, 4)`
D) `[[1, 2], (3, 4)]`

**Answer: B**

**Explanation:**
Explicit addition `+` between a list and a tuple is not supported; operands must be the same type. You must cast one: `[1, 2] + list((3, 4))` works. Note: `+=` (in-place) *does* work (`l += t`) because it uses the iterable protocol.

---

**Q3.19: Expert - [Operator Overloading]**

Which magic method is called when `x + y` is executed?

A) `x.__add__(y)`
B) `x.__plus__(y)`
C) `x.__sum__(y)`
D) `x.__append__(y)`

**Answer: A**

**Explanation:**
`__add__` is the dunder method for the `+` operator. If `x` doesn't support it, `y.__radd__(x)` (reflected add) is checked.

---

**Q3.20: Intermediate - [Dict Merge]**

In Python 3.9+, what does the `|` operator do for dictionaries?

A) Bitwise OR of keys.
B) Set union of keys.
C) Merges two dictionaries.
D) Intersects two dictionaries.

**Answer: C**

**Explanation:**
Python 3.9 introduced the dictionary merge operator `|`. `d1 | d2` creates a new dictionary with combined pairs. If keys overlap, `d2` wins.

---

**Q3.21: Advanced - [Comparison Chaining 2]**

What is the result of `False == False in [False]`?

A) `True`
B) `False`
C) Error
D) `[False]`

**Answer: A**

**Explanation:**
Chained comparison again!
`False == False in [False]` is evaluated as `(False == False) and (False in [False])`.
1. `False == False` is `True`.
2. `False in [False]` is `True`.
Result: `True`.

---

**Q3.22: Intermediate - [Floor Division]**

What is `-3 // 2`?

A) `-1`
B) `-2`
C) `-1.5`
D) `1`

**Answer: B**

**Explanation:**
Floor division rounds down to the nearest integer. `-1.5` rounded down (towards negative infinity) is `-2`.

---

**Q3.23: Basic - [Augmented Assignment]**

What does `x /= 2` do?

A) `x = x // 2`
B) `x = x / 2`
C) `x = 2 / x`
D) `x = int(x / 2)`

**Answer: B**

**Explanation:**
`/=` corresponds to true division `/`. The result is a float (in Python 3).

---

**Q3.24: Advanced - [Is vs == small ints]**
(Revisiting concept with operator focus)
`a = 256; b = 256`. `a is b` -> True.
`a = 300; b = 300`. `a is b` -> ?

A) True (always)
B) False (usually, in console)
C) Error
D) True (in Python 3.10+ only)

**Answer: B**

**Explanation:**
For integers outside the cached range [-5, 256], Python usually creates new objects, so `is` returns False. Note that in script files (not REPL), compiler optimizations might make them point to the same object, but broadly speaking, it is False.

---

**Q3.25: Expert - [Matrix Multiplication]**

What is the `@` operator used for in Python?

A) Decorators (only).
B) Matrix Multiplication.
C) Email validation.
D) Asynchronous calls.

**Answer: B**

**Explanation:**
In expression context, `@` is the matrix multiplication operator (PEP 465), implemented via `__matmul__`. It is used by libraries like NumPy (`A @ B`). (It is also used for decorator syntax, but that is not an operator in an expression context).

---

**Q3.26: Basic - [Equality]**

Which statement regarding `==` and `!=` is true?

A) `10 == 10.0` is False because types differ.
B) `10 == 10.0` is True because values are numerically equal.
C) `10 != 10.0` is True.
D) They raise TypeError when comparing different types.

**Answer: B**

**Explanation:**
Python coerces numeric types for comparison. `10` (int) and `10.0` (float) represent the same value, so `==` returns True.

---

**Q3.27: Advanced - [Short Circuit Logic]**

What is the return value of `print("A") or print("B")`?

A) "A" then "B"
B) `None` (after printing "A" and "B")
C) `None` (after printing "A")
D) `True`

**Answer: B**

**Explanation:**
`print()` returns `None`, which is Falsy.
1. `print("A")` runs, outputting "A", returns `None`.
2. `or` sees Falsy, so it evaluates the second operand.
3. `print("B")` runs, outputting "B", returns `None`.
4. Final result is `None`.

---

**Q3.28: Intermediate - [String Multiplication]**

What happens if you try `"abc" * -2`?

A) `"abcabc"` (absolute value)
B) `ValueError`
C) `""` (empty string)
D) `TypeError`

**Answer: C**

**Explanation:**
Multiplying a sequence by a number $\le 0$ results in an empty sequence.

---

**Q3.29: Advanced - [Precedence Chains]**

What is the result of `False == False or True`?

A) `True`
B) `False`
C) `None`
D) Error

**Answer: A**

**Explanation:**
`==` has higher precedence than `or`.
1. `False == False` -> `True`.
2. `True or True` -> `True`.

---

**Q3.30: Expert - [Bitwise Not Truthiness]**

For which integer `x` is `not ~x` True?

A) `0`
B) `-1`
C) `1`
D) No integer.

**Answer: B**

**Explanation:**
`~x` is $$-(x + 1)$$.
`not ~x` is True only if `~x` is 0 (Falsy).
$$-(x + 1) = 0 \implies x + 1 = 0 \implies x = -1$$.
So `~(-1)` is `0`, and `not 0` is `True`.

---

**Q3.31: Intermediate - [List Comparison]**

How does Python compare two lists `[1, 2]` and `[1, 3]`?

A) It compares the sums of elements.
B) It compares length first, then elements.
C) It compares lexicographically (element by element).
D) It compares memory addresses.

**Answer: C**

**Explanation:**
Sequences are compared lexicographically. The first elements `1` and `1` are equal. The second elements `2` and `3` are compared. Since `2 < 3`, `[1, 2] < [1, 3]` is True.

---

**Q3.32: Advanced - [Set Operators]**

What is the equivalent of the `&` operator for sets `A` and `B`?

A) `A.union(B)`
B) `A.intersection(B)`
C) `A.difference(B)`
D) `A.symmetric_difference(B)`

**Answer: B**

**Explanation:**
`&` performs set intersection. `|` is union. `-` is difference. `^` is symmetric difference.

---

**Q3.33: Basic - [Keyword In]**

Which method is implicitly called by `x in y`?

A) `y.__contains__(x)`
B) `x.__in__(y)`
C) `y.__check__(x)`
D) `y.has(x)`

**Answer: A**

**Explanation:**
The `in` operator delegates to `y.__contains__(x)`. If that doesn't exist, Python tries to iterate over `y` via `__iter__` or `__getitem__`.

---

**Q3.34: Intermediate - [Tuple Parentheses]**

Is `x = 1, 2` a valid tuple assignment?

A) No, parentheses are required: `(1, 2)`
B) Yes, the comma creates the tuple.
C) No, it's a syntax error.
D) Yes, but only in Python 2.

**Answer: B**

**Explanation:**
The comma `,` allows tuple creation. Parentheses are implicit here. `x` becomes `(1, 2)`. Parentheses are mandatory only for empty tuples `()` or to disambiguate expression (e.g., inside function calls).

---

**Q3.35: Advanced - [Slice Assignment]**

Given `a = [1, 2, 3]`, what does `a[1:2] = [4, 5]` do?

A) `a` becomes `[1, 4, 5, 2, 3]`
B) `a` becomes `[1, 4, 5, 3]`
C) `ValueError` (size mismatch)
D) `a` becomes `[1, [4, 5], 3]`

**Answer: B**

**Explanation:**
Slice assignment replaces the slice (index 1 to 2, which is `[2]`) with the iterable elements `[4, 5]`.
Original: `1`, `2`, `3`
Replace `2` with `4, 5`
Result: `1, 4, 5, 3`.

---

**Q3.36: Expert - [Custom Truthiness]**

How do you customize the Truthy/Falsy value of a user-defined class instance?

A) Implement `__bool__` or `__len__`.
B) Implement `__true__`.
C) Inherit from `bool`.
D) You cannot; all instances are True.

**Answer: A**

**Explanation:**
Python calls `obj.__bool__()`. If not defined, it calls `obj.__len__()` (0 is False, >0 is True). If neither is defined, the object is considered True.

---

**Q3.37: Intermediate - [Is None]**

Why is `x is not None` preferred over `not x is None`?

A) Performance.
B) Readability and adherence to PEP 8.
C) The latter is a syntax error.
D) Operator precedence difference.

**Answer: B**

**Explanation:**
Both compile to widely similar optimizations, but `is not` is a specific operator in Python intended for readability. PEP 8 recommends `if x is not None`.

---

**Q3.38: Advanced - [Generator Expression]**

What produces the object `<generator object ...>`?

A) `[x for x in range(3)]`
B) `(x for x in range(3))`
C) `{x for x in range(3)}`
D) `gen(x for x in range(3))`

**Answer: B**

**Explanation:**
Parentheses `()` around a comprehension syntax create a **generator expression**. Brackets `[]` create a list. Braces `{}` create a set (or dict).

---

**Q3.39: Basic - [Equality vs Identity]**

If `a = 500` and `b = 500`; `a == b` is:

A) True
B) False

**Answer: A**

**Explanation:**
`==` compares values. 500 equals 500. (Even though `a is b` implies False).

---

**Q3.40: Intermediate - [Sequence Multiplication]**

What is the result of `[[]] * 3`?

A) `[[], [], []]` (3 distinct empty lists)
B) `[[], [], []]` (3 references to the **same** empty list)
C) `TypeError`
D) `[[3]]`

**Answer: B**

**Explanation:**
It creates a list containing 3 references to the *same* inner list object.
`x = [[]] * 3`
`x[0].append(1)`
`print(x)` -> `[[1], [1], [1]]`.

---

**Q3.41: Advanced - [Infinity Math]**

What is `float('inf') - float('inf')`?

A) `0.0`
B) `nan` (Not a Number)
C) `inf`
D) `ValueError`

**Answer: B**

**Explanation:**
Infinity minus infinity is undefined in floating point arithmetic, resulting in `nan`.

---

**Q3.42: Expert - [All/Any]**

What is the result of `all([])` and `any([])`?

A) True, True
B) False, False
C) True, False
D) False, True

**Answer: C**

**Explanation:**
- `all([])`: Are all elements in empty list true? Yes (vacuously true).
- `any([])`: Are there any true elements in empty list? No.

---

**Q3.43: Intermediate - [Operator Module]**

Which standard module provides functional equivalents to built-in operators (like `add` for `+`)?

A) `functions`
B) `sys`
C) `math`
D) `operator`

**Answer: D**

**Explanation:**
The `operator` module exports a set of efficient functions corresponding to the intrinsic operators (e.g., `operator.add(x, y)`).

---

**Q3.44: Comparison - [Sorting]**

When using `sort()`, which operator is used to compare elements?

A) `>`
B) `>=`
C) `<`
D) `==`

**Answer: C**

**Explanation:**
Python's sort definition relies on the "less than" `<` operator (`__lt__`). It assumes a total ordering.

---

**Q3.45: Advanced - [Format String]**

What does the comparison `x <= y <= z` compile to?

A) `(x <= y) and (y <= z)` (but `y` is evaluated once)
B) `(x <= y) and (y <= z)` (y evaluated twice)
C) `operator.le(x, y, z)`
D) It is syntactic sugar for a range check `x in range(y, z)`.

**Answer: A**

**Explanation:**
Chained comparisons evaluate each operand exactly once (except the first). `y` is not re-evaluated, making it efficient and side-effect safe compared to manual `and`.

---

**Q3.46: Basic - [Modulus Sign]**

What is the sign of the result of `%` operator in Python?

A) Same as the dividend (left operand).
B) Same as the divisor (right operand).
C) Always positive.
D) Always negative.

**Answer: B**

**Explanation:**
In Python, the result of the modulo operator matches the sign of the **divisor** (right-hand operand).
`-10 % 3 = 2` (sign of 3)
`10 % -3 = -2` (sign of -3).
This differs from C/Java where it matches the dividend.

---

**Q3.47: Expert - [Compare Exceptions]**

What happens if a comparison raises an exception inside a chain? e.g. `a < b < c` where `a < b` raises.

A) The whole expression evaluates to False.
B) The exception propagates immediately.
C) It continues to check `b < c`.
D) It returns `None`.

**Answer: B**

**Explanation:**
Exceptions propagate immediately. Short-circuiting logic only applies to boolean `True`/`False` results.

---

**Q3.48: Intermediate - [Bytes/Int]**

Which operator allows converting bytes to int in Python 3.2+?

A) `int.from_bytes(b, 'big')`
B) `bytes.to_int()`
C) `int(b)`
D) `b >> 0`

**Answer: A**

**Explanation:**
`int.from_bytes()` is the class method to convert a byte sequence into an integer, requiring the byte order ('big' or 'little').

---

**Q3.49: Basic - [Membership]**

`"apple" not in ["apple", "banana"]`.

A) True
B) False

**Answer: B**

**Explanation:**
"apple" IS in the list, so `not in` is False.

---

**Q3.50: Advanced - [Call Operator]**

Which operator implies that an object is callable (like a function)?

A) `.` (dot)
B) `()` (parentheses)
C) `->`
D) `call`

**Answer: B**

**Explanation:**
The parentheses operator `()` invokes the `__call__` method of the object.

---

---

## Review Notes (2026-02-06)

- Q3.39 and Q3.49 use only A/B options, which is inconsistent with the predominant 4-option MCQ format.
