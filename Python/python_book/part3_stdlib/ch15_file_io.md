# Chapter 15: File I/O & Serialization

> **Topics Covered**: open(), file modes, text vs binary, encoding, pathlib, os.path, file operations, json, pickle, csv, yaml, shelve, tempfile, file descriptors, buffering

---

## Questions

---

**Q15.1: Basic - [open() Function]**

What is the default mode for `open('file.txt')`?

A) `"w"` (write)
B) `"r"` (read text)
C) `"rb"` (read binary)
D) `"a"` (append)

**Answer: B**

**Explanation:**
Default mode is `"r"` — read text mode. File must exist (FileNotFoundError if not). Default encoding is platform-dependent (usually UTF-8 on modern systems). Always specify encoding explicitly.

---

**Q15.2: Basic - [File Modes]**

What does mode `"w"` do?

A) Read file
B) Open for writing, truncate if exists, create if not
C) Append to file
D) Read and write

**Answer: B**

**Explanation:**
`"w"` opens for writing. If file exists, it's truncated (emptied). If not, it's created. ⚠️ Careful: `"w"` destroys existing content! Use `"a"` for append or check existence first.

---

**Q15.3: Basic - [Reading File]**

What is the output?
```python
with open('test.txt', 'w') as f:
    f.write('Hello')

with open('test.txt', 'r') as f:
    print(f.read())
```

A) `Hello`
B) Empty
C) Error
D) `test.txt`

**Answer: A**

**Explanation:**
First `with` writes "Hello" and closes file. Second reads entire content with `read()`. Result: "Hello". `with` ensures files are properly closed even if exceptions occur.

---

**Q15.4: Intermediate - [read() vs readline() vs readlines()]**

What's the difference between `read()`, `readline()`, and `readlines()`?

A) No difference
B) read() = entire file; readline() = one line; readlines() = list of all lines
C) read() = one character; readline() = one word; readlines() = one paragraph
D) They're all deprecated

**Answer: B**

**Explanation:**
`read()` returns entire file as string. `readline()` returns next line (with \n). `readlines()` returns list of all lines. For iteration, `for line in file:` is most memory efficient — doesn't load all at once.

---

**Q15.5: Intermediate - [Iteration Over File]**

What is the most memory-efficient way to process a large file line by line?

A) `file.readlines()`
B) `file.read().split('\n')`
C) `for line in file:` (iterate directly)
D) While loop with readline

**Answer: C**

**Explanation:**
`for line in file:` iterates lazily — one line at a time in memory. `readlines()` loads everything. For GB-sized files, direct iteration is essential. Lines include trailing `\n`; use `line.strip()`.

---

**Q15.6: Basic - [Text vs Binary Mode]**

What's the difference between `"r"` and `"rb"`?

A) No difference
B) "r" is text (str, newline translation); "rb" is binary (bytes, no translation)
C) "rb" is faster
D) "r" is deprecated

**Answer: B**

**Explanation:**
Text mode: returns `str`, handles encoding/decoding, may translate newlines. Binary mode: returns `bytes`, raw data as-is. Use binary for images, PDFs, pickles. Use text for .txt, .json, .csv.

---

**Q15.7: Intermediate - [Encoding]**

What is the output?
```python
with open('test.txt', 'w', encoding='utf-8') as f:
    f.write('Héllo')

with open('test.txt', 'r', encoding='latin-1') as f:
    print(f.read())
```

A) `Héllo`
B) `HÃ©llo` (garbled)
C) Error
D) Empty

**Answer: B**

**Explanation:**
⚠️ Encoding mismatch! Written as UTF-8 (é = 2 bytes), read as Latin-1 (each byte separate character). Result is garbled. Always use consistent encoding. Best practice: always specify `encoding='utf-8'`.

---

**Q15.8: Intermediate - [newline Parameter]**

What does `newline=''` do in open()?

A) Nothing
B) Disables newline translation — critical for CSV
C) Removes all newlines
D) Adds extra newlines

**Answer: B**

**Explanation:**
`newline=''` prevents Python from translating `\r\n` ↔ `\n`. Essential for CSV to prevent double newlines on Windows. Let the csv module handle newlines itself. Default behavior varies by platform.

---

**Q15.9: Basic - [os.path Functions]**

