# Chapter 21: Cryptography & Security

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `secrets` module, `hashlib` (SHA/MD5), `hmac`, `base64`, `ssl` basics, Password hashing (concepts only + `bcrypt` mention), Randomness (`random` vs `secrets`), Safe temporary files (`tempfile`), Injection risks (`sql`, `shell`), `pickle` security.

---

**Q21.1: Basic - [Secrets Module]**

For generating cryptographically strong random numbers (e.g., tokens, passwords), use:

A) `random` module.
B) `secrets` module.
C) `math` module.
D) `os.urandom` directly only.

**Answer: B**

**Explanation:**
`secrets` (introduced in Python 3.6) is designed specifically for security, whereas `random` uses a Mersenne Twister which is predictable.

---

**Q21.2: Intermediate - [Hashlib Algorithms]**

Which hashing algorithm is considered broken and unsafe for security signatures?

A) SHA-256
B) SHA-3
C) MD5 (and SHA-1)
D) BLAKE2

**Answer: C**

**Explanation:**
MD5 and SHA-1 have known collision vulnerabilities. Use SHA-256 or better for security.

---

**Q21.3: Advanced - [HMAC]**

`hmac` stands for:

A) Hash-based Message Authentication Code.
B) High Memory Access Code.
C) Hashed Memory Allocation.
D) Heavy Metal Access Control.

**Answer: A**

**Explanation:**
It combines a cryptographic hash function with a secret key to verify both data integrity and authenticity.

---

**Q21.4: Basic - [Base64 Encoding]**

`base64` encoding is used to:

A) Encrypt data.
B) Compress data.
C) Represent binary data in an ASCII string format (e.g., for email/URL).
D) Hide data.

**Answer: C**

**Explanation:**
It is an encoding scheme, *not encryption*. It provides no security, just transport compatibility.

---

**Q21.5: Intermediate - [Pickle Security]**

Unpickling data received from an untrusted source is:

A) Safe if checked.
B) A major security risk (Arbitrary Code Execution).
C) Safe in Python 3.
D) Recommended.

**Answer: B**

**Explanation:**
`pickle` can deserialize arbitrary objects and execute their `__reduce__` logic, allowing attackers to run shell commands. Never unpickle untrusted data.

---

**Q21.6: Advanced - [Password Storage]**

When storing user passwords, you should store:

A) Plain text.
B) Simple Hash (SHA-256).
C) Encrypted text.
D) Salted and Peppered Hash using a slow algorithm (e.g., bcrypt, Argon2, PBKDF2).

**Answer: D**

**Explanation:**
Simple hashes are vulnerable to rainbow tables. Slow algorithms make brute-forcing expensive.

---

**Q21.7: Basic - [Random Seed]**

Setting `random.seed(42)` makes `random` output:

A) Unpredictable.
B) Deterministic (reproducible).
C) Stronger.
D) Slower.

**Answer: B**

**Explanation:**
Useful for tests/simulations, but fatal for security. Never seed a generator used for crypto.

---

**Q21.8: Intermediate - [SSL Context]**

`ssl.create_default_context()`:

A) Creates an insecure context.
B) Creates a context with recommended security settings (CA certificates, hostname check).
C) Is deprecated.
D) Creates a blank context.

**Answer: B**

**Explanation:**
The best practice for modern TLS connections in Python (e.g., for `urllib` or `http.client`).

---

**Q21.9: Advanced - [Timing Attack]**

`hmac.compare_digest(a, b)` is better than `a == b` for checking passwords/hashes because:

A) It is faster.
B) It takes constant time, preventing timing analysis attacks.
C) It ignores case.
D) It supports None.

**Answer: B**

**Explanation:**
Standard `==` returns False as soon as a mismatch is found (leaking length of common prefix). `compare_digest` checks all bytes to normalize the check duration.

---

**Q21.10: Expert - [Secrets Compare]**

`secrets.compare_digest` is an alias for:

