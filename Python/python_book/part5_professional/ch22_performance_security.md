# Chapter 22: Performance & Security

> **Topics Covered**: Profiling, optimization, cProfile, memory profiling, big-O complexity, security best practices, injection attacks, input validation, secrets management, cryptography basics, common vulnerabilities

---

## Questions

---

**Q22.1: Basic - [Premature Optimization]**

What is "premature optimization"?

A) Optimization that's too early in project
B) Optimizing before measuring — wasted effort on non-bottlenecks
C) Fast optimization
D) Good practice

**Answer: B**

**Explanation:**
"Premature optimization is the root of all evil" — Knuth. First: make it work correctly. Then: measure to find actual bottlenecks. Optimize only what matters. Guessing wastes time.

---

**Q22.2: Basic - [Profiling Purpose]**

Why profile code?

A) Make it run
B) Find actual bottlenecks — measure where time is spent
C) Documentation
D) Testing

**Answer: B**

**Explanation:**
Intuition about bottlenecks is often wrong. Profiling shows real data: which functions take most time, how many calls. Only optimize what profiler identifies as slow.

---

**Q22.3: Intermediate - [cProfile]**

What does `cProfile` do?

A) Compiles Python
B) Measures function call times and counts
C) Checks types
D) Memory profiling

**Answer: B**

**Explanation:**
`python -m cProfile script.py` or `cProfile.run('func()')`. Shows: total time, per-call time, call count per function. Standard library. Identify expensive functions.

---

**Q22.4: Intermediate - [cProfile Output]**

What does this cProfile output tell you?
```
ncalls  tottime  cumtime  filename:lineno(function)
1000    0.500    0.500    module.py:10(slow_func)
1       0.001    2.000    module.py:1(main)
```

A) main is slowest
B) slow_func takes 0.5s, called 1000 times — likely optimization target
C) No issues
D) 2 seconds total

**Answer: B**

**Explanation:**
`tottime` = time in function only. `cumtime` = including sub-calls. slow_func: 0.5s total over 1000 calls. main: 0.001s itself but 2s including calls. Optimize slow_func or reduce 1000 calls.

---

**Q22.5: Intermediate - [timeit Module]**

What is the output?
```python
import timeit
result = timeit.timeit('sum(range(100))', number=10000)
print(type(result))
```

A) `<class 'int'>`
B) `<class 'float'>` (total seconds for 10000 runs)
C) `<class 'str'>`
D) Error

**Answer: B**

**Explanation:**
`timeit` runs code many times, returns total time. For micro-benchmarks: `timeit.timeit(stmt, number=1000)`. Handles GC, warmup. More accurate than manual timing for small code.

---

**Q22.6: Intermediate - [Big-O Basics]**

What is O(n)?

A) Error notation
B) Linear time — time grows proportionally with input size
C) Optimal speed
D) Memory usage

**Answer: B**

**Explanation:**
O(n): double input → double time. O(1): constant. O(n²): double input → 4× time. O(log n): near-constant for large n. Describes algorithm scaling, not absolute speed.

---

**Q22.7: Intermediate - [Common Complexities]**

Match complexity to operation:
- List append
- List search
- Dict lookup
- Nested loops over list

A) All O(n)
B) Append O(1), search O(n), dict O(1), nested O(n²)
C) All O(1)
D) All O(log n)

**Answer: B**

**Explanation:**
Append: amortized O(1). Search (in): O(n) scan. Dict lookup: O(1) hash. Nested loops: inner loop runs n times for each outer iteration = O(n²). Know data structure complexities.

---

**Q22.8: Intermediate - [Algorithm Choice]**

Why is dict lookup faster than list search?

A) Magic
B) Dict uses hash table — O(1) average; list is O(n) linear scan
C) More memory
D) No difference

**Answer: B**

**Explanation:**
Hash table: compute hash → direct access. List: check each element until found. For 1M items: list search ~500K comparisons average, dict ~1 lookup. Use dicts/sets for membership.

---

**Q22.9: Intermediate - [Generator Memory]**

Why are generators memory-efficient?

A) Compression
B) Yield one item at a time — entire collection not in memory
C) Faster
D) No difference

**Answer: B**

**Explanation:**
`[x for x in range(1000000)]` creates list with 1M items in memory. `(x for x in range(1000000))` generates one at a time. Generators: O(1) memory for iteration.

---

**Q22.10: Intermediate - [Memory Profiling]**

How to profile memory usage?

A) cProfile
B) memory_profiler, tracemalloc (stdlib), objgraph
C) timeit
D) Not possible

**Answer: B**

