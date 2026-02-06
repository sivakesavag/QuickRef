# Chapter 15: Concurrency & Parallelism

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: GIL, `threading`, `multiprocessing`, `concurrent.futures`, `asyncio` basics, Synchronization (`Lock`, `Event`), Race conditions, CPU vs I/O bound.

---

**Q15.1: Basic - [GIL Definition]**

What is the Global Interpreter Lock (GIL) in CPython?

A) A lock that prevents multiple threads from executing Python bytecodes at once.
B) A security feature to prevent code injection.
C) A lock that prevents multiple processes from running.
D) A memory garbage collector.

**Answer: A**

**Explanation:**
The GIL ensures that only one thread holds control of the Python interpreter at any one time, simplifying memory management (refcounting) but limiting CPU-bound parallelism.

---

**Q15.2: Intermediate - [I/O Bound vs CPU Bound]**

Threading is most effective for which type of tasks in Python?

A) CPU-bound tasks (e.g., matrix multiplication).
B) I/O-bound tasks (e.g., network requests, file I/O).
C) Tasks requiring heavy recursion.
D) Image processing.

**Answer: B**

**Explanation:**
For I/O-bound tasks, threads release the GIL while waiting for I/O, allowing other threads to run. CPU-bound tasks battle for the GIL, often making threading slower than serial execution due to switching overhead.

---

**Q15.3: Advanced - [ProcessPoolExecutor]**

To bypass the GIL and utilize multiple CPU cores for heavy computation, you should use:

A) `threading.Thread`
B) `asyncio`
C) `multiprocessing` (or `ProcessPoolExecutor`)
D) `subprocess.run`

**Answer: C**

**Explanation:**
Multiprocessing spawns separate Python processes, each with its own memory space and GIL, enabling true parallelism on multi-core CPUs.

---

**Q15.4: Basic - [Starting a Thread]**

How do you start a thread `t = threading.Thread(target=func)`?

A) `t.run()`
B) `t.start()`
C) `t.init()`
D) `t.execute()`

**Answer: B**

**Explanation:**
`start()` schedules the thread to run and invokes the `run()` method in a separate thread of control. Calling `run()` directly executes it in the *current* thread (blocking).

---

**Q15.5: Intermediate - [Thread Join]**

`t.join()` does what?

A) Adds the thread to a pool.
B) Merges the thread's memory.
C) Blocks the calling thread until thread `t` terminates.
D) Kills thread `t`.

**Answer: C**

**Explanation:**
Used to wait for a thread to finish its work before proceeding.

---

**Q15.6: Advanced - [Race Condition]**

A race condition occurs when:

A) Two threads run at different speeds.
B) One thread finishes before another.
C) Multiple threads access/modify shared state concurrently without synchronization, leading to unpredictable results.
D) The GIL is released.

**Answer: C**

**Explanation:**
It is a bug where the output depends on the timing of uncontrolled events (e.g. `x += 1` is not atomic).

---

**Q15.7: Basic - [Asyncio Keywords]**

Which keywords are used for defining and waiting on coroutines?

A) `def / yield`
B) `async def / await`
C) `coroutine / wait`
D) `thread / join`

**Answer: B**

**Explanation:**
Modern Python (3.5+) uses `async def` to define a native coroutine and `await` to pause execution until a future/coroutine completes.

---

**Q15.8: Intermediate - [Lock Usage]**

`lock.acquire()` and `lock.release()` are best used with:

A) A `try...finally` block or a `with` statement.
B) An `if` statement.
C) A `while` loop.
D) `asyncio`.

**Answer: A**

**Explanation:**
Using `with lock:` ensures the lock is released even if an exception occurs inside the critical section, preventing deadlocks.

---

**Q15.9: Advanced - [Daemon Threads]**

If a thread is set as `daemon=True`:

A) It runs with higher priority.
B) It cannot access files.
C) The program exits without waiting for this thread to finish.
D) It survives after the main program exits.

**Answer: C**

**Explanation:**
Daemon threads are background threads. The Python interpreter exits as soon as all non-daemon threads have completed, killing any remaining daemon threads abruptly.

---