A) `hmac.compare_digest`
B) `os.compare`
C) `random.compare`
D) It's a unique C function.

**Answer: A**

**Explanation:**
Exposed in `secrets` for convenience and discoverability.

---

**Q21.11: Basic - [SQL Injection]**

The correct way to execute SQL with input parameters (using DB-API) is:

A) `cursor.execute("SELECT * FROM users WHERE name = '" + name + "'")`
B) `cursor.execute(f"SELECT * FROM users WHERE name = '{name}'")`
C) `cursor.execute("SELECT * FROM users WHERE name = %s", (name,))`
D) `cursor.exec(name)`

**Answer: C**

**Explanation:**
Using placeholders (`%s` or `?`) allows the database driver to escape inputs properly, preventing SQL injection.

---

**Q21.12: Intermediate - [Tempfile]**

`tempfile.NamedTemporaryFile(delete=True)`:

A) Creates a file that is automatically deleted when closed.
B) Creates a permanent file.
C) Creates a folder.
D) Is insecure.

**Answer: A**

**Explanation:**
Standard safe way to handle temporary data.

---

**Q21.13: Advanced - [Shell Injection]**

Using `subprocess.run(cmd_string, shell=True)` with untrusted input is dangerous because:

A) It is slow.
B) Attackers can inject shell operators (`; rm -rf /`) into the command string.
C) It fails on Windows.
D) It prints too much.

**Answer: B**

**Explanation:**
Always prefer `shell=False` and pass a list of arguments `['ls', '-l']` to bypass the shell interpreter.

---

**Q21.14: Basic - [Secrets Token]**

`secrets.token_hex(16)` generates:

A) A 16-character string.
B) A random hexadecimal string representing 16 bytes (so 32 chars length).
C) A 16-bit integer.
D) A UUID.

**Answer: B**

**Explanation:**
Each byte is 2 hex chars. Secure tokens for API keys or password resets.

---

**Q21.15: Intermediate - [UUID]**

`uuid.uuid4()` generates:

A) A determinisitc UUID based on MAC address.
B) A random UUID (Universally Unique Identifier).
C) A sequential ID.
D) A timestamp ID.

**Answer: B**

**Explanation:**
Good for unique IDs where collision probability is negligible, but use `secrets` for auth tokens.

---

**Q21.16: Advanced - [Xml Etree]**

`xml.etree.ElementTree` is vulnerable to:

A) XML Injection.
B) Billion Laughs Attack (Entity Expansion DoS).
C) It is totally safe.
D) None.

**Answer: B**

**Explanation:**
Standard `ElementTree` is not secure against maliciously constructed XML data. Use `defusedxml` if parsing untrusted XML.

---

**Q21.17: Expert - [Assert]**

Why should you NEVER use `assert` for security checks (e.g., `assert user.is_admin`)?

A) It throws AssertionError.
B) It is slow.
C) Assertions are optimized out (removed) when Python is run with `-O` (optimize) flag.
D) It is unpythonic.

**Answer: C**

**Explanation:**
A deployment set to optimization mode would completely skip the security check.

---

**Q21.18: Intermediate - [Requests SSL]**

When using the `requests` library, `verify=False`:

A) Enables strict verification.
B) Disables SSL certificate verification (insecure, allow MITM).
C) Is default.
D) Vernifies locally.

**Answer: B**

**Explanation:**
Never use `verify=False` in production code.

---

**Q21.19: Basic - [Hash Property]**

Cryptographic hashes are "one-way", meaning:

A) It is computationally infeasible to reverse the hash to get the original input.
B) You can decrypt them with a key.
C) They are reversible.
D) They are always integers.

**Answer: A**

**Explanation:**
Essential for password storage.

---

**Q21.20: Advanced - [Salt]**

A "Salt" in password hashing is:

A) A secret key.
B) A random value added to the password before hashing to ensure identical passwords have different hashes.
C) Pepper.
D) The algorithm name.

**Answer: B**

**Explanation:**
Defends against Rainbow Table attacks (precomputed hash lists).

