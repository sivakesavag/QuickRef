# Chapter 4: Control Flow

**Target MCQs**: 50-60
**Current Batch**: 1-25
**Topics Covered**: Conditionals, Loops (for, while), Control Transfer, Loop-Else, Match-Case (Intro)

---

**Q4.1: Basic - [If-Elif-Else]**

What is the output of the following code?
```python
x = 10
if x > 20:
    print("A")
elif x > 5:
    print("B")
elif x > 8:
    print("C")
else:
    print("D")
```

A) B
B) B then C
C) C
D) A

**Answer: A**

**Explanation:**
Python evaluates `if-elif` branches sequentially. Once a condition is met (`x > 5` is True), that block executes, and the rest of the chain is skipped. Even though `x > 8` is also true, the `elif` ensures mutual exclusion.

---

**Q4.2: Intermediate - [Loop Else]**

When does the `else` block attached to a `for` loop execute?

A) Only if the loop encounters a `break` statement.
B) Only if the loop completes normally without encountering a `break` statement.
C) Always, after the loop finishes.
D) Never; `else` cannot be used with `for`.

**Answer: B**

**Explanation:**
The `else` clause in a loop is unique to Python. It executes only if the loop exhausts the iterable (finishes naturally). If the loop is terminated by a `break` statement, the `else` block is skipped.

---

**Q4.3: Basic - [While Loop]**

What is the risk of the following code?
```python
while True:
    pass
```

A) Syntax Error.
B) RecursionError.
C) Infinite Loop (High CPU usage).
D) It exits immediately.

**Answer: C**

**Explanation:**
`while True` creates an infinite loop. `pass` does nothing but consumes a CPU cycle. Without a `break` or external termination (signal), this runs forever, potentially freezing the program or consuming 100% of a CPU core.

---

**Q4.4: Advanced - [Ternary Precedence]**

What is the result of:
`"Yes" if 0 else "No" if 1 else "Maybe"`

A) "Yes"
B) "No"
C) "Maybe"
D) Syntax Error

**Answer: B**

**Explanation:**
This is a chained ternary operator. It parses as `"Yes" if 0 else ("No" if 1 else "Maybe")`.
1. Condition `0` is False.
2. Evaluate else part: `"No" if 1 else "Maybe"`.
3. Condition `1` is True. Result is "No".

---

**Q4.5: Intermediate - [Range]**

Which of the following generates the sequence `10, 8, 6`?

A) `range(10, 5)`
B) `range(10, 5, -2)`
C) `range(10, 6, -2)`
D) `range(6, 10, 2)`

**Answer: B**

**Explanation:**
`range(start, stop, step)`.
Start at 10. Step -2 means sequence is 10, 8, 6.
Next is 4, which is not > 5 (stop), so it stops.
Option C stops *before* 6 (exclusive), so it would generate `10, 8`.

---

**Q4.6: Basic - [Break vs Continue]**

What does the `continue` statement do?

A) Exits the loop immediately.
B) Skips the rest of the current iteration and jumps to the next iteration.
C) Restarts the loop from the beginning (index 0).
D) Does nothing (placeholder).

**Answer: B**

**Explanation:**
`continue` stops the execution of statements in the current iteration of the loop and checks the loop condition/fetches the next item to start the next iteration. `break` exits the loop entirely.

---

**Q4.7: Advanced - [Match Case]**

Introduced in Python 3.10, which pattern matches a sequence starting with "HEAD" in a `match` statement?

A) `case ["HEAD", *rest]:`
B) `case "HEAD" + rest:`
C) `case ("HEAD", ...):`
D) `case start="HEAD":`

**Answer: A**

**Explanation:**
Python's Structural Pattern Matching allows sequence unpacking. `["HEAD", *rest]` matches any list/tuple where the first element is "HEAD" and binds the remaining elements to the variable `rest`.

---

**Q4.8: Intermediate - [Enumerate]**

What is the output type of elements when iterating `for x in enumerate(['a', 'b']):`?

A) list
B) tuple
C) dict
D) Index (int)

**Answer: B**

**Explanation:**
`enumerate()` yields tuples containing a count (from start which defaults to 0) and the values obtained from iterating over the sequence. E.g., `(0, 'a'), (1, 'b')`.

---

**Q4.9: Expert - [For Loop Variable Scope]**

What is the value of `i` after this code runs?
```python
i = 100
for i in range(5):
    pass
print(i)
```

A) 100
B) 5
C) 4
D) `NameError` (i is local to loop)

**Answer: C**

