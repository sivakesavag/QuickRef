# Chapter 4: Control Flow

> **Topics Covered**: if-elif-else, ternary expressions, for loops, while loops, else clauses in loops, break, continue, pass, match-case (Python 3.10+), loop optimization, comprehensions control flow

---

## Questions

---

**Q4.1: Basic - [if Statement]**

What is the correct syntax for an if statement in Python?

A) `if x > 5 { print("yes") }`
B) `if (x > 5): print("yes")`
C) `if x > 5: print("yes")`
D) `if x > 5 then print("yes")`

**Answer: C**

**Explanation:**
Python uses colons and indentation, not braces or `then` keywords. Parentheses around the condition are optional (B works but is not idiomatic). The most Pythonic form is without parentheses: `if x > 5:`. Indentation defines the block.

---

**Q4.2: Basic - [if-elif-else]**

What is the output?
```python
x = 15
if x > 20:
    print("A")
elif x > 10:
    print("B")
elif x > 5:
    print("C")
else:
    print("D")
```

A) `A`
B) `B`
C) `B` and `C`
D) `C`

**Answer: B**

**Explanation:**
Only the first matching condition executes. `x > 20` is False, `x > 10` is True (15 > 10), so "B" prints. Even though `x > 5` is also True, it's never checked because we already matched. `elif` chains are mutually exclusive.

---

**Q4.3: Basic - [if Falsy Values]**

What is the output?
```python
if []:
    print("truthy")
else:
    print("falsy")
```

A) `truthy`
B) `falsy`
C) Error
D) Nothing

**Answer: B**

**Explanation:**
Empty sequences ([], (), {}, "", set()) are falsy in Python. Non-empty sequences are truthy. The empty list `[]` evaluates to False in boolean context. This allows idiomatic code like `if my_list:` instead of `if len(my_list) > 0:`.

---

**Q4.4: Intermediate - [Nested Conditions]**

Which is equivalent to `if a and b:`?

A) `if a: if b:`
B) `if a or b:`
C) `if a == b:`
D) `if a then b:`

**Answer: A**

**Explanation:**
`if a and b:` executes the block only if both `a` and `b` are truthy. This is equivalent to nested ifs: if `a` is truthy, then check `b`. With nested ifs, the inner block runs only when both conditions are met.

---

**Q4.5: Basic - [for Loop]**

What is the output?
```python
for i in range(3):
    print(i, end=" ")
```

A) `1 2 3`
B) `0 1 2`
C) `0 1 2 3`
D) `1 2`

**Answer: B**

**Explanation:**
`range(3)` generates `0, 1, 2` (start=0, stop=3, exclusive). Python ranges are 0-indexed and exclude the stop value. The `end=" "` makes print separate values with space instead of newline.

---

**Q4.6: Basic - [range Function]**

What is the output of `list(range(2, 8, 2))`?

A) `[2, 4, 6, 8]`
B) `[2, 4, 6]`
C) `[2, 3, 4, 5, 6, 7]`
D) `[0, 2, 4, 6]`

**Answer: B**

**Explanation:**
`range(start, stop, step)` generates values from `start` to `stop` (exclusive) with given step. `range(2, 8, 2)` gives 2, 4, 6. The value 8 is excluded. Step of 2 means every other number.

---

**Q4.7: Intermediate - [Negative Range]**

What is the output of `list(range(5, 0, -1))`?

A) `[5, 4, 3, 2, 1, 0]`
B) `[5, 4, 3, 2, 1]`
C) `[]`
D) `[0, 1, 2, 3, 4, 5]`

**Answer: B**

**Explanation:**
Negative step counts down. `range(5, 0, -1)` starts at 5, decrements by 1, stops before 0. Result: 5, 4, 3, 2, 1. The stop value (0) is always excluded. For inclusive: `range(5, -1, -1)` gives 5, 4, 3, 2, 1, 0.

---

**Q4.8: Basic - [while Loop]**

What is the output?
```python
x = 3
while x > 0:
    print(x, end=" ")
    x -= 1
```

A) `3 2 1 0`
B) `3 2 1`
C) `2 1 0`
D) Infinite loop

**Answer: B**

**Explanation:**
Loop executes while `x > 0`. Print x, then decrement. Iterations: x=3 (print 3), x=2 (print 2), x=1 (print 1), x=0 (condition false, exit). Output: `3 2 1`. Note: 0 is never printed because the condition is checked before the body executes.