---

**Q21.21: Expert - [Hashlib Update]**

`h = hashlib.sha256(); h.update(b'foo'); h.update(b'bar')` is equivalent to:

A) `hashlib.sha256(b'bar')`
B) `hashlib.sha256(b'foobar')`
C) `hashlib.sha256(b'foo')`
D) Error.

**Answer: B**

**Explanation:**
`update` allows processing data in chunks (streaming). The result is the hash of the concatenation.

---

**Q21.22: Intermediate - [Base64 URL Safe]**

`base64.urlsafe_b64encode()` uses which characters instead of `+` and `/`?

A) `-` and `_`
B) `!` and `@`
C) `.` and `,`
D) `*` and `$`

**Answer: A**

**Explanation:**
Replacing loop/slash ensures the string is safe to use in URLs and filenames without further escaping.

---

**Q21.23: Basic - [Str Encode]**

To hash a string, you must first:

A) Encrypt it.
B) Encode it to bytes (e.g., `s.encode('utf-8')`).
C) Zip it.
D) Print it.

**Answer: B**

**Explanation:**
Hash functions operate on bytes, not Unicode strings.

---

**Q21.24: Advanced - [PBKDF2]**

`hashlib.pbkdf2_hmac` is used for:

A) Fast hashing.
B) Password hashing (Key Derivation Function) with iteration count (stretching).
C) Creating random numbers.
D) Checking files.

**Answer: B**

**Explanation:**
Standard mechanism in Python's hashlib to derive keys/hashes safely from passwords.

---

**Q21.25: Intermediate - [Eval Harm]**

`eval(user_input)` is:

A) A powerful feature to be used freely.
B) Extremely dangerous (allows execution of arbitrary Python code).
C) Safe if input is string.
D) Fast.

**Answer: B**

**Explanation:**
"Eval is evil". Never use it on untrusted input. Use `ast.literal_eval` safely for literal structures.

---

**Q21.26: Expert - [Global Interpreter Lock Security]**

The GIL:

A) Provides thread safety for atomic bytecode operations (preventing memory corruption), but not logical thread safety.
B) Encrypts threads.
C) Prevents access to globals.
D) Is a security feature.

**Answer: A**

**Explanation:**
While not a security feature per se, it limits low-level race conditions in memory management, though developers still need locks for logical consistency.

---

**Q21.27: Basic - [Input Sanitization]**

The first rule of security is:

A) Trust all input.
B) Never trust user input.
C) Use C++.
D) Hide your code.

**Answer: B**

**Explanation:**
Assume all input is malicious until validated/sanitized.

---

**Q21.28: Advanced - [YAML Load]**

`yaml.load(data)` (in PyYAML < 5.1/standard load) is dangerous because:

A) It spawns processes.
B) It can construct arbitrary Python objects.
C) It is XML.
D) It crashes.

**Answer: B**

**Explanation:**
Use `yaml.safe_load()` to restrict loading to simple data structures only.

---

**Q21.29: Intermediate - [Directory Traversal]**

`open(os.path.join("/var/www", filename))` where filename is `../../etc/passwd` leads to:

A) Directory Traversal / Path Traversal vulnerability.
B) File Not Found.
C) Safe reading.
D) Encryption.

**Answer: A**

**Explanation:**
Always validate paths or use `os.path.abspath` and check common prefix to prevent escaping the intended directory.

---

**Q21.30: Expert - [Time Module Security]**

Is `time.time()` safe for security timestamps?

A) Yes.
B) No, it can go backwards (system clock change) or be spoofed.
C) No, it's irrelevant.
D) Yes, it is atomic.

**Answer: B**

**Explanation:**
System time is mutable. Clocks sync/drift. This can impact token expiration logic if not careful (monotonic time is safer for durations).

---

**Q21.31: Intermediate - [XML Defused]**

`defusedxml` library is the recommended way to:

A) Create XML.
B) Parse untrusted XML data safely (preventing entity expansion attacks).
C) Compress XML.
D) Encrypt XML.