What does `os.path.join('dir', 'file.txt')` return?

A) `'dir/file.txt'` or `'dir\\file.txt'` (platform-appropriate)
B) `'dir' + 'file.txt'`
C) `'dirfile.txt'`
D) Error

**Answer: A**

**Explanation:**
`os.path.join()` constructs paths with correct separator for the OS. Unix: `'dir/file.txt'`, Windows: `'dir\\file.txt'`. Never concatenate paths with `+`! Use join for portability.

---

**Q15.10: Intermediate - [pathlib.Path]**

What is the output?
```python
from pathlib import Path
p = Path('dir') / 'subdir' / 'file.txt'
print(p)
```

A) Error
B) `dir/subdir/file.txt` (or Windows equivalent)
C) `dir + subdir + file.txt`
D) `Path object`

**Answer: B**

**Explanation:**
pathlib uses `/` operator for path joining (overloaded). Creates proper path for current OS. More Pythonic than os.path.join. `Path` objects have methods like `.exists()`, `.read_text()`, `.mkdir()`.

---

**Q15.11: Intermediate - [Path Methods]**

What does `Path('dir/file.txt').stem` return?

A) `'file.txt'`
B) `'file'`
C) `'.txt'`
D) `'dir'`

**Answer: B**

**Explanation:**
`.stem` = filename without extension. `.suffix` = `'.txt'`. `.name` = `'file.txt'`. `.parent` = `Path('dir')`. pathlib provides clean access to path components.

---

**Q15.12: Intermediate - [Reading/Writing with pathlib]**

What is the output?
```python
from pathlib import Path
p = Path('test.txt')
p.write_text('Hello')
print(p.read_text())
```

A) `Hello`
B) Error
C) `Path object`
D) `test.txt`

**Answer: A**

**Explanation:**
pathlib has convenient methods: `read_text()`, `write_text()`, `read_bytes()`, `write_bytes()`. No need for `with open()` for simple cases. Handles opening/closing internally.

---

**Q15.13: Basic - [JSON Basics]**

What does `json.dumps()` do?

A) Loads JSON
B) Converts Python object to JSON string
C) Dumps to file
D) Downloads JSON

**Answer: B**

**Explanation:**
`dumps` = "dump string" — converts Python (dict, list, etc.) to JSON string. `loads` = "load string" — parses JSON string to Python. `dump`/`load` work with file objects.

---

**Q15.14: Intermediate - [JSON data types]**

Which Python types can be directly serialized to JSON?

A) All types
B) dict, list, str, int, float, bool, None only
C) Only strings
D) Only numbers

**Answer: B**

**Explanation:**
JSON supports: object (dict), array (list), string, number (int/float), true/false (bool), null (None). No tuples, sets, dates, custom objects. Use `default` parameter or custom encoder for others.

---

**Q15.15: Intermediate - [JSON with Custom Objects]**

What is the output?
```python
import json
class Point:
    def __init__(self, x, y):
        self.x, self.y = x, y

p = Point(1, 2)
print(json.dumps(p))
```

A) `{"x": 1, "y": 2}`
B) TypeError: Object not JSON serializable
C) `"Point(1, 2)"`
D) `null`

**Answer: B**

**Explanation:**
JSON can't serialize custom classes by default. Fix: `json.dumps(p.__dict__)` or implement custom encoder: `default=lambda o: o.__dict__`. For complex cases, use `JSONEncoder` subclass.

---

**Q15.16: Intermediate - [JSON Custom Serialization]**

What is the output?
```python
import json
data = {"name": "test", "values": {1, 2, 3}}
result = json.dumps(data, default=list)
print(result)
```

A) Error
B) `{"name": "test", "values": [1, 2, 3]}`
C) `{"name": "test", "values": null}`
D) `{"name": "test", "values": "set"}`

**Answer: B**

**Explanation:**
Sets aren't JSON serializable. `default=list` is called for non-serializable objects, converting set to list. Result has values as array. Order may vary (sets are unordered).

---

**Q15.17: Basic - [pickle Module]**

What is the difference between JSON and pickle?

A) No difference
B) JSON is text/portable; pickle is binary/Python-specific but handles more types
C) pickle is faster
D) JSON is deprecated

