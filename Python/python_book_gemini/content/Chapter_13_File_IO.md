# Chapter 13: File I/O & Serialization

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: File modes (`r`, `w`, `a`, `x`, `b`), Encoding, `json` module, `pickle` security, `csv` module, `pathlib` basics, `io` streams (`StringIO`, `BytesIO`), Buffering.

---

**Q13.1: Basic - [Open Default Mode]**

`open('file.txt')` is equivalent to:

A) `open('file.txt', 'w')`
B) `open('file.txt', 'rb')`
C) `open('file.txt', 'rt')`
D) `open('file.txt', 'a')`

**Answer: C**

**Explanation:**
The default mode is `'rt'` (read text).

---

**Q13.2: Intermediate - [Exclusive Creation]**

Which mode opens a file for writing *only if* it does not already exist?

A) `'w'`
B) `'a'`
C) `'x'`
D) `'n'`

**Answer: C**

**Explanation:**
`'x'` (exclusive creation) raises `FileExistsError` if the file already exists.

---

**Q13.3: Advanced - [JSON Keys]**

When using `json.dumps({1: 'a'})`, the output dictionary key will be:

A) Integer `1`.
B) String `"1"`.
C) Raises TypeError.
D) `1.0`.

**Answer: B**

**Explanation:**
JSON standard requires keys to be strings. Python's `json` module automatically converts non-string dictionary keys (like ints) to strings during serialization.

---

**Q13.4: Basic - [Readlines]**

`f.readlines()` returns:

A) A generator.
B) A list of strings (lines).
C) A single string containing the whole file.
D) The number of lines.

**Answer: B**

**Explanation:**
It reads the entire file and returns a list where each element is a line (including the newline character).

---

**Q13.5: Intermediate - [Pickle Protocol]**

What is a major security risk of `pickle.load()`?

A) It is slow.
B) It can execute arbitrary code during deserialization.
C) It cannot handle circular references.
D) It creates huge files.

**Answer: B**

**Explanation:**
Pickle is not secure. Loading untrusted data can execute malicious code because the pickle format allows specifying arbitrary callables to construct objects.

---

**Q13.6: Advanced - [File Pointer Seek]**

`f.seek(offset, whence)`: `whence=2` means:

A) From the beginning.
B) From the current position.
C) From the end of the file.
D) From the start of the line.

**Answer: C**

**Explanation:**
`0`: Start (default), `1`: Current, `2`: End. (Note: In text mode, `seek` relative to end is restricted).

---

**Q13.7: Basic - [Context Manager File]**

The best way to open a file is:

A) `f = open(...)` then `f.close()`
B) `with open(...) as f:`
C) `try: open(...) except:`
D) `f = File(...)`

**Answer: B**

**Explanation:**
The `with` statement ensures the file is closed automatically even if exceptions occur.

---

**Q13.8: Intermediate - [Buffering]**

When opening a file with `buffering=0` (unbuffered), the mode must be:

A) Text (`'t'`)
B) Binary (`'b'`)
C) Append (`'a'`)
D) Read (`'r'`)

**Answer: B**

**Explanation:**
Unbuffered I/O is only allowed in binary mode. Text mode requires buffering to handle encoding/decoding efficiently.

---

**Q13.9: Advanced - [Pathlib Join]**

Using `pathlib`, how do you join paths?

A) `os.path.join(p, 'sub')`
B) `p.join('sub')`
C) `p / 'sub'`
D) `p + 'sub'`

**Answer: C**

**Explanation:**
The `/` operator is overloaded for `Path` objects to join path components.

---

**Q13.10: Expert - [JSON Custom Encoder]**

To serialize a custom object `obj` to JSON, you pass a `default` function to `dump` which should:

A) Return a JSON string.
B) Return a serializable object (like dict/list) or raise `TypeError`.
C) Modify `obj` in place.
D) Return `None`.

**Answer: B**

