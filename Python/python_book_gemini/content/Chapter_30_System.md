# Chapter 30: System Programming

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `ctypes`, `cffi` (Interfacing with C/C++), `socket` programming (TCP servers/clients), Signals (`signal`), Memory Management (`sys.getrefcount`, `gc`), OS interaction.

---

**Q30.1: Basic - [Ctypes]**

The `ctypes` library in Python is used to:

A) Call functions in shared libraries (DLLs/.so files) written in C.
B) Type text.
C) Check types.
D) Compile Python.

**Answer: A**

**Explanation:**
Part of the standard library for Foreign Function Interface (FFI).

---

**Q30.2: Intermediate - [Socket Create]**

To create a standard TCP socket, you use:

A) `s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)`
B) `s = socket.socket(socket.TCP)`
C) `s = socket.create_tcp()`
D) `s = socket.connect()`

**Answer: A**

**Explanation:**
`AF_INET` = IPv4, `SOCK_STREAM` = TCP.

---

**Q30.3: Advanced - [GIL Impact]**

With respect to system programming, the GIL (Global Interpreter Lock) primarily limits:

A) True parallelism of CPU-bound Python threads.
B) Disk I/O.
C) Network I/O.
D) Process creation.

**Answer: A**

**Explanation:**
But it does not block system calls or C extensions (if they release the GIL).

---

**Q30.4: Basic - [GC Enable]**

Python's Garbage Collector (`gc`) handles:

A) Automatic memory management (detecting and freeing reference cycles).
B) Collecting trash files.
C) Global Config.
D) Graphics.

**Answer: A**

**Explanation:**
Normally enabled by default. `gc.collect()` forces a run.

---

**Q30.5: Intermediate - [Socket Bind]**

Before a server can listen for connections, it must:

A) `bind()` to a specific address (IP) and port.
B) `connect()` to the client.
C) `send()`.
D) `close()`.

**Answer: A**

**Explanation:**
`s.bind(('localhost', 8080))`.

---

**Q30.6: Advanced - [Signal Handler]**

When you register a signal handler with `signal.signal(signal.SIGINT, handler)`, the handler function is called when:

A) The process receives an interrupt signal (usually Ctrl+C).
B) The signal is green.
C) The process starts.
D) The internet connects.

**Answer: A**

**Explanation:**
Allows for graceful shutdowns.

---

**Q30.7: Expert - [CFFI vs Ctypes]**

`cffi` (C Foreign Function Interface) is generally considered superior to `ctypes` for complex projects because:

A) It parses C header files directly (API mode) and can compile C extension modules (ABI mode), offering better performance and safer type checking (checking at compile time rather than runtime crashes).
B) It is built-in.
C) It is older.
D) It is simpler.

**Answer: A**

**Explanation:**
Used heavily by PyPy and cryptography libraries.

---

**Q30.8: Basic - [Sys Refcount]**

`sys.getrefcount(obj)` returns:

A) The number of references to `obj`.
B) The memory size.
C) The type.
D) The value.

**Answer: A**

**Explanation:**
Note: it returns one higher than expected because passing it to the function creates a temporary reference.

---

**Q30.9: Intermediate - [UDP Socket]**

For a UDP (User Datagram Protocol) socket, you use:

A) `socket.SOCK_DGRAM`
B) `socket.SOCK_STREAM`
C) `socket.SOCK_UDP`
D) `socket.SOCK_RAW`

**Answer: A**

**Explanation:**
Connectionless, unreliable (but fast) protocol.

---

**Q30.10: Advanced - [Memory View]**

A `memoryview` object allows:

A) Accessing the internal data of an object (like bytes/bytearray) without copying it (Zero-copy).
B) Viewing memory usage.
C) Creating memory.
D) Deleting memory.

**Answer: A**

**Explanation:**
Essential for high-performance I/O operations on large buffers.

---

**Q30.11: Basic - [Socket Listen]**

`s.listen(5)` on a server socket:

A) Enables the server to accept connections, with a backlog queue of 5 pending connections.
B) Listens for 5 seconds.
C) Connects to 5 servers.
D) Prints 5 lines.

**Answer: A**

**Explanation:**
The backlog controls how many clients can queue up before being refused.

---

**Q30.12: Intermediate - [Struct Module]**

The `struct` module (`struct.pack`, `struct.unpack`) is used to:

A) Convert between Python values and C structs represented as Python bytes (e.g., packing an integer into 4 bytes for network transmission).
B) Create classes.
C) Organize files.
D) Structure code.

**Answer: A**

**Explanation:**
Binary protocol implementation (e.g., `struct.pack('!I', 1024)`).

