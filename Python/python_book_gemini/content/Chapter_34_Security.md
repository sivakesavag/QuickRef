# Chapter 34: Security & Best Practices

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: SQL Injection, XSS, Pickle Insecurity, Shell Injection (`subprocess`), Cryptography (`secrets`, `hashlib`), Input Validation, `assert` in production, YAML/XML vulnerabilities, Timing Attacks.

---

**Q34.1: Basic - [SQL Injection]**

The correct, secure way to execute a SQL query with user input in Python (e.g., using `sqlite3` or `psycopg2`) is:

A) Parameterized queries: `cursor.execute("SELECT * FROM users WHERE name = ?", (user_input,))`.
B) F-strings: `cursor.execute(f"SELECT * FROM users WHERE name = '{user_input}'")`.
C) String concatenation: `cursor.execute("SELECT * FROM users WHERE name = '" + user_input + "'")`.
D) String formatting: `cursor.execute("SELECT * FROM users WHERE name = %s" % user_input)`.

**Answer: A**

**Explanation:**
Never inject variable strings directly into SQL commands. Let the database driver handle escaping.

---

**Q34.2: Intermediate - [Pickle Danger]**

Why is the `pickle` module considered insecure?

A) Unpickling validation data allows arbitrary code execution. A malicious user can craft a pickle byte stream that, when loaded, executes system commands.
B) It is slow.
C) It creates large files.
D) It is text-only.

**Answer: A**

**Explanation:**
Never unpickle data from untrusted sources. Use JSON instead.

---

**Q34.3: Advanced - [Shell Injection]**

Which `subprocess` call is vulnerable to Shell Injection if `filename` comes from user input?

A) `subprocess.run(f"cat {filename}", shell=True)`
B) `subprocess.run(["cat", filename])`
C) `subprocess.run(["ls", "-l"])`
D) `subprocess.call(["echo", "hello"])`

**Answer: A**

**Explanation:**
`shell=True` invokes the system shell, which interprets metacharacters (e.g., `; rm -rf /`).

---

**Q34.4: Expert - [Assert in Production]**

Relying on `assert user_is_admin()` for security checks is dangerous because:

A) Optimization flags (`python -O`) remove all `assert` statements from the compiled bytecode, effectively bypassing the check in production.
B) It raises `SystemError`.
C) It is slow.
D) It crashes the server.

**Answer: A**

**Explanation:**
Use `if not user_is_admin(): raise PermissionError(...)` instead.

---

**Q34.5: Basic - [Random vs Secrets]**

For generating passwords, tokens, or cryptographic keys, you should use:

A) `secrets` module (CSPRNG - Cryptographically Secure Pseudo-Random Number Generator).
B) `random` module (Mersenne Twister).
C) `time.time()`.
D) `os.getpid()`.

**Answer: A**

**Explanation:**
`random` is deterministic if the seed is known and is not designed for security.

---

**Q34.6: Intermediate - [YAML Safety]**

When parsing YAML files (using `PyYAML`), the safe function to use is:

A) `yaml.safe_load()`
B) `yaml.load()`
C) `yaml.parse()`
D) `yaml.read()`

**Answer: A**

**Explanation:**
`yaml.load()` (in older versions) could instantiate arbitrary Python objects, leading to RCE (Remote Code Execution).

---

**Q34.7: Advanced - [Timing Attack]**

To compare secret strings (like hashes or API keys) securely to prevent Timing Attacks, use:

A) `secrets.compare_digest(a, b)` (constant time comparison).
B) `a == b`
C) `a is b`
D) `strcmp(a, b)`

**Answer: A**

**Explanation:**
Standard equality checks return false as soon as a mismatch is found, leaking information about the prefix length.

---

**Q34.8: Expert - [XML Vulnerabilities]**

The standard `xml.etree.ElementTree` module is vulnerable to:

A) Billion Laughs Attack (XML Bomb) and External Entity Expansion (XXE), which can cause DoS or local file disclosure.
B) Nothing.
C) SQL Injection.
D) XSS.

**Answer: A**

**Explanation:**
Use `defusedxml` library for safe XML parsing.

---

**Q34.9: Basic - [XSS]**

In web frameworks like Flask/Jinja2, Cross-Site Scripting (XSS) is primarily prevented by:

