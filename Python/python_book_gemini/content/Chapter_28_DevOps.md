# Chapter 28: DevOps & Automation

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `subprocess` (run, Popen, pipes), CLI arguments (`argparse`), `sys.argv`, CI/CD Concepts, Containerization (Docker basics, python docker sdk), Logging Strategies (`logging.config`, RotatingFileHandler), Cron Jobs, Shell interaction (`shutil`, `os`).

---

**Q28.1: Basic - [Subprocess Run]**

The modern, recommended function to run a system command and wait for it to complete is:

A) `os.system()`
B) `subprocess.run()`
C) `subprocess.call()`
D) `sys.run()`

**Answer: B**

**Explanation:**
Introduced in Python 3.5, it replaces older functions like `call` and `check_output`.

---

**Q28.2: Intermediate - [Capture Output]**

To capture the standard output (stdout) of a command run with `subprocess.run`:

A) Pass `capture_output=True` (or `stdout=subprocess.PIPE`).
B) Pass `get_text=True`.
C) Use `subprocess.output()`.
D) Read the monitor.

**Answer: A**

**Explanation:**
`result = subprocess.run(..., capture_output=True, text=True)`. Access via `result.stdout`.

---

**Q28.3: Advanced - [Argparse]**

The `argparse` library is used to:

A) Parse arguments in arguments.
B) Create user-friendly command-line interfaces (parsing sys.argv, generating help messages, type checking).
C) Parse JSON.
D) Parse HTML.

**Answer: B**

**Explanation:**
Essential for creating professional CLI tools.

---

**Q28.4: Basic - [Docker Concept]**

A Docker "Image" is:

A) A photograph.
B) A read-only template containing the application code, libraries, and dependencies needed to run it.
C) A running process.
D) A database.

**Answer: B**

**Explanation:**
A "Container" is a runnable instance of an Image.

---

**Q28.5: Intermediate - [Shebang]**

Adding `#!/usr/bin/env python3` at the top of a Python script on Unix:

A) Is a comment.
B) Tells the operating system which interpreter to use to execute the file when run directly (e.g., `./script.py`).
C) Imports python.
D) Is required for Windows.

**Answer: B**

**Explanation:**
The "Shebang" line.

---

**Q28.6: Advanced - [Logging Rotation]**

`RotatingFileHandler` is useful in DevOps because:

A) It spins the hard drive.
B) It automatically splits log files when they reach a certain size (or age), preventing disk space exhaustion from infinite log growth.
C) It deletes logs.
D) It encrypts logs.

**Answer: B**

**Explanation:**
Essential for long-running services.

---

**Q28.7: Expert - [Subprocess Pipe]**

`subprocess.Popen(['ls'], stdout=subprocess.PIPE)`:

A) Runs `ls` asynchronously and opens a pipe to read its output stream directly (non-blocking if managed correctly).
B) Waits for `ls` to finish immediately.
C) Prints to screen.
D) Errors.

**Answer: A**

**Explanation:**
`Popen` is the lower-level interface for advanced use cases (e.g., interacting with stdin/stdout in real-time).

---

**Q28.8: Basic - [Sys Argv]**

`sys.argv[0]` always contains:

A) The first argument passed by user.
B) The name of the script/program being executed.
C) The python version.
D) None.

**Answer: B**

**Explanation:**
User arguments start at `sys.argv[1]`.

---

**Q28.9: Intermediate - [Exit Code]**

An exit code of `0` typically indicates:

A) Success.
B) Failure.
C) File Not Found.
D) Permission Denied.

**Answer: A**

**Explanation:**
Non-zero codes indicate errors. `sys.exit(0)` is clean exit.

---

**Q28.10: Advanced - [CI/CD]**

CI (Continuous Integration) refers to:

A) Automatically building and testing code changes whenever they are committed to the repository.
B) Hiring developers continuously.
C) Deploying to production.
D) Writing code continuously.

**Answer: A**

**Explanation:**
Ensures new code doesn't break existing functionality (Integration Hell).

---

**Q28.11: Basic - [Environment Variables]**

In Python, you access environment variables (e.g., API keys) via:

A) `os.environ`
B) `sys.env`
C) `env.get()`
D) `config.env`

**Answer: A**

**Explanation:**
`os.environ.get('KEY')`. Safe way to handle secrets vs hardcoding.

---

**Q28.12: Intermediate - [Requirements.txt]**

