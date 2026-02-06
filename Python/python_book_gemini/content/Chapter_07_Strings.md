# Chapter 7: Strings & Text Processing

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: String Syntax, Formatting (f-strings, %, format), Unicode/Bytes, Standard Methods, Interning.

---

**Q7.1: Basic - [String Immutability]**

Which of the following operations raises an error?
```python
s = "hello"
```

A) `s = s + " world"`
B) `s = s.upper()`
C) `s[0] = "H"`
D) `s = "H" + s[1:]`

**Answer: C**

**Explanation:**
Strings in Python are immutable. You cannot modify characters in-place using item assignment (`s[0] = ...`). All string methods/operations return a *new* string.

---

**Q7.2: Intermediate - [Raw Strings]**

What is the primary purpose of a "raw" string `r"..."`?

A) It stores data in binary format.
B) It ignores escape sequences (like `\n`, `\t`) treating backslashes as literal characters.
C) It allows faster processing.
D) It is deprecated in favor of f-strings.

**Answer: B**

**Explanation:**
Raw strings treat backslashes as literal characters. `r"\n"` is a string of two characters (`\` and `n`), not a newline. Commonly used in Regex and file paths.

---

**Q7.3: Advanced - [Casefold]**

How does `str.casefold()` differ from `str.lower()`?

A) No difference.
B) `casefold` is more aggressive, converting more characters to lowercase (e.g., German 'ß' to 'ss') for full Unicode case-insensitive matching.
C) `casefold` only works on ASCII.
D) `lower` is deprecated.

**Answer: B**

**Explanation:**
`casefold()` is designed for caseless matching (normalization) and handles special Unicode cases (like the German sharp S 'ß' becoming 'ss') that `lower()` might miss.

---

**Q7.4: Basic - [Join Method]**

Syntax to join a list `words` with a comma?

A) `words.join(",")`
B) `",".join(words)`
C) `join(words, ",")`
D) `String.join(",", words)`

**Answer: B**

**Explanation:**
`join` is a string method, called on the *separator*. `separator.join(iterable)`.

---

**Q7.5: Intermediate - [Find vs Index]**

What happens if `s.find("x")` and `s.index("x")` do not find the substring?

A) Both return -1.
B) Both raise ValueError.
C) `find` returns -1, `index` raises ValueError.
D) `find` raises ValueError, `index` returns -1.

**Answer: C**

**Explanation:**
`find()` is safer (returns -1) if you expect failures. `index()` assumes presence and errors out if missing.

---

**Q7.6: Advanced - [String Interning]**

When does Python guarantee to "intern" (cache) strings?

A) All strings are interned.
B) Only compile-time string constants consisting mainly of ASCII identifiers (alphanumerics + underscore).
C) Only strings shorter than 20 chars.
D) Never automatically.

**Answer: B**

**Explanation:**
CPython automatically interns string literals that look like identifiers (only alphanumerics and underscores) to optimize dictionary lookups. Dynamic strings or strings with special chars are usually not interned unless `sys.intern()` is used.

---

**Q7.7: Basic - [F-String Debug]**

In Python 3.8+, what does `f"{val=}"` produce if `val=5`?

A) `"5"`
B) `"val=5"`
C) `"val"`
D) Error.

**Answer: B**

**Explanation:**
The `=` specifier in f-strings expands to the expression text, an equal sign, and the evaluated representation: `val=5`.

---

**Q7.8: Intermediate - [Strip Args]**

`"www.example.com".strip("w.com")` returns:

A) `"example"`
B) `"example.com"`
C) `"www.example"`
D) `"e"`

**Answer: A**

**Explanation:**
`strip` removes *any* character in the argument string from the leading/trailing ends. `w`, `.`, `c`, `o`, `m` are removed from both ends.
- Left: `www.` is stripped. `e` remains.
- Right: `m`, `o`, `c`, `.` are stripped. `e` remains.
Result: `"example"`.

---

**Q7.9: Advanced - [Encoding Error Handling]**

To decode bytes ignoring invalid characters:

A) `b.decode('utf-8', errors='ignore')`
B) `b.decode('utf-8', errors=True)`
C) `b.decode('utf-8', strict=False)`
D) `b.force_decode()`

**Answer: A**

**Explanation:**
The `errors` parameter dictates handling: `'strict'` (default, raises), `'ignore'` (drops chars), `'replace'` (inserts ).

---

**Q7.10: Expert - [String Concatenation Complexity]**

Adding strings in a loop `s += part` forces a re-allocation every time. Typical time complexity for N parts of total length L?

A) O(L)
B) O(N)
C) O(L^2) usually (quadratic).
D) O(L log L)

**Answer: C**

**Explanation:**
Naive concatenation creates a new string object copying all previous characters each iteration. Sum of 1+2+...+N length operations leads to quadratic behavior. (CPython has a peephole optimization for `s = s + t` in *some* cases, but generally it's considered O(N^2)).

---

**Q7.11: Basic - [Slicing Step]**

`"Python"[::-1]` returns:

A) `"Python"`
B) `"nohtyP"`
C) Error.
D) `['P', 'y', ...]`

**Answer: B**

**Explanation:**
A negative step `-1` reverses the string.

---

**Q7.12: Intermediate - [Partition]**

`"a:b:c".partition(":")` returns:

A) `['a', 'b', 'c']`
B) `('a', ':', 'b:c')`
C) `('a', 'b', 'c')`
D) `('a', ':', 'b')`

**Answer: B**

**Explanation:**
`partition(sep)` splits at the *first* occurrence of sep and returns a 3-tuple: `(before, sep, after)`.

---

**Q7.13: Advanced - [Title Case]**

`"hello's world".title()` results in:

A) `"Hello's World"`
B) `"Hello'S World"`
C) `"Hello's world"`
D) `"Hello'S world"`

**Answer: B**

**Explanation:**
`title()` works by algorithmically uppercasing the first letter after *any* non-letter character. Since `'` is non-letter, the `s` becomes `S`. This is often considered a "bug" or "feature" where `string.capwords` or custom logic is preferred for real text.

---

**Q7.14: Basic - [Bytes Literal]**

How do you denote a bytes literal?

A) `b"hello"`
B) `x"hello"`
C) `bytes("hello")`
D) `&"hello"`