**Explanation:**
`tracemalloc.start(); tracemalloc.get_traced_memory()` — tracks allocations. `memory_profiler`: line-by-line with `@profile`. Find memory leaks, high-memory functions.

---

**Q22.11: Intermediate - [String Concatenation]**

Why is this slow for many iterations?
```python
s = ""
for item in many_items:
    s += item
```

A) Not slow
B) String immutable — creates new string each time — O(n²) total
C) Memory leak
D) Type error

**Answer: B**

**Explanation:**
Each `+=` copies entire string plus new item. For n items: O(n²). Fix: `''.join(items)` builds once — O(n). Use list + join for string building.

---

**Q22.12: Intermediate - [Local Variables]**

Why are local variables faster than global?

A) Memory location
B) Lookup: local is optimized array index, global requires dict lookup
C) No difference
D) Less memory

**Answer: B**

**Explanation:**
CPython optimization: local variables are array positions (fast). Global/nonlocal require dict lookup. In hot loops, assign global to local: `local_func = global_func`. Micro-optimization.

---

**Q22.13: Intermediate - [Built-in Functions]**

Why prefer built-ins like `sum()`, `max()`?

A) Readability only
B) Implemented in C, much faster than Python loops
C) No difference
D) Required

**Answer: B**

**Explanation:**
Built-ins (sum, max, map, filter, sorted) are C code. Python loop = bytecode interpretation overhead. `sum(list)` faster than manual loop. Use built-ins when possible.

---

**Q22.14: Intermediate - [NumPy Performance]**

Why is NumPy faster for numeric operations?

A) Different language
B) Vectorized C operations on contiguous memory, no Python loop overhead
C) More memory
D) Compiled Python

**Answer: B**

**Explanation:**
`np.array * 2`: C loop over contiguous memory. Python `[x*2 for x in list]`: per-element Python overhead. 10-100× faster for large arrays. Use NumPy for numeric computation.

---

**Q22.15: Intermediate - [Caching Results]**

What does `@functools.lru_cache` do?

A) Clears cache
B) Caches function results — repeated calls with same args return cached value
C) Memory management
D) Type checking

**Answer: B**

**Explanation:**
Memoization: cache expensive function results. `@lru_cache(maxsize=128)` — LRU eviction. `fibonacci(n)` with cache: O(n) vs O(2^n). Trade memory for speed.

---

**Q22.16: Intermediate - [Lazy Evaluation]**

What is lazy evaluation?

A) Slow code
B) Compute values only when needed — generators, iterators
C) Delayed execution
D) Error handling

**Answer: B**

**Explanation:**
Eager: compute all upfront. Lazy: compute when accessed. Generators are lazy. Saves time if you don't need all results. Short-circuit: `first_match = next((x for x in items if condition), None)`.

---

**Q22.17: Intermediate - [slots for Memory]**

What is the memory saving with `__slots__`?

A) No saving
B) Removes instance __dict__ — significant for many small objects
C) Faster methods
D) Less code

**Answer: B**

**Explanation:**
```python
class Point:
    __slots__ = ['x', 'y']
```
No `__dict__` per instance. Saves ~40% memory for small objects. Million Point objects: major difference. Trade-off: can't add attributes dynamically.

---

**Q22.18: Intermediate - [Async Performance]**

When does async improve performance?

A) CPU-bound work
B) I/O-bound work — concurrent waiting instead of sequential
C) All code
D) Never

**Answer: B**

**Explanation:**
Async: multiple I/O operations "in flight" simultaneously. HTTP requests, database queries. One waits → run another. CPU-bound: use multiprocessing. Async doesn't speed up computation.

---

**Q22.19: Basic - [Security Mindset]**

What is the security mindset?

A) Trust users
B) Never trust input — validate, sanitize, assume malicious input
C) Use HTTPS only
D) Strong passwords

**Answer: B**

**Explanation:**
All input is suspect: user forms, APIs, files, environment. Validate types, ranges, formats. Sanitize for context (HTML, SQL). Defense in depth. Assume breach will happen.

---

**Q22.20: Intermediate - [SQL Injection]**

What's wrong here?
```python
cursor.execute(f"SELECT * FROM users WHERE id = {user_input}")
```

A) Nothing
B) SQL injection — user_input can contain SQL commands
C) Syntax error
D) Performance

**Answer: B**

**Explanation:**
`user_input = "1; DROP TABLE users"` → executes destructive SQL. Always use parameterized queries: `cursor.execute("SELECT * FROM users WHERE id = ?", (user_input,))`. Never format SQL with user input.

---