---

**Q4.9: Intermediate - [Infinite Loop]**

Which creates an intentional infinite loop?

A) `for i in range():`
B) `while True:`
C) `loop forever:`
D) `for ever:`

**Answer: B**

**Explanation:**
`while True:` is the standard idiom for infinite loops in Python. Exit with `break`, `return`, or `sys.exit()`. `range()` requires at least one argument. There are no `loop` or `for ever` constructs in Python.

---

**Q4.10: Basic - [break Statement]**

What is the output?
```python
for i in range(5):
    if i == 3:
        break
    print(i, end=" ")
```

A) `0 1 2 3`
B) `0 1 2`
C) `0 1 2 4`
D) `3`

**Answer: B**

**Explanation:**
`break` immediately exits the innermost loop. When i=3, break executes before print, so only 0, 1, 2 are printed. The loop doesn't continue to 4. `break` is typically used with a condition to exit early.

---

**Q4.11: Basic - [continue Statement]**

What is the output?
```python
for i in range(5):
    if i == 2:
        continue
    print(i, end=" ")
```

A) `0 1 2 3 4`
B) `0 1 3 4`
C) `0 1`
D) `2`

**Answer: B**

**Explanation:**
`continue` skips the rest of the current iteration and moves to the next. When i=2, it skips the print and continues with i=3. All values except 2 are printed. Unlike `break`, `continue` doesn't exit the loop.

---

**Q4.12: Basic - [pass Statement]**

What is the purpose of the `pass` statement?

A) Skip the current iteration
B) Exit the loop
C) Do nothing (placeholder)
D) Pass control to another function

**Answer: C**

**Explanation:**
`pass` is a null operation — a placeholder where syntax requires a statement but no action is needed. Common uses: empty function bodies, empty class definitions, placeholder in if/else branches. Unlike `continue`, it doesn't affect loop flow.

---

**Q4.13: Intermediate - [for-else]**

What is the output?
```python
for i in range(3):
    if i == 5:
        break
else:
    print("Complete")
```

A) Nothing
B) `Complete`
C) `5`
D) Error

**Answer: B**

**Explanation:**
The `else` clause of a `for` loop executes if the loop completes without hitting `break`. Since i never equals 5 in range(3), break never executes, so `else` runs. The `else` clause is skipped only when `break` is triggered. Useful for search loops.

---

**Q4.14: Intermediate - [for-else with break]**

What is the output?
```python
for i in range(5):
    if i == 3:
        break
else:
    print("Complete")
```

A) `Complete`
B) Nothing
C) `3`
D) Error

**Answer: B**

**Explanation:**
When i=3, `break` executes. This skips the `else` clause entirely. The `else` clause runs only on normal loop completion (exhausting the iterator). This pattern is useful for searches: `else` handles "not found" case.

---

**Q4.15: Intermediate - [while-else]**

What is the output?
```python
x = 0
while x < 3:
    x += 1
else:
    print("Done:", x)
```

A) `Done: 0`
B) `Done: 3`
C) Nothing
D) `Done: 2`

**Answer: B**

**Explanation:**
Like `for`, `while` can have an `else` clause that runs if the loop completes without `break`. After x increments to 3, the condition fails, loop exits normally, and `else` runs. The value of x is 3 (the value that caused the condition to be False).

---

**Q4.16: Intermediate - [Nested Loops and break]**

What does `break` do in nested loops?

A) Exits all loops
B) Exits only the innermost loop
C) Exits the outermost loop
D) Pauses all loops

**Answer: B**

**Explanation:**
`break` only exits the innermost enclosing loop. To exit multiple levels, use a flag variable, put loops in a function and use `return`, use exception handling, or restructure with itertools functions. Python doesn't have labeled break like Java.

---

**Q4.17: Advanced - [Nested Loop Exit Pattern]**

How can you exit multiple nested loops at once?

A) `break 2`
B) Use a flag variable and check it in outer loops
C) `break all`
D) Not possible in Python

**Answer: B**

**Explanation:**
Python lacks labeled breaks. Common patterns: (1) Set a flag `found = True` then `break`, check flag in outer loop. (2) Wrap in function and use `return`. (3) Use exception (not recommended for control flow). (4) Refactor using generator or itertools.

---

**Q4.18: Basic - [Iterating with index]**

What is the Pythonic way to iterate with index over a list?