**Q15.10: Expert - [Queue Thread Safety]**

Is `queue.Queue` thread-safe?

A) No, you must use locks.
B) Yes, it handles locking internally.
C) Only for integers.
D) Only `SimpleQueue`.

**Answer: B**

**Explanation:**
The `queue` module provides thread-safe, multi-producer, multi-consumer queues, which are the preferred way to communicate between threads.

---

**Q15.11: Basic - [Multiprocessing Main Guard]**

Why is `if __name__ == '__main__':` required when using `multiprocessing` on Windows?

A) To prevent infinite recursive spawning of processes.
B) It is a style guide recommendation.
C) To import faster.
D) To enable the GIL.

**Answer: A**

**Explanation:**
On Windows (and MacOS relying on 'spawn'), new processes import the main module. Without the guard, the import triggers a new process, which imports again, causing an infinite loop (RuntimeError).

---

**Q15.12: Intermediate - [Executor Map]**

`executor.map(func, iterable)`:

A) Returns a list immediately.
B) Returns an iterator that yields results in the order of the input iterable.
C) Returns results as they finish (out of order).
D) Runs strictly sequentially.

**Answer: B**

**Explanation:**
It preserves the order of inputs in the results, iterating as results become available (potentially buffering).

---

**Q15.13: Advanced - [Asyncio Gather]**

`asyncio.gather(*coros)` is used to:

A) Run multiple coroutines concurrently and return their results as a list.
B) Select the first one that finishes.
C) Gather thread results.
D) Stop the event loop.

**Answer: A**

**Explanation:**
It schedules the coroutines in the event loop and waits for all to complete.

---

**Q15.14: Basic - [Sleep]**

`time.sleep(1)` blocks:

A) Only the current thread.
B) The entire process (all threads).
C) The CPU.
D) The GIL.

**Answer: A**

**Explanation:**
It suspends the calling thread, releasing the GIL so other threads can run.

---

**Q15.15: Intermediate - [Event Object]**

`threading.Event` is used for:

A) Triggering callbacks.
B) Simple communication between threads where one sets a flag and others wait for it.
C) Logging events.
D) Handling exceptions.

**Answer: B**

**Explanation:**
Objects wait on `event.wait()`. When another thread calls `event.set()`, all waiting threads wake up.

---

**Q15.16: Advanced - [ThreadPoolExecutor vs ProcessPoolExecutor]**

ThreadPoolExecutor is lighter weight but limited by GIL. ProcessPoolExecutor has higher overhead but bypasses GIL.
Which overhead is significant in ProcessPool?

A) Thread creation.
B) Serialization (pickling) of data sent to/from processes.
C) Context switching.
D) Memory allocation.

**Answer: B**

**Explanation:**
Inter-process communication requires pickling arguments and return values, which can be expensive if data is large.

---

**Q15.17: Expert - [RLock logic]**

If a thread acquires a normal `Lock` twice, it deadlocks. What about `RLock`?

A) It deadlocks.
B) It allows it, but requires an equal number of release calls.
C) It allows it and releases immediately on first release.
D) It raises RuntimeError.

**Answer: B**

**Explanation:**
A Reentrant Lock can be acquired multiple times by the *same* thread. It maintains a recursion level counter and is only effectively released when the counter reaches zero.

---

**Q15.18: Intermediate - [Future Object]**

A `Future` returned by `executor.submit()` allows you to:

A) Cancel the task (if not started).
B) Check if it is done (`done()`).
C) Get the result or exception (`result()`).
D) All of the above.

**Answer: D**

**Explanation:**
It represents the eventual result of an asynchronous computation.

---

**Q15.19: Basic - [Async Sleep]**

Inside an `async def` function, to wait for 1 second non-blocking:

A) `time.sleep(1)`
B) `await asyncio.sleep(1)`
C) `yield 1`
D) `asyncio.wait(1)`

**Answer: B**

**Explanation:**
`time.sleep` blocks the entire loop. `asyncio.sleep` suspends the coroutine, allowing the loop to run other tasks.

---

**Q15.20: Advanced - [Semaphore]**

A `Semaphore` initialized with 3 allows:

A) Only 3 threads to exist.
B) At most 3 threads to enter a critical section simultaneously.
C) 3 Locks to be created.
D) 3 processes.

**Answer: B**

**Explanation:**
It manages an internal counter decrementing on `acquire` and incrementing on `release`. Useful for rate limiting or connection pooling.

---

**Q15.21: Expert - [Run In Executor]**

To run a blocking I/O call (like `requests.get`) inside an asyncio loop without freezing it:

A) Just call it.
B) Use `await requests.get(...)`.
C) Use `await loop.run_in_executor(None, requests.get, ...)` (or `asyncio.to_thread`).
D) Use `asyncio.create_task`.

**Answer: C**

**Explanation:**
Since standard blocking calls do not support await, you must offload them to a thread pool (default executor) so the main event loop remains responsive.

---

**Q15.22: Intermediate - [Process Shared Memory]**

`multiprocessing.Value('i', 0)` creates:

A) An integer 0 in the current process only.
B) An immutable integer.
C) A shared, process-safe integer (stored in shared memory).
D) A copy of 0 for each process.

**Answer: C**

**Explanation:**
It allocates a ctypes object in shared memory that different processes can read/write (usually requiring a lock).

---

**Q15.23: Basic - [Current Thread]**

To get the current thread object:

A) `threading.current_thread()`
B) `threading.get_ident()`
C) `threading.this()`
D) `self`

**Answer: A**

**Explanation:**
Returns the `Thread` object corresponding to the caller's thread of control.

---

**Q15.24: Advanced - [Deadlock]**

A minimal deadlock involves:

A) One lock held forever.
B) Two threads, where T1 holds LockA waiting for LockB, and T2 holds LockB waiting for LockA.
C) An infinite loop.
D) GIL contention.

**Answer: B**

**Explanation:**
Circular dependency on resources.

---

**Q15.25: Intermediate - [Asyncio Run]**

The standard entry point to run a top-level coroutine `main()` in asyncio (Python 3.7+) is:

A) `main().start()`
B) `asyncio.run(main())`
C) `asyncio.get_event_loop().run_until_complete(main())` (Old way).
D) `await main()`

**Answer: B**

**Explanation:**
`asyncio.run()` handles creating the loop, running the coroutine, and closing the loop/cleanup.

---

**Q15.26: Expert - [ThreadPool Exception]**

If a task submitted to `ThreadPoolExecutor` raises an exception:

A) The program crashes immediately.
B) The exception is printed to stderr.
C) The exception is captured and raised when you call `future.result()`.
D) It is ignored silently.

**Answer: C**

**Explanation:**
Exceptions in concurrent futures are swallowed until you explicit retrieve the result.

---

**Q15.27: Basic - [CPU Count]**

To find the number of logical CPUs:

A) `sys.cpu_count`
B) `os.cpu_count()` (or `multiprocessing.cpu_count()`)
C) `threading.count()`
D) `psutil.cpu()`

**Answer: B**

**Explanation:**
Useful for determining the size of a process pool.

---

**Q15.28: Advanced - [Barrier]**

`threading.Barrier(n)` is used to:

A) Block threads until `n` threads have reached the barrier.
B) Limit threads to `n`.
C) Protect memory.
D) Stop threads.

**Answer: A**

**Explanation:**
Synchronization primitive where threads wait for each other to reach a common point before proceeding simultaneously.

---

**Q15.29: Intermediate - [Timer Thread]**

`threading.Timer(5.0, func).start()`:

A) Runs `func` every 5 seconds.
B) Waits 5 seconds, then runs `func` in a new thread.
C) Pauses current thread for 5 seconds.
D) Counts time.

**Answer: B**

**Explanation:**
It's a one-shot delayed execution.

---

**Q15.30: Expert - [GIL Release]**

Which C-API macro allows extension modules to release the GIL?

A) `Py_BEGIN_ALLOW_THREADS` / `Py_END_ALLOW_THREADS`
B) `Py_UNLOCK_GIL`
C) `Py_RELEASE`
D) `PyEval_ReleaseLock`

**Answer: A**

**Explanation:**
C extensions (like NumPy) use these macros around long-running C operations to let other Python threads run.

