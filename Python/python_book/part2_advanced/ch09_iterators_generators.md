# Chapter 9: Iterators & Generators

> **Topics Covered**: Iterator protocol, __iter__, __next__, generators, yield, generator expressions, yield from, StopIteration, itertools module, lazy evaluation, memory efficiency, coroutines basics

---

## Questions

---

**Q9.1: Basic - [Iteration Basics]**

What makes an object iterable in Python?

A) Having a `loop()` method
B) Having an `__iter__()` method that returns an iterator
C) Being a list
D) Being numeric

**Answer: B**

**Explanation:**
An object is iterable if it has `__iter__()` returning an iterator. The `for` loop calls `iter(obj)` which invokes `__iter__()`. Strings, lists, dicts are iterable because they have `__iter__`.

---

**Q9.2: Basic - [Iterator Protocol]**

What methods define an iterator?

A) `__loop__` and `__end__`
B) `__iter__` and `__next__`
C) `start` and `stop`
D) `begin` and `end`

**Answer: B**

**Explanation:**
Iterator protocol: `__iter__` returns the iterator (often `self`), `__next__` returns the next value or raises `StopIteration`. Every iterator is also iterable (has `__iter__`).

---

**Q9.3: Intermediate - [iter() Function]**

What does `iter(obj)` do?

A) Modifies obj
B) Returns an iterator by calling obj.__iter__()
C) Iterates through obj
D) Counts items in obj

**Answer: B**

**Explanation:**
`iter(obj)` calls `obj.__iter__()` and returns the iterator. This iterator can then be used with `next()`. For objects with `__getitem__` but no `__iter__`, Python creates an iterator that calls `__getitem__` with 0, 1, 2, etc.

---

**Q9.4: Basic - [next() Function]**

What is the output?
```python
lst = [1, 2, 3]
it = iter(lst)
print(next(it), next(it))
```

A) `1, 1`
B) `1, 2`
C) `2, 3`
D) `1, [2, 3]`

**Answer: B**

**Explanation:**
`iter(lst)` creates an iterator. Each `next()` call advances it and returns the next value. First call → 1, second call → 2. The iterator remembers its position.

---

**Q9.5: Intermediate - [StopIteration]**

What is the output?
```python
it = iter([1])
print(next(it))
print(next(it))
```

A) `1, 1`
B) `1, None`
C) `1`, then StopIteration exception
D) `1, []`

**Answer: C**

**Explanation:**
First `next(it)` returns 1. Second call has no more elements → raises `StopIteration`. This exception signals end of iteration. The `for` loop catches it to stop gracefully.

---

**Q9.6: Intermediate - [next() with Default]**

What is the output?
```python
it = iter([1])
print(next(it))
print(next(it, "done"))
```

A) `1, StopIteration`
B) `1, done`
C) `1, None`
D) Error

**Answer: B**

**Explanation:**
`next(iterator, default)` returns default instead of raising StopIteration when exhausted. First call → 1. Second call → iterator exhausted → returns "done". Useful to avoid exception handling.

---

**Q9.7: Intermediate - [Custom Iterator]**

What is the output?
```python
class Counter:
    def __init__(self, max):
        self.max = max
        self.n = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.n >= self.max:
            raise StopIteration
        self.n += 1
        return self.n

print(list(Counter(3)))
```

A) `[1, 2, 3]`
B) `[0, 1, 2]`
C) `[0, 1, 2, 3]`
D) Error

**Answer: A**

**Explanation:**
Counter is an iterator (has `__iter__` returning self, `__next__` returning values). Counts from 1 to max, then stops. `list()` consumes the iterator → `[1, 2, 3]`.

---

**Q9.8: Basic - [Generator Function]**

What makes a function a generator?

A) Returning a list
B) Using the `yield` keyword
C) Having `generator` in its name
D) Using a while loop

**Answer: B**

**Explanation:**
Any function with `yield` is a generator function. When called, it returns a generator object (an iterator), not the computed value. Execution pauses at each `yield` until `next()` is called.

---

**Q9.9: Basic - [Generator Basics]**