**Explanation:**
In Python (unlike some languages with block scope like C++ or Java), loop variables leak into the enclosing function scope. `i` takes values 0, 1, 2, 3, 4. After the loop finishes, `i` retains the last value, which is 4.

---

**Q4.10: Basic - [Pass]**

When is the `pass` statement commonly used?

A) To terminate a loop.
B) To skip an iteration.
C) As a syntactic placeholder for empty bodies (classes, functions, loops).
D) To pass arguments to a function.

**Answer: C**

**Explanation:**
`pass` is a null operation. It is required syntactically in Python because empty blocks are not allowed (e.g., `def func():` must have a body).

---

**Q4.11: Advanced - [Modifying list in loop]**

What happens if you iterate over a list while removing items from it?
```python
nums = [1, 2, 3, 4]
for n in nums:
    if n % 2 == 0:
        nums.remove(n)
```

A) It correctly removes all even numbers.
B) Variable results/skips elements due to index shifting.
C) Raises `RuntimeError`.
D) Infinite Loop.

**Answer: B**

**Explanation:**
Modifying a list while iterating over it is dangerous.
1. `n=1` (index 0). Keep.
2. `n=2` (index 1). Remove 2. List becomes `[1, 3, 4]`.
3. Loop increments index to 2. Item at index 2 in `[1, 3, 4]` is 4.
**Skipped 3!** 4 is even, removed.
Best practice: Iterate over a copy (`nums[:]`) or create a new list.

---

**Q4.12: Intermediate - [Zip]**

What determines the length of the result of `zip(list1, list2)`?

A) The length of `list1`.
B) The length of the shorter list.
C) The length of the longer list.
D) Error if lengths differ.

**Answer: B**

**Explanation:**
`zip()` stops when the shortest input iterable is exhausted. Integers from longer lists are ignored. (Use `itertools.zip_longest` to pad instead).

---

**Q4.13: Advanced - [Loop Unpacking]**

Is this valid Python code?
`for key, val in {"a": 1, "b": 2}.items():`

A) Yes, assuming dictionary order.
B) No, `.items()` returns a special object, not tuples.
C) Yes, it unpacks the (key, value) tuples yielded by items().
D) No, unpacking requires parentheses.

**Answer: C**

**Explanation:**
`dict.items()` returns a view that yields `(key, value)` tuples. The for-loop unpacking syntax `for k, v in ...` correctly handles these tuples.

---

**Q4.14: Basic - [Conditions]**

Which value evaluates to False in an `if` condition?

A) `-1`
B) `[0]`
C) `""` (empty string)
D) `"False"`

**Answer: C**

**Explanation:**
Empty sequences (strings, lists, tuples) and zero are Falsy. Non-empty sequences are Truthy.

---

**Q4.15: Expert - [While Else Break]**

```python
i = 0
while i < 3:
    if i == 1:
        break
    i += 1
else:
    print("Done")
```
What is printed?

A) "Done"
B) Nothing
C) "Done" twice
D) Error

**Answer: B**

**Explanation:**
The loop is terminated by `break` (when `i` is 1). Therefore, the `else` block (which runs only on natural exhaustion) is **skipped**. Nothing is printed.

---

**Q4.16: Intermediate - [Iterator vs Iterable]**

Which statement is true?

A) Every iterable is an iterator.
B) Every iterator is an iterable.
C) Lists are iterators.
D) `for` loops only work on iterators, not iterables.

**Answer: B**

**Explanation:**
- An **iterable** has `__iter__` returning an iterator (e.g., list, str).
- An **iterator** has `__iter__` (returning self) and `__next__`.
- Thus, all iterators are iterable, but lists (iterables) are not iterators (they don't have `__next__`).

---

**Q4.17: Basic - [Nested Loops]**

How many times does "X" print?
```python
for i in range(3):
    for j in range(2):
        print("X")
```

A) 5
B) 6
C) 9
D) 2

**Answer: B**

**Explanation:**
Outer loop runs 3 times. Inner loop runs 2 times per outer iteration. Total: $3 \times 2 = 6$.

---

**Q4.18: Advanced - [Wildcard Match]**

In a `match` statement, what does `case _:` signify?

A) Determine the type automatically.
B) Matches `None` only.
C) Wildcard match (default case), matches anything.
D) Syntax Error.

**Answer: C**

**Explanation:**
`_` is the wildcard pattern. It matches anything and is typically used as the fallback (like `default` in switch-case) at the end of a `match` block.

---

**Q4.19: Intermediate - [Range Memory]**

Does `range(1000000)` create a list of a million integers in memory in Python 3?

A) Yes, it's memory intensive.
B) No, it returns a range object (lazy sequence).
C) Yes, but it uses compression.
D) Depends on the OS.