**Answer: B**

**Explanation:**
JSON: text format, language-agnostic, limited types. Pickle: binary, Python-only, serializes almost any Python object (classes, functions, etc.). ⚠️ Never unpickle untrusted data — security risk!

---

**Q15.18: Intermediate - [pickle Example]**

What is the output?
```python
import pickle
data = {'key': [1, 2, 3], 'func': len}
pickled = pickle.dumps(data)
restored = pickle.loads(pickled)
print(restored['func']([1, 2, 3, 4]))
```

A) `4`
B) Error
C) `len`
D) `[1, 2, 3, 4]`

**Answer: A**

**Explanation:**
Pickle serializes the function reference (`len`). After unpickling, `restored['func']` is `len`. Calling it on list returns 4. Pickle handles functions, classes, etc. (by reference, not code).

---

**Q15.19: Intermediate - [pickle Security]**

Why is unpickling untrusted data dangerous?

A) It's slow
B) Pickle can execute arbitrary code during unpickling
C) It uses too much memory
D) It's not actually dangerous

**Answer: B**

**Explanation:**
⚠️ Pickle can encode arbitrary Python code execution. Malicious pickle data can run code when unpickled. Never `pickle.load()` data from untrusted sources (network, user input). Use JSON or signed pickles for untrusted data.

---

**Q15.20: Intermediate - [CSV Reading]**

What is the output?
```python
import csv
from io import StringIO

data = "name,age\nAlice,30\nBob,25"
reader = csv.reader(StringIO(data))
print(list(reader))
```

A) `[['name', 'age'], ['Alice', '30'], ['Bob', '25']]`
B) `{'name': ['Alice', 'Bob'], 'age': ['30', '25']}`
C) Error
D) `'name,age\nAlice,30\nBob,25'`

**Answer: A**

**Explanation:**
`csv.reader` returns iterator of lists (rows). Each row is a list of strings. Header is first row. Use `csv.DictReader` for dict per row with header keys.

---

**Q15.21: Intermediate - [CSV DictReader]**

What is the output?
```python
import csv
from io import StringIO

data = "name,age\nAlice,30"
reader = csv.DictReader(StringIO(data))
print(list(reader))
```

A) `[['name', 'age'], ['Alice', '30']]`
B) `[{'name': 'Alice', 'age': '30'}]`
C) `{'name': 'Alice', 'age': '30'}`
D) Error

**Answer: B**

**Explanation:**
`DictReader` uses first row as keys. Each subsequent row becomes a dict. More readable than index access: `row['name']` vs `row[0]`. Similarly, `DictWriter` writes from dicts.

---

**Q15.22: Intermediate - [CSV Writing]**

What's wrong with this code on Windows?
```python
import csv
with open('out.csv', 'w') as f:
    writer = csv.writer(f)
    writer.writerow(['a', 'b'])
```

A) Nothing wrong
B) Missing `newline=''` — may cause blank lines between rows
C) Wrong mode
D) Missing encoding

**Answer: B**

**Explanation:**
On Windows, without `newline=''`, csv writes `\r\n` and Python's text mode adds another `\r` → blank lines. Fix: `open('out.csv', 'w', newline='')`. Also add `encoding='utf-8'` for safety.

---

**Q15.23: Intermediate - [tempfile Module]**

What does `tempfile.NamedTemporaryFile()` do?

A) Creates permanent file
B) Creates temp file with name, auto-deleted on close
C) Creates temp directory
D) Names existing file

**Answer: B**

**Explanation:**
Creates temporary file with unique name. Access via `.name`. Deleted automatically when closed (on Unix) or after context exit. Use `delete=False` to keep file. Secure — avoids race conditions.

---

**Q15.24: Intermediate - [tempfile.mkdtemp]**

What does `tempfile.TemporaryDirectory()` do?

A) Changes directory
B) Creates temp directory, auto-cleaned up with context manager
C) Lists temp files
D) Clears temp folder

**Answer: B**

**Explanation:**
```python
with TemporaryDirectory() as tmpdir:
    # use tmpdir path
# directory and contents deleted
```
Convenient for tests needing temp workspace. Auto-cleanup on exit. Returns path string.

---

**Q15.25: Intermediate - [shelve Module]**

What is `shelve`?