What is the output?
```python
def gen():
    yield 1
    yield 2
    yield 3

g = gen()
print(type(g))
```

A) `<class 'function'>`
B) `<class 'generator'>`
C) `<class 'list'>`
D) `<class 'iterator'>`

**Answer: B**

**Explanation:**
Calling a generator function returns a generator object, not the yielded values. The function body hasn't run yet. You must iterate (with `next()` or `for`) to get values.

---

**Q9.10: Intermediate - [Generator Execution]**

What is the output?
```python
def gen():
    print("Starting")
    yield 1
    print("After first")
    yield 2

g = gen()
print("Created")
print(next(g))
```

A) `Starting, Created, 1`
B) `Created, Starting, 1`
C) `Created, 1, Starting`
D) `Starting, 1, Created`

**Answer: B**

**Explanation:**
Creating the generator doesn't execute the function body yet. "Created" prints first. Then `next(g)` runs until first `yield` — prints "Starting", then yields 1. Execution pauses AFTER yielding.

---

**Q9.11: Intermediate - [Generator State]**

What is the output?
```python
def gen():
    x = 0
    while True:
        x += 1
        yield x

g = gen()
print(next(g), next(g), next(g))
```

A) `1, 1, 1`
B) `1, 2, 3`
C) `0, 1, 2`
D) Error: infinite loop

**Answer: B**

**Explanation:**
Generators maintain state between calls. `x` persists across `next()` calls. Each call resumes where it left off. The while True doesn't block — it pauses at `yield`. Returns 1, 2, 3...

---

**Q9.12: Intermediate - [Generator vs List]**

Why are generators more memory-efficient than lists?

A) They compress data
B) They generate values on-demand (lazy) instead of storing all at once
C) They use C under the hood
D) They're not more efficient

**Answer: B**

**Explanation:**
Generators are lazy — they compute values one at a time. A list of 1 million numbers stores all in memory. A generator for the same produces them on demand. Critical for large datasets or infinite sequences.

---

**Q9.13: Basic - [Generator Expression]**

What is the output?
```python
gen = (x**2 for x in range(4))
print(type(gen))
print(list(gen))
```

A) `<class 'list'>, [0, 1, 4, 9]`
B) `<class 'generator'>, [0, 1, 4, 9]`
C) `<class 'tuple'>, (0, 1, 4, 9)`
D) Error

**Answer: B**

**Explanation:**
Parentheses with comprehension syntax create a generator expression (not tuple). Same lazy behavior as generator functions but more concise. Consumed once when converted to list.

---

**Q9.14: Intermediate - [Generator Expression vs List Comprehension]**

What's the difference between `[x for x in range(1000000)]` and `(x for x in range(1000000))`?

A) No difference
B) List creates all values immediately in memory; generator creates on demand
C) Generator is faster to create AND access
D) List is always better

**Answer: B**

**Explanation:**
List comprehension creates a complete list (takes memory for 1 million items). Generator expression creates a generator object (minimal memory). Generator is better when you only need to iterate once or might not need all values.

---

**Q9.15: Intermediate - [Generator Exhaustion]**

What is the output?
```python
gen = (x for x in [1, 2, 3])
print(sum(gen))
print(sum(gen))
```

A) `6, 6`
B) `6, 0`
C) `6, Error`
D) `6, []`

**Answer: B**

**Explanation:**
⚠️ Generators can only be consumed once. First `sum(gen)` exhausts it → 6. Second `sum(gen)` gets empty iterator → 0. To reuse, either store as list or recreate the generator.

---

**Q9.16: Intermediate - [yield from]**

What is the output?
```python
def sub():
    yield 1
    yield 2

def main():
    yield 0
    yield from sub()
    yield 3

print(list(main()))
```

A) `[0, (1, 2), 3]`
B) `[0, 1, 2, 3]`
C) `[0, sub, 3]`
D) Error

**Answer: B**

**Explanation:**
`yield from iterable` is equivalent to `for x in iterable: yield x`. It delegates to another generator/iterable. Yields all values from `sub()` (1, 2) inline. Result: 0, 1, 2, 3.

---

**Q9.17: Advanced - [yield from with Return]**