**Answer: B**

**Explanation:**
In Python 3, `range()` returns an immutable sequence type (range object) that generates numbers on demand. It consumes small, fixed amount of memory regardless of size. (In Python 2, `range()` created a list, `xrange()` was lazy).

---

**Q4.20: Advanced - [Named Loop Break]**

How do you break out of nested loops (both inner and outer) in Python?

A) `break 2`
B) `break all`
C) Python doesn't support labeled breaks; use a flag variable, exception, or return (if in function).
D) `goto end`

**Answer: C**

**Explanation:**
Python (unlike PHP or Java) does not support labeled breaks (e.g., `break loop1`). Standard patterns use a flag variable, wrapping loops in a function and using `return`, or raising a custom exception.

---

**Q4.21: Expert - [Bytecode Jump]**

Which bytecode instruction is primarily responsible for `if` statements jumping over code?

A) `CMP_OP`
B) `POP_JUMP_IF_FALSE` (or similar variants in newer Python)
C) `LOAD_CONST`
D) `RETURN_VALUE`

**Answer: B**

**Explanation:**
`POP_JUMP_IF_FALSE` checks the condition (top of stack). If false, it updates the instruction pointer to jump to the `else` block or next statement, effectively skipping the `if` body.

---

**Q4.22: Intermediate - [Conditional Assignment]**

Is `x = 5 if True` valid syntax?

A) Yes, `x` becomes 5.
B) No, missing `else`.
C) Yes, `x` becomes `True`.
D) No, `if` cannot be used in assignment.

**Answer: B**

**Explanation:**
The ternary operator strictly requires an `else` clause. `Value if Condition else Value`. Without `else`, it is a SyntaxError.

---

**Q4.23: Basic - [Multiple Conditions]**

What is the result of `if 5 > 10 and 2 < 4:`?

A) The block executes.
B) The block is skipped.
C) Error.
D) Partial execution.

**Answer: B**

**Explanation:**
`5 > 10` is False. `False and ...` is False. The condition fails, so the block is skipped.

---

**Q4.24: Advanced - [Try Finally Loop]**

If a `break` occurs inside a `try` block within a loop, does the `finally` block execute?

A) No, break exits immediately.
B) Yes, `finally` always runs before leaving the try/except construct.
C) Only if there was an exception.
D) Depends on the loop type.

**Answer: B**

**Explanation:**
`finally` is guaranteed to run. If `break` (or `return`) is encountered, current flow is suspended, `finally` block executes, and then the control flow action (`break`) continues.

---

**Q4.25: Intermediate - [Dict Iteration]**

Iterating over a dictionary `for x in my_dict:` yields:

A) Keys
B) Values
C) (Key, Value) tuples
D) Items

**Answer: A**

**Explanation:**
Default iteration over a dictionary yields its keys. Use `.values()` or `.items()` for others.

---

**Q4.26: Basic - [While Else]**

Will the `else` block run here?
```python
x = 5
while x > 0:
    x -= 1
else:
    print("Done")
```

A) Yes
B) No
C) Error
D) Only if x > 0 initially

**Answer: A**

**Explanation:**
Loop finishes naturally when `x > 0` becomes False. No `break` was encountered. `else` runs.

---

**Q4.27: Advanced - [Match Case Class]**

How do you match an object by class pattern?
`case Point(x=1, y=var):`

A) Checks if object is instance of Point, x is 1, and captures y into var.
B) Checks if object is named "Point".
C) Creates a new Point object.
D) Error, case only matches primitives.

**Answer: A**

**Explanation:**
Class patterns check `isinstance()` and attributes. `Point(x=1, y=var)` matches if the subject is an instance of `Point`, attribute `x` equals 1, and binds attribute `y` to variable `var`.

---

**Q4.28: Intermediate - [Break Nesting]**

In a nested loop, `break` terminates:

A) The innermost loop only.
B) The outermost loop.
C) Both loops.
D) The function.

**Answer: A**

**Explanation:**
`break` applies effectively to the nearest enclosing loop scope.

---

**Q4.29: Expert - [Compiling Control Flow]**

What is the bytecode instruction `SETUP_LOOP` (in older Python) or its replacement handling loop blocks pushed to the block stack?

A) It initializes the loop iterator.
B) It sets up a block so `break` and `continue` know where to jump.
C) It checks the condition.
D) It optimizes the loop.

**Answer: B**

**Explanation:**
`SETUP_LOOP` (removed in 3.8+, logic moved/changed, but historically relevant) pushes a block to the block stack so that `break` statements know which block to pop and where to jump (end of loop).