A) `for i in range(len(lst)): item = lst[i]`
B) `for i, item in enumerate(lst):`
C) `for item.index in lst:`
D) `for item with index in lst:`

**Answer: B**

**Explanation:**
💡 **Best practice**: `enumerate()` returns (index, item) tuples. It's more Pythonic than using range(len()) and indexing. `enumerate(lst, start=1)` can start counting from 1 instead of 0. This is cleaner and avoids off-by-one errors.

---

**Q4.19: Intermediate - [enumerate]**

What is the output?
```python
for i, char in enumerate("abc", start=1):
    print(i, char)
```

A) `0 a, 1 b, 2 c`
B) `1 a, 2 b, 3 c`
C) `a 0, b 1, c 2`
D) Error

**Answer: B**

**Explanation:**
`enumerate("abc", start=1)` produces `(1, 'a'), (2, 'b'), (3, 'c')`. The `start` parameter sets the initial count value. Useful for 1-based line numbers or human-readable indexing.

---

**Q4.20: Intermediate - [zip Function]**

What is the output?
```python
for a, b in zip([1, 2], ['x', 'y', 'z']):
    print(a, b)
```

A) `1 x, 2 y, None z`
B) `1 x, 2 y`
C) Error: mismatched lengths
D) `1 x, 2 y, z`

**Answer: B**

**Explanation:**
`zip()` pairs elements from multiple iterables, stopping at the shortest one. With lists of 2 and 3 elements, it produces 2 pairs: (1, 'x') and (2, 'y'). The 'z' is ignored. Use `itertools.zip_longest` to include all elements with fillvalue.

---

**Q4.21: Intermediate - [Multiple Assignment in Loop]**

What is the output?
```python
pairs = [(1, 'a'), (2, 'b')]
for num, letter in pairs:
    print(letter, num)
```

A) `(1, 'a') (2, 'b')`
B) `a 1, b 2`
C) `1 a, 2 b`
D) Error

**Answer: B**

**Explanation:**
Tuple unpacking in for loops assigns each element of the tuple to separate variables. Each pair is unpacked into `num` and `letter`. The print statement outputs letter first, then num: `a 1` then `b 2`.

---

**Q4.22: Basic - [Iterating over Dictionary]**

What is the output?
```python
d = {'a': 1, 'b': 2}
for x in d:
    print(x, end=" ")
```

A) `a 1 b 2`
B) `a b`
C) `1 2`
D) `('a', 1) ('b', 2)`

**Answer: B**

**Explanation:**
Iterating over a dictionary iterates over its **keys** by default. To iterate over values: `for v in d.values()`. For key-value pairs: `for k, v in d.items()`. This is a common point of confusion for beginners.

---

**Q4.23: Intermediate - [Dictionary items()]**

What is the output?
```python
d = {'x': 10, 'y': 20}
for k, v in d.items():
    print(f"{k}={v}", end=" ")
```

A) `x 10 y 20`
B) `x=10 y=20`
C) `('x', 10) ('y', 20)`
D) Error

**Answer: B**

**Explanation:**
`d.items()` returns key-value pairs as tuples. Unpacking `k, v` separates them. F-string formatting produces `x=10` and `y=20`. As of Python 3.7+, dictionaries maintain insertion order.

---

**Q4.24: Intermediate - [Modifying List During Iteration]**

What is the problem with this code?
```python
lst = [1, 2, 3, 4]
for item in lst:
    if item % 2 == 0:
        lst.remove(item)
```

A) No problem
B) Modifying a list while iterating can skip elements
C) SyntaxError
D) lst.remove() doesn't exist

**Answer: B**

**Explanation:**
⚠️ **Gotcha**: Modifying a list during iteration causes unexpected behavior. When you remove item 2, indices shift — item 4 moves to index 2, but the iterator moves to index 2, which is now 4 (3 is skipped). Use list comprehension or iterate over a copy: `for item in lst[:]:`.

---

**Q4.25: Advanced - [Safe List Modification]**

Which is the safest way to remove items from a list while iterating?

A) `for i in range(len(lst)): if condition: del lst[i]`
B) `for item in lst: if condition: lst.remove(item)`
C) `lst = [item for item in lst if not condition]`
D) `while lst: if condition: lst.pop()`

**Answer: C**