**Answer: A**

**Explanation:**
Prefix `b` creates a `bytes` object (sequence of bytes, restricted to ASCII range characters in literal, use `\xNN` for others).

---

**Q7.15: Intermediate - [Zfill]**

`"42".zfill(5)` returns:

A) `"42000"`
B) `"00042"`
C) `"42   "`
D) `"   42"`

**Answer: B**

**Explanation:**
`zfill(width)` pads the string on the left with zeros until width is reached.

---

**Q7.16: Advanced - [Format Map]**

`"{name} is {age}".format_map({'name': 'Ali', 'age': 30})` is similar to `.format()`, but:

A) It creates a new dictionary.
B) It avoids copying the dictionary (uses it directly).
C) It allows list arguments.
D) It uses f-strings internally.

**Answer: B**

**Explanation:**
`format_map` takes a mapping object directly. Useful if passing a subclass of dict (like `defaultdict` or custom lookup) without unpacking it into `**kwargs` (which creates a new dict).

---

**Q7.17: Expert - [UTF-8 properties]**

UTF-8 encoding of English text (ASCII) is:

A) 2 bytes per char.
B) 4 bytes per char.
C) Identical to ASCII (1 byte).
D) Variable (1-4 bytes), but 2 for ASCII.

**Answer: C**

**Explanation:**
UTF-8 is backward compatible with ASCII. Characters 0-127 are encoded as single 8-bit bytes identical to ASCII values.

---

**Q7.18: Intermediate - [Isspace]**

`"\n \t".isspace()` returns:

A) True
B) False
C) Error
D) None

**Answer: A**

**Explanation:**
`isspace()` returns True if all characters are whitespace (spaces, tabs, newlines, etc.) and there is at least one character.

---

**Q7.19: Basic - [Multiline String]**

What is the output?
```python
x = """
A
B"""
len(x)
```
(Assuming standard newline `\n`).

A) 2
B) 3
C) 4
D) 5

**Answer: C**

**Explanation:**
It starts with a newline (after `"""`), then `A`, then newline, then `B`. Total 4: `\n`, `A`, `\n`, `B`. (Note: many editors might strip trailing newline or indentation, but strictly `"""<enter>` includes the enter).
Actually let's trace: `"""\nA\nB"""`. Yes `\n` (1) `A` (1) `\n` (1) `B` (1). Length 4.

