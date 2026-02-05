# Chapter 13: Async Programming

> **Topics Covered**: async/await, asyncio event loop, coroutines, Tasks, futures, asyncio.gather, asyncio.wait, asyncio.create_task, asyncio.run, async context managers, async iterators, sync vs async, concurrency vs parallelism, common pitfalls

---

## Questions

---

**Q13.1: Basic - [Concurrency vs Parallelism]**

What's the difference between concurrency and parallelism?

A) Same thing
B) Concurrency = handling multiple tasks; parallelism = executing multiple tasks simultaneously
C) Parallelism is slower
D) Concurrency requires multiple CPUs

**Answer: B**

**Explanation:**
Concurrency: managing multiple tasks (interleaving). Parallelism: truly simultaneous execution (needs multiple cores). asyncio is concurrent on single thread. multiprocessing achieves parallelism. Concurrency without parallelism still improves I/O-bound tasks.

---

**Q13.2: Basic - [async/await Purpose]**

What problem does async/await solve?

A) Makes code faster always
B) Efficient handling of I/O-bound operations without blocking
C) Memory management
D) Type checking

**Answer: B**

**Explanation:**
I/O (network, file, DB) involves waiting. Traditional code blocks the thread. async/await lets other code run during waits. Single thread handles many connections efficiently. Not faster for CPU-bound work — use processes for that.

---

**Q13.3: Basic - [Coroutine Definition]**

What makes a function a coroutine?

A) Using `yield`
B) Using `async def`
C) Using `@coroutine` decorator
D) Returning a future

**Answer: B**

**Explanation:**
`async def` defines a coroutine function. Calling it returns a coroutine object (not executed yet). Must be awaited or run in event loop. Modern syntax since Python 3.5; replaces older generator-based coroutines.

---

**Q13.4: Basic - [Calling Coroutines]**

What is the output?
```python
async def greet():
    return "Hello"

result = greet()
print(type(result))
```

A) `str`
B) `coroutine`
C) `Hello`
D) Error

**Answer: B**

**Explanation:**
Calling `greet()` returns a coroutine object — NOT the result. The function body hasn't executed. To get "Hello", must await it: `await greet()` or `asyncio.run(greet())`. Warning usually printed about unawaited coroutine.

---

**Q13.5: Basic - [await Keyword]**

What does `await` do?

A) Makes function wait forever
B) Pauses coroutine until awaited object completes, allowing other tasks to run
C) Creates a new thread
D) Returns immediately

**Answer: B**

**Explanation:**
`await expression` suspends the current coroutine until the awaited coroutine/future completes. Control returns to event loop, which can run other tasks. When complete, execution resumes after await.

---

**Q13.6: Intermediate - [asyncio.run()]**

What is the output?
```python
import asyncio

async def main():
    return "Done"

result = asyncio.run(main())
print(result)
```

A) `<coroutine object>`
B) `Done`
C) `None`
D) Error

**Answer: B**

**Explanation:**
`asyncio.run(coro)` creates an event loop, runs the coroutine to completion, closes the loop, and returns the result. It's the "entry point" for async programs. Returns "Done" here.

---

**Q13.7: Intermediate - [asyncio.sleep()]**

What is the output (concept)?
```python
import asyncio

async def delayed():
    await asyncio.sleep(1)
    return "Hello"

result = asyncio.run(delayed())
print(result)
```

A) Prints immediately
B) Prints "Hello" after 1 second
C) Prints "Hello" and then waits
D) Never prints

**Answer: B**

**Explanation:**
`asyncio.sleep(1)` is an async sleep — suspends coroutine for 1 second without blocking. Program waits, then "Hello" is returned and printed. Unlike `time.sleep()`, allows other async tasks to run.

---

**Q13.8: Intermediate - [Concurrent Tasks]**

What is the benefit of this pattern?
```python
async def main():
    task1 = asyncio.create_task(fetch_data())
    task2 = asyncio.create_task(fetch_data())
    result1 = await task1
    result2 = await task2
```

A) Sequential execution
B) Both tasks run concurrently — total time closer to max(time1, time2)
C) Parallel execution
D) No benefit

**Answer: B**

**Explanation:**
`create_task()` schedules coroutines immediately. Both start running before awaits. If each takes 1 second, total ≈ 1 second (concurrent), not 2 seconds (sequential). Key async pattern.

---

**Q13.9: Intermediate - [asyncio.gather()]**