---

**Q15.31: Intermediate - [Atomic Operation]**

Which of the following operations is atomic in CPython (thread-safe without locks)?

A) `x += 1`
B) `L.append(x)`
C) `x = x + 1`
D) `d[key] += 1`

**Answer: B**

**Explanation:**
`L.append(x)` is a single bytecode instruction (`LIST_APPEND`) and is atomic. Augment assignments like `x += 1` involve reading, adding, and writing back, which can be interrupted.

---

**Q15.32: Advanced - [Asyncio Task]**

`asyncio.create_task(coro())`:

A) Runs the coroutine immediately (blocking).
B) Schedules the execution of the coroutine wrapped in a `Task` and returns the Task object immediately.
C) Waits for the coroutine to finish.
D) Creates a thread.

**Answer: B**

**Explanation:**
It runs the coroutine concurrently in the background and returns a handle (Task) to await or cancel it later.

---

**Q15.33: Basic - [Multiprocessing Pipe]**

`Pipe()` returns:

A) A single connection object.
B) A pair of connection objects `(conn1, conn2)` representing the two ends of the pipe.
C) A specialized Queue.
D) A shared memory block.

**Answer: B**

**Explanation:**
It creates a duplex (two-way) pipe by default, returning two Connection objects.

---

**Q15.34: Expert - [Condition Variable]**

`threading.Condition` is useful when:

A) You need a simple lock.
B) Threads need to wait for a specific condition to be true (signaled by another thread) while holding a lock.
C) You need to count threads.
D) You want to stop all threads.

**Answer: B**

**Explanation:**
It combines a Lock with a "wait" loop. One thread waits (releasing the lock) until another thread notifies that state has changed.

---

**Q15.35: Intermediate - [Async With]**

`async with lock:` is valid if:

A) `lock` is `threading.Lock`.
B) `lock` is `asyncio.Lock`.
C) `lock` is a context manager.
D) `lock` is a function.

**Answer: B**

**Explanation:**
Standard threading locks block the entire thread/loop. Asyncio code must use `asyncio.Lock` which suspends the coroutine (await) instead of blocking the thread.

---

**Q15.36: Advanced - [Executor Shutdown]**

`executor.shutdown(wait=True)`:

A) Kills all tasks immediately.
B) Signals the executor to free resources but waits for pending futures to complete.
C) Stops accepting new tasks but does not wait for pending ones.
D) Reboots the machine.

**Answer: B**

**Explanation:**
Standard cleanup method. It ensures all scheduled tasks finish before returning.

---

**Q15.37: Basic - [Async For]**

`async for item in gen:` works if `gen` is:

A) A standard generator.
B) An asynchronous generator (defines `__aiter__` and `__anext__`).
C) A list.
D) A thread.

**Answer: B**

**Explanation:**
Used to iterate over asynchronous iterators where getting the next item might involve I/O (awaiting).

---

**Q15.38: Intermediate - [Pool Starmap]**

`pool.starmap(func, [(1,2), (3,4)])` is equivalent to:

A) `[func((1,2)), func((3,4))]`
B) `[func(1,2), func(3,4)]`
C) `func(1, 2, 3, 4)`
D) `pool.map(func, [1, 2, 3, 4])`

**Answer: B**

**Explanation:**
`starmap` unpacks user arguments from the iterable elements, allowing you to pass multiple arguments to the target function (which `map` cannot easily do).

---

**Q15.39: Advanced - [ContextVar]**

`contextvars` (Python 3.7+) are primarily designed for:

A) Global variables.
B) Managing context-local state in asynchronous code (where thread-local storage fails).
C) Managing process state.
D) Storing configuration files.

**Answer: B**

**Explanation:**
`threading.local` doesn't work well with asyncio because multiple tasks run in the same thread. `ContextVar` ensures state is local to the asynchronous task.

---

**Q15.40: Expert - [Thread Abort]**

How do you forcibly kill a thread in Python from another thread?

A) `t.kill()`
B) `t.stop()`
C) `ctypes.pythonapi.PyThreadState_SetAsyncExc(...)` (Injecting an exception).
D) You cannot, reliably.