`pip freeze > requirements.txt`:

A) Freezes the computer.
B) Saves a list of all installed packages and their exact versions to a file.
C) Uninstalls packages.
D) Installs packages.

**Answer: B**

**Explanation:**
Ensures reproducibility of the environment.

---

**Q28.13: Advanced - [Dockerpython]**

The `docker` python library allows you to:

A) Run docker inside python.
B) Control the Docker daemon from Python code (list containers, build images, run containers), ideal for automation scripts.
C) Draw whales.
D) Is fake.

**Answer: B**

**Explanation:**
`client.containers.run("alpine", "echo hello world")`.

---

**Q28.14: Expert - [Signal Handling]**

Handling `signal.SIGINT` allows your script to:

A) Crash graciously.
B) Catch the "Ctrl+C" interrupt and perform cleanup (graceful shutdown) instead of terminating abruptly.
C) Connect to wifi.
D) Ignore errors.

**Answer: B**

**Explanation:**
Crucial for daemons/services to close DB connections or save state before exiting.

---

**Q28.15: Intermediate - [Shutil]**

To copy a directory tree recursively:

A) `os.cp()`
B) `shutil.copytree()`
C) `subprocess.run('cp')`
D) `shutil.move()`

**Answer: B**

**Explanation:**
`os` module handles low-level files; `shutil` handles high-level file operations.

---

**Q28.16: Basic - [Cron]**

A "Cron Job" is:

A) A scheduled task that runs automatically at specified intervals on a Unix-like system.
B) A web server.
C) A database query.
D) A python loop.

**Answer: A**

**Explanation:**
Python scripts are often triggered by cron for periodic automation.

---

**Q28.17: Advanced - [Virtualenv impact]**

Why is using a virtual environment critical in DevOps/Deployment?

A) It isolates execution.
B) It ensures the application uses its specific dependency versions, avoiding conflicts with system-wide packages or other applications.
C) It adds encryption.
D) It makes python faster.

**Answer: B**

**Explanation:**
"It works on my machine" prevention.

---

**Q28.18: Intermediate - [Argparse Flag]**

In `parser.add_argument('--verbose', action='store_true')`, if the user runs `--verbose`:

A) The variable `verbose` becomes `True`.
B) The variable `verbose` becomes `False`.
C) It prompts for input.
D) It errors.

**Answer: A**

**Explanation:**
`store_true` creates a boolean flag that defaults to False if omitted.

---

**Q28.19: Basic - [Echo]**

The shell command `echo $?` (on Unix) or `%ERRORLEVEL%` (on Windows) checks:

A) The exit status of the previously executed command.
B) The time.
C) The user name.
D) The path.

**Answer: A**

**Explanation:**
Useful for chaining commands (e.g., `&&` only runs if previous was 0).

---

**Q28.20: Expert - [Fabric/Ansible]**

Tools like Fabric (Python library) or Ansible are used for:

A) Web scraping.
B) Configuration Management and Remote Execution (deploying code/commands to multiple servers over SSH).
C) Designing UI.
D) Testing.

**Answer: B**

**Explanation:**
Infrastructure as Code.

---

**Q28.21: Intermediate - [YAML]**

YAML is preferred over JSON for configuration files (like Docker Compose, K8s) because:

A) It supports comments and is more human-readable.
B) It is faster.
C) It supports binary.
D) It is smaller.

**Answer: A**

**Explanation:**
Strict indentation based, similar to Python.

---

**Q28.22: Basic - [StdErr]**

`sys.stderr` is used to:

A) Print error messages, separate from standard output.
B) Print normal text.
C) Read input.
D) Close files.

**Answer: A**

**Explanation:**
Allows piping stdout to a file while still seeing errors on screen.

---

**Q28.23: Advanced - [Check Call]**

`subprocess.check_call()` differs from `call()` by:

A) Checking the phone.
B) Raising a `CalledProcessError` exception if the command returns a non-zero exit code.
C) Being silent.
D) Running in background.

**Answer: B**

**Explanation:**
Makes error handling explicit/automatic in scripts.

---

**Q28.24: Expert - [Tox]**

`tox` is a tool for:

A) Cleaning viruses.
B) Automating testing across multiple Python environments/versions (e.g., testing on Py3.6, Py3.8, Py3.9) using virtualenvs.
C) deploying docker.
D) format code.

**Answer: B**

**Explanation:**
Standard for libraries to ensure compatibility.

---