What is the output?
```python
import asyncio

async def say(msg, delay):
    await asyncio.sleep(delay)
    return msg

async def main():
    results = await asyncio.gather(
        say("A", 1),
        say("B", 2),
        say("C", 1)
    )
    print(results)

asyncio.run(main())
```

A) `['A', 'B', 'C']`
B) `['B', 'C', 'A']`
C) `['A', 'C', 'B']`
D) Error

**Answer: A**

**Explanation:**
`gather()` runs coroutines concurrently and returns results in the ORDER they were passed, not completion order. All three run concurrently; results collected after all complete. Order preserved: A, B, C.

---

**Q13.10: Intermediate - [gather with return_exceptions]**

What is the output?
```python
import asyncio

async def fail():
    raise ValueError("Error")

async def succeed():
    return "OK"

async def main():
    results = await asyncio.gather(
        fail(),
        succeed(),
        return_exceptions=True
    )
    print([type(r).__name__ for r in results])

asyncio.run(main())
```

A) Error raised
B) `['ValueError', 'str']`
C) `['OK']`
D) `['ValueError', 'OK']`

**Answer: B**

**Explanation:**
`return_exceptions=True` catches exceptions as results instead of propagating them. First result is ValueError exception, second is string "OK". Useful for handling partial failures.

---

**Q13.11: Intermediate - [asyncio.wait()]**

How does `asyncio.wait()` differ from `gather()`?

A) Same function
B) `wait()` returns (done, pending) sets; more control over completion handling
C) `wait()` is synchronous
D) `gather()` is deprecated

**Answer: B**

**Explanation:**
`wait()` returns two sets: completed tasks and pending tasks. Can specify `return_when=FIRST_COMPLETED` to handle as they finish. More flexible than gather but more complex. Returns Task objects, not results directly.

---

**Q13.12: Intermediate - [asyncio.create_task()]**

What does `asyncio.create_task(coro)` return?

A) Coroutine
B) Task object that's scheduled to run
C) Result of coroutine
D) Thread

**Answer: B**

**Explanation:**
`create_task()` wraps coroutine in a Task (a Future subclass), schedules it in the event loop, and returns the Task. The task runs "in background" until awaited or cancelled. Preferred way to run concurrent coroutines.

---

**Q13.13: Intermediate - [Task Cancellation]**

What is the output?
```python
import asyncio

async def long_task():
    try:
        await asyncio.sleep(10)
    except asyncio.CancelledError:
        print("Cancelled")
        raise

async def main():
    task = asyncio.create_task(long_task())
    await asyncio.sleep(0.1)
    task.cancel()
    try:
        await task
    except asyncio.CancelledError:
        print("Task was cancelled")

asyncio.run(main())
```

A) Nothing
B) `Cancelled` then `Task was cancelled`
C) Hangs for 10 seconds
D) Error

**Answer: B**

**Explanation:**
`task.cancel()` raises CancelledError inside the task. Task catches it, prints "Cancelled", re-raises. Awaiting cancelled task raises CancelledError in main. Pattern for graceful cancellation.

---

**Q13.14: Intermediate - [Event Loop]**

What is the event loop?

A) A while loop in code
B) The core that schedules and runs async tasks, manages I/O callbacks
C) A data structure
D) Thread manager

**Answer: B**

**Explanation:**
Event loop: the central scheduler. Runs tasks, handles I/O events, manages callbacks. `asyncio.run()` creates and runs one. Only one loop per thread. It selects ready coroutines and runs them until they await.

---

**Q13.15: Intermediate - [Running Sync in Async]**

How do you run blocking sync code in async context?

A) Just call it — it's fine
B) Use `loop.run_in_executor()` to run in thread/process pool
C) Use `await sync_function()`
D) Convert it to async

**Answer: B**

**Explanation:**
Blocking calls (time.sleep, file I/O, CPU work) block the event loop. `run_in_executor(None, func, *args)` runs in thread pool (default), returning awaitable. Keeps event loop responsive.

---

**Q13.16: Intermediate - [Async Context Manager]**

What methods define an async context manager?

A) `__enter__` and `__exit__`
B) `__aenter__` and `__aexit__`
C) `async_enter` and `async_exit`
D) Same as sync with await

**Answer: B**

**Explanation:**
Async context managers use `__aenter__` and `__aexit__` — both are coroutines. Used with `async with`. For async setup/teardown: connections, sessions. Both methods should be `async def`.