**Explanation:**
💡 **Best practice**: Use list comprehension to create a new filtered list. It's clean, efficient, and avoids mutation issues. Alternatives: iterate backwards `for i in range(len(lst)-1, -1, -1)`, or iterate over a copy `lst[:]`. Never modify while iterating forward.

---

**Q4.26: Basic - [match-case Basics]**

🐍 What Python version introduced match-case statements?

A) Python 3.8
B) Python 3.9
C) Python 3.10
D) Python 3.11

**Answer: C**

**Explanation:**
Pattern matching with `match-case` (PEP 634-636) was introduced in Python 3.10. It provides structural pattern matching similar to switch statements but with powerful destructuring capabilities. It's more expressive than chained if-elif.

---

**Q4.27: Intermediate - [match-case Syntax]**

🐍 What is the output?
```python
status = 404
match status:
    case 200:
        print("OK")
    case 404:
        print("Not Found")
    case _:
        print("Unknown")
```

A) `OK`
B) `Not Found`
C) `Unknown`
D) Error: invalid syntax

**Answer: B**

**Explanation:**
`match-case` matches the value against patterns. `status` is 404, matching the second case. The `_` pattern is a wildcard (like default in switch). Unlike if-elif, match-case is designed for structural pattern matching, not just value comparison.

---

**Q4.28: Intermediate - [match-case Wildcard]**

🐍 What does `case _:` represent in match-case?

A) Match underscore character
B) Wildcard pattern (matches anything)
C) Private case
D) Error case

**Answer: B**

**Explanation:**
`_` in pattern matching is a wildcard that matches anything without binding a name. It's commonly used as the final case to handle all unmatched patterns (like `default` in switch statements). It MUST be last or it will match everything.

---

**Q4.29: Advanced - [match-case Destructuring]**

🐍 What is the output?
```python
point = (1, 2)
match point:
    case (0, 0):
        print("Origin")
    case (x, 0):
        print(f"On x-axis at {x}")
    case (0, y):
        print(f"On y-axis at {y}")
    case (x, y):
        print(f"Point at {x}, {y}")
```

A) `Origin`
B) `On x-axis at 1`
C) `On y-axis at 2`
D) `Point at 1, 2`

**Answer: D**

**Explanation:**
Pattern matching with destructuring extracts values. `(1, 2)` doesn't match (0,0), (x,0), or (0,y). It matches `(x, y)`, binding x=1 and y=2. This is structural pattern matching — matching shape AND binding values simultaneously.

---

**Q4.30: Advanced - [match-case with Guards]**

🐍 What is the output?
```python
num = 5
match num:
    case n if n < 0:
        print("Negative")
    case n if n == 0:
        print("Zero")
    case n if n > 0:
        print("Positive")
```

A) `Negative`
B) `Zero`
C) `Positive`
D) No output

**Answer: C**

**Explanation:**
Guards (`if condition`) add extra constraints to patterns. The pattern `n` matches anything and binds it to `n`, then the guard checks the condition. `5 > 0` is True, so "Positive" prints. Guards allow complex matching logic beyond simple value comparison.

---

**Q4.31: Advanced - [match-case Class Pattern]**

🐍 What type of pattern matches object attributes?
```python
case Point(x=0, y=y):
    print(f"On y-axis at {y}")
```

A) Literal pattern
B) Capture pattern
C) Class pattern
D) Mapping pattern

**Answer: C**

**Explanation:**
Class patterns match objects by type and their attributes. `Point(x=0, y=y)` matches Point instances where x attribute is 0, capturing y attribute. The class must define `__match_args__` or use keyword patterns. This enables sophisticated object decomposition.

---

**Q4.32: Advanced - [match-case OR Pattern]**

🐍 What is the output?
```python
status = 401
match status:
    case 200 | 201 | 204:
        print("Success")
    case 400 | 401 | 403 | 404:
        print("Client Error")
    case _:
        print("Other")
```

A) `Success`
B) `Client Error`
C) `Other`
D) Error: invalid |

**Answer: B**

**Explanation:**
The `|` operator in patterns means OR — matches if any sub-pattern matches. 401 matches the second case `400 | 401 | 403 | 404`. This is cleaner than multiple separate cases for similar handling. You cannot capture in OR patterns (no variable binding).

---

**Q4.33: Intermediate - [Loop Variable Scope]**

What is the output?
```python
for i in range(3):
    pass
print(i)
```

A) Error: i is not defined
B) `2`
C) `3`
D) `None`

**Answer: B**