A) Auto-escaping context (converting `<` to `&lt;`, etc.) in templates by default.
B) Disabling JavaScript.
C) Using HTTPS.
D) Encrypting HTML.

**Answer: A**

**Explanation:**
Be careful when using `| safe` or `Markup()`—only do so for trusted HTML.

---

**Q34.10: Intermediate - [Hash Functions]**

For storing passwords, you should use:

A) A slow, salted hashing algorithm like Argon2, bcrypt, or PBKDF2.
B) MD5.
C) SHA1.
D) Base64.

**Answer: A**

**Explanation:**
Fast hashes (SHA256, MD5) are bad for passwords because they allow rapid brute-force/rainbow table attacks.

---

**Q34.11: Advanced - [Tempfile]**

`tempfile.mktemp()` is deprecated and insecure because:

A) It returns a filename that *might* exist by the time you try to create it (Race Condition / TOCTOU), allowing an attacker to pre-create a malicious link.
B) It creates a directory.
C) It is slow.
D) It leaks memory.

**Answer: A**

**Explanation:**
Use `tempfile.mkstemp()` (which creates the file and returns a handle) or `tempfile.TemporaryFile`.

---

**Q34.12: Expert - [Eval Alternative]**

If you need to evaluate a string containing a Python literal (like a dictionary representation), the safe alternative to `eval()` is:

A) `ast.literal_eval()`
B) `exec()`
C) `compile()`
D) `subprocess.run()`

**Answer: A**

**Explanation:**
It only parses safe literals (strings, numbers, tuples, lists, dicts, booleans, None), avoiding code execution.

---

**Q34.13: Basic - [Hardcoded Secrets]**

Where should API keys and database passwords be stored?

A) Environment variables (read via `os.getenv()`) or a secure vault (Secrets Manager).
B) Directly in the source code.
C) In `readme.md`.
D) In comments.

**Answer: A**

**Explanation:**
Never commit secrets to Git.

---

**Q34.14: Intermediate - [Requests SSL]**

When making HTTP requests (`requests.get`), setting `verify=False`:

A) Disables SSL/TLS certificate verification, exposing the connection to Man-in-the-Middle (MitM) attacks.
B) Makes it secure.
C) Encrypts the data.
D) Compresses the data.

**Answer: A**

**Explanation:**
Only use for local testing with self-signed certs, never in production.

---

**Q34.15: Advanced - [Re DOS]**

"ReDoS" (Regular Expression Denial of Service) occurs when:

A) A poorly written regex (e.g., with nested quantifiers `(a+)+`) takes exponential time to match certain inputs, causing the server to hang.
B) Regex is deleted.
C) Regex matches everything.
D) Regex is compiled.

**Answer: A**

**Explanation:**
Avoid catastrophic backtracking.

---

**Q34.16: Expert - [Hashlib]**

`hashlib.sha256()` is good for:

A) File integrity checks and digital signatures (where speed is fine), but NOT for password storage (too fast).
B) Passwords.
C) Encryption.
D) Compression.

**Answer: A**

**Explanation:**
Hashing is one-way. Encryption is reversible.

---

**Q34.17: Basic - [Pip Install]**

To prevent "Dependency Confusion" or installing malicious packages typesquatted on PyPI:

A) Use a `requirements.txt` with Hashes (`--require-hashes`) and version pinning/locking (e.g., using `pip-tools` or `poetry`).
B) `pip install package` blindly.
C) Download zip files.
D) Use `easy_install`.

**Answer: A**

**Explanation:**
Lock files ensure you get exactly the same bytes you tested.

---

**Q34.18: Intermediate - [Open Redirect]**

An "Open Redirect" vulnerability in a web app allows:

A) An attacker to construct a URL (e.g., `example.com/login?next=http://evil.com`) that redirects the user to a malicious site after a legitimate action, often used for phishing.
B) Opening files.
C) Redirecting standard output.
D) Nothing.

**Answer: A**

**Explanation:**
Always validate the `next` URL (ensure it is relative or whitelisted).

---

**Q34.19: Advanced - [Bind All Interfaces]**

Binding a server socket to `0.0.0.0` means:

A) It listens on ALL available network interfaces (public internet + local), potentially exposing it to the world if no firewall is present.
B) It listens only on localhost.
C) It is disabled.
D) It listens on a random IP.

**Answer: A**

**Explanation:**
Use `127.0.0.1` (localhost) if it shouldn't be accessible externally.

---

**Q34.20: Expert - [LBYL vs EAFP Security]**

In security-critical contexts (like checking file permissions before opening), EAFP (Try/Except) is preferred over LBYL (Look Before You Leap, e.g., `if os.path.exists...`) because:

A) LBYL is prone to Race Conditions (TOCTOU - Time of Check to Time of Use): the file/permissions could change between the check and the use.
B) EAFP is faster.
C) LBYL is deprecated.
D) Python forces EAFP.

**Answer: A**

**Explanation:**
The atomic operation is "try to open it and handle failure".

---

**Q34.21: Basic - [Input Type]**

In Python 2, `input()` was equivalent to `eval(raw_input())`, which was a major security flaw. In Python 3:

A) `input()` creates a string (safe), equivalent to Python 2's `raw_input()`.
B) It executes code.
C) It is removed.
D) It returns bytes.

**Answer: A**

**Explanation:**
Python 3 fixed this.

---

**Q34.22: Intermediate - [Danders]**

Accessing `__subclasses__()` or `__globals__` on objects provided by user input (e.g., in a template injection scenario) is dangerous because:

A) It allows traversing the object graph to reach internal modules (like `os` or `subprocess`) and execute arbitrary code (SSTI - Server Side Template Injection).
B) It is slow.
C) It raises errors.
D) It does nothing.

**Answer: A**

**Explanation:**
Template engines should be sandboxed.

---

**Q34.23: Advanced - [CSRF]**

Cross-Site Request Forgery (CSRF) protection involves:

A) Requiring a secret, unpredictable token (CSRF Token) in every state-changing request (POST/PUT/DELETE) that verify the request came from the real site.
B) Using cookies.
C) Using HTTPS.
D) Checking IP address.

**Answer: A**

**Explanation:**
Cookies are sent automatically by the browser, even for forged requests from other tabs.

---

**Q34.24: Expert - [JWT logic]**

A common critical vulnerability in JWT (JSON Web Token) implementation is:

A) Accepting tokens with `alg: "none"` (algorithm none), which allows an attacker to forge a token without a signature.
B) Using JSON.
C) Using base64.
D) Using HTTPS.

**Answer: A**

**Explanation:**
Always enforce the expected algorithm (e.g., HS256).

---

**Q34.25: Basic - [Debug Mode]**

Leaving `DEBUG = True` (in Django/Flask) in production is dangerous because:

A) It exposes detailed tracebacks (showing source code snippets, environment variables, settings) effectively leaking secrets and architecture details to attackers on any error.
B) It is slower.
C) It uses more memory.
D) It looks ugly.

**Answer: A**

**Explanation:**
Never deploy with Debug True.

---

**Q34.26: Intermediate - [Path Traversal]**

"Directory Traversal" attacks (e.g., `../../etc/passwd`) work by:

A) Manipulating file path inputs to access files outside the intended directory.
B) Walking in directories.
C) Deleting directories.
D) Sorting files.

**Answer: A**

**Explanation:**
Use `os.path.abspath` and check common prefixes, or `pathlib.resolve()`.

---

**Q34.27: Advanced - [Hash Salt]**

The purpose of a "Salt" in password hashing is to:

A) Ensure that two users with the same password have different hashes, and to prevent the use of pre-computed "Rainbow Tables" to reverse the hashes.
B) Make it taste better.
C) Encrypt the password.
D) Speed up hashing.

**Answer: A**

**Explanation:**
Salt must be unique per user.

---

**Q34.28: Expert - [Subprocess Env]**

When running `subprocess`, the `env` argument:

A) Defines the environment variables for the new process. If `None` (default), it inherits the *entire* environment of the parent process (potentially leaking keys).
B) Is meaningless.
C) Is empty.
D) Is secure by default.

**Answer: A**

**Explanation:**
Explicitly passing `env={}` or a specific subset is safer.

---

**Q34.29: Intermediate - [Mutable Global State]**