---

**Q13.17: Intermediate - [async with Example]**

What is the output?
```python
import asyncio

class AsyncResource:
    async def __aenter__(self):
        print("Entering")
        return self
    
    async def __aexit__(self, *args):
        print("Exiting")

async def main():
    async with AsyncResource() as r:
        print("Inside")

asyncio.run(main())
```

A) `Entering, Inside, Exiting`
B) `Inside, Entering, Exiting`
C) `Entering, Exiting, Inside`
D) Error

**Answer: A**

**Explanation:**
`async with` awaits `__aenter__` (prints "Entering"), executes block (prints "Inside"), awaits `__aexit__` (prints "Exiting"). Same flow as sync context manager but with async support.

---

**Q13.18: Intermediate - [Async Iterator]**

What methods define an async iterator?

A) `__iter__` and `__next__`
B) `__aiter__` and `__anext__`
C) `async_iter` and `async_next`
D) `yield` with async

**Answer: B**

**Explanation:**
`__aiter__` returns the async iterator (often self). `__anext__` returns awaitable that produces next value or raises `StopAsyncIteration`. Use with `async for`. Enables streaming data from async sources.

---

**Q13.19: Intermediate - [async for Example]**

What is the output?
```python
import asyncio

async def async_gen():
    for i in range(3):
        await asyncio.sleep(0.1)
        yield i

async def main():
    result = []
    async for x in async_gen():
        result.append(x)
    print(result)

asyncio.run(main())
```

A) `[0, 1, 2]`
B) `<async_generator>`
C) Error
D) `[]`

**Answer: A**

**Explanation:**
`async def` with `yield` creates an async generator. `async for` iterates over it, awaiting each value. Values 0, 1, 2 are yielded with delays. Result: [0, 1, 2].

---

**Q13.20: Advanced - [asyncio.Queue]**

What is `asyncio.Queue` for?

A) Data storage
B) Producer-consumer pattern with async puts/gets
C) Message queue
D) Priority sorting

**Answer: B**

**Explanation:**
`asyncio.Queue` is like queue.Queue but async. `await queue.put(item)` and `await queue.get()` are coroutines. Multiple producers/consumers can work concurrently. Common pattern for task distribution.

---

**Q13.21: Intermediate - [Common Mistake - Missing await]**

What is wrong here?
```python
async def fetch():
    return "data"

async def main():
    result = fetch()  # Missing await
    print(result)
```

A) Nothing wrong
B) Prints coroutine object instead of "data" — missing await
C) Raises error
D) Works but slow

**Answer: B**

**Explanation:**
⚠️ Common mistake: forgetting `await`. `fetch()` returns coroutine, not result. RuntimeWarning about unawaited coroutine. Always await coroutines: `result = await fetch()`.

---

**Q13.22: Intermediate - [Common Mistake - Blocking Call]**

What's wrong here?
```python
import time
import asyncio

async def slow():
    time.sleep(5)  # Not asyncio.sleep!
    return "done"

async def main():
    await asyncio.gather(slow(), slow())
```

A) Nothing wrong
B) `time.sleep` blocks the event loop — should use `asyncio.sleep`
C) Works correctly
D) faster than expected

**Answer: B**

**Explanation:**
⚠️ `time.sleep(5)` blocks the entire thread/event loop. Both tasks run sequentially (10 seconds total). Use `asyncio.sleep(5)` for non-blocking sleep. Always use async versions of I/O operations.

---

**Q13.23: Intermediate - [await in sync function]**

What is the output?
```python
async def async_func():
    return 42

def sync_func():
    result = await async_func()  # Wrong!
    return result
```

A) `42`
B) `SyntaxError: 'await' outside async function`
C) Works fine
D) Returns coroutine

**Answer: B**

**Explanation:**
`await` can only be used inside `async def` functions. Using it in regular function is a syntax error. To call async from sync: use `asyncio.run()` or `loop.run_until_complete()`.

---

**Q13.24: Intermediate - [Semaphore for Rate Limiting]**

What does this pattern do?
```python
semaphore = asyncio.Semaphore(10)

async def limited_fetch(url):
    async with semaphore:
        return await fetch(url)
```

A) Makes requests sequential
B) Limits concurrent requests to 10
C) Creates 10 threads
D) Nothing useful

**Answer: B**