**Q22.21: Intermediate - [XSS Attack]**

What is XSS (Cross-Site Scripting)?

A) Cross-site requests
B) Attacker injects malicious JavaScript that runs in victim's browser
C) SQL attack
D) Password attack

**Answer: B**

**Explanation:**
User submits: `<script>stealCookies()</script>`. Displayed unescaped → runs in other users' browsers. Prevention: escape HTML output, Content-Security-Policy headers. Template engines typically auto-escape.

---

**Q22.22: Intermediate - [Input Validation]**

What should input validation check?

A) Only type
B) Type, format, length, range, allowed characters, business rules
C) Spelling
D) Nothing

**Answer: B**

**Explanation:**
Email: format + length. Age: integer, positive, reasonable range. Filename: no path traversal (`../`). Whitelist approach better than blacklist. Reject invalid input early with clear errors.

---

**Q22.23: Intermediate - [Path Traversal]**

What's the vulnerability here?
```python
filename = request.args['file']
with open(f'/uploads/{filename}') as f:
    return f.read()
```

A) Nothing
B) Path traversal — filename="../../../etc/passwd" reads system files
C) Slow
D) Memory issue

**Answer: B**

**Explanation:**
Attacker uses `../` to escape upload directory. Prevention: sanitize filename (`os.path.basename`), validate against whitelist, use random generated names, don't use user input directly in paths.

---

**Q22.24: Intermediate - [Command Injection]**

What's wrong here?
```python
os.system(f"convert {user_input} output.png")
```

A) Nothing
B) Command injection — user_input can include shell commands
C) Slow
D) Memory

**Answer: B**

**Explanation:**
`user_input = "file.jpg; rm -rf /"` executes destructive command. Use subprocess with list arguments: `subprocess.run(['convert', user_input, 'output.png'])`. Never shell=True with user input.

---

**Q22.25: Intermediate - [Password Hashing]**

Why use bcrypt/argon2 over SHA-256 for passwords?

A) Faster
B) Designed for passwords — intentionally slow, includes salt
C) More secure hash
D) Same thing

**Answer: B**

**Explanation:**
SHA-256: fast — attackers can try billions per second. bcrypt/argon2: intentionally slow (configurable), includes salt (no rainbow tables). Use `passlib` or `argon2-cffi`. Never roll your own.

---

**Q22.26: Intermediate - [Secrets Management]**

How to handle API keys and passwords?

A) In source code
B) Environment variables, secrets manager, never in git
C) Config file in repo
D) Database

**Answer: B**

**Explanation:**
Never commit secrets. Use: environment variables, `.env` files (gitignored), cloud secrets managers (AWS Secrets Manager, HashiCorp Vault). Rotate compromised secrets. Audit access.

---

**Q22.27: Intermediate - [HTTPS]**

Why is HTTPS important?

A) Faster
B) Encrypts traffic — prevents eavesdropping, MITM attacks
C) Looks professional
D) Required by law

**Answer: B**

**Explanation:**
HTTP: plaintext, anyone on network can read passwords, data. HTTPS: TLS encryption. Also: authenticity (certificate proves server identity). Always HTTPS for auth, sensitive data. Let's Encrypt for free certs.

---

**Q22.28: Intermediate - [CSRF Protection]**

How does CSRF token protection work?

A) Encrypts form
B) Server includes unique token in form, verifies on submit — proves request is from your form
C) User authentication
D) Rate limiting

**Answer: B**

**Explanation:**
Form includes hidden token. Submit: server checks token matches session. Attacker's form on different site doesn't have valid token. Most frameworks handle automatically.

---

**Q22.29: Intermediate - [Pickle Security]**

Why is unpickling dangerous?

A) Slow
B) Pickle can execute arbitrary code during deserialization
C) Large files
D) Not dangerous

**Answer: B**

**Explanation:**
⚠️ Pickle can contain code that runs on load. Never unpickle untrusted data (user uploads, external APIs). Use JSON for external data. Sign pickled data if necessary.

---

**Q22.30: Intermediate - [Secure Random]**

Which should you use for security tokens?
```python
# A
import random
token = random.randint(0, 1000000)

# B
import secrets
token = secrets.token_hex(16)
```

A) A is better
B) B is better — cryptographically secure
C) Same
D) Neither

**Answer: B**

**Explanation:**
`random` module: predictable (pseudorandom), not for security. `secrets`: cryptographically secure random. Use for: passwords, tokens, session IDs, anything security-related.

---

**Q22.31: Intermediate - [Dependency Vulnerabilities]**

How to check for vulnerable dependencies?