What is the output?
```python
def sub():
    yield 1
    return "done"

def main():
    result = yield from sub()
    print(f"Result: {result}")

list(main())
```

A) Prints nothing
B) Prints "Result: done"
C) Prints "Result: None"
D) Error

**Answer: B**

**Explanation:**
`yield from` can capture the return value of a generator with `return`. When `sub()` completes, its return value becomes the value of the `yield from` expression. Advanced feature for coroutine-like patterns.

---

**Q9.18: Intermediate - [itertools.count]**

What does `itertools.count(start, step)` do?

A) Counts occurrences
B) Creates an infinite iterator of numbers: start, start+step, start+2*step, ...
C) Counts to a limit
D) Returns a range

**Answer: B**

**Explanation:**
`count(10, 2)` generates 10, 12, 14, 16, ... infinitely. Useful with `zip()` to add indices or with `islice()` to limit. Never use in `list()` directly — it won't stop!

---

**Q9.19: Intermediate - [itertools.cycle]**

What is the output?
```python
from itertools import cycle, islice
c = cycle('ABC')
print(list(islice(c, 7)))
```

A) `['A', 'B', 'C']`
B) `['A', 'B', 'C', 'A', 'B', 'C', 'A']`
C) `['ABCABCA']`
D) Error

**Answer: B**

**Explanation:**
`cycle()` repeats an iterable infinitely: A, B, C, A, B, C, A, B, C, ... `islice(iter, n)` takes first n elements. Result: 7 elements cycling through 'ABC'.

---

**Q9.20: Intermediate - [itertools.repeat]**

What is `itertools.repeat(x, n)`?

A) Repeats function n times
B) Creates an iterator yielding x, n times
C) Returns x * n
D) Creates n copies of x

**Answer: B**

**Explanation:**
`repeat(5, 3)` yields 5, 5, 5 (three times). Without n, repeats infinitely. Useful with `map()`: `map(pow, [2,3,4], repeat(2))` squares each. Memory efficient — same object yielded.

---

**Q9.21: Intermediate - [itertools.chain]**

What is the output?
```python
from itertools import chain
a = [1, 2]
b = [3, 4]
c = [5]
print(list(chain(a, b, c)))
```

A) `[[1, 2], [3, 4], [5]]`
B) `[1, 2, 3, 4, 5]`
C) `[(1, 2), (3, 4), (5,)]`
D) Error

**Answer: B**

**Explanation:**
`chain()` concatenates iterables, yielding elements one by one from each. More memory-efficient than `a + b + c` for lists. Works with any iterables, doesn't create intermediate lists.

---

**Q9.22: Intermediate - [itertools.islice]**

What is the output?
```python
from itertools import islice
gen = (x for x in range(100))
print(list(islice(gen, 5, 10)))
```

A) `[5, 6, 7, 8, 9]`
B) `[0, 1, 2, 3, 4]`
C) `[5, 10]`
D) `[6, 7, 8, 9, 10]`

**Answer: A**

**Explanation:**
`islice(iterable, start, stop)` is like slice but for iterators. Returns elements from index 5 to 9 (exclusive stop). Consumes elements up to that point. The original generator advances.

---

**Q9.23: Intermediate - [itertools.takewhile/dropwhile]**

What is the output?
```python
from itertools import takewhile
nums = [1, 3, 5, 2, 4, 6]
print(list(takewhile(lambda x: x < 5, nums)))
```

A) `[1, 3]`
B) `[1, 3, 5]`
C) `[1, 3, 2, 4]`
D) `[1, 3, 5, 2, 4]`

**Answer: A**

**Explanation:**
`takewhile(pred, iter)` yields elements WHILE predicate is True. Stops at first False (5 < 5 is False). Doesn't restart — later elements (2, 4) that match are ignored. `dropwhile` is opposite: drops while True.

---

**Q9.24: Intermediate - [itertools.zip_longest]**

What is the output?
```python
from itertools import zip_longest
a = [1, 2, 3]
b = [4, 5]
print(list(zip_longest(a, b, fillvalue=0)))
```