**Explanation:**
The `default(obj)` function is called for objects that `json` doesn't know how to serialize. It should reduce the object to a standard type (dict, list, str, etc.) that *is* serializable.

---

**Q13.11: Basic - [CSV Reading]**

`csv.reader(f)` returns:

A) A list of lists.
B) An iterator yielding lists of strings.
C) A dict reader.
D) A pandas DataFrame.

**Answer: B**

**Explanation:**
It returns an iterator where each row is returned as a list of strings.

---

**Q13.12: Intermediate - [Globbing]**

`Path('.').glob('**/*.py')` does what?

A) Finds all `.py` files in current directory only.
B) Finds all `.py` files recursively in current and sub-directories.
C) Raises SyntaxError.
D) Returns a list immediately.

**Answer: B**

**Explanation:**
The `**` pattern implies recursive searching through subdirectories. It returns a generator.

---

**Q13.13: Advanced - [BytesIO]**

`io.BytesIO(b'data')` behaves like:

A) A string.
B) A file opened in binary mode (`'rb'/'wb'`) but in memory.
C) A file opened in text mode.
D) A bytearray.

**Answer: B**

**Explanation:**
It provides a file-like interface (read, write, seek) for bytes data stored in memory buffers.

---

**Q13.14: Basic - [Mode 'w+']**

Mode `'w+'` means:

A) Write and Append.
B) Read and Write (Truncate existing).
C) Write only (Strict).
D) Write and Create.

**Answer: B**

**Explanation:**
`+` indicates updating (read/write). The `w` indicates it invalidates (truncates) the file contents on open. (Contrast with `r+` which opens for update without truncating).

---

**Q13.15: Intermediate - [Flush]**

`f.flush()`:

A) Clears the file content.
B) Forces the write buffer to be emptied (written to OS).
C) Closes the file.
D) Resets the pointer.

**Answer: B**

**Explanation:**
It ensures that data stored in the internal application buffer is pushed to the Operating System's file buffer.

---

**Q13.16: Advanced - [Tell Position]**

`f.tell()` returns:

A) The file name.
B) The current file pointer position (in bytes or chars).
C) The size of the file.
D) The file mode.

**Answer: B**

**Explanation:**
In binary mode, it's the byte offset. In text mode, it's an opaque number (rarely useful for calculation, mostly for passing back to `seek`).

---

**Q13.17: Expert - [TextIOWrapper]**

To change the encoding of an already open binary file `f_bin` to read text:

A) `f_bin.encoding = 'utf-8'`
B) `io.TextIOWrapper(f_bin, encoding='utf-8')`
C) `str(f_bin.read())`
D) It's impossible.

**Answer: B**

**Explanation:**
You can wrap a binary stream (buffered reader) in `TextIOWrapper` to handle decoding/encoding transparently.

---

**Q13.18: Intermediate - [JSON Load vs Loads]**

Difference between `json.load` and `json.loads`:

A) `load` is for files (takes file-like object), `loads` is for strings (s = string).
B) No difference.
C) `load` is faster.
D) `loads` is for lists.

**Answer: A**

**Explanation:**
Common convention in Python serialization modules: `load`/`dump` work with files, `loads`/`dumps` work with strings/bytes.

---

**Q13.19: Basic - [Newline Argument]**

`open('f.txt', newline='')` is used to:

A) Remove newlines.
B) Disable universal newlines translation (return newlines as is `\r`, `\n`, or `\r\n`).
C) Add newlines automatically.
D) Ignore empty lines.

**Answer: B**

**Explanation:**
By default, Python translates all line endings to `\n` on read. `newline=''` prevents this translation, preserving the original bytes/chars. Essential for working with CSV module.

---

**Q13.20: Advanced - [Shelve Module]**

The `shelve` module provides:

A) A dict-like interface to a persistent storage (using pickle).
B) A shelf for UI.
C) A SQL database wrapper.
D) A way to run shell commands.