**Explanation:**
⚠️ Unlike many languages, Python's loop variable persists after the loop ends with its final value. After `range(3)`, the last value of `i` is 2. This can be useful but also leads to bugs if you expect the variable to be undefined. Be careful with variable reuse.

---

**Q4.34: Intermediate - [Empty Loop]**

What happens with `for i in []:`?

A) Error: empty iterable
B) The loop body never executes
C) Infinite loop
D) i is set to None

**Answer: B**

**Explanation:**
Iterating over an empty iterable simply means zero iterations — the loop body never executes. No error is raised. The variable `i` won't be defined if it wasn't defined before (causes NameError if accessed after). This is normal behavior for empty sequences.

---

**Q4.35: Basic - [List Comprehension Control Flow]**

What is the output?
```python
result = [x for x in range(5) if x % 2 == 0]
print(result)
```

A) `[0, 1, 2, 3, 4]`
B) `[0, 2, 4]`
C) `[1, 3]`
D) `[2, 4]`

**Answer: B**

**Explanation:**
List comprehension with condition: `[expression for item in iterable if condition]`. Only items where the condition is True are included. 0, 2, 4 are even (% 2 == 0), so result is `[0, 2, 4]`. The `if` filters before the expression is evaluated.

---

**Q4.36: Intermediate - [Nested Comprehension]**

What is the output?
```python
result = [x*y for x in [1, 2] for y in [10, 20]]
print(result)
```

A) `[10, 20, 20, 40]`
B) `[10, 40]`
C) `[[10, 20], [20, 40]]`
D) `[10, 20]`

**Answer: A**

**Explanation:**
Multiple `for` clauses work like nested loops. First loop: x=1, then for each y: 1*10=10, 1*20=20. Second loop: x=2, then for each y: 2*10=20, 2*20=40. Result: `[10, 20, 20, 40]`. The outer loop is first, inner loop varies faster.

---

**Q4.37: Advanced - [Comprehension vs Generator]**

What is the difference between `[x for x in range(1000)]` and `(x for x in range(1000))`?

A) No difference
B) `[]` creates a list (memory for all), `()` creates a generator (lazy evaluation)
C) `()` is faster
D) `[]` can only hold integers

**Answer: B**

**Explanation:**
💡 Square brackets create a list (all values in memory). Parentheses create a generator expression (lazy — computes values on demand). For large sequences, generators are memory-efficient. Lists allow indexing; generators are one-pass iterators.

---

**Q4.38: Intermediate - [Ternary in Comprehension]**

What is the output?
```python
result = [x if x > 2 else 0 for x in range(5)]
print(result)
```

A) `[0, 0, 0, 3, 4]`
B) `[3, 4]`
C) `[0, 1, 2, 3, 4]`
D) `[False, False, False, True, True]`

**Answer: A**

**Explanation:**
The ternary `x if x > 2 else 0` is in the expression position, applied to EVERY item. For x=0,1,2: condition False, output 0. For x=3,4: condition True, output x. Result: `[0, 0, 0, 3, 4]`. Note: this is different from filtering (which uses `if` at the end).

---

**Q4.39: Intermediate - [Dictionary Comprehension]**

What is the output?
```python
result = {x: x**2 for x in range(3)}
print(result)
```

A) `[(0, 0), (1, 1), (2, 4)]`
B) `{0: 0, 1: 1, 2: 4}`
C) `{0, 1, 4}`
D) `[0, 1, 4]`

**Answer: B**

**Explanation:**
Dict comprehension: `{key_expr: value_expr for item in iterable}`. Creates key-value pairs. For x=0,1,2: pairs are 0:0, 1:1, 2:4. Result is a dictionary. Curly braces with colons = dict; curly braces without = set.

---

**Q4.40: Intermediate - [Set Comprehension]**

What is the output?
```python
result = {x % 3 for x in range(10)}
print(result)
```

A) `{0, 1, 2, 0, 1, 2, 0, 1, 2, 0}`
B) `{0, 1, 2}`
C) `[0, 1, 2, 0, 1, 2, 0, 1, 2, 0]`
D) `{0: 3, 1: 3, 2: 4}`

**Answer: B**

**Explanation:**
Set comprehension creates a set (unique values only). `% 3` gives remainders 0, 1, or 2 only. Sets eliminate duplicates, so regardless of how many 0s, 1s, 2s are generated, result is `{0, 1, 2}`. Order may vary in output.