A) Manual review
B) Tools: pip-audit, safety, dependabot, snyk
C) Not possible
D) Update everything blindly

**Answer: B**

**Explanation:**
Dependencies have vulnerabilities. `pip-audit` checks against vulnerability database. Dependabot/Renovate auto-update. Regular audits. Don't use unmaintained packages for security-critical code.

---

**Q22.32: Intermediate - [Timing Attacks]**

What is a timing attack?

A) Slow code
B) Measuring response time to extract information — e.g., password correct letters faster
C) DoS attack
D) Clock attack

**Answer: B**

**Explanation:**
Naive string comparison: returns early on first mismatch. Attacker measures: "a" slower than "b"? First char is "a". Prevention: `secrets.compare_digest()` — constant-time comparison.

---

**Q22.33: Intermediate - [Session Security]**

What makes sessions secure?

A) Long session ID
B) Secure random ID, HTTPS-only, httponly flag, short expiration
C) User password
D) Server-side only

**Answer: B**

**Explanation:**
Session ID: secrets.token_hex (unpredictable). Cookie flags: Secure (HTTPS only), HttpOnly (no JS access), SameSite. Short expiration. Server-side session storage. Regenerate ID on login.

---

**Q22.34: Intermediate - [Rate Limiting Purpose]**

What attacks does rate limiting mitigate?

A) SQL injection
B) Brute force, DoS, scraping — limits requests per user/IP
C) XSS
D) Path traversal

**Answer: B**

**Explanation:**
Brute force: try thousands of passwords. Rate limit: max 5 attempts per minute. Also limits API abuse, scraping. Implement per-endpoint, per-user. Return 429 Too Many Requests.

---

**Q22.35: Intermediate - [Content Security Policy]**

What is CSP (Content-Security-Policy)?

A) Content compression
B) HTTP header that restricts what resources page can load — mitigates XSS
C) Cache policy
D) Privacy policy

**Answer: B**

**Explanation:**
`Content-Security-Policy: script-src 'self'` — only load scripts from same origin. Blocks injected scripts, inline JS. Defense-in-depth against XSS. Configure based on needs.

---

**Q22.36: Intermediate - [Error Messages Security]**

What's wrong with showing full tracebacks to users?

A) Nothing
B) Reveals internal structure, file paths, potentially sensitive data
C) Ugly only
D) Confusing

**Answer: B**

**Explanation:**
Tracebacks show: code structure, file paths, variable values, library versions. Attackers use for reconnaissance. Production: generic errors to users, detailed logs for developers.

---

**Q22.37: Intermediate - [Cryptography Basics]**

When to use encryption vs hashing?

A) Same thing
B) Encryption: need to decrypt (data at rest, transit). Hashing: one-way (passwords, checksums)
C) Always encryption
D) Always hashing

**Answer: B**

**Explanation:**
Encryption: reversible with key. Use for: storing sensitive data, HTTPS. Hashing: irreversible. Use for: passwords (verify without storing), file integrity. Different tools.

---

**Q22.38: Intermediate - [Fernet for Encryption]**

What is cryptography.Fernet?

A) FTP tool
B) Symmetric authenticated encryption — easy, secure encryption for Python
C) Hash function
D) Password storage

**Answer: B**

**Explanation:**
```python
from cryptography.fernet import Fernet
key = Fernet.generate_key()
f = Fernet(key)
encrypted = f.encrypt(b"data")
decrypted = f.decrypt(encrypted)
```
Symmetric: same key encrypts/decrypts. Authenticated: detects tampering. Recommended for simple encryption needs.

---

**Q22.39: Intermediate - [Principle of Least Privilege]**

What is least privilege?

A) Minimal code
B) Give only minimum permissions needed — limit damage from compromise
C) User privileges
D) Admin access

**Answer: B**

**Explanation:**
Database user: only permissions needed, not root. API key: scope to required operations. Process: non-root user. If compromised, damage is limited. Security fundamental.

---

**Q22.40: Intermediate - [Logging Security Events]**

What security events should be logged?

A) Everything
B) Login attempts, failures, permission changes, sensitive operations
C) Nothing for privacy
D) Only errors

**Answer: B**

**Explanation:**
Log: authentication attempts (success/fail), authorization failures, sensitive data access, admin actions. Don't log: passwords, tokens, PII unnecessarily. Audit trail for investigation.

---

**Q22.41: Intermediate - [subprocess Security]**

Which is safer?
```python
# A
subprocess.run(f"ls {user_input}", shell=True)

# B
subprocess.run(["ls", user_input])
```

A) A is safer
B) B is safer — no shell, can't inject commands
C) Same
D) Neither is safe