A) `[(1, 4), (2, 5)]`
B) `[(1, 4), (2, 5), (3, 0)]`
C) `[(1, 4), (2, 5), (3, None)]`
D) Error

**Answer: B**

**Explanation:**
Regular `zip` stops at shortest. `zip_longest` continues to longest, using `fillvalue` for missing elements. Result: pairs (1,4), (2,5), and (3,0) where 0 fills the shorter.

---

**Q9.25: Intermediate - [itertools.product]**

What is the output?
```python
from itertools import product
print(list(product([1, 2], ['a', 'b'])))
```

A) `[(1, 'a'), (2, 'b')]`
B) `[(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b')]`
C) `['1a', '1b', '2a', '2b']`
D) Error

**Answer: B**

**Explanation:**
`product()` computes Cartesian product — all combinations. Like nested loops: `for x in [1,2]: for y in ['a','b']`. Returns tuples. `repeat` parameter allows `product(A, repeat=2)` = `product(A, A)`.

---

**Q9.26: Intermediate - [itertools.permutations]**

What is the output?
```python
from itertools import permutations
print(list(permutations([1, 2, 3], 2)))
```

A) `[(1, 2), (2, 3), (1, 3)]`
B) `[(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]`
C) `[(1, 2, 3), (1, 3, 2), ...]`
D) `[(1, 1), (2, 2), (3, 3)]`

**Answer: B**

**Explanation:**
`permutations(iterable, r)` returns r-length permutations (order matters). All ways to pick 2 from [1,2,3] where order matters: 6 results. (1,2) ≠ (2,1). Without r, full-length permutations.

---

**Q9.27: Intermediate - [itertools.combinations]**

What is the output?
```python
from itertools import combinations
print(list(combinations([1, 2, 3], 2)))
```

A) `[(1, 2), (1, 3), (2, 3)]`
B) `[(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]`
C) `[(1, 2, 3)]`
D) `[(1, 1), (2, 2), (3, 3)]`

**Answer: A**

**Explanation:**
`combinations(iterable, r)` returns r-length combinations (order doesn't matter). 3 ways to choose 2 from [1,2,3]: (1,2), (1,3), (2,3). No (2,1) — that's same as (1,2) for combinations.

---

**Q9.28: Intermediate - [itertools.groupby]**

What does `itertools.groupby()` do?

A) Groups all equal elements
B) Groups consecutive elements with same key
C) Sorts then groups
D) Creates group objects

**Answer: B**

**Explanation:**
`groupby(iterable, key)` groups CONSECUTIVE elements with same key. Must sort first if you want all matching elements together. Returns iterator of (key, group). Each group is an iterator.

---

**Q9.29: Advanced - [groupby Example]**

What is the output?
```python
from itertools import groupby
data = [('a', 1), ('a', 2), ('b', 3), ('a', 4)]
groups = [(k, list(g)) for k, g in groupby(data, key=lambda x: x[0])]
print(groups)
```

A) `[('a', [...]), ('b', [...])]`
B) `[('a', [('a', 1), ('a', 2)]), ('b', [('b', 3)]), ('a', [('a', 4)])]`
C) `[('a', [1, 2, 4]), ('b', [3])]`
D) Error

**Answer: B**

**Explanation:**
⚠️ `groupby` groups CONSECUTIVE elements. First two 'a's, then 'b', then another 'a' (separate group). To group all 'a's together, sort first: `sorted(data, key=lambda x: x[0])`.

---

**Q9.30: Intermediate - [itertools.accumulate]**

What is the output?
```python
from itertools import accumulate
print(list(accumulate([1, 2, 3, 4])))
```

A) `[1, 2, 3, 4]`
B) `[1, 3, 6, 10]`
C) `10`
D) `[10, 9, 7, 4]`

**Answer: B**

**Explanation:**
`accumulate()` returns running totals (by default). 1, 1+2=3, 3+3=6, 6+4=10. With `func` parameter: `accumulate([1,2,3], operator.mul)` → 1, 2, 6 (running product). Like `sum()` but yields intermediate values.

---

**Q9.31: Intermediate - [itertools.filterfalse]**