---

**Q7.20: Advanced - [Str vs Repr]**

The goal of `__str__` is readability, the goal of `__repr__` is:

A) Accuracy/Debugging (unambiguous).
B) Serialization to JSON.
C) Fancy formatting.
D) Speed.

**Answer: A**

**Explanation:**
`__repr__` aims to be unambiguous and, if possible, a valid Python expression that could recreate the object (e.g. quotes around strings).

---

**Q7.21: Intermediate - [Split Maxsplit]**

`"a b c d".split(" ", 2)` returns:

A) `['a', 'b', 'c d']`
B) `['a', 'b', 'c', 'd']`
C) `['a', 'b c d']`
D) `['a', 'b', 'c']`

**Answer: A**

**Explanation:**
`maxsplit=2` means split *at most* 2 times. Results in 3 parts: `a`, `b`, and the remainder `c d`.

---

**Q7.22: Basic - [Bytes Indexing]**

If `b = b"ABC"`, `b[0]` returns:

A) `"A"`
B) `b"A"`
C) `65` (Int)
D) `[65]`

**Answer: C**

**Explanation:**
Indexing a `bytes` object returns the integer value (0-255) of that byte. Slicing `b[0:1]` returns a `bytes` object `b"A"`.

---

**Q7.23: Advanced - [Ord vs Chr]**

`chr(ord('a') + 1)` returns:

A) `'b'`
B) `98`
C) `b'b'`
D) Error.

**Answer: A**

**Explanation:**
`ord('a')` is 97. `97+1=98`. `chr(98)` is `'b'`.

---

**Q7.24: Expert - [String Comparison]**

Python compares strings using:

A) Random order.
B) Length first.
C) Unicode Code Point keys (lexicographically).
D) Locale-dependent rules.

**Answer: C**

**Explanation:**
Comparison is strict character-by-character based on Unicode code point numbers. `"Z" < "a"` because 90 < 97. It does NOT depend on standard locale sorting unless using `locale.strcoll`.

---

**Q7.25: Intermediate - [Center Alignment]**

`"HI".center(5, "-")` results in:

A) `"--HI-"` (biased left) or `"-HI--"`
B) `"  HI "`
C) `"HI---"`
D) `"---HI"`

**Answer: A**

**Explanation:**
For odd padding (5-2=3), standard Python behavior puts the extra character on the right: `"-HI--"`.

---

**Q7.26: Basic - [Formatting %]**

`"%.2f" % 3.14159` produces:

A) `"3.14"`
B) `"3.14159"`
C) `"3.15"` (Rounding?)
D) `"03.14"`

**Answer: A**

**Explanation:**
`%.2f` denotes a float with 2 decimal places. 3.14.

---

**Q7.27: Advanced - [Expandtabs]**

`"A\tB".expandtabs(4)` essentially:

A) Replaces `\t` with 4 spaces.
B) Replaces `\t` with enough spaces to reach the next multiple of 4 column.
C) Inserts 4 tabs.
D) Removes tabs.

**Answer: B**

**Explanation:**
It's not a fixed replacement. It behaves like a tab stop, padding to the next 4-char alignment boundary.

---

**Q7.28: Intermediate - [Encode Default]**

`"hello".encode()` uses which encoding by default?

A) ASCII
B) UTF-8
C) UTF-16
D) Latin-1

**Answer: B**

**Explanation:**
Python 3 defaults to UTF-8 for string encoding tasks.

---

**Q7.29: Expert - [Isidentifier]**

Which string returns `False` for `.isidentifier()`?

A) `_var`
B) `var1`
C) `1var`
D) `你好` (Chinese valid in Py3)

**Answer: C**

**Explanation:**
Identifiers cannot start with a digit. `1var` is invalid. Python 3 supports Unicode identifiers, so `你好` is True.

---

**Q7.30: Basic - [Newlines]**

To create a string spanning multiple lines, you can use:

A) `\n` characters.
B) Triple quotes `"""`.
C) Parentheses with adjacent strings (e.g. `("A" "B")`).
D) All of the above.

**Answer: D**

**Explanation:**
All are valid mechanics. `\n` is the char. `"""` facilitates typing it. Implicit concatenation inside parenthesis `("Line1\n" "Line2")` works too.