---

**Q4.30: Advanced - [Match OR]**

How do you match multiple alternatives in a single case?

A) `case 401 | 403 | 404:`
B) `case 401 or 403 or 404:`
C) `case 401, 403, 404:`
D) `case [401, 403, 404]:`

**Answer: A**

**Explanation:**
The `|` pipe operator represents "OR" in patterns. `case 401 | 403:` matches 401 OR 403.

---

**Q4.31: Intermediate - [Reversed]**

What is the most memory-efficient way to iterate a large range in reverse in Python 3?

A) `range(100)[::-1]`
B) `reversed(range(100))` or `range(99, -1, -1)`
C) `list(range(100)).reverse()`
D) `sorted(range(100), reverse=True)`

**Answer: B**

**Explanation:**
`range` objects support `reversed()` efficiently (returning a range_iterator) without creating a full list. `range(start, stop, -1)` works natively too. `[::-1]` on a range creates a new range object (efficient). Options C and D create full lists in memory.

---

**Q4.32: Basic - [Step Slice]**

What does `range(1, 10, 3)` produce?

A) 1, 4, 7
B) 1, 4, 7, 10
C) 1, 2, 3
D) 3, 6, 9

**Answer: A**

**Explanation:**
Start 1. Add 3 -> 4. Add 3 -> 7. Add 3 -> 10.
Stop is 10 (exclusive). So 10 is not included. Result: 1, 4, 7.

---

**Q4.33: Advanced - [Iter Next]**

When a `for` loop iterates over an object, what exception specifically signals "End of Loop"?

A) `LoopError`
B) `IndexError`
C) `StopIteration`
D) `EOFError`

**Answer: C**

**Explanation:**
The underlying `__next__()` call raises `StopIteration` when there are no more items. The `for` loop internals catch this exception and terminate the loop cleanly.

---

**Q4.34: Expert - [Computed Goto]**

Does Python support computed gotos (jumping to a dynamic line number)?

A) Yes, via `goto` module.
B) No, unrelated to control flow structure.
C) Only in CPython via `ctypes`.
D) Yes, using `case` statement.

**Answer: B**

**Explanation:**
Python is a structured language and does not support arbitrary `goto` or computed jumps to line numbers natively. Control flow is handled strictly via loops, branches, functions, and exceptions.

---

**Q4.35: Intermediate - [Enumerate Start]**

How do you finish `enumerate` to start counting from 1 instead of 0?

A) `enumerate(seq, start=1)`
B) `enumerate(seq, 1)`
C) `enumerate(seq, index=1)`
D) Both A and B

**Answer: D**

**Explanation:**
`enumerate` accepts a second positional argument `start`.

---

**Q4.36: Advanced - [Guard Clause]**

In a match statement, what is the role of `if`?
`case [x] if x > 0:`

A) Syntax Error.
B) A **guard**; the pattern matches only if the boolean expression is true.
C) Initializes x if x > 0.
D) Defaults x to 0.

**Answer: B**

**Explanation:**
This is a Pattern Guard. The case matches only if the structural pattern (`[x]`) matches AND the guard condition (`x > 0`) evaluates to True.

---

**Q4.37: Basic - [Empty Range]**

What does `range(5, 0)` produce?

A) 5, 4, 3, 2, 1
B) 0, 1, 2, 3, 4
C) Empty sequence
D) Error

**Answer: C**

**Explanation:**
Default step is +1. Start (5) is already >= Stop (0), so the range is empty. You need a negative step `range(5, 0, -1)` to go down.

---

**Q4.38: Intermediate - [Multiple Assignment Loop]**

`for x, y in [(1, 2), (3, 4)]:`

A) `x` gets (1, 2), `y` gets (3, 4).
B) `x` gets 1 then 3; `y` gets 2 then 4.
C) Error.
D) `x` gets index, `y` gets tuple.

**Answer: B**

**Explanation:**
Loop unpacking. In first iteration, `(1, 2)` is unpacked into `x=1`, `y=2`. In second, `x=3`, `y=4`.

---

**Q4.39: Advanced - [Set Comprehension vs Loop]**

Which is usually faster to create a set from a list?
1. `s = set(); for x in lst: s.add(x)`
2. `s = {x for x in lst}`

A) 1
B) 2
C) Same
D) 1 is faster because it's explicit.

**Answer: B**

**Explanation:**
Comprehensions are generally faster than explicit loops because the loop overhead is handled in C speed within the interpreter loop, avoiding byte-code interpretation overhead for each `.add()` method lookup and call.

---

**Q4.40: Expert - [Else block Scope]**