What is the output?
```python
from itertools import filterfalse
nums = [1, 2, 3, 4, 5, 6]
print(list(filterfalse(lambda x: x % 2, nums)))
```

A) `[1, 3, 5]`
B) `[2, 4, 6]`
C) `[1, 2, 3, 4, 5, 6]`
D) `[]`

**Answer: B**

**Explanation:**
`filterfalse` keeps elements where predicate is False. `x % 2` is truthy for odd, falsy for even. Keeps even numbers (predicate returns 0/False). Opposite of `filter()`.

---

**Q9.32: Intermediate - [itertools.starmap]**

What is the output?
```python
from itertools import starmap
pairs = [(2, 5), (3, 2), (10, 3)]
print(list(starmap(pow, pairs)))
```

A) `[32, 9, 1000]`
B) `[(2, 5), (3, 2), (10, 3)]`
C) `[25, 8, 1000]`
D) Error

**Answer: A**

**Explanation:**
`starmap(func, iterable)` applies func to each item where item is unpacked as arguments. `pow(2, 5)` = 32, `pow(3, 2)` = 9, `pow(10, 3)` = 1000. Like `map()` but with argument unpacking.

---

**Q9.33: Intermediate - [itertools.tee]**

What does `itertools.tee(iterator, n)` do?

A) Displays iterator
B) Creates n independent iterators from one source
C) Tees into a file
D) Terminates iterator

**Answer: B**

**Explanation:**
`tee(it, n)` returns n independent iterators that each yield all items from the original. Useful when you need to iterate multiple times. Warning: uses memory to store items that one iter has consumed but others haven't.

---

**Q9.34: Advanced - [Generator send()]**

What is the output?
```python
def gen():
    x = yield 1
    yield x + 10

g = gen()
print(next(g))
print(g.send(5))
```

A) `1, 15`
B) `1, 11`
C) `5, 15`
D) Error

**Answer: A**

**Explanation:**
`send(value)` resumes generator and sends value which becomes the result of the `yield` expression. `next(g)` → yields 1. `send(5)` → `x = 5`, then yields 5 + 10 = 15. Two-way communication!

---

**Q9.35: Advanced - [Generator throw()]**

What does `generator.throw(exception)` do?

A) Logs the exception
B) Raises exception at the yield point where generator is paused
C) Ignores the exception
D) Returns the exception

**Answer: B**

**Explanation:**
`throw(exception)` raises the exception inside the generator at the current `yield`. The generator can catch it with try/except. Used for signaling errors or special conditions to running generators.

---

**Q9.36: Advanced - [Generator close()]**

What does `generator.close()` do?

A) Closes a file
B) Raises GeneratorExit at current yield, allowing cleanup
C) Saves state
D) Deletes the generator

**Answer: B**

**Explanation:**
`close()` throws `GeneratorExit` at the yield point. The generator should either not catch it or re-raise after cleanup. This allows generators to clean up resources (close files, etc.) when no longer needed.

---

**Q9.37: Intermediate - [Lazy Evaluation Benefit]**

Which scenario best demonstrates generator benefits?
```python
# A
data = [process(x) for x in range(10000000)]
result = sum(data)

# B
data = (process(x) for x in range(10000000))
result = sum(data)
```

A) A is better — faster access
B) B is better — doesn't store 10M items in memory
C) Same performance
D) Neither is good

**Answer: B**

**Explanation:**
A stores 10 million processed items in memory. B generates one at a time, sums it, moves to next — constant memory usage regardless of size. With generators, processing 10 billion items is feasible.

---

**Q9.38: Intermediate - [map() Returns Iterator]**

What is the output?
```python
m = map(str.upper, ['a', 'b', 'c'])
print(type(m))
print(list(m))
print(list(m))
```

A) `map, ['A', 'B', 'C'], ['A', 'B', 'C']`
B) `<class 'map'>, ['A', 'B', 'C'], []`
C) `list, ['A', 'B', 'C'], ['A', 'B', 'C']`
D) Error

**Answer: B**

**Explanation:**
`map()` returns an iterator (lazy), not a list. First `list(m)` consumes it. Second `list(m)` gets empty — iterator is exhausted. Same for `filter()`, `zip()`. Convert once or re-create.