---

**Q4.41: Basic - [while True pattern]**

What is the common pattern for a loop that runs until explicitly broken?

A) `while(True) { ... break; }`
B) `while True: ... break`
C) `do { ... } while False`
D) `loop: ... end`

**Answer: B**

**Explanation:**
`while True:` with `break` inside based on condition is idiomatic Python for "do-while" style or indefinite loops. Python doesn't have `do-while`. Check condition at any point in the loop body, then `break`. Ensure there's a `break` or the loop runs forever.

---

**Q4.42: Intermediate - [Sentinel Loop Pattern]**

What does this pattern do?
```python
while (line := input()) != "quit":
    print(line)
```

A) Infinite loop
B) Reads input until user types "quit"
C) Error: walrus in while
D) Prints "quit"

**Answer: B**

**Explanation:**
🐍 Walrus operator in while condition: assigns input to `line` AND checks if it's "quit" in one expression. Loop continues while input isn't "quit", printing each line. When user types "quit", condition is False, loop exits.

---

**Q4.43: Intermediate - [iter with sentinel]**

What does `iter(callable, sentinel)` do?

A) Creates an infinite iterator
B) Calls `callable` repeatedly until it returns `sentinel`, then stops
C) Iterates from 0 to sentinel
D) Throws error if sentinel found

**Answer: B**

**Explanation:**
The two-argument form of `iter(callable, sentinel)` creates an iterator that calls `callable()` with no arguments until it returns a value equal to `sentinel`, then stops. Useful for reading until a marker: `iter(lambda: f.read(1), '')` reads char-by-char until EOF.

---

**Q4.44: Advanced - [Loop Optimization]**

Why is `for i in range(n)` preferred over `while i < n: i += 1`?

A) It looks better
B) Range is implemented in C and avoids Python-level increment overhead
C) While loops can't iterate n times
D) There's no difference

**Answer: B**

**Explanation:**
💡 `range()` is a C-level iterator — incrementing happens in C without Python overhead. `while` with `i += 1` creates new integer objects each iteration (Python overhead). For large n, `range()` is significantly faster. Also, `range()` is clearer and less error-prone.

---

**Q4.45: Basic - [assert Statement]**

What happens when an assertion fails?

A) Program continues normally
B) AssertionError is raised
C) Warning is printed
D) Python automatically fixes the error

**Answer: B**

**Explanation:**
`assert condition, message` raises AssertionError if condition is False. Used for debugging and invariant checking. Assertions can be disabled with `-O` flag (optimization mode), so don't use them for runtime validation that must always run. Use for development-time checks.

---

**Q4.46: Intermediate - [try-except in loops]**

What is the output?
```python
for i in range(5):
    try:
        if i == 2:
            raise ValueError("error")
    except ValueError:
        continue
    print(i, end=" ")
```

A) `0 1 2 3 4`
B) `0 1 3 4`
C) `0 1`
D) Error

**Answer: B**

**Explanation:**
When i=2, ValueError is raised, caught, and `continue` skips the print. Other values print normally. The exception handling doesn't break the loop — we explicitly `continue`. Result: `0 1 3 4`. This pattern allows skipping problematic items.

---

**Q4.47: Advanced - [Walrus in Comprehensions]**

🐍 What is the output?
```python
results = [y for x in range(5) if (y := x**2) > 5]
print(results)
```

A) `[9, 16]`
B) `[3, 4]`
C) `[6, 7, 8, 9]`
D) Error

**Answer: A**

**Explanation:**
Walrus operator in comprehension: assigns `x**2` to `y`, then filters where `y > 5`. For x=0,1,2: y=0,1,4 (≤5, filtered out). For x=3,4: y=9,16 (>5, included). The expression outputs `y`, not `x`. Result: `[9, 16]`.

---

**Q4.48: Expert - [Bytecode and Loops]**

What bytecode instruction implements the Python for loop?

A) LOOP
B) FOR_LOOP
C) FOR_ITER
D) ITERATE

**Answer: C**

**Explanation:**
`FOR_ITER` is the bytecode instruction that advances the iterator and handles StopIteration. When the iterator is exhausted, `FOR_ITER` jumps to the instruction after the loop (handling the else clause if present). You can see this with `dis.dis()`.

---

**Q4.49: Intermediate - [Named Loops Alternative]**

