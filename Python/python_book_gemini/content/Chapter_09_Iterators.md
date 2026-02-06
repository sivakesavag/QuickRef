# Chapter 9: Iterators & Generators

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: Iterator Protocol (`__iter__`, `__next__`), Generator Functions (`yield`), Generator Expressions, built-in iteration tools.

---

**Q9.1: Basic - [Iterable Definition]**

An object is "iterable" if it implements which method?

A) `__next__`
B) `__iter__`
C) `__loop__`
D) `__generate__`

**Answer: B**

**Explanation:**
To be iterable (usable in a `for` loop), an object must implement `__iter__`, which returns an iterator.

---

**Q9.2: Intermediate - [Iterator Protocol]**

What happens when an iterator runs out of items?

A) It returns `None`.
B) It raises `IndexError`.
C) It raises `StopIteration`.
D) It resets to the beginning.

**Answer: C**

**Explanation:**
The iterator protocol specifies that `next()` raises `StopIteration` to signal that there are no further items.

---

**Q9.3: Advanced - [Generator Return]**

If a generator function uses `return "Done"`, what happens when it is consumed?

A) It yields "Done" as the last value.
B) It raises `StopIteration` with "Done" as the value attribute.
C) It raises `SyntaxError`.
D) The return value Is ignored silenty.

**Answer: B**

**Explanation:**
In a generator, `return value` is equivalent to raising `StopIteration(value)`. The value is essentially the return value of the generator-iterator's execution (often used in `yield from`), but it is not yielded in a `for` loop.

---

**Q9.4: Basic - [Yield Keyword]**

What characterizes a generator function?

A) It uses `return`.
B) It uses `yield`.
C) It is defined with `def*`.
D) It inherits from `Generator`.

**Answer: B**

**Explanation:**
Using the `yield` keyword in a function definition makes it a generator function, which returns a generator object when called.

---

**Q9.5: Intermediate - [Generator Expression]**

Which syntax creates a generator expression?

A) `[x for x in data]`
B) `{x for x in data}`
C) `(x for x in data)`
D) `<x for x in data>`

**Answer: C**

**Explanation:**
Parentheses `(...)` around a comprehension syntax create a generator expression, not a tuple (tuple comprehension doesn't exist directly like that).

---

**Q9.6: Advanced - [Yield From]**

`yield from subgen()` is equivalent to:

A) `yield subgen()`
B) `for x in subgen(): yield x` (plus bidirectional communication handling).
C) `return subgen()`
D) `yield list(subgen())`

**Answer: B**

**Explanation:**
`yield from` delegates part of the generator's operations to another generator (sub-generator). It yields values from the sub-generator transparently and also handles sending values/exceptions *into* the sub-generator.

---

**Q9.7: Basic - [Next Function]**

How do you manually retrieve the next item from an iterator `it`?

A) `it.next()`
B) `next(it)`
C) `it.get()`
D) `it.__step__`

**Answer: B**

**Explanation:**
The built-in function `next(iterator)` calls the iterator's `__next__()` method.

---

**Q9.8: Intermediate - [Iter Function]**

`iter(callable, sentinel)` creates an iterator that:

A) Calls `callable(sentinel)` once.
B) Calls `callable()` until it returns `sentinel`.
C) Iterates over `callable` methods.
D) Errors if sentinel is passed.

**Answer: B**

**Explanation:**
The two-argument form of `iter()` repeatedly calls the first argument (must be callable) until the return value equals the second argument (sentinel), at which point `StopIteration` is raised.

---

**Q9.9: Advanced - [Generator State]**

Can you restart a generator once it is exhausted?

A) Yes, call `next()` again.
B) Yes, call `iter()` on it again.
C) No, you must create a new generator object by calling the function again.
D) Yes, use `gen.reset()`.

**Answer: C**

**Explanation:**
Generators are one-time-use iterators. Once exhausted (raised `StopIteration`), they cannot be reset. You must create a fresh instance.

---

**Q9.10: Expert - [Send Method]**

`val = yield x`. What does `val` receive?

A) `x`.
B) The value sent via `gen.send(value)`.
C) `None` by default.
D) Both B and C.

**Answer: D**

**Explanation:**
The result of the `yield` expression is the value passed to `.send()`. If `next()` is called (which is `send(None)`), it returns `None`.