A) File organizer
B) Persistent dict-like object backed by file (uses pickle)
C) Bookshelf UI
D) Archive tool

**Answer: B**

**Explanation:**
`shelve.open('data')` creates persistent dictionary. Keys must be strings. Values can be any pickleable object. Changes saved to file. Like a simple key-value database. ⚠️ Same pickle security concerns apply.

---

**Q15.26: Intermediate - [shelve Example]**

What is the output?
```python
import shelve

with shelve.open('test_shelf') as db:
    db['key'] = [1, 2, 3]

with shelve.open('test_shelf') as db:
    print(db['key'])
```

A) `[1, 2, 3]`
B) Error
C) `None`
D) `'key'`

**Answer: A**

**Explanation:**
First `with` saves list to shelf file. Second reopens and retrieves it. Data persists between program runs. Works like a dict but stored on disk. Uses pickle internally.

---

**Q15.27: Intermediate - [File exists Check]**

Which checks if a path exists?

A) `os.path.exists(path)` or `Path(path).exists()`
B) `os.file.check(path)`
C) `file.exists(path)`
D) `try open(path)`

**Answer: A**

**Explanation:**
Both work. `os.path.exists()` — traditional. `Path(path).exists()` — pathlib style. Also: `.is_file()`, `.is_dir()` for specific checks. For EAFP style, use try/except with operation.

---

**Q15.28: Intermediate - [Creating Directories]**

What does `os.makedirs('a/b/c', exist_ok=True)` do?

A) Creates only 'c'
B) Creates 'a', 'a/b', and 'a/b/c'; no error if exists
C) Raises error if any exists
D) Deletes directories

**Answer: B**

**Explanation:**
`makedirs` creates intermediate directories (like `mkdir -p`). `exist_ok=True` prevents error if already exists. pathlib: `Path('a/b/c').mkdir(parents=True, exist_ok=True)`.

---

**Q15.29: Intermediate - [File Deletion]**

How do you delete a file and a directory?

A) `del file`
B) `os.remove(file)` for files; `os.rmdir(dir)` or `shutil.rmtree(dir)` for directories
C) `os.delete(path)`
D) `Path.delete()`

**Answer: B**

**Explanation:**
`os.remove(path)` — deletes file. `os.rmdir(path)` — deletes empty directory. `shutil.rmtree(path)` — deletes directory and all contents. pathlib: `.unlink()` for file, `.rmdir()` for empty dir.

---

**Q15.30: Intermediate - [shutil Module]**

What does `shutil` provide?

A) Shell utilities
B) High-level file operations: copy, move, archive
C) User interface
D) Networking

**Answer: B**

**Explanation:**
`shutil.copy(src, dst)` — copy file. `shutil.move()` — move. `shutil.copytree()` — copy directory tree. `shutil.rmtree()` — remove tree. `shutil.make_archive()` — create zip/tar. Higher-level than os.

---

**Q15.31: Intermediate - [File Copying]**

What's the difference between `shutil.copy()` and `shutil.copy2()`?

A) No difference
B) copy2 preserves metadata (timestamps, permissions)
C) copy2 is faster
D) copy2 copies directories

**Answer: B**

**Explanation:**
`copy()` — copies content and permission bits. `copy2()` — also copies metadata (mtime, atime). `copyfile()` — content only. `copytree()` — recursive directory copy. Choose based on metadata needs.

---

**Q15.32: Intermediate - [Walking Directory Tree]**

What does `os.walk(path)` yield?

A) File contents
B) Tuples of (dirpath, dirnames, filenames) for each directory
C) List of all files
D) Directory sizes

**Answer: B**

**Explanation:**
`os.walk()` traverses directory tree recursively. Each iteration: current directory path, list of subdirectory names, list of filenames. Use for finding files, calculating sizes, etc.

---

**Q15.33: Intermediate - [glob Pattern Matching]**

What is the output?
```python
from pathlib import Path
# Assuming files: a.txt, b.txt, c.py exist
print([p.name for p in Path('.').glob('*.txt')])
```

A) All files
B) `['a.txt', 'b.txt']`
C) `['*.txt']`
D) Error

**Answer: B**