---

**Q30.13: Advanced - [Daemon Threads]**

A "Daemon Thread" (`thread.daemon = True`):

A) A thread that runs in the background and is automatically killed when the main program exits.
B) A superuser thread.
C) A persistent thread.
D) An evil thread.

**Answer: A**

**Explanation:**
Useful for background monitoring tasks that shouldn't prevent the program from closing.

---

**Q30.14: Expert - [Buffer Protocol]**

The "Buffer Protocol" allows Python objects to:

A) Expose their raw memory array to other Python objects (like C extensions or `memoryview`) for efficient access.
B) Buffer video.
C) Slow down execution.
D) Print buffers.

**Answer: A**

**Explanation:**
Underpins NumPy arrays and standard `bytes`.

---

**Q30.15: Intermediate - [Set Recursion Limit]**

`sys.setrecursionlimit(2000)`:

A) Increases the maximum depth of the Python interpreter stack (default is usually 1000).
B) Sets the loop limit.
C) Sets memory limit.
D) Disables recursion.

**Answer: A**

**Explanation:**
Dangerous if set too high (can cause C-level stack overflow/segfault).

---

**Q30.16: Basic - [Socket Accept]**

When a server calls `conn, addr = s.accept()`:

A) It blocks until a new client connects, returning a new socket object (`conn`) and the client's address (`addr`).
B) It accepts the terms of service.
C) It connects to the internet.
D) It crashes.

**Answer: A**

**Explanation:**
You communicate with the client using `conn`, not the original listener `s`.

---

**Q30.17: Advanced - [Mmap]**

The `mmap` module allows:

A) Memory-mapping a file, so it behaves like both a bytearray and a file object (accessing file content via memory addresses without reading the whole file into RAM).
B) Mapping the world.
C) Making maps.
D) GPS.

**Answer: A**

**Explanation:**
Extremely efficient for random access to large files.

---

**Q30.18: Expert - [Select Module]**

The `select` module (`select.select`) is used for:

A) I/O Multiplexing (monitoring multiple sockets to see which are ready for reading/writing) in a single thread.
B) Selecting text.
C) Database queries.
D) Choosing options.

**Answer: A**

**Explanation:**
The basis of event loops (though `selectors` or `asyncio` are modern wrappers).

---

**Q30.19: Intermediate - [Weakref]**

A `weakref` (Weak Reference) to an object:

A) Allows you to reference an object without increasing its reference count (so it can still be garbage collected).
B) Is a weak variable.
C) Is deprecated.
D) Is a copy.

**Answer: A**

**Explanation:**
Useful for caches to avoid memory leaks.

---

**Q30.20: Basic - [Send vs Sendall]**

For TCP sockets, `sendall(data)` is preferred over `send(data)` because:

A) `send()` might only send part of the data if buffers are full; `sendall()` loops until *all* data is sent.
B) It is faster.
C) It sends to all users.
D) It encrypts.

**Answer: A**

**Explanation:**
`send()` returns the number of bytes sent; you must check it.

---

**Q30.21: Advanced - [Subprocess Communicate]**

`stdout, stderr = process.communicate(input_data)`:

A) Sends input to the subprocess's stdin, closes it, and reads data from stdout/stderr until EOF.
B) Chats with the process.
C) Prints to screen.
D) Connects via wifi.

**Answer: A**

**Explanation:**
Prevents deadlocks compared to using `process.stdout.read()` directly.

---

**Q30.22: Intermediate - [Byteorder]**

`sys.byteorder` tells you:

A) The native byte order (endianness) of the system ('little' or 'big').
B) The size of a byte.
C) The memory limit.
D) The order of bytes in a string.

**Answer: A**

**Explanation:**
Important when exchanging binary data between different architectures.

---

**Q30.23: Expert - [Os Fork]**

`os.fork()` (on Unix):

A) Creates a child process that is an exact duplicate of the parent process.
B) Creates a thread.
C) Eats with a fork.
D) Splits the file.

**Answer: A**

**Explanation:**
Returns 0 in the child, and the child's PID in the parent.

---

**Q30.24: Basic - [Recv]**

Socekt `recv(1024)`:

A) Receives *up to* 1024 bytes from the socket.
B) Receives exactly 1024 bytes.
C) Waits 1024 seconds.
D) Sends 1024 bytes.

**Answer: A**

**Explanation:**
You often need to call it in a loop to get a full message.

---

**Q30.25: Intermediate - [Blocking vs Non-Blocking]**

If you set `socket.setblocking(False)`:

A) Socket operations (recv/send) will raise a `BlockingIOError` immediately if they cannot complete instantly, instead of waiting.
B) The socket stops working.
C) It blocks everything.
D) It becomes faster automatically.

**Answer: A**

**Explanation:**
Foundation for async I/O.

---

**Q30.26: Advanced - [Shared Memory]**

The `multiprocessing.shared_memory` module (Python 3.8+) allows:

A) Different processes to access the same block of memory directly, avoiding serialization overhead (pickling) when passing data.
B) Sharing ideas.
C) Global variables.
D) Network sharing.

**Answer: A**

**Explanation:**
Great for IPC with large numpy arrays.

---

**Q30.27: Expert - [Slots]**

Using `__slots__` in a class definition:

A) Saves memory by explicitly declaring data members and preventing the creation of `__dict__` for each instance.
B) Makes it slower.
C) Is for casino games.
D) Reserved for inheritance.

**Answer: A**

**Explanation:**
Optimization for classes with millions of instances.

---

**Q30.28: Intermediate - [Get Hostname]**

To get the name of the machine the script is running on:

A) `socket.gethostname()`
B) `os.name()`
C) `sys.platform()`
D) `socket.name()`

**Answer: A**

**Explanation:**
Returns the string hostname.

---

**Q30.29: Basic - [Waitpid]**

`os.waitpid(pid, options)`:

A) Waits for a child process with the given PID to execute/terminate.
B) Waits for input.
C) Waits for network.
D) Stops the OS.

**Answer: A**

**Explanation:**
Prevents "Zombie" processes.

---

**Q30.30: Advanced - [LSOF]**

While not a python function, the concept of "File Descriptors" (FD) is key in system programming. In Python, `sys.stdin.fileno()` returns:

A) The integer file descriptor (usually 0 for stdin).
B) The file name.
C) The content.
D) None.

**Answer: A**

**Explanation:**
0=stdin, 1=stdout, 2=stderr.

---

**Q30.31: Intermediate - [Thread vs Process]**

The main difference between a Thread and a Process in Python is:

A) Processes have their own separate memory space (no shared global variables by default, bypassing GIL), while Threads share the same memory space (subject to GIL).
B) Threads are faster.
C) Processes are smaller.
D) Threads are processes.

**Answer: A**

**Explanation:**
"Threads share memory; Processes share nothing (by default)."

---

**Q30.32: Advanced - [Sendfile]**

`os.sendfile(out, in, offset, count)`:

A) Copies data from one file descriptor to another *within the kernel* (Zero-copy), avoiding copying data to user-space buffers.
B) Sends a file via email.
C) Copies a file.
D) Deletes a file.

**Answer: A**

**Explanation:**
Highly efficient for static file servers (like Nginx uses).

---

**Q30.33: Basic - [Uname]**

To get system information (OS name, network node, release, version, machine):

A) `platform.uname()` (or `os.uname()` on Unix).
B) `os.info()`
C) `sys.info()`
D) `platform.info()`

**Answer: A**

**Explanation:**
Returns a `namedtuple`.

---

**Q30.34: Expert - [Setuid]**

`os.setuid(uid)` checks if:

A) The current process has appropriate privileges (usually root) to change its User ID.
B) The user is logged in.
C) The ID is valid.
D) The user is root.

**Answer: A**

**Explanation:**
Commonly used by daemons started as root to drop privileges to a less privileged user for security.

---

**Q30.35: Intermediate - [Socket Setsockopt]**

To allow a server to restart immediately on the same port (avoiding "Address already in use" error):

A) `s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)`
B) `s.restart(True)`
C) `s.reuse(True)`
D) `s.bind(..., reuse=True)`

**Answer: A**

**Explanation:**
Critical for development servers.

---

**Q30.36: Advanced - [Fcntl]**

The `fcntl` module allows:

A) Performing file control and I/O control on file descriptors (e.g., file locking `flock`, non-blocking flags).
B) Font control.
C) Function control.
D) File creation.

**Answer: A**

**Explanation:**
Unix-only tool for low-level file manipulation.

---

**Q30.37: Basic - [Shell False]**

When using `subprocess.run(['ls', '-l'])`, arguments are passed as a list. This implies:

A) `shell=False` (default), which is safer because arguments are passed directly to the OS exec function, avoiding shell parsing.
B) It will error.
C) It is slower.
D) It uses shell.

**Answer: A**

**Explanation:**
Always prefer list arguments over string arguments.

---

**Q30.38: Intermediate - [Memory Profiler]**

To profile memory usage line-by-line, the external library `memory_profiler` uses the decorator:

A) `@profile`
B) `@memory`
C) `@track`
D) `@log`