---

**Q7.31: Intermediate - [Regex Search vs Match]**

`import re`. What is the main difference between `re.match()` and `re.search()`?

A) `match` checks the start of the string; `search` scans the whole string.
B) `match` scans the whole string; `search` checks the start.
C) `match` returns all occurrences; `search` returns the first.
D) `match` is case-sensitive; `search` is not.

**Answer: A**

**Explanation:**
`re.match()` matches only from the beginning of the string. `re.search()` scans through the string looking for the first location where the pattern produces a match.

---

**Q7.32: Advanced - [Regex Groups]**

Given `m = re.match(r"(\w+) (\d+)", "Item 42")`. `m.group(0)` returns:

A) `"Item"`
B) `"42"`
C) `"Item 42"` (The whole match)
D) `("Item", "42")`

**Answer: C**

**Explanation:**
`group(0)` (or simply `group()`) returns the entire matching string. `group(1)` is the first captured subgroup ("Item").

---

**Q7.33: Basic - [Replace Count]**

`"banana".replace("a", "o", 2)` returns:

A) `"bonono"`
B) `"bonona"`
C) `"banono"`
D) `"banana"`

**Answer: B**

**Explanation:**
The third argument limits the count of replacements. Only the first two 'a's are replaced.

---

**Q7.34: Intermediate - [Textwrap]**

Which module provides tools for wrapping text to a specific width?

A) `text`
B) `string`
C) `textwrap`
D) `format`

**Answer: C**

**Explanation:**
The `textwrap` module (e.g., `textwrap.fill()`) is the standard tool for wrapping/indenting text paragraphs.

---

**Q7.35: Expert - [Re Compile]**

Why use `re.compile()`?

A) It is required for functionality.
B) It caches the regex engine state, improving performance for patterns used repeatedly.
C) It allows recursive patterns.
D) It supports more regex features than module-level functions.

**Answer: B**

**Explanation:**
`re.compile` compiles the pattern string into a RegexObject. If you reuse the pattern inside a loop, compiling it once avoids the overhead of parsing/caching it on every call. (Note: `re` module functions also have an internal cache, but explicit compile is cleaner for reuse).

---

**Q7.36: Advanced - [Str Translate]**

`str.translate()` requires:

A) A dictionary mapping chars to chars/None/integers.
B) Two string arguments (source, dest).
C) A callback function.
D) A list of replacements.

**Answer: A**

**Explanation:**
It takes a translation table (dict mapping codepoints to codepoints). Usually created via `str.maketrans()`.

---

**Q7.37: Basic - [Escape Quotes]**

How to represent the string `It's` using single quotes?

A) `'It's'`
B) `'It\'s'`
C) `'It"s'`
D) `r'It's'`

**Answer: B**

**Explanation:**
You must escape the internal single quote with a backslash.

---

**Q7.38: Intermediate - [Format Alignment]**

`"{:>10}".format("test")` aligns text to:

A) Left
B) Right
C) Center
D) Justified

**Answer: B**

**Explanation:**
`>` specifies right alignment. `<` is left (default for strings), `^` is center.

---

**Q7.39: Advanced - [Bytearray Immutability]**

`b = bytearray(b"hello")`. Is `b[0] = 65` valid?

A) Yes, it changes to `b"Aello"`.
B) No, bytes are immutable.
C) Yes, but it appends.
D) No, must use strings.

**Answer: A**

**Explanation:**
`bytearray` is the mutable counterpart to `bytes`. Modification in place is allowed.

---

**Q7.40: Expert - [String Canonicalization]**

Which method is best for converting a string to a standard format for case-insensitive comparison (handling Unicode edge cases like Greek Sigma)?

A) `lower()`
B) `casefold()`
C) `normalize()`
D) `standardize()`

**Answer: B**

**Explanation:**
As covered partially before, `casefold()` is the stronger normalization. Specifically for Greek Sigma 'Σ', it handles final sigma forms.

---

**Q7.41: Intermediate - [Regex Findall]**

`re.findall(r"\d+", "a12b3c")` returns:

A) `['12', '3']`
B) `[12, 3]` (Intervals)
C) `MatchObject`
D) `('12', '3')`

**Answer: A**

**Explanation:**
`findall` returns a list of all non-overlapping matches as strings.

---