**Answer: A**

**Explanation:**
It creates a persistent, dictionary-like object backed by a database file (dbm), where values are pickled Python objects.

---

**Q13.21: Expert - [File Descriptors]**

`f.fileno()` returns:

A) The filename.
B) The integer file descriptor (fd) used by the OS.
C) The file size.
D) `None` for real files.

**Answer: B**

**Explanation:**
It returns the low-level integer file descriptor (e.g., 0 for stdin, 1 for stdout) used by the OS kernel. Not all file-like objects (e.g., `StringIO`) have one.

---

**Q13.22: Intermediate - [Write Lines]**

`f.writelines(list_of_strings)`:

A) Writes strings and adds newlines automatically.
B) Writes strings concatenated (does NOT add newlines).
C) Raises error if newlines are missing.
D) Write a list object.

**Answer: B**

**Explanation:**
Despite the name, `writelines` does *not* append newlines. You must ensure the strings in the list already have `\n`.

---

**Q13.23: Basic - [Pathlib Exists]**

Check if a path exists:

A) `Path('obj').exists()`
B) `Path('obj').check()`
C) `os.exists('obj')`
D) `Path('obj').is_file()`

**Answer: A**

**Explanation:**
The `exists()` method checks for the presence of either a file or directory.

---

**Q13.24: Advanced - [Json SkipKeys]**

`json.dump(data, skipkeys=True)`:

A) Skips dictionary keys that are not basic types (instead of raising TypeError).
B) Skips private keys.
C) Skips missing keys.
D) Skips `None`.

**Answer: A**

**Explanation:**
Allows serialization to proceed by ignoring dict keys that are not strings, numbers, or None (which would otherwise cause a TypeError).

---

**Q13.25: Intermediate - [Seek from End Text]**

In text mode (`'t'`), `seek(offset, 2)` (from end) is:

A) Allowed for any offset.
B) Allowed only for offset 0 (seek to end).
C) Ignored.
D) The default.

**Answer: B**

**Explanation:**
In text mode, because of variable-length encoding, seeking partially from the end is undefined/forbidden. Only `seek(0, 2)` (jumping to the very end) is supported.

---

**Q13.26: Expert - [Iterating File]**

Is `for line in f:` preferred over `for line in f.readlines():`?

A) No.
B) Yes, because it uses lazy loading (memory efficient).
C) They are identical.
D) No, `readlines` is faster.

**Answer: B**

**Explanation:**
Direct iteration over the file object reads lines one by one, whereas `readlines()` loads the entire file into memory as a list first.

---

**Q13.27: Basic - [Latin-1 Encoding]**

`latin-1` (or `iso-8859-1`) encoding:

A) Maps byte values 0-255 directly to unicode code points 0-255.
B) Is the default in Python 3.
C) Cannot handle all bytes.
D) Is variable width.

**Answer: A**

**Explanation:**
It effectively maps bytes 1:1 to the first 256 Unicode characters. It can decode *any* byte stream (never raises UnicodeDecodeError), unlike UTF-8.

---

**Q13.28: Advanced - [Ctypes Structure]**

To allow `pickle` to handle a custom class `__getstate__` should return:

A) The object itself.
B) The state (usually `__dict__`) to be pickled.
C) True.
D) JSON string.

**Answer: B**

**Explanation:**
`__getstate__` allows customizing what exactly gets pickled (e.g. omitting open file handles or locks). `__setstate__` restores it.

---

**Q13.29: Intermediate - [Pathlib Parent]**

`Path('/a/b/c.txt').parent` is:

A) `'/a'`
B) `'/a/b'` (Path object)
C) `'b'`
D) `c.txt`

**Answer: B**

**Explanation:**
It returns the directory containing the file.

---

**Q13.30: Expert - [Universal Newlines]**

If a file has `\r\n` (Windows) line endings and is opened in `'r'` (text) mode:

A) `read()` sees `\r\n`.
B) `read()` sees `\n` (translated).
C) `read()` sees `\r`.
D) Error.

**Answer: B**

**Explanation:**
Python's universal newlines support (default in text mode) translates external line endings (`\r\n`, `\r`) into `\n` internally.

---

**Q13.31: Intermediate - [Pathlib ReadText]**

`Path('file.txt').read_text()`:

A) Opens, reads content, and closes the file.
B) Returns a generator.
C) Reads only one line.
D) Leaves the file open.

**Answer: A**

**Explanation:**
It's a convenience method that handles opening, reading the entire content as a string, and closing the file automatically.

---

**Q13.32: Advanced - [File Truncate]**

`f.truncate(size)`:

A) Truncates the file to `size` bytes. If `size` is larger, it pads with nulls (platform dependent).
B) Deletes the file.
C) Cuts the file from the beginning.
D) Splits the file.

**Answer: A**

**Explanation:**
Resizes the file to the given size. If `size` is omitted, uses the current position.

---

**Q13.33: Basic - [Pickle Dumps]**

`pickle.dumps(obj)` returns:

A) A string.
B) A bytes object.
C) A file object.
D) None.

**Answer: B**

**Explanation:**
Pickle serializes to a binary format, so it produces `bytes`, unlike JSON which produces `str`.

---

**Q13.34: Expert - [Buffer Policy]**

Standard standard output (`sys.stdout`) is usually:

A) Unbuffered.
B) Line-buffered (if connected to a terminal).
C) Fully buffered.
D) Randomly buffered.

**Answer: B**

**Explanation:**
Interactive terminals default to line buffering (flushes on `\n`). Redirecting to a file usually switches to block buffering.

---

**Q13.35: Intermediate - [Read Byte]**

`f.read(1)` in binary mode (`'rb'`) returns:

A) A string of length 1.
B) An integer.
C) A bytes object of length 1.
D) `None` at EOF.

**Answer: C**

**Explanation:**
It returns a `bytes` object (e.g., `b'x'`). At EOF, it returns empty bytes `b''`.

---

**Q13.36: Advanced - [JSON Separators]**

To generate compact JSON (no spaces):

A) `json.dumps(data, separators=(',', ':'))`
B) `json.dumps(data, compact=True)`
C) `json.dumps(data, indent=0)`
D) It's the default.

**Answer: A**

**Explanation:**
By default, JSON uses `(', ', ': ')` (adding whitespace). Passing `(',', ':')` removes the spaces.

---

**Q13.37: Basic - [Path Resolving]**

`Path('..').resolve()` returns:

A) The relative path.
B) The absolute path, resolving symlinks and `..` segments.
C) Variable.
D) Error.

**Answer: B**

**Explanation:**
It makes the path absolute and canonical.

---

**Q13.38: Intermediate - [CSV Dictionary Writer]**

`csv.DictWriter` requires:

A) Just the file object.
B) The file object and a `fieldnames` list.
C) A pandas dataframe.
D) Nothing.

**Answer: B**

**Explanation:**
You must provide `fieldnames` so it knows the order of columns and which keys to map to which column.

---

**Q13.39: Advanced - [String Formatting in Write]**

`f.write(f'{x}')` vs `print(x, file=f)`:

A) `write` automatically adds newline, `print` doesn't.
B) `print` converts `x` to string and adds newline (by default), `write` requires string and adds nothing.
C) Identical.
D) `write` is slower.

**Answer: B**

**Explanation:**
`f.write()` only accepts strings and writes exactly what is passed. `print` handles type conversion and formatting (newlines/separators).

---

**Q13.40: Expert - [IOBase Class]**

`io.IOBase` is:

A) The abstract base class for all I/O classes.
B) A concrete class for reading text.
C) Same as `file`.
D) A integer descriptor.

**Answer: A**