**Answer: D**

**Explanation:**
There is no standard, safe API to kill a thread because it could be holding locks or in a critical section, leading to corruption/deadlocks. Option C acts as a "hack" but is risky. The correct way is to use a flag (Event) to ask the thread to exit nicely.

---

**Q15.41: Intermediate - [Daemon Process]**

If a `multiprocessing.Process` is daemonized:

A) It can create children.
B) It cannot create child processes.
C) It runs forever.
D) It is invisible.

**Answer: B**

**Explanation:**
Daemon processes are not allowed to spawn children (orphan prevention complexity).

---

**Q15.42: Basic - [Queue Full]**

If `q = queue.Queue(maxsize=1)` and you call `q.put(2)` when it already has an item:

A) It raises `QueueFull` immediately.
B) It blocks until space is available.
C) It overwrites the old item.
D) It returns False.

**Answer: B**

**Explanation:**
Standard behavior for synchronous queues is to block the producer. Use `put_nowait` (or `block=False`) to raise exception.

---

**Q15.43: Advanced - [Asyncio To Thread]**

`asyncio.to_thread(func, *args)` (Python 3.9+):

A) Converts a thread to a coroutine.
B) Runs `func` in a separate thread and returns a coroutine to await the result.
C) Is deprecated.
D) Moves the event loop to a thread.

**Answer: B**

**Explanation:**
High-level convenience function to easily offload blocking work to a separate thread (internally uses `run_in_executor`).

---

**Q15.44: Expert - [Concurrent Future Exception]**

When using `as_completed(futures)`, if a future raised an exception, iterating over it:

A) Does not raise; you must call `future.result()` to see the exception.
B) Raises the exception immediately at the loop level.
C) Stops the loop.
D) Skips the future.

**Answer: A**

**Explanation:**
`as_completed` yields the *future* object itself. The exception is encapsulated. It is re-raised only when you call `future.result()`.

---

**Q15.45: Intermediate - [Multiprocessing Start Method]**

The default start method on macOS (since Python 3.8) and Windows is:

A) `fork`
B) `spawn`
C) `forkserver`
D) `thread`

**Answer: B**

**Explanation:**
`spawn` starts a fresh python interpreter process. `fork` (default on Linux) copies the parent process memory, which can be unsafe with threads (hence changed on macOS).

---

**Q15.46: Basic - [Main Thread]**

The `threading.main_thread()` function returns:

A) The thread that started the Python interpreter.
B) The currently running thread.
C) The biggest thread.
D) None.

**Answer: A**

**Explanation:**
Identifies the bootstrap thread.

---

**Q15.47: Advanced - [Event Loop Policy]**

To change the event loop implementation (e.g. use `uvloop`), you typically:

A) Recompile Python.
B) `asyncio.set_event_loop_policy(...)`
C) Edit `site-packages`.
D) Use a decorator.

**Answer: B**

**Explanation:**
Policies control how the event loop is created and accessed.

---

**Q15.48: Expert - [GIL Release I/O]**

Does the GIL get released during purely computational ctypes calls?

A) Yes, automatically.
B) No, unless the C code explicitly releases it.
C) Yes, if it takes > 5ms.
D) Only in Python 3.

**Answer: B**

**Explanation:**
The GIL is released automatically for I/O operations (by the OS level call wrapper), but for CPU-bound C extensions, the extension author *must* manually release it.

---

**Q15.49: Intermediate - [Queue Task Done]**

When using `queue.Queue`, `q.task_done()` is used to:

A) Mark a task as complete so `q.join()` knows progress.
B) Delete the queue.
C) Stop the consumer.
D) Return the result.

**Answer: A**

**Explanation:**
For every item `get()` from the queue, a call to `task_done()` tells the queue that processing on that item is complete. `join()` blocks until unfinished tasks drop to zero.

---

**Q15.50: Basic - [Priority Queue]**

`queue.PriorityQueue` retrieves items in:

A) FIFO order.
B) LIFO order.
C) Priority order (lowest valued entries first).
D) Random order.

**Answer: C**

**Explanation:**
Standard heap-based priority queue. Elements are typically tuples `(priority_number, data)`.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