If variables are defined strictly inside the `else` block of a loop, are they visible after?
```python
for x in []:
    pass
else:
    y = 5
print(y)
```

A) Yes, `y` is 5.
B) No, `NameError`.
C) Only if loop ran at least once.
D) Yes, but only in Python 2.

**Answer: A**

**Explanation:**
The `else` block executed (empty loop is "exhausted" immediately). `y` is assigned 5. Python blocks (except functions/classes) do not create new scopes. `y` leaks to the surrounding scope.

---

**Q4.41: Intermediate - [Sentinel Loop]**

What is the 'iter-call' form `iter(callable, sentinel)` used for?

A) Creating infinite loops.
B) Repeatedly calling `callable()` until it returns `sentinel`.
C) Filtering a list.
D) Error handling.

**Answer: B**

**Explanation:**
`iter(func, STOP)` repeatedly calls `func()` and yields the result. It stops when the result equals `STOP`. useful for reading files chunk by chunk: `for chunk in iter(lambda: f.read(4096), ''):`.

---

**Q4.42: Basic - [If Not]**

`if not []` evaluates to:

A) True (enters block).
B) False (skips block).

**Answer: A**

**Explanation:**
`[]` is Falsy. `not False` is True.

---

**Q4.43: Advanced - [While Assignment]**

Why can't you write `while x = next(it):` in standard Python (pre-3.8)?

A) Assignment is a statement, not an expression.
B) It's valid syntax.
C) Logic error.
D) `next` is not a keyword.

**Answer: A**

**Explanation:**
Before the walrus operator (`:=`), assignment `x = ...` was a statement and couldn't be used in a condition expression. `while (x := next(it, None)) is not None:` is the modern way.

---

**Q4.44: Intermediate - [Match Capture]**

`case [x, y] as point:` matches a list of two items. What is `point`?

A) The first item `x`.
B) The entire list `[x, y]`.
C) A string "point".
D) Syntax Error.

**Answer: B**

**Explanation:**
`as name` captures the entire matched pattern subject into the variable `name`.

---

**Q4.45: Expert - [Async For]**

`async for` is used to iterate over:

A) Generators.
B) Asynchronous iterators (`__aiter__`, `__anext__`).
C) Threads.
D) Futures.

**Answer: B**

**Explanation:**
`async for` waits for `await iterator.__anext__()` in each iteration. It requires an object implementing the Asynchronous Iterator protocol.

---

**Q4.46: Basic - [Try Except Else]**

When does the `else` block in a `try...except...else` structure run?

A) If an exception occurs.
B) If NO exception occurs in the try block.
C) Always.
D) Only if `finally` is missing.

**Answer: B**

**Explanation:**
`else` runs if the `try` block completes successfully without raising exceptions. It's useful for code that should run only on success but shouldn't be protected by the exception handler.

---

**Q4.47: Advanced - [Context Manager Loop]**

If you use `with open(...)` inside a loop, when is the file closed?

A) At the end of the script.
B) At the end of each iteration loop block.
C) Only when garbage collected.
D) Never.

**Answer: B**

**Explanation:**
The `with` statement ensures `__exit__` is called (closing the file) as soon as execution leaves the `with` block scope, which happens at the end of each iteration.

---

**Q4.48: Intermediate - [Infinite Loop construct]**

Which is preferred for an infinite loop?

A) `while 1:`
B) `while True:`
C) `for i in iter(int, 1):`
D) `loop:`

**Answer: B**

**Explanation:**
`while True:` is the idiomatic, readable standard. (Python optimization treats `while 1` and `while True` identically now, but `True` is clearer).

---

**Q4.49: Expert - [Dispatcher Pattern]**

Before `match` (3.10), what was the common idiom to replace massive `if-elif` chains for value dispatch?

A) Dictionary mapping keys to functions/callables.
B) Nested classes.
C) `eval()`.
D) Exceptions.

**Answer: A**

**Explanation:**
`dispatch = {'cmd1': func1, 'cmd2': func2}`. Then `dispatch.get(cmd, default_func)()`.

---

**Q4.50: Intermediate - [Continue Finally]**

If `continue` is executed in a try block with a `finally` clause:

A) `finally` is skipped.
B) `finally` executes before the next iteration starts.
C) `continue` is ignored.
D) Error.

**Answer: B**

**Explanation:**
Before jumping to the next iteration, Python executes the `finally` block to ensure cleanup mechanisms (like releasing locks) are respected.

---

---

## Review Notes (2026-02-06)

- Q4.42 uses only A/B options, which is inconsistent with the predominant 4-option MCQ format.