**Answer: B**

**Explanation:**
It monkey-patches or provides safe replacements for standard XML parsers that are vulnerable to DoS attacks.

---

**Q21.32: Advanced - [Open Redirect]**

In web apps, `redirect(request.args.get('next'))` is vulnerable to:

A) Open Redirect Vulnerability.
B) XSS.
C) SQL Injection.
D) CSRF.

**Answer: A**

**Explanation:**
An attacker can supply `?next=http://malicious-site.com` to phish users. Always validate the target URL (e.g., ensure it's relative or whitelist domains).

---

**Q21.33: Basic - [HTTPS Request]**

When making an HTTP request to an API with an API key, the key should be passed in:

A) The URL parameters (`?key=...`).
B) The Request Headers (e.g., `Authorization`).
C) The HTML body.
D) Cookies (always).

**Answer: B**

**Explanation:**
URL parameters are logged in proxy/server access logs and browser history, leaking the key. Headers are encrypted over HTTPS.

---

**Q21.34: Expert - [Replay Attack]**

A Replay Attack can be prevented by using:

A) A strong password.
B) A Nonce (Number used once) or Timestamp in the signed request.
C) Compression.
D) Longer keys.

**Answer: B**

**Explanation:**
Ensures that a captured valid request cannot be resent by an attacker later because the nonce/timestamp will be invalid/duplicate.

---

**Q21.35: Intermediate - [Jinja2 Escaping]**

In Jinja2 (used by Flask), auto-escaping:

A) Is disabled by default.
B) Is enabled by default for `.html` templates, converting special chars like `<` to `&lt;` to prevent XSS.
C) Deletes headers.
D) Runs SQL.

**Answer: B**

**Explanation:**
Crucial for preventing Cross-Site Scripting (XSS) when rendering user input.

---

**Q21.36: Advanced - [Timing Safe Memcmp]**

`crypto_memcmp` (in C libraries) or Python's `secrets.compare_digest` is implemented to:

A) Run as fast as possible.
B) Run in constant time regardless of where the difference occurs in the byte strings.
C) Use hardware acceleration.
D) Use less memory.

**Answer: B**

**Explanation:**
Prevents "timing side-channel attacks" where an attacker guesses inputs byte-by-byte based on response time variations.

---

**Q21.37: Basic - [Dotenv]**

`python-dotenv` is commonly used to:

A) Encrypt environment variables.
B) Load environment variables (configuration/secrets) from a `.env` file into `os.environ` during development.
C) Delete `.env` files.
D) Send emails.

**Answer: B**

**Explanation:**
Keeps secrets out of source code commits. The `.env` file should be git-ignored.

---

**Q21.38: Intermediate - [Requests Timeout]**

`requests.get(url)` without a `timeout` argument:

A) Defaults to 30 seconds.
B) Hangs indefinitely (blocks forever) if the server accepts the connection but sends no data.
C) Times out instantly.
D) Is safe.

**Answer: B**

**Explanation:**
A potential Denial of Service (DoS) vector if your application relies on external APIs. Always set a timeout.

---

**Q21.39: Advanced - [Argon2]**

Argon2 is:

A) A gas.
B) The winner of the Password Hashing Competition (2015), modern standard for password hashing (memory-hard).
C) An encryption algorithm.
D) A database.

**Answer: B**

**Explanation:**
It is memory-hard, making it resistant to GPU/ASIC cracking, superior to bcrypt/PBKDF2.

---

**Q21.40: Expert - [Cryptography Lib]**

The `cryptography` library (PyCA) `Fernet` recipe provides:

A) Symmetric encryption (AES-128-CBC + HMAC-SHA256) with misuse-resistant tokens.
B) Asymmetric encryption.
C) Hashing.
D) SSL.

**Answer: A**

**Explanation:**
"Fernet" guarantees that a message encrypted cannot be manipulated or read without the key (Authenticated Encryption).

---

**Q21.41: Basic - [Log Injection]**