**Answer: A**

**Explanation:**
Prints memory consumption after each line execution.

---

**Q30.39: Advanced - [Socket Timeouts]**

`socket.settimeout(5.0)`:

A) Raises `socket.timeout` (a subclass of OSError) if any socket operation takes longer than 5 seconds.
B) Waits 5 seconds.
C) Closes socket.
D) Resets socket.

**Answer: A**

**Explanation:**
Essential for network robustness.

---

**Q30.40: Expert - [Epoll]**

`select.epoll()` (Linux only) is superior to `select()` because:

A) It scales to thousands of concurrent connections (O(1) vs O(N) scanning) and uses kernel notifications.
B) It is easier.
C) It is older.
D) It is pythonic.

**Answer: A**

**Explanation:**
The underlying mechanism for high-performance servers (Node.js, Nginx, Python asyncio).

---

**Q30.41: Basic - [Get Pid]**

To get the Process ID of the current running script:

A) `os.getpid()`
B) `os.pid()`
C) `sys.pid`
D) `process.id`

**Answer: A**

**Explanation:**
Unique integer identifier.

---

**Q30.42: Intermediate - [Kill Process]**

To terminate a process with PID 1234:

A) `os.kill(1234, signal.SIGTERM)`
B) `os.stop(1234)`
C) `sys.kill(1234)`
D) `process.kill(1234)`

**Answer: A**

**Explanation:**
Sends a signal (doesn't explicitly "kill" unless using SIGKILL).

---

**Q30.43: Advanced - [Tracemalloc]**

The standard library `tracemalloc` is used to:

A) Trace memory allocations and identify the source (file/line) of memory leaks.
B) Trace execution path.
C) Trace network packets.
D) Trace CPU usage.

**Answer: A**

**Explanation:**
Can compare two snapshots to see what memory was allocated in between.

---

**Q30.44: Expert - [Subprocess Preexec_fn]**

`subprocess.Popen(..., preexec_fn=os.setsid)` is commonly used to:

A) Make the child process a session leader (detaching from the parent's controlling terminal), essential for daemonizing.
B) Run code before execution.
C) Set the ID.
D) Nothing.

**Answer: A**

**Explanation:**
Ensures the subprocess doesn't receive signals sent to the parent group.

---

**Q30.45: Intermediate - [Endianness]**

`struct.pack('>I', 1024)`:

A) Packs the integer 1024 as a Big-Endian (Network Byte Order) 4-byte unsigned integer.
B) Packs as Little-Endian.
C) Packs as a String.
D) Errors.

**Answer: A**

**Explanation:**
`>` = Big-Endian, `<` = Little-Endian. Network protocols use Big-Endian.

---

**Q30.46: Basic - [Cpu Count]**

To find the number of CPU cores available:

A) `os.cpu_count()` (or `multiprocessing.cpu_count()`).
B) `sys.cpu()`
C) `platform.cpu()`
D) `os.cores()`

**Answer: A**

**Explanation:**
Useful for determining how many worker processes to spawn.

---

**Q30.47: Advanced - [Select Retry]**

When using `select()`, if it is interrupted by a signal (like SIGCHLD), it raises:

A) `InterruptedError` (errno.EINTR). You must retry the call.
B) `TimeoutError`.
C) `MemoryError`.
D) Nothing.

**Answer: A**

**Explanation:**
PEP 475 now handles this retry automatically in Python 3.5+, but historically a major pain point.

---

**Q30.48: Expert - [Os Umask]**

`os.umask(0o022)`:

A) Sets the file mode creation mask (permissions to *mask out* / remove) for new files.
B) Sets permissions.
C) Deletes files.
D) Hides files.

**Answer: A**

**Explanation:**
If umask is 022, new files (666) become 644 (rw-r--r--).

---

**Q30.49: Intermediate - [ContextVar]**

The `contextvars` module (Python 3.7+) is designed to:

A) Manage/store context-local state (like global variables but scoped to the current running async task/thread).
B) Variable context.
C) Store text.
D) Manage database.

**Answer: A**

**Explanation:**
Crucial for `asyncio` where "Thread Local" storages fail because multiple tasks share one thread.

---

**Q30.50: Basic - [Socket Close]**

Closing a socket with `s.close()`:

A) Releases the file descriptor and disconnects.
B) Ends the script.
C) Deletes the file.
D) Sends EOF.

**Answer: A**

**Explanation:**
Always close resources!

---

---

## Review Notes (2026-02-06)

- Question numbering mismatch: `Q29.29` appears inside Chapter 30 and should be renumbered to match chapter numbering.