---

**Q9.11: Basic - [Range Type]**

Is `range(10)` an iterator?

A) Yes.
B) No, it is an iterable (sequence).
C) No, it is a list.
D) Yes, it yields values.

**Answer: B**

**Explanation:**
`range` object is an immutable sequence (iterable). It is *not* an iterator itself (you can call `iter(range_obj)` to get an iterator). This allows multiple passes over the same range object.

---

**Q9.12: Intermediate - [File Iteration]**

Iterating over a file object (`for line in f:`) reads:

A) The whole file into memory.
B) One character at a time.
C) One line at a time (lazy loading).
D) One block at a time.

**Answer: C**

**Explanation:**
File objects in Python are iterators that yield lines one by one, allowing efficient processing of huge files without loading everything into RAM.

---

**Q9.13: Advanced - [Itertools Chain]**

`itertools.chain([1, 2], [3, 4])` produces:

A) `[[1, 2], [3, 4]]`
B) `1, 2, 3, 4` (sequence).
C) A list `[1, 2, 3, 4]`.
D) An error.

**Answer: B**

**Explanation:**
`chain` creates an iterator that returns elements from the first iterable until it is exhausted, then proceeds to the next, treating them as a single consecutive sequence.

---

**Q9.14: Basic - [Zip Stop]**

`zip([1, 2], [3, 4, 5])` stops after:

A) 2 items (shortest input).
B) 3 items (longest input, filling with None).
C) 3 items (error on missing).
D) 5 items.

**Answer: A**

**Explanation:**
Standard `zip` stops when the shortest input iterable is exhausted. (Use `itertools.zip_longest` for behavior B).

---

**Q9.15: Intermediate - [Enumerate Start]**

To start counting from 1 in `enumerate(['a', 'b'])`:

A) `enumerate(['a', 'b']) + 1`
B) `enumerate(['a', 'b'], start=1)`
C) `enumerate(['a', 'b'], 1)`
D) Both B and C.

**Answer: D**

**Explanation:**
`enumerate` accepts an optional second argument (or keyword `start`) to define the starting index.

---

**Q9.16: Advanced - [Tee]**

`itertools.tee(iterator, n=2)` provides:

A) The first 2 items of iterator.
B) n independent iterators from a single iterable.
C) Splits the iterator into chunks of size 2.
D) Threads the iterator.

**Answer: B**

**Explanation:**
`tee` returns *n* independent iterators (by caching/buffering values) from a single iterable, allowing you to iterate over the stream multiple times (e.g. current and next comparison).

---

**Q9.17: Expert - [Throw Method]**

`gen.throw(TypeError)` allows you to:

A) Raise an exception inside the generator at the point where it is suspended (yield).
B) Throw away the generator.
C) Cause a TypeError in the caller.
D) Skip the next value.

**Answer: A**

**Explanation:**
`throw` raises the passed exception at the current suspension point inside the generator function, allowing the generator to catch it (`try...except`) and handle it or cleanup.

---

**Q9.18: Intermediate - [Iterator Identity]**

The `__iter__` method of an *iterator* (as opposed to an iterable) typically returns:

A) A new iterator.
B) `self`.
C) `None`.
D) A copy.

**Answer: B**

**Explanation:**
Iterators are also iterables. Their `__iter__` method returns `self` so they can be used in `for` loops directly.

---

**Q9.19: Basic - [Any Short Circuit]**

`any(gen())` stops consuming the generator:

A) Immediately.
B) As soon as it encounters a Truthy value.
C) When the generator finishes.
D) Never.

**Answer: B**

**Explanation:**
`any` short-circuits. It returns True immediately upon finding the first Truthy element, leaving the rest of the iterator unconsumed (if it hasn't finished).

---

**Q9.20: Advanced - [Cycle]**

`itertools.cycle([1, 2])` creates:

A) `[1, 2, 1, 2]`
B) An infinite iterator `1, 2, 1, 2, ...`
C) A circular linked list.
D) Error.

**Answer: B**

**Explanation:**
`cycle` saves a copy of the elements and repeats them indefinitely.

---

**Q9.21: Intermediate - [Zip Unpack]**

If `z = zip(list1, list2)`, how do you "unzip" it?