---

**Q9.39: Intermediate - [filter() Returns Iterator]**

In Python 3, what does `filter()` return?

A) A list
B) An iterator
C) A tuple
D) A filter object (which is an iterator)

**Answer: D**

**Explanation:**
`filter()` returns a filter object that implements iterator protocol. Must wrap with `list()` to get all values at once. This changed from Python 2 (returned list) for memory efficiency.

---

**Q9.40: Advanced - [Coroutine Basics]**

What is a coroutine in Python (pre-async/await)?

A) A fast routine
B) A generator that receives values via send(), enabling two-way communication
C) A C function
D) A parallel routine

**Answer: B**

**Explanation:**
Before `async/await`, coroutines were generators using `yield` to receive AND produce values. `value = yield result` both sends a result and receives the next input. Foundation for async programming.

---

**Q9.41: Intermediate - [__iter__ Returns New Iterator]**

Why should an iterable's `__iter__` return a new iterator each time?

A) Python requires it
B) So multiple loops can iterate independently without interfering
C) For memory efficiency
D) It doesn't need to

**Answer: B**

**Explanation:**
If `__iter__` returns `self` (like an iterator does), you can only have one active loop. Iterables (like list) return a NEW iterator each time. Multiple `for` loops over the same list work correctly because each gets fresh iterator.

---

**Q9.42: Intermediate - [Infinite Generators]**

What is the output?
```python
def infinite():
    n = 0
    while True:
        yield n
        n += 1

gen = infinite()
print([next(gen) for _ in range(5)])
```

A) Error: infinite loop
B) `[0, 1, 2, 3, 4]`
C) `[infinite, infinite, ...]`
D) Never terminates

**Answer: B**

**Explanation:**
The generator has infinite `while True`, but `yield` pauses execution. We only request 5 values with the comprehension. Generator waits patiently. This is how infinite sequences are practical with generators.

---

**Q9.43: Intermediate - [Generator for File Processing]**

Why use a generator for reading large files?
```python
def read_lines(file):
    for line in open(file):
        yield line.strip()
```

A) Faster reading
B) Memory efficient — processes one line at a time instead of loading entire file
C) Required by Python
D) Better formatting

**Answer: B**

**Explanation:**
A 10GB file loaded entirely would need 10GB+ memory. Generator yields one line at a time — constant memory regardless of file size. Essential for big data processing.

---

**Q9.44: Intermediate - [reversed() Returns Iterator]**

What is the output?
```python
r = reversed([1, 2, 3])
print(type(r))
print(list(r))
print(list(r))
```

A) `list, [3, 2, 1], [3, 2, 1]`
B) `<class 'list_reverseiterator'>, [3, 2, 1], []`
C) `list, [1, 2, 3], [1, 2, 3]`
D) Error

**Answer: B**

**Explanation:**
`reversed()` returns an iterator (list_reverseiterator). First `list(r)` exhausts it. Second gives empty list. Compare with `[::-1]` slice which creates a new list (reusable) but uses more memory.

---

**Q9.45: Advanced - [Generator as Context Manager]**

Can generators be used as context managers?

A) No
B) Yes, with @contextlib.contextmanager decorator
C) Only with async/await
D) Only built-in generators

**Answer: B**

**Explanation:**
`@contextmanager` wraps a generator: code before `yield` is `__enter__`, code after is `__exit__`. Simpler than writing a class with both methods. Example:
```python
@contextmanager
def managed(): setup(); yield; cleanup()
```

---

**Q9.46: Intermediate - [enumerate() Returns Iterator]**

What is the output?
```python
e = enumerate(['a', 'b', 'c'], start=1)
print(type(e))
print(list(e))
```

A) `<class 'list'>, [(1, 'a'), (2, 'b'), (3, 'c')]`
B) `<class 'enumerate'>, [(1, 'a'), (2, 'b'), (3, 'c')]`
C) `<class 'enumerate'>, [(0, 'a'), (1, 'b'), (2, 'c')]`
D) Error

**Answer: B**