**Explanation:**
`glob()` matches files by pattern. `*.txt` matches all .txt files. `**/*.txt` matches recursively. Returns Path objects. Also available as `glob.glob('*.txt')` returning strings.

---

**Q15.34: Intermediate - [Binary File Operations]**

What is the output?
```python
with open('binary.bin', 'wb') as f:
    f.write(b'\x00\x01\x02')

with open('binary.bin', 'rb') as f:
    data = f.read()
    print(type(data), len(data))
```

A) `<class 'str'>, 3`
B) `<class 'bytes'>, 3`
C) `<class 'list'>, 3`
D) Error

**Answer: B**

**Explanation:**
Binary mode (`'rb'`/`'wb'`) works with bytes objects. Write/read raw binary data. `len(data)` is 3 bytes. Use for images, audio, any non-text files.

---

**Q15.35: Intermediate - [struct Module]**

What does `struct.pack('!I', 1000)` do?

A) Creates struct
B) Packs integer 1000 as network byte order (big-endian) 4-byte unsigned int
C) Compresses data
D) Hashes data

**Answer: B**

**Explanation:**
`struct` converts between Python values and C structs/binary data. `!I` = network order unsigned int. `struct.unpack('!I', data)` reverses. Essential for binary protocols, file formats.

---

**Q15.36: Intermediate - [File Position]**

What do `tell()` and `seek()` do?

A) File size and creation
B) tell() returns current position; seek() moves to a position
C) Read and write
D) Open and close

**Answer: B**

**Explanation:**
`f.tell()` returns byte offset from file start. `f.seek(offset, whence)` moves position. `whence`: 0=start, 1=current, 2=end. Used for random access in binary files.

---

**Q15.37: Intermediate - [File Buffering]**

What does `open(file, buffering=0)` mean?

A) Default buffering
B) Unbuffered — write immediately (binary mode only)
C) Maximum buffering
D) Line buffering

**Answer: B**

**Explanation:**
`buffering=0` — unbuffered (only valid for binary). `1` — line buffered (text mode). `>1` — buffer size in bytes. `-1` or omit — system default. Unbuffered means immediate I/O, no caching.

---

**Q15.38: Intermediate - [Flushing]**

What does `file.flush()` do?

A) Clears the file
B) Writes buffered data to underlying file immediately
C) Refreshes file handle
D) Clears read buffer

**Answer: B**

**Explanation:**
`flush()` forces buffered data to be written. Normally, buffer flushes on close or when full. Use `flush()` when you need data visible before closing (e.g., for other processes to read).

---

**Q15.39: Intermediate - [stdin/stdout]**

What are `sys.stdin`, `sys.stdout`, `sys.stderr`?

A) Strings
B) File-like objects for standard input, output, and error streams
C) Functions
D) Constants

**Answer: B**

**Explanation:**
Standard streams are file-like objects. `print()` writes to `sys.stdout`. `input()` reads from `sys.stdin`. You can redirect: `sys.stdout = open('log.txt', 'w')`. Restore original from `sys.__stdout__`.

---

**Q15.40: Intermediate - [Open Mode "x"]**

What does mode `"x"` do?

A) Execute file
B) Exclusive creation — fails if file exists
C) Extended write
D) External file

**Answer: B**

**Explanation:**
`"x"` creates file, fails with FileExistsError if already exists. Prevents accidental overwrite. Safer than `"w"` when you want to create new file only. Combine with `b` for binary: `"xb"`.

---

**Q15.41: Intermediate - [Open Mode "r+"]**

What does mode `"r+"` do?

A) Read only
B) Read and write (file must exist, no truncation)
C) Write only
D) Append

**Answer: B**

**Explanation:**
`"r+"` opens for reading AND writing. File must exist. Doesn't truncate. Position starts at beginning. Compare: `"w+"` truncates first; `"a+"` appends. All + modes allow both read and write.

---

**Q15.42: Intermediate - [with Statement Importance]**

Why is `with open()` preferred over manual open/close?

A) Faster
B) Guarantees file closure even if exception occurs
C) Shorter code only
D) Required by Python

**Answer: B**

**Explanation:**
`with` uses context manager protocol. `__exit__` is called on block exit — normal or exception. Prevents resource leaks. Manual `f.close()` might not run if exception occurs before it.

---