A) `zip(*z)`
B) `unzip(z)`
C) `list(z).unzip()`
D) `zip(z, reverse=True)`

**Answer: A**

**Explanation:**
`zip(*z)` takes the tuples yielded by `z` and passes them as separate arguments to `zip`, effectively transposing the rows back into columns.

---

**Q9.22: Basic - [Map Return]**

`map(func, iterable)` returns:

A) A list.
B) A tuple.
C) An iterator.
D) A set.

**Answer: C**

**Explanation:**
In Python 3, `map` returns an iterator (lazy evaluation), not a list (unlike Python 2).

---

**Q9.23: Advanced - [Accumulate]**

`itertools.accumulate([1, 2, 3])` yields:

A) `6` (Sum).
B) `1, 3, 6` (Running totals).
C) `1, 2, 3`.
D) `3, 2, 1`.

**Answer: B**

**Explanation:**
`accumulate` returns running totals (or running application of a binary function) for each element. `1`, `1+2=3`, `1+2+3=6`.

---

**Q9.24: Expert - [Yield from Return]**

`result = yield from subgen()`. `result` captures:

A) The last yielded value.
B) The value returned by `subgen` (via `return` statement).
C) `None`.
D) A list of all yielded values.

**Answer: B**

**Explanation:**
`yield from` is an expression. Its value is the `return` value of the sub-generator (the value inside `StopIteration`).

---

**Q9.25: Intermediate - [Dropwhile]**

`itertools.dropwhile(lambda x: x < 5, [1, 4, 6, 4, 1])` yields:

A) `[1. 4. 4. 1]`
B) `[6, 4, 1]`
C) `[6]`
D) `[1, 4]`

**Answer: B**

**Explanation:**
`dropwhile` drops elements *as long as* the predicate is true. Once the predicate becomes false (at 6), it yields that element and *all* subsequent elements (even if they match the predicate later, like 4 and 1).

---

**Q9.26: Basic - [Slice Iterator]**

Can you slice an iterator `it[0:5]`?

A) Yes.
B) No.
C) Only if converted to list first.
D) Only generator objects.

**Answer: B**

**Explanation:**
Iterators do not support slicing defined in `__getitem__`. You must use `itertools.islice()` or consume them into a list.

---

**Q9.27: Advanced - [Starmap]**

`itertools.starmap(pow, [(2,5), (3,2)])` is equivalent to:

A) `pow((2,5)), pow((3,2))`
B) `pow(2,5), pow(3,2)`
C) `pow([2,5]), pow([3,2])`
D) `map(pow, (2,5), (3,2))`

**Answer: B**

**Explanation:**
`starmap` unpacks (splats) the arguments from the iterable elements. `pow(*args)`.

---

**Q9.28: Intermediate - [Generator Close]**

What happens if you call `gen.close()`?

A) `StopIteration` is raised inside generator.
B) `GeneratorExit` is raised inside generator.
C) The generator simply disappears.
D) Error.

**Answer: B**

**Explanation:**
`close()` raises `GeneratorExit` inside the generator. The generator should catch it (or let it bubble) to perform cleanup. Using `yield` inside a `try/finally` block is common for cleanup.

---

**Q9.29: Expert - [Re-entrant Generator]**

If you iterate over a generator twice: `g = gen(); list(g); list(g)`, the second list is:

A) Identical to the first.
B) Empty.
C) Error.
D) Reversed.

**Answer: B**

**Explanation:**
Generators can only be consumed once. After the first loop, the pointer is at the end. The second loop finds it empty.

---

**Q9.30: Basic - [Sorted Iterator]**

`sorted(iterator)` returns:

A) An iterator.
B) A list.
C) A tuple.
D) Error.

**Answer: B**

**Explanation:**
`sorted()` always consumes the entire iterable into memory, sorts it, and returns a new list.

---

**Q9.31: Intermediate - [Compress]**

`itertools.compress('ABC', [1, 0, 1])` yields:

A) `'A', 'C'`
B) `'A', 'B'`
C) `'B'`
D) `'ABC'`

**Answer: A**

**Explanation:**
`compress` filters elements from data returning only those that have a corresponding element in selectors that evaluates to True. `A`(1), `C`(1). `B` is skipped (0).