Logging user input directly (e.g., `logging.info("User: " + username)`) without usage of placeholders or cleaning can lead to:

A) Log Injection / Forging.
B) Logging stopping.
C) Code execution.
D) Slow logs.

**Answer: A**

**Explanation:**
Attackers can insert newlines (`\n`) to fake log entries, confusing admins or log analysis tools.

---

**Q21.42: Intermediate - [Shredding]**

To securely delete a file in Python, `os.remove()` is:

A) Sufficient against FBI forensics.
B) Insufficient; it only unlinks the pointer. The data remains on disk. Overwriting (shredding) is needed for high security.
C) Is deprecated.
D) Is perfect.

**Answer: B**

**Explanation:**
For high-security needs, you must overwrite the file content with random data before unlinking it.

---

**Q21.43: Advanced - [XXE]**

XXE stands for:

A) XML External Entity attack.
B) X-ray Encryption.
C) XSS Execution.
D) Xenon Extraction.

**Answer: A**

**Explanation:**
Attack against XML parsers using external entity references to access local files or internal networks.

---

**Q21.44: Expert - [Subprocess Shell False]**

If `subprocess.call(cmd, shell=False)` is used, but `cmd` is a string `"ls -l"`, what happens?

A) It executes `ls -l`.
B) It tries to find an executable literally named `"ls -l"` (with space) and likely fails (FileNotFoundError).
C) It works like shell=True.
D) It crashes python.

**Answer: B**

**Explanation:**
With `shell=False` (default), the first argument must be the executable path, and subsequent arguments must be in a list `["ls", "-l"]`. Passing a single string treats it as the filename.

---

**Q21.45: Intermediate - [Cookie HttpOnly]**

Setting the `HttpOnly` flag on a session cookie:

A) Forces HTTPS.
B) Prevents client-side JavaScript (`document.cookie`) from accessing the cookie.
C) Encrypts the cookie.
D) Compresses the cookie.

**Answer: B**

**Explanation:**
Critical mitigation for XSS; even if an attacker runs JS, they cannot steal the session cookie.

---

**Q21.46: Basic - [Virtualenv]**

Using a virtual environment (`venv`) enhances security by:

A) Isolating dependencies (avoiding system-wide package conflicts and malware affecting the whole OS).
B) Encrypting files.
C) Hiding IP.
D) Speeding up python.

**Answer: A**

**Explanation:**
Isolation limits the blast radius of compromised packages and maintains reproducible builds.

---

**Q21.47: Advanced - [SameSite Cookie]**

`SameSite=Strict` cookie attribute helps prevent:

A) CXRF (CSRF).
B) XSS.
C) SQLi.
D) DoS.

**Answer: A**

**Explanation:**
The browser will not send the cookie on cross-site requests, blocking CSRF attacks.

---

**Q21.48: Expert - [Scrypt]**

`hashlib.scrypt` (Python 3.6+) is beneficial because:

A) It is memory-hard (requires RAM to compute), resisting hardware-accelerated attacks.
B) It is fast.
C) It is reversible.
D) It is an old standard.

**Answer: A**

**Explanation:**
Like Argon2, it targets the tradeoff of memory usage to thwart ASIC/FPGA crackers.

---

**Q21.49: Intermediate - [Bandit]**

`bandit` is a tool for:

A) Stealing code.
B) Static Application Security Testing (SAST) to find common security issues in Python code.
C) Dynamic testing.
D) Formatting code.

**Answer: B**

**Explanation:**
Scans for `exec`, `eval`, hardcoded passwords, unsafe `subprocess` usage, etc.

---

**Q21.50: Basic - [Django Secret Key]**

In Django (and Flask), the `SECRET_KEY`:

A) Can be shared publicly.
B) Must be kept secret. It is used for cryptographic signing of session cookies and CSRF tokens.
C) Is optional.
D) Changes every restart.

**Answer: B**

**Explanation:**
If leaked, attackers can forge session cookies and take over any account.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