**Answer: B**

**Explanation:**
`shell=True`: command goes through shell, can inject. List form: arguments passed directly to program, each as separate argument. Still validate user_input, but no command injection.

---

**Q22.42: Intermediate - [eval() Danger]**

What's wrong with `eval(user_input)`?

A) Slow
B) Executes arbitrary Python code — complete system compromise
C) Syntax errors
D) Nothing

**Answer: B**

**Explanation:**
⚠️ `eval()` executes ANY Python code. User input could: `__import__('os').system('rm -rf /')`. NEVER eval user input. Use `ast.literal_eval()` for safe literal parsing (dicts, lists).

---

**Q22.43: Intermediate - [Memory Leak Detection]**

How to detect memory leaks?

A) Watch RAM
B) tracemalloc, memory_profiler, objgraph — track allocations over time
C) cProfile
D) Not possible

**Answer: B**

**Explanation:**
Memory leak: objects not freed, memory grows. `tracemalloc.compare_to(snapshot)` shows growth. `objgraph.show_growth()` shows object count changes. Common cause: caches without limits, circular references.

---

**Q22.44: Intermediate - [GC Impact]**

When might garbage collection impact performance?

A) Never
B) Many object allocations, cyclic structures — GC pauses can cause latency spikes
C) Always
D) Only in loops

**Answer: B**

**Explanation:**
GC runs periodically to free cyclic garbage. In latency-sensitive code: noticeable pauses. Solutions: `gc.disable()` if no cycles, `gc.freeze()` for long-lived objects, design to avoid cycles.

---

**Q22.45: Intermediate - [Security Headers]**

What are common security headers?

A) Only Content-Type
B) X-Frame-Options, X-Content-Type-Options, Strict-Transport-Security, CSP
C) Cache headers
D) CORS only

**Answer: B**

**Explanation:**
`X-Frame-Options: DENY` — prevent clickjacking. `X-Content-Type-Options: nosniff` — prevent MIME confusion. `Strict-Transport-Security` — force HTTPS. Add to all responses. Defense-in-depth.

---

**Q22.46: Intermediate - [Multithreaded Performance]**

Why doesn't threading speed up CPU-bound Python code?

A) It does
B) GIL allows only one thread to execute Python bytecode at a time
C) Thread overhead
D) Memory limits

**Answer: B**

**Explanation:**
GIL: only one thread runs Python code. Threading helps I/O-bound (threads wait on I/O). CPU-bound: use `multiprocessing` (separate processes, each with own GIL) or C extensions that release GIL.

---

**Q22.47: Intermediate - [Connection Pool Benefits]**

How do connection pools improve performance?

A) Faster connections
B) Reuse connections — avoid creation overhead per request
C) More connections
D) Security

**Answer: B**

**Explanation:**
Creating connections: TCP handshake, authentication, TLS negotiation. Pool: maintain N open connections, reuse for requests. Major speedup for database-heavy applications.

---

**Q22.48: Intermediate - [Optimization Checklist]**

Optimization priority order?

A) Guess and optimize
B) Measure → algorithm → data structures → caching → parallel → low-level
C) Low-level first
D) Random

**Answer: B**

**Explanation:**
1) Measure (profile). 2) Better algorithm (O(n²) → O(n log n)). 3) Right data structures. 4) Caching. 5) Parallel processing. 6) Low-level tricks last. Big wins first.

---

**Q22.49: Intermediate - [Security Audit]**

What should a security audit check?

A) Performance
B) Input validation, authentication, authorization, secrets, dependencies, logging
C) Code style
D) Documentation

**Answer: B**

**Explanation:**
Audit: input handling (injection), auth (bypass), secrets (exposure), dependencies (CVEs), access control, logging, error handling. Regular audits. Penetration testing for critical systems.

---

**Q22.50: Intermediate - [Defense in Depth]**

What is defense in depth?

A) Deep code
B) Multiple security layers — if one fails, others still protect
C) Complex security
D) Maximum encryption

**Answer: B**

**Explanation:**
Layers: input validation + parameterized queries + least privilege + WAF + monitoring. Each layer catches what others miss. Single point of failure: one bypass → complete compromise. Layer security.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 4 | 8% |
| Intermediate | 46 | 92% |
| Advanced | 0 | 0% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- Profiling with cProfile, timeit
- Big-O complexity
- Memory profiling
- Performance optimization techniques
- Security mindset and common attacks
- Input validation
- Secrets management
- Cryptography basics
- Common vulnerabilities (SQL injection, XSS, CSRF)
- Defense in depth