**Explanation:**
Semaphore limits concurrent access. At most 10 coroutines inside `async with` block at once. Others wait. Useful for rate limiting, connection pools, resource management.

---

**Q13.25: Intermediate - [Lock for Mutual Exclusion]**

What is `asyncio.Lock` for?

A) File locking
B) Preventing concurrent access to shared state in async code
C) Thread locking
D) Database locks

**Answer: B**

**Explanation:**
`asyncio.Lock` ensures only one coroutine executes critical section at a time. Others await. Unlike thread locks, doesn't block — coroutines yield while waiting. Use `async with lock:`.

---

**Q13.26: Advanced - [asyncio.wait_for Timeout]**

What is the output?
```python
import asyncio

async def slow():
    await asyncio.sleep(10)
    return "done"

async def main():
    try:
        result = await asyncio.wait_for(slow(), timeout=1)
    except asyncio.TimeoutError:
        print("Timed out")

asyncio.run(main())
```

A) `done`
B) `Timed out`
C) Hangs 10 seconds
D) Error

**Answer: B**

**Explanation:**
`wait_for(coro, timeout)` cancels the coroutine if it takes longer than timeout seconds. After 1 second, TimeoutError is raised, task is cancelled. Prevents hanging on slow operations.

---

**Q13.27: Intermediate - [Task Result]**

What is the output?
```python
import asyncio

async def compute():
    return 42

async def main():
    task = asyncio.create_task(compute())
    await asyncio.sleep(0)  # Let task run
    print(task.result())

asyncio.run(main())
```

A) Error
B) `42`
C) `<coroutine>`
D) `Task`

**Answer: B**

**Explanation:**
`task.result()` returns the result if task completed successfully. After await lets task run, it completes with result 42. If task not done, raises InvalidStateError. If task raised exception, result() re-raises it.

---

**Q13.28: Advanced - [asyncio Patterns - Fan Out]**

What does "fan out" pattern mean in async?

A) Spreading code across files
B) Starting multiple concurrent operations from one source
C) Error handling
D) Closing connections

**Answer: B**

**Explanation:**
Fan out: one task spawns many concurrent tasks (e.g., fetch 100 URLs concurrently). Fan in: collecting results. Pattern: `tasks = [create_task(fetch(url)) for url in urls]; results = await gather(*tasks)`.

---

**Q13.29: Intermediate - [Event Loop Running]**

What is the output?
```python
import asyncio

async def say_hi():
    print("Hi")

loop = asyncio.new_event_loop()
loop.run_until_complete(say_hi())
loop.close()
```

A) Error
B) `Hi`
C) Nothing
D) `<coroutine>`

**Answer: B**

**Explanation:**
Lower-level API: `new_event_loop()` creates loop, `run_until_complete()` runs coroutine until done, `close()` cleans up. `asyncio.run()` does all this. This is the manual approach.

---

**Q13.30: Advanced - [Chaining Coroutines]**

What is the output?
```python
import asyncio

async def step1():
    return 10

async def step2(x):
    return x * 2

async def main():
    result = await step2(await step1())
    print(result)

asyncio.run(main())
```

A) `10`
B) `20`
C) Error
D) `<coroutine>`

**Answer: B**

**Explanation:**
Await expressions can be nested. `await step1()` returns 10, passed to `step2`. `await step2(10)` returns 20. Chaining coroutines is natural — await each in sequence.

---

**Q13.31: Intermediate - [Which to Use]**

When should you use `asyncio.gather` vs `asyncio.wait`?

A) Always use gather
B) gather for simple "run all"; wait for more control (first completed, cancellation)
C) wait is deprecated
D) No difference

**Answer: B**

**Explanation:**
`gather`: simple — run all, get results in order. `wait`: powerful — return_when options, access to pending tasks, better cancellation control. Use gather for common cases, wait for complex scheduling.

---

**Q13.32: Intermediate - [Shield from Cancellation]**

What does `asyncio.shield(coro)` do?

A) Prevents all errors
B) Protects coroutine from cancellation — outer cancel doesn't cancel shielded task
C) Creates backup
D) Encrypts task

**Answer: B**

**Explanation:**
`await shield(coro)` — if containing task is cancelled, the shielded task continues running. Useful for critical operations that must complete (cleanup, saving state). The shielded task runs independently.

---

**Q13.33: Advanced - [Current Task]**

How do you get the currently running task?

A) `asyncio.current_task()`
B) `asyncio.running_task()`
C) `asyncio.this_task()`
D) `self`