**Q7.42: Basic - [EndsWith Tuple]**

`filename = "pic.jpg"`
Can you check multiple extensions like `filename.endswith((".jpg", ".png"))`?

A) Yes.
B) No, must use regex.
C) No, must use `or`.
D) Yes, but need list `[...]`.

**Answer: A**

**Explanation:**
`startswith` and `endswith` accept a tuple of strings to check against.

---

**Q7.43: Advanced - [Formatting Types]**

In `f"{x:.2%}"`, if `x = 0.5`, result is:

A) `"0.50%"`
B) `"50.00%"`
C) `"0.25"`
D) Error.

**Answer: B**

**Explanation:**
The `%` type code multiplies by 100 and displays as a percentage. `.2` specifies 2 decimals.

---

**Q7.44: Expert - [Safe Eval alternative]**

To safely parse a string literal like `"{'a': 1}"` into a dict without using potentially dangerous `eval()`, use:

A) `json.loads` (requires double quotes)
B) `ast.literal_eval`
C) `sys.parse`
D) `re.parse`

**Answer: B**

**Explanation:**
`ast.literal_eval` safely evaluates an expression node or a string containing a Python literal or container display. It cannot execute arbitrary code like `eval`.

---

**Q7.45: Intermediate - [Digit check]**

Difference between `isnumeric()` and `isdigit()`?

A) None.
B) `isnumeric` covers more Unicode characters (like Roman numerals, vulgar fractions).
C) `isdigit` covers Roman numerals.
D) `isnumeric` allows floats.

**Answer: B**

**Explanation:**
`isdigit` matches characters that are digits (0-9 and some unicode digits). `isnumeric` is broader, matching numeric characters like fractions (½) or Roman numerals (Ⅹ).

---

**Q7.46: Basic - [Unicode]**

Python 3 strings are sequences of:

A) Bytes
B) Unicode codepoints
C) ASCII chars
D) 16-bit integers

**Answer: B**

**Explanation:**
Python 3 `str` type represents Unicode characters (abstract text), abstracted away from the underlying UTF-8/UTF-16/UTF-32 storage representation in memory.

---

**Q7.47: Advanced - [String Hash]**

Are string hashes persistent across Python restarts?

A) Yes.
B) No, randomized by default for security.
C) Yes, if generated on same OS.
D) Only for ASCII strings.

**Answer: B**

**Explanation:**
By default, Python employs Hash Randomization (since 3.3) to prevent DoS attacks (HashDoS) based on predictable hash collisions. The hash seed changes per process. `PYTHONHASHSEED` environment variable can override this.

---

**Q7.48: Intermediate - [Splitlines]**

`"a\nb\r\nc".splitlines()` results in:

A) `['a', 'b', 'c']`
B) `['a\n', 'b\r\n', 'c']`
C) `['a', 'b\r', 'c']`
D) `['a', 'b', '', 'c']`

**Answer: A**

**Explanation:**
`splitlines()` handles universal newlines (`\n`, `\r`, `\r\n`) correctly, stripping them by default.

---

**Q7.49: Expert - [String Memory]**

Which is more memory efficient for large strings?

A) UTF-8 encoded `bytes`
B) Python `str` object
C) List of chars
D) Tuple of chars

**Answer: A**

**Explanation:**
Python `str` objects (since PEP 393) use flexible storage (1, 2, or 4 bytes per char + struct overhead). UTF-8 `bytes` is purely compact (1 byte for ASCII) but just raw data. For pure storage of ASCII-heavy text, `bytes` is smaller, but `str` is the proper text type. Compared to C/D, `str` is much better. Between A and B, A is raw storage, B is object.

---

**Q7.50: Basic - [Count overlap]**

`"aaaa".count("aa")` returns:

A) 1
B) 2
C) 3
D) 4

**Answer: B**

**Explanation:**
`count` returns non-overlapping occurrences. Index 0-1 matches. Index 2-3 matches. (Index 1-2 is skipped).

---

---

## Review Notes (2026-02-06)

- Q7.8 explanation contains scratch/drafting text ("Wait. Let's trace carefully.").
- Q7.25 option A is ambiguous (includes two different outputs in one option) and the explanation contains drafting text.
- Q7.18 uses only A/B/C options, which is inconsistent with the predominant 4-option MCQ format.