Modifying global state (like `sys.modules`, `os.environ`, or global dicts) in a library or thread is bad practice because:

A) It affects the entire process, potentially breaking other threads or parts of the application (Thread Safety issues).
B) It consumes memory.
C) It is slow.
D) It is illegal.

**Answer: A**

**Explanation:**
Context-local storage (`contextvars`) is preferred.

---

**Q34.30: Basic - [Virtualenv]**

Using a Virtual Environment (`venv`) is a best practice because:

A) It isolates project dependencies, preventing conflicts between different projects and system-wide packages.
B) It speeds up Python.
C) It encrypts code.
D) It is mandatory.

**Answer: A**

**Explanation:**
Avoid "Dependency Hell".

---

**Q34.31: Intermediate - [HMAC]**

To prevent tampering with a message (integrity check) using a secret key, use:

A) `hmac` module (Hash-based Message Authentication Code).
B) `hashlib`.
C) `random`.
D) `base64`.

**Answer: A**

**Explanation:**
Simple hashing (`hash(msg)`) is not secure if the attacker can just recalculate the hash. HMAC mixes the key and message securely.

---

**Q34.32: Advanced - [Zip Slip]**

"Zip Slip" is a vulnerability where extracting a zip file allows:

A) A malicious file inside the zip to be written outside the target directory (via path traversal like `../../evil.sh`), overwriting system files.
B) Disks to format.
C) Memory leaks.
D) Faster extraction.

**Answer: A**

**Explanation:**
Always validate paths inside zip archives before extracting.

---

**Q34.33: Basic - [Shlex Quote]**

If you MUST construct a shell command string (and can't use list-based `subprocess`), sanitize inputs using:

A) `shlex.quote()`
B) `str()`
C) `repr()`
D) `replace(' ', '')`

**Answer: A**

**Explanation:**
Properly escapes spaces and special characters.

---

**Q34.34: Expert - [Integer DOS]**

In newer Python versions (3.11+), string-to-int conversion (`int(str_val)`) and printing giant integers have a default limit (e.g., 4300 digits) to prevent:

A) Denial of Service (DoS) attacks via computationally expensive binary/decimal conversion (Quadratic complexity).
B) Floating point errors.
C) Integer overflow.
D) Memory leaks.

**Answer: A**

**Explanation:**
`sys.set_int_max_str_digits()` controls this.

---

**Q34.35: Intermediate - [Logging Secrets]**

When logging request data in production, you must ensure:

A) Sensitive fields (passwords, auth tokens, credit card numbers) are redacted or masked ("*****") before writing to disk.
B) Everything is logged for debugging.
C) Logs are deleted immediately.
D) Logs are encrypted.

**Answer: A**

**Explanation:**
Logs are a common leak vector.

---

**Q34.36: Advanced - [Argon2]**

The `argon2-cffi` library is often recommended for password hashing because:

A) It is memory-hard (requires RAM to compute), making FPGA/ASIC brute-force attacks prohibitively expensive.
B) It is fast.
C) It is old.
D) It is native.

**Answer: A**

**Explanation:**
Winner of the Password Hashing Competition.

---

**Q34.37: Basic - [Secure Cookies]**

Setting the `HttpOnly` flag on a session cookie:

A) Prevents client-side JavaScript (`document.cookie`) from accessing the cookie, mitigating XSS cookie theft.
B) Encrypts the cookie.
C) Compresses it.
D) Deletes it when the browser closes.

**Answer: A**

**Explanation:**
Essential defense-in-depth.

---

**Q34.38: Intermediate - [HTTPS Only]**

HSTS (HTTP Strict Transport Security) header tells the browser:

A) To ONLY communicate with this domain using HTTPS (never HTTP) for a specified period, preventing SSL Stripping attacks.
B) To cache images.
C) To block popups.
D) To use HTTP/2.

**Answer: A**

**Explanation:**
Prevents "Down grade" attacks.

---

**Q34.39: Advanced - [CodeOp]**

The `codeop` module provides utilities for:

A) Emulating the Python read-eval-print loop (REPL), useful for building custom shells or debuggers.
B) Securing code.
C) Optimizing code.
D) Opening files.

**Answer: A**

**Explanation:**
Rarely used, but good to know for tool builders.

---