**Q28.25: Intermediate - [Getpass]**

`import getpass; getpass.getpass()` is used to:

A) Get a passport.
B) Securely prompt the user for a password without confirming (echoing) characters to the screen.
C) Generate a password.
D) Login.

**Answer: B**

**Explanation:**
Security best practice for interactive CLI tools.

---

**Q28.26: Basic - [Relative Path]**

In automation, using `__file__` helps to:

A) Read the file.
B) Determine the absolute path of the current script, allowing reliable relative path resolution (e.g., finding a config file next to the script).
C) Delete the file.
D) Rename the file.

**Answer: B**

**Explanation:**
`os.path.dirname(os.path.abspath(__file__))`.

---

**Q28.27: Advanced - [Daemon Process]**

A "Daemon" process:

A) Is a virus.
B) Runs in the background, detached from the controlling terminal.
C) Is a root user.
D) Is a fast process.

**Answer: B**

**Explanation:**
Services like nginx, postgres, or your custom background worker.

---

**Q28.28: Expert - [Click]**

The `click` library (Command Line Interface Creation Kit) improves on `argparse` by:

A) Being built into Python.
B) Using decorators (`@click.command`, `@click.option`) to define CLI interfaces with less boilerplate and robust composability.
C) Being faster.
D) Nothing.

**Answer: B**

**Explanation:**
Created by the Flask authors (Pallets). Extremely popular for modern CLIs.

---

**Q28.29: Intermediate - [Glob]**

`glob.glob('*.log')`:

A) Deletes log files.
B) Returns a list of filenames matching the wildcard pattern.
C) Creates log files.
D) Is global.

**Answer: B**

**Explanation:**
Useful for batch processing files.

---

**Q28.30: Basic - [Chmod]**

`os.chmod('script.py', 0o755)`:

A) Changes file mode/permissions (e.g., making it executable).
B) Changes modification time.
C) Compiles the file.
D) Deletes the file.

**Answer: A**

**Explanation:**
Equivalent to shell `chmod`.

---

**Q28.31: Intermediate - [Positional Arguments]**

In `argparse`, arguments defined without a `-` or `--` prefix (e.g., `parser.add_argument('filename')`) are:

A) Positional arguments (mandatory and order-dependent).
B) Optional arguments.
C) Ignored.
D) Errors.

**Answer: A**

**Explanation:**
The user must provide them.

---

**Q28.32: Advanced - [Rmtree]**

To delete a directory that is not empty (like `rm -rf`):

A) `os.rmdir()`
B) `shutil.rmtree()`
C) `os.remove()`
D) `delete_tree()`

**Answer: B**

**Explanation:**
`os.rmdir` only works on empty directories. Be careful!

---

**Q28.33: Basic - [Log Levels]**

Which log level is higher (more severe) than `WARNING`?

A) `INFO`
B) `DEBUG`
C) `ERROR`
D) `NOTSET`

**Answer: C**

**Explanation:**
Order: DEBUG < INFO < WARNING < ERROR < CRITICAL.

---

**Q28.34: Expert - [ConfigParser]**

The `configparser` module is commonly used to read configuration files in the format of:

A) XML.
B) JSON.
C) INI files (Sections like `[Database]` followed by `key = value`).
D) Binary.

**Answer: C**

**Explanation:**
Standard Windows/Linux config format.

---

**Q28.35: Intermediate - [Os Path Join]**

`os.path.join('folder', 'subfolder', 'file.txt')` is better than `'folder/subfolder/file.txt'` because:

A) It handles operating system specific path separators correctly (backslash on Windows, forward slash on Unix).
B) It is shorter.
C) It creates the file.
D) It sorts the path.

**Answer: A**

**Explanation:**
Cross-platform compatibility.

---

**Q28.36: Advanced - [Subprocess Timeout]**

`subprocess.run(..., timeout=5)`:

A) Pauses for 5 seconds.
B) Raises `TimeoutExpired` exception if the process takes longer than 5 seconds to complete.
C) Runs the process 5 times.
D) Returns 5.

**Answer: B**

**Explanation:**
Prevents scripts from hanging indefinitely if a command gets stuck.

---

**Q28.37: Basic - [StdIn]**

To read input piped into a script (e.g., `cat file.txt | python script.py`):

A) Use `sys.stdin`.
B) Use `input()`.
C) Use `sys.read()`.
D) Use `os.pipe()`.

**Answer: A**