**Q15.43: Intermediate - [fileinput Module]**

What does `fileinput` module do?

A) Creates file inputs
B) Iterates over lines from multiple files (like Unix tools)
C) File input validation
D) UI forms

**Answer: B**

**Explanation:**
`for line in fileinput.input(['file1.txt', 'file2.txt']):` iterates over all lines from multiple files. If no files, reads stdin. filename() and lineno() give current position. Unix filter pattern.

---

**Q15.44: Intermediate - [io.StringIO / io.BytesIO]**

What is the output?
```python
from io import StringIO

buffer = StringIO()
buffer.write('Hello')
buffer.seek(0)
print(buffer.read())
```

A) Error
B) `Hello`
C) Empty
D) `StringIO`

**Answer: B**

**Explanation:**
`StringIO` is in-memory file-like object for strings. `BytesIO` for bytes. Write to buffer, seek to start, read back. Useful for testing, when API expects file but you have string/bytes.

---

**Q15.45: Intermediate - [File Descriptors]**

What are file descriptors?

A) File descriptions
B) Low-level integer handles to open files/streams
C) File types
D) File sizes

**Answer: B**

**Explanation:**
OS uses integers (0=stdin, 1=stdout, 2=stderr) to track open files. `f.fileno()` gets descriptor. Low-level I/O with `os.read(fd, n)`. Python files wrap descriptors with buffering and encoding.

---

**Q15.46: Advanced - [configparser]**

What format does `configparser` handle?

A) JSON
B) INI-style configuration files
C) YAML
D) XML

**Answer: B**

**Explanation:**
`configparser` reads/writes INI files: `[section]` headers, `key = value` pairs. Common for configuration. `config.read('file.ini'); config['section']['key']`. Standard library alternative to JSON/YAML for config.

---

**Q15.47: Advanced - [mmap for Large Files]**

What is `mmap` advantage for large files?

A) Compression
B) Memory-mapped access — OS handles paging, random access without loading entire file
C) Encryption
D) Speed

**Answer: B**

**Explanation:**
`mmap.mmap(file.fileno(), 0)` maps file to memory. Access like bytearray. OS loads only needed pages. Efficient for large files with random access. Can share between processes.

---

**Q15.48: Intermediate - [JSON Formatting]**

What is the output?
```python
import json
data = {'a': 1, 'b': 2}
print(json.dumps(data, indent=2, sort_keys=True))
```

A) `{"a":1,"b":2}`
B) Pretty-printed JSON with keys sorted alphabetically
C) Error
D) `{'a': 1, 'b': 2}`

**Answer: B**

**Explanation:**
`indent=2` adds newlines and 2-space indentation. `sort_keys=True` alphabetizes keys. Output is human-readable. Default `indent=None` is compact. `separators=(',', ':')` for minimal size.

---

**Q15.49: Intermediate - [YAML (PyYAML)]**

What is YAML better for than JSON?

A) Speed
B) Human readability, comments, complex structures (but requires external library)
C) Security
D) Nothing

**Answer: B**

**Explanation:**
YAML: human-readable, supports comments, multi-line strings, references. JSON: simpler, built-in. Use `pyyaml` package. ⚠️ Use `yaml.safe_load()` not `yaml.load()` for security (similar to pickle). Good for config files.

---

**Q15.50: Intermediate - [File Locking]**

How do you lock a file for exclusive access?

A) Use `Lock()` from threading
B) Use `fcntl.flock()` (Unix) or `msvcrt.locking()` (Windows), or `portalocker` library
C) Open in 'x' mode
D) Files are automatically locked

**Answer: B**

**Explanation:**
File locking is OS-specific. Unix: `fcntl.flock(f.fileno(), fcntl.LOCK_EX)`. Windows: `msvcrt.locking()`. Cross-platform: `portalocker` or `filelock` packages. Prevents concurrent writes from multiple processes.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 8 | 16% |
| Intermediate | 40 | 80% |
| Advanced | 2 | 4% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- open() modes and parameters
- Text vs binary mode
- Encoding handling
- pathlib.Path vs os.path
- JSON serialization
- pickle (and security warnings)
- CSV reading/writing
- tempfile module
- shelve for persistence
- File operations (copy, move, delete)
- Directory handling
- Binary data with struct