---

**Q9.32: Advanced - [Yield vs Yield From]**

If you use `yield subgen()` instead of `yield from subgen()`:

A) It works the same.
B) The generator yields the generator object `subgen()` itself as a single item.
C) It raises an error.
D) It yields the first item of `subgen`.

**Answer: B**

**Explanation:**
`yield` yields whatever object you pass it. If you pass a generator object, it yields that object. `yield from` iterates over that object and yields its items.

---

**Q9.33: Basic - [Reversed Iterator]**

`reversed([1, 2, 3])` returns:

A) A list `[3, 2, 1]`.
B) A reverse iterator object.
C) A tuple.
D) Error.

**Answer: B**

**Explanation:**
`reversed()` returns an iterator that accesses the sequence in reverse order. It does not create a reversed copy of the list in memory (unlike `[::-1]`).

---

**Q9.34: Intermediate - [Zip Strict]**

In Python 3.10+, `zip(..., strict=True)`:

A) Enforces types.
B) Raises `ValueError` if iterables have different lengths.
C) Speeds up processing.
D) Ignores errors.

**Answer: B**

**Explanation:**
The `strict` argument ensures that all input iterables are of the same length, raising `ValueError` otherwise.

---

**Q9.35: Advanced - [Predicate Iteration]**

`iter(list.pop, [])` is invalid because:

A) `list.pop` is not callable.
B) `list.pop` needs an instance (it's unbound).
C) `[]` is not a sentinel.
D) The sentinel must be callable.

**Answer: B**

**Explanation:**
`list.pop` is an unbound method. You need a bound method like `my_list.pop` (if `my_list` is defined) or a lambda `lambda: my_list.pop()`. (Also `iter` continues until sentinel is returned, popping from empty list raises IndexError, not returning sentinel).

---

**Q9.36: Expert - [Pep 342]**

PEP 342 enhanced generators by adding:

A) `yield from`
B) `.send()`, `.throw()`, `.close()`
C) `async` / `await`
D) List comprehensions

**Answer: B**

**Explanation:**
PEP 342 (Coroutines via Enhanced Generators) turned generators into coroutines by allowing values to be passed *into* the generator via `send()`, and exceptions via `throw()`.

---

**Q9.37: Intermediate - [Product]**

`itertools.product('AB', 'xy')` yields:

A) `Ax, By`
B) `Ax, Ay, Bx, By`
C) `Ax, Bx, Ay, By`
D) `AB, xy`

**Answer: B**

**Explanation:**
`product` computes the cartesian product. A pairs with x, y. B pairs with x, y. `('A', 'x'), ('A', 'y'), ('B', 'x'), ('B', 'y')`.

---

**Q9.38: Basic - [Loop Variable Leaking]**

In Python 3: `x = 10; [x for x in range(5)]`. After this, `x` is:

A) 4
B) 10
C) 5
D) Undefined.

**Answer: B**

**Explanation:**
List comprehensions (and generator expressions) in Python 3 have their own scope. The loop variable `x` does not leak into the enclosing scope. (Unlike Python 2).

---

**Q9.39: Advanced - [Groupby Requirement]**

`itertools.groupby(iterable)` requires the input to be:

A) A list.
B) Sorted by the grouping key.
C) Finite.
D) Unique.

**Answer: B**

**Explanation:**
`groupby` only groups *consecutive* elements. If the data is not sorted by the key, identical keys separated by other values will form separate groups.

---

**Q9.40: Expert - [Start Iteration]**

When you create a generator `g = my_gen()`, execution:

A) Starts immediately.
B) Starts when you call `next(g)`.
C) Starts when you call `g.start()`.
D) Starts when you call `iter(g)`.

**Answer: B**

**Explanation:**
Calling the generator function only creates the object. The code body does not execute until the first value is requested via `next()` (or `send(None)`), advancing to the first `yield`.

---

**Q9.41: Intermediate - [Count Step]**

`itertools.count(10, 2)` generates:

A) `10, 12, 14, ...` (infinite)
B) `10, 11, 12, ...`
C) `10, 12` (stops).
D) Error.

**Answer: A**

**Explanation:**
`count(start, step)` produces an infinite arithmetic progression.

---

**Q9.42: Basic - [Infinite Iterator]**