**Answer: A**

**Explanation:**
`asyncio.current_task()` returns the Task running in the current coroutine. Returns None if not in async context. Useful for introspection, logging, debugging. Also `asyncio.all_tasks()` for all tasks.

---

**Q13.34: Intermediate - [aiohttp for HTTP]**

Why use `aiohttp` instead of `requests`?

A) aiohttp is faster inherently
B) aiohttp is async — allows concurrent HTTP requests without blocking
C) requests is deprecated
D) aiohttp has more features

**Answer: B**

**Explanation:**
`requests` library is synchronous — blocks during HTTP calls. `aiohttp` is async — use with await, allows concurrent requests. For async web scraping/APIs handling many connections, aiohttp is essential.

---

**Q13.35: Advanced - [Debug Mode]**

What does `asyncio.run(main(), debug=True)` do?

A) Adds print statements
B) Enables extra checks: slow callbacks, unawaited coroutines, etc.
C) Pauses execution
D) Nothing different

**Answer: B**

**Explanation:**
Debug mode: warns about slow callbacks (>100ms), unawaited coroutines, wrong thread access. Helps find async bugs. Also set via `PYTHONASYNCIODEBUG=1` environment variable.

---

**Q13.36: Intermediate - [to_thread]**

What does `asyncio.to_thread(func, *args)` do? (Python 3.9+)

A) Creates a thread
B) Runs blocking function in thread pool, returns awaitable
C) Converts function to async
D) Threads the event loop

**Answer: B**

**Explanation:**
`await to_thread(blocking_func, arg1, arg2)` runs the blocking function in a thread pool executor. Cleaner than `run_in_executor`. Perfect for calling sync libraries from async code.

---

**Q13.37: Advanced - [Exception Handling in Tasks]**

What happens if a task raises an exception and is never awaited?

A) Program crashes
B) Exception is stored in task; warning printed when task is garbage collected
C) Exception is ignored
D) Event loop stops

**Answer: B**

**Explanation:**
Unhandled task exceptions don't crash. When task is GC'd without result being retrieved, "Task exception was never retrieved" warning appears. Always handle task results or use exception handlers.

---

**Q13.38: Intermediate - [Task Groups]**

What is `asyncio.TaskGroup` (Python 3.11+)?

A) Groups of unrelated tasks
B) Structured concurrency — ensures all tasks complete or all are cancelled on error
C) Task categories
D) Threading groups

**Answer: B**

**Explanation:**
```python
async with asyncio.TaskGroup() as tg:
    tg.create_task(coro1())
    tg.create_task(coro2())
```
If any task fails, all are cancelled. Ensures no "orphan" tasks. Structured concurrency pattern for cleaner error handling.

---

**Q13.39: Advanced - [asyncio vs threading]**

When use asyncio vs threading?

A) asyncio for I/O-bound; threading for CPU-bound
B) asyncio for single-threaded high concurrency I/O; threading for blocking calls or parallelism
C) Always use threading
D) Always use asyncio

**Answer: B**

**Explanation:**
asyncio: great for I/O-bound with many connections (web servers, scrapers). Single thread, no GIL issues. Threading: for parallelizing blocking calls, CPU-bound (though multiprocessing is better for CPU). Can combine both.

---

**Q13.40: Intermediate - [Writing Async Libraries]**

What's the key rule when writing async library code?

A) Always use threads
B) Never call blocking operations — they block the entire event loop
C) Use global state
D) Avoid await

**Answer: B**

**Explanation:**
Async library code must never block. Use async I/O libraries (aiohttp, asyncpg), or run sync ops in executors. One blocking call can freeze all concurrent tasks. Test with debug mode.

---

**Q13.41: Intermediate - [Callback Based to Async]**

How to wrap callback-based API in async/await?

A) Not possible
B) Use `asyncio.Future` — set result in callback, await the future
C) Ignore callbacks
D) Use threading

**Answer: B**

**Explanation:**
Create Future, pass callback that calls `future.set_result(value)`. Await the future in async code. Pattern bridges old callback APIs to modern async/await. `loop.create_future()` creates the future.

---

**Q13.42: Advanced - [Run Multiple Event Loops]**

Can you run multiple event loops?

A) No, one per process
B) Yes, one per thread
C) Only with multiprocessing
D) No, one per program

**Answer: B**