**Explanation:**
`enumerate()` returns an enumerate iterator. With `start=1`, counting begins at 1. Yields (index, value) tuples. More Pythonic than `for i in range(len(lst))`.

---

**Q9.47: Intermediate - [zip() Returns Iterator]**

What is the output?
```python
z = zip([1, 2], ['a', 'b'])
print(type(z))
print(list(z))
print(list(z))
```

A) `<class 'zip'>, [(1, 'a'), (2, 'b')], [(1, 'a'), (2, 'b')]`
B) `<class 'zip'>, [(1, 'a'), (2, 'b')], []`
C) `<class 'list'>, [(1, 'a'), (2, 'b')], [(1, 'a'), (2, 'b')]`
D) Error

**Answer: B**

**Explanation:**
`zip()` returns an iterator (since Python 3). Once consumed, it's empty. For reuse, convert to list first: `list(zip(...))` or re-call `zip()`.

---

**Q9.48: Intermediate - [any() and all() with Generators]**

What is the output?
```python
print(any(x > 5 for x in [1, 2, 10, 3]))
print(all(x > 0 for x in [1, 2, 3, 0]))
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
`any()` returns True if ANY element is truthy — 10 > 5 is True. `all()` returns True if ALL are truthy — 0 > 0 is False. Both short-circuit: `any` stops at first True, `all` stops at first False.

---

**Q9.49: Advanced - [Generator Pipelines]**

What is a generator pipeline?
```python
nums = range(100)
evens = (x for x in nums if x % 2 == 0)
squares = (x**2 for x in evens)
result = sum(squares)
```

A) A complex syntax
B) Chaining generators where each feeds the next — all lazy until consumed
C) Parallel processing
D) A design pattern only

**Answer: B**

**Explanation:**
Each generator lazily transforms data and feeds the next. Nothing executes until `sum()` consumes the final generator. Memory efficient — only one value exists at a time through the pipeline. Unix pipes concept in Python.

---

**Q9.50: Intermediate - [range() is Not Generator]**

Is `range()` a generator?

A) Yes
B) No, it's a lazy sequence that supports indexing and multiple iteration
C) It depends on Python version
D) Yes, but special

**Answer: B**

**Explanation:**
`range()` is NOT a generator — it's a range object. It's lazy (doesn't store all values) but unlike generators: supports indexing (`range(100)[50]`), `len()`, `in`, and can be iterated multiple times. It's a sequence.

---

**Q9.51: Advanced - [iter() with Sentinel]**

What is the output?
```python
from functools import partial
from io import StringIO

s = StringIO("a\nb\nc\n")
lines = iter(partial(s.readline), '')
print(list(lines))
```

A) `['a\n', 'b\n', 'c\n']`
B) `['a', 'b', 'c']`
C) `['a\n', 'b\n', 'c\n', '']`
D) Error

**Answer: A**

**Explanation:**
`iter(callable, sentinel)` calls callable until it returns sentinel. `readline()` returns '' at EOF. So it reads all lines, stopping when empty string (after 'c\n'). Two-argument iter is powerful for such patterns.

---

**Q9.52: Expert - [Generator-Based Coroutine]**

What was the purpose of `yield from` for coroutines?

A) Faster yields
B) Delegate to sub-generators while passing send/throw through
C) Create from expressions
D) Iterate files

**Answer: B**

**Explanation:**
`yield from` creates a bidirectional pipe: values pass through, `send()` and `throw()` reach the subgenerator. Essential for "trampoline" style coroutines and async. Now largely replaced by `async/await`.

---

**Q9.53: Intermediate - [Memory Comparison]**

```python
# A: List
sum([x * x for x in range(10000000)])