**Explanation:**
The top-level abstract base class in the `io` hierarchy.

---

**Q13.41: Intermediate - [Json Decode Error]**

`json.loads("{'a': 1}")` raises:

A) `ValueError` (JSONDecodeError).
B) `TypeError`.
C) Nothing, returns dict.
D) SyntaxError.

**Answer: A**

**Explanation:**
JSON requires double quotes `"` for strings. Single quotes `'` are invalid JSON syntax.

---

**Q13.42: Basic - [Open With Encoding]**

If you open a text file without specifying encoding:

A) It uses UTF-8 always.
B) It uses `locale.getpreferredencoding()` (platform dependent).
C) It raises an error.
D) It uses ASCII.

**Answer: B**

**Explanation:**
Default encoding is platform-dependent (e.g., `cp1252` on Windows, `utf-8` on Linux). (Note: Python 3.15+ changes this default to UTF-8, but historically/currently it depends on locale).

---

**Q13.43: Advanced - [Seekable]**

`sys.stdin.seekable()` typically returns:

A) `True`.
B) `False`.
C) Raises Error.
D) `None`.

**Answer: B**

**Explanation:**
Standard input is a stream (pipe or terminal input), which is not seekable (cannot go back).

---

**Q13.44: Expert - [CSV Sniffer]**

`csv.Sniffer().sniff(sample)` determines:

A) If the file is malicious.
B) The dialect (delimiter, quotechar) of the CSV format.
C) The encoding.
D) The number of rows.

**Answer: B**

**Explanation:**
It analyzes a sample of the file to guess its format (comma vs tab delimited, interactions of quotes, etc.).

---

**Q13.45: Intermediate - [Pathlib Stem]**

`Path('/path/to/archive.tar.gz').stem` returns:

A) `archive`
B) `archive.tar`
C) `tar.gz`
D) `.gz`

**Answer: B**

**Explanation:**
`.stem` returns the final component name without the *last* suffix (`.gz`). If you want `archive`, you might need to call stem twice or parse suffixes.

---

**Q13.46: Basic - [Readlines Hint]**

`f.readlines(hint)`:

A) Reads exactly `hint` lines.
B) Reads lines until the total number of bytes/characters exceeds `hint`.
C) Reads line number `hint`.
D) Is deprecated.

**Answer: B**

**Explanation:**
The argument controls the approximate number of bytes to read, not lines.

---

**Q13.47: Advanced - [Nameless BytesIO]**

Does `io.BytesIO` have a `name` attribute?

A) Yes, always `<bytesio>`.
B) No.
C) Yes, if passed in constructor.
D) Only `StringIO`.

**Answer: B**

**Explanation:**
In-memory streams do not have a `name` attribute by default (unlike real file objects). Accessing it raises `AttributeError` unless you manually set it.

---

**Q13.48: Expert - [Fcntl]**

The `fcntl` module (file control) is available on:

A) Windows and Unix.
B) Unix/Linux only.
C) Windows only.
D) Mac only.

**Answer: B**

**Explanation:**
`fcntl` provides low-level file control (locking, etc.) specific to Unix-like systems. For cross-platform file locking, libraries like `portalocker` are used.

---

**Q13.49: Intermediate - [Json Dump Sort Keys]**

`json.dump(data, sort_keys=True)` is useful for:

A) Performance.
B) Deterministic output (essential for hashing/comparing JSON).
C) Numerical sorting.
D) Syntax highlighting.

**Answer: B**

**Explanation:**
It outputs dictionary keys in sorted order, ensuring that the same data produces the exact same string representation every time.

---

**Q13.50: Basic - [Closing with Exception]**

If `f.close()` is called twice:

A) It raises an error the second time.
B) It does nothing the second time.
C) It re-opens the file.
D) It crashes interpreter.

**Answer: B**

**Explanation:**
Closing an already closed file is a no-op (safe).

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