Which of these is NOT an infinite iterator?

A) `itertools.count()`
B) `itertools.cycle()`
C) `itertools.repeat()`
D) `range(10000000)`

**Answer: D**

**Explanation:**
`range` is finite (even if large). `repeat` is infinite by default (unless `times` arg is given). `count` and `cycle` are infinite.

---

**Q9.43: Advanced - [Tee Memory]**

Using `t1, t2 = tee(it)`. If you consume `t1` fully while leaving `t2` untouched:

A) No memory impact.
B) High memory usage (buffers entire `it`).
C) `t2` becomes empty.
D) `t1` raises Error.

**Answer: B**

**Explanation:**
`tee` must store values drawn from the source iterator until *all* teed iterators have consumed them. If one advances far ahead of the others, `tee` buffers the difference in memory.

---

**Q9.44: Intermediate - [Map Length]**

`len(map(func, data))` returns:

A) The length of data.
B) Error.
C) The count of processed items.
D) `None`.

**Answer: B**

**Explanation:**
`map` returns an iterator. Iterators do not have a `__len__`, because their length is unknown until consumed. Attempting `len()` raises `TypeError`.

---

**Q9.45: Expert - [Return in Yield From]**

When `yield from` finishes, the value of the expression is:

A) `None`.
B) The value of the `StopIteration` exception raised by the sub-iterator.
C) The last yielded value.
D) `True`.

**Answer: B**

**Explanation:**
Mechanically, `yield from` catches `StopIteration` from the sub-iterator, extracts its `value` attribute (the return value of the sub-generator), and makes that the value of the `yield from` expression.

---

**Q9.46: Basic - [Filter Output]**

`filter(None, [1, 0, 2, [], 'a'])` filters out:

A) None values only.
B) Falsy values (`0`, `[]`).
C) Nothing.
D) All values.

**Answer: B**

**Explanation:**
If the function argument is `None`, `filter` uses the identity function, removing all elements that evaluate to False in a boolean context.

---

**Q9.47: Intermediate - [Permutations]**

`len(list(itertools.permutations('ABC', 2)))` is:

A) 3
B) 6
C) 9
D) 8

**Answer: B**

**Explanation:**
Permutations of length 2 from 3 items: $P(3, 2) = 3 \times 2 = 6$. (`AB, AC, BA, BC, CA, CB`).

---

**Q9.48: Advanced - [Yield in converting]**

If `def f(): yield 1`, then `bool(f())` is:

A) False
B) True
C) Error
D) 1

**Answer: B**

**Explanation:**
`f()` returns a generator object. All objects in Python are Truthy unless defined otherwise (via `__bool__` or `__len__`). Generator objects are Truthy. It does *not* run the generator to check if it yields values.

---

**Q9.49: Expert - [StopIteration Catching]**

Since PEP 479, if `StopIteration` bubbles up from a generator (not properly caught/handled):

A) It stops the loop normally.
B) It is converted into a `RuntimeError`.
C) It is ignored.
D) It resets the generator.

**Answer: B**

**Explanation:**
PEP 479 changed the behavior so that if a `StopIteration` is raised inside a generator (and not cleared), it is converted to `RuntimeError`. This prevents `StopIteration` from accidentally stopping a `yield from` or a loop wrapping the generator unexpectedly.

---

**Q9.50: Intermediate - [IsSlice Copy]**

`itertools.islice(list_obj, 5)` returns:

A) A list (copy of first 5).
B) An iterator yielding first 5.
C) A view.
D) A tuple.

**Answer: B**

**Explanation:**
`islice` always returns an iterator, performing lazy slicing.

---

**Q9.51: Basic - [Set Comprehension]**

`{x for x in [1, 2, 1]}` creates:

A) A set `{1, 2}`.
B) A list `[1, 2, 1]`.
C) A dictionary.
D) An iterator.

**Answer: A**

**Explanation:**
Curly braces with loop syntax `{x for ...}` creates a set comprehension, automatically handling uniqueness.

---

**Q9.52: Advanced - [Generator Memory]**

`sum(range(1000000))` vs `sum([i for i in range(1000000)])`. Why is the first better?

A) `range` uses `int32`.
B) The second creates a huge list in memory before summing. The first iterates lazily (in Py3 range is lazy).
C) `range` is a C function.
D) No difference.