**Explanation:**
`sys.stdin.read()` reads the entire input stream.

---

**Q28.38: Intermediate - [Expand User]**

`os.path.expanduser('~')` returns:

A) The path to the current user's home directory.
B) The root directory.
C) A random user.
D) The path to python.

**Answer: A**

**Explanation:**
Handling the tilde character is crucial for CLI tools.

---

**Q28.39: Advanced - [Platform]**

To run code only on Windows:

A) `if sys.platform.startswith('win'):`
B) `if os.name == 'windows':`
C) `if platform.is_windows():`
D) `if os.windows:`

**Answer: A**

**Explanation:**
`sys.platform` returns 'win32', 'linux', 'darwin' (macOS), etc.

---

**Q28.40: Expert - [Logging Format]**

To include the timestamp and log level in every log message:

A) Use `logging.basicConfig(format='%(asctime)s - %(levelname)s - %(message)s')`.
B) Print it manually.
C) Use f-strings.
D) Use `logging.time()`.

**Answer: A**

**Explanation:**
Standard log formatting.

---

**Q28.41: Basic - [Os Cwd]**

To get the Current Working Directory:

A) `os.getcwd()`
B) `os.pwd()`
C) `os.dir()`
D) `os.where()`

**Answer: A**

**Explanation:**
Where the script is running from.

---

**Q28.42: Intermediate - [Argparse Help]**

`argparse` automatically generates a help message (showing flags and descriptions) when the user runs the script with:

A) `-h` or `--help`.
B) `--info`.
C) `help`.
D) `?`.

**Answer: A**

**Explanation:**
This is why `argparse` is better than manually parsing `sys.argv`.

---

**Q28.43: Advanced - [Mktemp]**

The `tempfile` module is best for:

A) Creating temporary files and directories that are automatically cleaned up when closed or when the script exits.
B) Creating viruses.
C) Storing permanent data.
D) Checking temperature.

**Answer: A**

**Explanation:**
`with tempfile.NamedTemporaryFile() as tmp:`

---

**Q28.44: Expert - [Subprocess Shell]**

Using `shell=True` in `subprocess.run`:

A) Is necessary for using shell features like wildcards (`*`), pipes (`|`), or environment variable expansion (`$HOME`) directly in the command string, but introduces security risks (Shell Injection).
B) Makes it faster.
C) Is default.
D) Is safe.

**Answer: A**

**Explanation:**
Avoid unless absolutely necessary. Prefer passing list of arguments `['ls', '-l']`.

---

**Q28.45: Intermediate - [Env Var Default]**

`os.getenv('API_KEY', 'default_value')`:

A) Returns 'default_value' if 'API_KEY' is not set in the environment.
B) Sets the API key.
C) Errors if not found.
D) Deletes the key.

**Answer: A**

**Explanation:**
Safe retrieval.

---

**Q28.46: Basic - [Diff]**

The `difflib` standard library module is used for:

A) Comparing sequences (like lines of text) and generating human-readable differences (deltas).
B) Math differentiation.
C) Different libraries.
D) Nothing.

**Answer: A**

**Explanation:**
Useful for regression testing output.

---

**Q28.47: Advanced - [Pprint]**

`pprint.pprint(data)` is useful in DevOps scripts because:

A) It "pretty-prints" complex data structures (nested dicts/lists) in a readable, indented format, aiding debugging.
B) It prints faster.
C) It prints to the printer.
D) It prints in color.

**Answer: A**

**Explanation:**
A standard library gem.

---

**Q28.48: Expert - [Zipfile]**

To create a standard `.zip` archive programmatically:

A) `zipfile.ZipFile('archive.zip', 'w')`.
B) `shutil.zip()`.
C) `os.zip()`.
D) `subprocess.run('rar')`.

**Answer: A**

**Explanation:**
`shutil.make_archive` also works for high-level use.

---

**Q28.49: Intermediate - [Sleep]**

`time.sleep(10)`:

A) Pauses program execution for 10 seconds.
B) Sleeps for 10 minutes.
C) Stops the CPU.
D) Exits.

**Answer: A**

**Explanation:**
Common in polling loops (waiting for a server to come online).

---

**Q28.50: Basic - [Basename]**

`os.path.basename('/home/user/script.py')` returns:

A) `script.py`
B) `/home/user`
C) `py`
D) `script`

**Answer: A**

**Explanation:**
Extracts just the filename. `dirname` gets the folder.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