# B: Generator
sum(x * x for x in range(10000000))
```
What's the main difference?

A) A is faster
B) B uses O(1) memory vs A's O(n) memory
C) Same memory usage
D) B is incorrect syntax

**Answer: B**

**Explanation:**
A creates a list of 10 million squares in memory before summing. B generates squares one at a time — constant memory. For large n, A might cause MemoryError while B completes fine.

---

**Q9.54: Intermediate - [next() on List]**

What is the output?
```python
lst = [1, 2, 3]
print(next(lst))
```

A) `1`
B) `[1, 2, 3]`
C) TypeError: 'list' object is not an iterator
D) `None`

**Answer: C**

**Explanation:**
Lists are iterable, not iterators. They don't have `__next__`. Must call `iter(lst)` first to get an iterator. `next(iter(lst))` would work, returning 1.

---

**Q9.55: Intermediate - [Iterable vs Iterator]**

What's the difference between iterable and iterator?

A) Same thing
B) Iterable has __iter__; iterator has both __iter__ and __next__
C) Iterator is faster
D) Iterable is a subclass

**Answer: B**

**Explanation:**
Iterable: has `__iter__` returning an iterator (list, string, dict). Iterator: has BOTH `__iter__` (returns self) AND `__next__` (returns next value). All iterators are iterable, but not all iterables are iterators.

---

**Q9.56: Advanced - [yield in try-finally]**

What is the output?
```python
def gen():
    try:
        yield 1
        yield 2
    finally:
        print("Cleanup")

g = gen()
print(next(g))
g.close()
```

A) `1` then `Cleanup`
B) `1` then nothing
C) `1, 2` then `Cleanup`
D) Error

**Answer: A**

**Explanation:**
`next(g)` yields 1 (pauses in try block). `close()` raises GeneratorExit at yield point, triggering `finally`. "Cleanup" prints. Finally blocks in generators run on close/exception — good for resource cleanup.

---

**Q9.57: Advanced - [Generator State Methods]**

What are the valid states a generator can be in?

A) Created, Running, Finished
B) GEN_CREATED, GEN_RUNNING, GEN_SUSPENDED, GEN_CLOSED
C) Active, Inactive
D) Open, Closed

**Answer: B**

**Explanation:**
Check with `gen.gi_frame` (None if closed) or `inspect.getgeneratorstate(gen)`. Created (not started), Running (executing), Suspended (at yield), Closed (completed/closed). Important for debugging coroutines.

---

**Q9.58: Intermediate - [Generator Expression Scope]**

What is the output?
```python
x = 10
gen = (x for _ in range(3))
x = 20
print(list(gen))
```

A) `[10, 10, 10]`
B) `[20, 20, 20]`
C) `[10, 20, 20]`
D) Error

**Answer: B**

**Explanation:**
⚠️ Generator expressions evaluate variables when consumed, not when created (lazy). When `list(gen)` runs, `x` is 20. This is different from list comprehensions where values are captured immediately.

---

**Q9.59: Expert - [Sub-generator Return]**

What is the value of `result`?
```python
def sub():
    yield 1
    yield 2
    return "final"

def main():
    result = yield from sub()
    yield result

print(list(main()))
```

A) `[1, 2]`
B) `[1, 2, 'final']`
C) `['final']`
D) Error

**Answer: B**

**Explanation:**
`yield from` first yields all values from sub() (1, 2). Then the return value of sub() becomes the value of the `yield from` expression. This is assigned to `result` and yielded.

---

**Q9.60: Intermediate - [itertools.compress]**

What is the output?
```python
from itertools import compress
data = ['a', 'b', 'c', 'd']
selectors = [1, 0, 1, 0]
print(list(compress(data, selectors)))
```

A) `['a', 'c']`
B) `['b', 'd']`
C) `['a', 1, 'c', 1]`
D) `[1, 0, 1, 0]`

**Answer: A**

**Explanation:**
`compress(data, selectors)` returns data elements where corresponding selector is truthy. Positions 0 and 2 have truthy selectors (1), so 'a' and 'c' are included. Like masking in NumPy.

---

## Chapter Summary

**Total MCQs: 60**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 9 | 15% |
| Intermediate | 39 | 65% |
| Advanced | 10 | 17% |
| Expert | 2 | 3% |

**Key Topics Covered:**
- Iterator protocol (__iter__, __next__)
- Generator functions and yield
- Generator expressions
- yield from delegation
- itertools module (comprehensive coverage)
- Lazy evaluation benefits
- Memory efficiency patterns
- Generator pipelines
- send(), throw(), close() methods