**Answer: B**

**Explanation:**
Using `[]` forces the creation of a list with 1 million integers in memory. Iterating over the iterator/iterable directly (using generator expression or lazy iterable) yields one item at a time, keeping memory usage constant.

---

A) `('A', 'B'), ('A', 'A'), ('B', 'A')`
B) `('A', 'B'), ('A', 'A'), ('B', 'A')` (Same as A) - *Error in options generation*
C) `('A', 'B'), ('A', 'A'), ('B', 'A')`
D) `('A', 'B'), ('A', 'A'), ('B', 'A')`

*Correction*: The previous options were malformed. `itertools.combinations('ABA', 2)` produces `('A', 'B'), ('A', 'A'), ('B', 'A')`. This is because it treats elements by position.
Let's restate the question with distinct options.

**Q9.53: Intermediate - [Combinations Iteration]**

`list(itertools.combinations('ABA', 2))` produces how many items?

A) 2
B) 3
C) 6
D) 1

**Answer: B**

**Explanation:**
`combinations` emits tuples based on *position*. Indices: 0('A'), 1('B'), 2('A'). Pairs: (0,1)->AB, (0,2)->AA, (1,2)->BA. Total 3 items.

---

**Q9.54: Expert - [Context Manager Generator]**

Using `@contextlib.contextmanager`, a generator must yield:

A) Exactly once.
B) Twice.
C) As many times as lines in the `with` block.
D) Never.

**Answer: A**

**Explanation:**
The decorated generator must yield exactly once. The code before yield runs on `__enter__`, the value yielded is bound to variable (`as var`). The code after yield runs on `__exit__`.

---

**Q9.55: Intermediate - [Itertools Cycle Limit]**

`cycle` consumes memory proportional to:

A) Infinite.
B) The length of the input iterable.
C) 1 element.
D) Zero.

**Answer: B**

**Explanation:**
`cycle` must store a copy of the entire input iterable to repeat it.

---

**Q9.56: Basic - [Next Default]**

`next(it, 'end')` returns:

A) The next item, or 'end' if references are exhausted.
B) Error if exhausted.
C) 'end' always.
D) The iterator itself.

**Answer: A**

**Explanation:**
`next` accepts an optional default value to prevent raising `StopIteration`.

---

**Q9.57: Advanced - [Send to Unstarted]**

Sending a non-None value to a just-created generator:

A) Works fine.
B) Raises `TypeError`.
C) Raises `ValueError`.
D) Queues the value.

**Answer: B**

**Explanation:**
You cannot send a value to a generator that hasn't started. You must prime it with `next(g)` or `g.send(None)`. Sending non-None raises `TypeError`.

---

**Q9.58: Intermediate - [Filterfalse]**

`itertools.filterfalse(None, [1, 0, 2])` yields:

A) `1, 2`
B) `0`
C) `1, 0, 2`
D) `[]`

**Answer: B**

**Explanation:**
It yields elements that are False. (Inverse of `filter`). 0 is False.

---

**Q9.59: Expert - [Yield evaluation]**

`x = yield y`
Which happens first?

A) `x` is assigned, then `y` is yielded.
B) `y` is yielded to the caller; generator pauses; value sent back becomes `x`.
C) Simultaneous.
D) `x` is assigned `None`, then `y` is yielded.

**Answer: B**

**Explanation:**
The expression on the right (`y`) is evaluated and yielded. The generator suspends. When resumed (via send), the sent value replaces the `yield` expression, and is assigned to `x`.

---

**Q9.60: Basic - [Simple Generator]**

```python
def g():
    yield 1
    yield 2
```
`list(g())` is:
A) `[1, 2]`
B) `[1]`
C) `[2]`
D) Error

**Answer: A**

**Explanation:**
It runs until exhaustion, collecting all yielded values.

---

---

## Review Notes (2026-02-06)

- Q9.53 has an answer-key/content mismatch: explanation enumerates 3 outputs but `**Answer: D**` indicates only 2 outputs.
- Q9.53 explanation includes scratch/drafting text ("Wait...", "Strictly...").
- Q9.59 uses only A/B/C options, which is inconsistent with the predominant 4-option MCQ format.