Since Python doesn't have labeled break/continue, what's a clean alternative for exiting nested loops?

A) `goto`
B) Extract to a function and use `return`
C) `exit all`
D) `break(2)`

**Answer: B**

**Explanation:**
💡 Extract the nested loops into a function. When you need to break out of all loops, use `return`. This is cleaner than flag variables and makes the code more modular. You can return values too: `return result` when found, `return None` otherwise.

---

**Q4.50: Intermediate - [any() and all()]**

What is the output?
```python
nums = [2, 4, 6, 8]
print(all(x % 2 == 0 for x in nums))
print(any(x > 10 for x in nums))
```

A) `True, True`
B) `False, True`
C) `True, False`
D) `False, False`

**Answer: C**

**Explanation:**
`all()` returns True if all elements are truthy (all even → True). `any()` returns True if any element is truthy (none > 10 → False). These functions short-circuit: `all()` stops at first False, `any()` stops at first True. Cleaner than explicit loops for such checks.

---

**Q4.51: Intermediate - [Loop with else - Search Pattern]**

What is the purpose of `for-else` in this pattern?
```python
for item in items:
    if item == target:
        print("Found")
        break
else:
    print("Not found")
```

A) Else always runs after for
B) Else runs only if break was never hit (item not found)
C) Else runs if item equals target
D) Else handles exceptions

**Answer: B**

**Explanation:**
💡 **Search pattern**: The `else` clause runs only if the loop completes without `break`. This is perfect for "search" scenarios: if found, `break` (else skipped). If not found, loop exhausts naturally, `else` runs. It's more elegant than using a flag variable.

---

**Q4.52: Advanced - [itertools.takewhile]**

What does `itertools.takewhile(pred, iterable)` do?

A) Takes elements forever
B) Yields elements while predicate is True, stops at first False
C) Filters elements where predicate is True throughout
D) Always takes exactly one element

**Answer: B**

**Explanation:**
`takewhile` yields elements from iterable AS LONG AS predicate returns True. First False stops iteration completely. Different from `filter` which checks each element independently. `takewhile(lambda x: x<5, [1,2,6,3,4])` yields 1, 2 (stops at 6, doesn't yield 3,4).

---

**Q4.53: Advanced - [itertools.dropwhile]**

What does `itertools.dropwhile(pred, iterable)` do?

A) Drops all elements
B) Skips elements while predicate is True, yields rest
C) Removes elements where predicate is True throughout
D) Drops the first element only

**Answer: B**

**Explanation:**
`dropwhile` is opposite of `takewhile`. It skips elements while predicate is True, then yields ALL remaining elements once predicate becomes False. `dropwhile(lambda x: x<5, [1,2,6,3,4])` skips 1,2, yields 6,3,4 (including 3,4 even though they're <5).

---

**Q4.54: Basic - [range vs list(range)]**

What is the difference between `range(5)` and `list(range(5))`?

A) No difference
B) `range(5)` is a lazy range object; `list(range(5))` is an actual list
C) `list(range(5))` is faster
D) `range(5)` can't be used in for loops

**Answer: B**

**Explanation:**
`range()` returns a range object — a lazy sequence that computes values on demand. It doesn't store all values in memory. `list(range())` forces evaluation into an actual list. For large ranges, the range object is much more memory-efficient. Both work in for loops.

---

**Q4.55: Expert - [Loop Unrolling and Optimization]**

Why might `for i in range(1000000): pass` be surprisingly fast?

A) Python is always fast
B) The bytecode interpreter optimizes empty loops
C) pass is a special no-op that's optimized away
D) Python pre-computes the result

**Answer: B**

**Explanation:**
Modern Python has optimizations in the bytecode interpreter. The `FOR_ITER` instruction is highly optimized C code. Empty loops still iterate but with minimal Python-level overhead per iteration. Full optimization/elimination requires JIT (like PyPy), but CPython's interpreter is still reasonably efficient.

---

## Chapter Summary

**Total MCQs: 55**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 17 | 31% |
| Intermediate | 27 | 49% |
| Advanced | 9 | 16% |
| Expert | 2 | 4% |

**Key Topics Covered:**
- if-elif-else statements
- for and while loops
- break, continue, pass
- Loop else clauses
- enumerate, zip, range
- match-case pattern matching (Python 3.10+)
- List/dict/set comprehensions
- Control flow in comprehensions
- Loop optimization techniques
- any() and all() functions