**Explanation:**
One event loop per thread. Main thread typically runs the main loop. Other threads can have their own loops: `loop = asyncio.new_event_loop(); asyncio.set_event_loop(loop)`. Rarely needed but possible.

---

**Q13.43: Intermediate - [fire and forget]**

How to "fire and forget" a coroutine?

A) Just call it
B) Create task without awaiting: `asyncio.create_task(coro())`
C) Use threading
D) Not possible

**Answer: B**

**Explanation:**
`create_task()` schedules execution; you don't have to await immediately. Task runs in background. But handle exceptions somehow (callback, later await). Unawaited results generate warnings on GC.

---

**Q13.44: Advanced - [synchronize_async_generator]**

What is the issue with this?
```python
results = [x async for x in async_gen()]  # In sync code
```

A) Nothing wrong
B) SyntaxError — async for requires async context
C) Works fine
D) Performance issue

**Answer: B**

**Explanation:**
`async for` and async comprehensions require async context. Can't use in sync functions. Must be inside `async def`. Wrap in coroutine and use `asyncio.run()`.

---

**Q13.45: Intermediate - [asyncio.sleep(0)]**

What does `await asyncio.sleep(0)` do?

A) Nothing
B) Yields control to event loop — allows other tasks to run
C) Sleeps for 1 second
D) Error

**Answer: B**

**Explanation:**
`sleep(0)` is a "yield point" — suspends coroutine momentarily, letting event loop run other ready tasks. Then resumes. Useful for long CPU-bound async sections to avoid starving other tasks. Minimal overhead.

---

**Q13.46: Advanced - [Signal Handling]**

How do you handle SIGINT (Ctrl+C) gracefully in asyncio?

A) try/except KeyboardInterrupt
B) `loop.add_signal_handler()` or exception handling around run
C) Ignore it
D) Can't handle signals

**Answer: B**

**Explanation:**
`loop.add_signal_handler(signal.SIGINT, handler)` for custom handling. Or wrap `asyncio.run()` in try/except KeyboardInterrupt for cleanup. Graceful shutdown: cancel tasks, close connections.

---

**Q13.47: Intermediate - [Testing Async Code]**

How do you test async code with pytest?

A) Normal tests
B) Use `pytest-asyncio` and mark tests with `@pytest.mark.asyncio`
C) Can't test async
D) Use threading

**Answer: B**

**Explanation:**
```python
@pytest.mark.asyncio
async def test_something():
    result = await my_coroutine()
    assert result == expected
```
`pytest-asyncio` plugin handles event loop setup/teardown. Makes testing async code straightforward.

---

**Q13.48: Advanced - [Async Generators Cleanup]**

What's special about async generator cleanup?

A) Nothing special
B) Must be properly closed with `await agen.aclose()` or context manager
C) Auto-cleaned
D) Can't be cleaned

**Answer: B**

**Explanation:**
Async generators need explicit cleanup for finally blocks to run. GC isn't synchronous enough. Use `async with aclosing(agen):` from contextlib. Or explicitly `await agen.aclose()`. Prevents resource leaks.

---

**Q13.49: Intermediate - [Error in gather]**

What happens if one coroutine in `gather()` raises (default behavior)?

A) All continue
B) gather raises the exception, pending tasks cancelled
C) Only that one fails
D) Returns None for failed

**Answer: B**

**Explanation:**
Default: exception propagates, other tasks are cancelled. With `return_exceptions=True`: exception becomes result, others continue. Design decision based on whether partial failure is acceptable.

---

**Q13.50: Advanced - [Performance Pitfall]**

Why is this slow?
```python
for url in urls:
    result = await fetch(url)  # Sequential!
```

A) It's fast
B) Sequential awaits — each waits for previous to complete
C) Too many awaits
D) Memory issue

**Answer: B**

**Explanation:**
⚠️ Sequential awaits = no concurrency! Each fetch completes before next starts. For concurrency: `tasks = [fetch(url) for url in urls]; results = await gather(*tasks)`. Runs all fetches concurrently.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 8 | 16% |
| Intermediate | 32 | 64% |
| Advanced | 10 | 20% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- async/await syntax
- Coroutines and awaitables
- Event loop basics
- asyncio.run(), gather(), create_task(), wait()
- Async context managers and iterators
- Cancellation and timeouts
- Common pitfalls (blocking calls, missing await)
- Locks, semaphores, queues
- Testing async code
- TaskGroup (structured concurrency)