**Q34.40: Expert - [Clickjacking]**

The `X-Frame-Options: DENY` (or `SAMEORIGIN`) header prevents Clickjacking by:

A) Instructing the browser not to display the page inside an `<iframe>` (which invisible layers could use to trick users into clicking buttons).
B) Disabling clicks.
C) Blocking JavaScript.
D) Blocking cookies.

**Answer: A**

**Explanation:**
Modern alternative: CSP `frame-ancestors`.

---

**Q34.41: Basic - [Sudo Pip]**

Running `sudo pip install package` is generally discouraged because:

A) It installs packages globally, potentially overwriting system-managed files (which can break `apt` / `yum` or the OS itself) and running setup scripts as root.
B) It is slow.
C) It fails often.
D) It is deprecated.

**Answer: A**

**Explanation:**
Use `pip install --user` or (better) a virtualenv.

---

**Q34.42: Intermediate - [SameSite Cookie]**

The `SameSite=Strict` cookie attribute helps prevent:

A) CSRF (Cross-Site Request Forgery) by ensuring the cookie is not sent with cross-site requests.
B) XSS.
C) SQL Injection.
D) Clickjacking.

**Answer: A**

**Explanation:**
The browser itself enforces the policy.

---

**Q34.43: Advanced - [Content Security Policy]**

Context Security Policy (CSP) is an HTTP header that:

A) Whitelists sources of executable scripts (e.g., "only allow JS from my domain and google analytics"), drastically reducing the impact of XSS.
B) Encrypts content.
C) Compresses content.
D) Speeds up loading.

**Answer: A**

**Explanation:**
A powerful mitigation against XSS.

---

**Q34.44: Expert - [Paramiko]**

When using `paramiko` for SSH connections, you should strictly verify:

A) The Host Key (to prevent Man-in-the-Middle attacks), typically by checking against a known `known_hosts` file.
B) The username.
C) The IP.
D) The port.

**Answer: A**

**Explanation:**
`AutoAddPolicy` is convenient for dev, but dangerous for prod.

---

**Q34.45: Intermediate - [Requests Session]**

Using `s = requests.Session()` is better than `requests.get()` for multiple calls to the same host because:

A) It reuses the underlying TCP connection (Keep-Alive), persists cookies, and improves performance.
B) It is faster for one call.
C) It is encrypted.
D) It parses JSON.

**Answer: A**

**Explanation:**
Handshake overhead is significant in HTTPS.

---

**Q34.46: Basic - [Least Privilege]**

The "Principle of Least Privilege" implies:

A) Processes (and users) should run with the minimum permissions necessary to do their job (e.g., don't run web servers as root).
B) Be nice to users.
C) Grant all permissions.
D) Use minimal code.

**Answer: A**

**Explanation:**
Limits the blast radius if compromised.

---

**Q34.47: Advanced - [Ftplib]**

The `ftplib` module creates connections that are:

A) Unencrypted (Plaintext), meaning passwords and data can be sniffed. Use `ftplib.FTP_TLS` instead.
B) Secure.
C) Fast.
D) Compressed.

**Answer: A**

**Explanation:**
FTP is a legacy protocol; avoid if possible (use SFTP/SCP).

---

**Q34.48: Expert - [Pyc Bytecode Injection]**

If an attacker can write to your `__pycache__` directory:

A) They can replace `.pyc` files with malicious bytecode, which Python will execute instead of the source code (if timestamps match/are forced).
B) Nothing happens.
C) They can delete files.
D) They can read logic.

**Answer: A**

**Explanation:**
Ensure strict permissions on cache directories.

---

**Q34.49: Intermediate - [Bcrypt]**

`bcrypt` is often preferred over `PBKDF2` because:

A) It handles salt generation automatically and is specifically designed to resist hardware acceleration (GPU) attacks.
B) It is included in stdlib.
C) It is faster.
D) It is simpler.

**Answer: A**

**Explanation:**
Work factor (cost) is adjustable.

---

**Q34.50: Basic - [Audit Log]**

An "Audit Log" records:

A) "Who did what, and when" (for security accountability and forensics).
B) Errors only.
C) Debug info only.
D) Performance stats.

**Answer: A**

**Explanation:**
Essential for post-incident analysis.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
