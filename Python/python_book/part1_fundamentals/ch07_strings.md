# Chapter 7: Strings & Text Processing

> **Topics Covered**: String methods, formatting (%, .format(), f-strings), raw strings, bytes vs strings, encoding/decoding, Unicode handling, regular expressions (re module), string interning, catastrophic backtracking

---

## Questions

---

**Q7.1: Basic - [String Creation]**

Which of these creates a valid string in Python?

A) `s = 'hello'`
B) `s = "hello"`
C) `s = '''hello'''`
D) All of the above

**Answer: D**

**Explanation:**
Python strings can be created with single quotes, double quotes, or triple quotes (both `'''` and `"""`). All are equivalent for simple strings. Triple quotes allow multi-line strings and can contain unescaped single/double quotes.

---

**Q7.2: Basic - [String Immutability]**

What happens when you try `s = "hello"; s[0] = 'H'`?

A) Changes s to "Hello"
B) TypeError: strings are immutable
C) Creates a new string
D) IndexError

**Answer: B**

**Explanation:**
Strings are immutable — you cannot change individual characters. To modify, create a new string: `s = 'H' + s[1:]`. This immutability allows string interning and other optimizations.

---

**Q7.3: Basic - [String Concatenation]**

What is the output?
```python
s = "Hello" + " " + "World"
print(s)
```

A) `Hello World`
B) `HelloWorld`
C) `["Hello", " ", "World"]`
D) Error

**Answer: A**

**Explanation:**
`+` concatenates strings. Three strings are joined: "Hello" + " " + "World" = "Hello World". For many strings, `''.join(list)` is more efficient than repeated `+`.

---

**Q7.4: Basic - [String Repetition]**

What is the output?
```python
print("ab" * 3)
```

A) `ab3`
B) `ababab`
C) `ab ab ab`
D) Error

**Answer: B**

**Explanation:**
`*` repeats a string n times. `"ab" * 3` produces `"ababab"`. Useful for creating separators: `"-" * 40` or padding. `0 * "ab"` or `"ab" * 0` gives empty string.

---

**Q7.5: Basic - [String Indexing]**

What is the output?
```python
s = "Python"
print(s[-1], s[-2])
```

A) `n, o`
B) `P, y`
C) Error
D) `o, n`

**Answer: A**

**Explanation:**
Negative indices count from the end. `-1` is last character ('n'), `-2` is second-to-last ('o'). Positive indices: 0='P', 1='y', etc. Negative: -1='n', -2='o', etc.

---

**Q7.6: Intermediate - [String Slicing]**

What is the output?
```python
s = "Hello World"
print(s[0:5], s[6:])
```

A) `Hello, World`
B) `Hello World`
C) `Hello,  World`
D) `Hell, World`

**Answer: A**

**Explanation:**
`s[0:5]` = indices 0-4 = "Hello". `s[6:]` = index 6 to end = "World". Slice `[start:end]` excludes end. Omitting end means "to the end". Note: space is at index 5.

---

**Q7.7: Basic - [String Methods - Case]**

What is the output?
```python
s = "Hello World"
print(s.upper(), s.lower())
```

A) `HELLO WORLD, hello world`
B) `Hello World, Hello World`
C) `HELLO WORLD hello world`
D) Error

**Answer: A**

**Explanation:**
`upper()` returns all-uppercase copy. `lower()` returns all-lowercase copy. Original string is unchanged (immutable). These are essential for case-insensitive comparisons: `s1.lower() == s2.lower()`.

---

**Q7.8: Basic - [String Methods - strip]**

What is the output?
```python
s = "   hello   "
print(f"[{s.strip()}]")
```

A) `[   hello   ]`
B) `[hello]`
C) `[hello   ]`
D) `[   hello]`

**Answer: B**

**Explanation:**
`strip()` removes leading and trailing whitespace. `lstrip()` removes only leading, `rstrip()` only trailing. With argument: `s.strip('xy')` removes 'x' and 'y' characters from both ends.

---

**Q7.9: Intermediate - [String Methods - split]**

What is the output?
```python
s = "a,b,c,d"
print(s.split(','))
```

A) `['a', 'b', 'c', 'd']`
B) `'a' 'b' 'c' 'd'`
C) `('a', 'b', 'c', 'd')`
D) `abcd`

**Answer: A**

**Explanation:**
`split(sep)` splits string at separator, returns list. Without argument, splits on any whitespace. `maxsplit` parameter limits splits: `s.split(',', 2)` splits at most 2 times.

---

**Q7.10: Intermediate - [String Methods - join]**

What is the output?
```python
words = ['Hello', 'World']
print(' '.join(words))
```

A) `['Hello', 'World']`
B) `Hello World`
C) `HelloWorld`
D) `' '.Hello.World`

**Answer: B**

**Explanation:**
`separator.join(iterable)` joins strings with separator between them. `' '.join(['Hello', 'World'])` = "Hello World". The separator is the string you call `.join()` on. More efficient than `+` in loops.

---

**Q7.11: Intermediate - [String Methods - replace]**

What is the output?
```python
s = "hello hello hello"
print(s.replace("hello", "hi", 2))
```

A) `hi hi hello`
B) `hi hi hi`
C) `hello hello hello`
D) `hi hello hello`

**Answer: A**

**Explanation:**
`replace(old, new, count)` replaces occurrences. Optional `count` limits replacements. Here, only first 2 "hello" are replaced. Without count: all occurrences replaced. Returns new string (original unchanged).

---

**Q7.12: Basic - [String Methods - find]**

What is the output?
```python
s = "Hello World"
print(s.find("World"), s.find("xyz"))
```

A) `6, -1`
B) `7, None`
C) `6, None`
D) `6, Error`

**Answer: A**

**Explanation:**
`find(sub)` returns index of first occurrence, or -1 if not found. "World" starts at index 6. "xyz" isn't found → -1. Compare with `index()` which raises ValueError if not found.

---

**Q7.13: Intermediate - [String Methods - startswith/endswith]**

What is the output?
```python
filename = "document.pdf"
print(filename.endswith('.pdf'), filename.startswith('doc'))
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: A**

**Explanation:**
`endswith(suffix)` checks if string ends with suffix. `startswith(prefix)` checks beginning. Both return boolean. Can also accept tuple of strings: `filename.endswith(('.pdf', '.doc'))`.

---

**Q7.14: Intermediate - [String Methods - count]**

What is the output?
```python
s = "banana"
print(s.count('a'), s.count('ana'))
```

A) `3, 2`
B) `3, 1`
C) `2, 1`
D) `2, 2`

**Answer: B**

**Explanation:**
`count(sub)` counts non-overlapping occurrences. 'a' appears 3 times. 'ana' appears once (non-overlapping). The second 'ana' overlaps with the first. For overlapping matches, use regex.

---

**Q7.15: Basic - [String Formatting - %]**

What is the output?
```python
name = "Alice"
age = 30
print("Name: %s, Age: %d" % (name, age))
```

A) `Name: Alice, Age: 30`
B) `Name: %s, Age: %d`
C) `Name: Alice, Age: 30.0`
D) Error

**Answer: A**

**Explanation:**
`%` formatting (old style): `%s` for string, `%d` for integer, `%f` for float. Values in tuple after `%`. Still works but f-strings or `.format()` are preferred for readability.

---

**Q7.16: Intermediate - [String Formatting - format()]**

What is the output?
```python
print("Hello, {}! You are {} years old.".format("Bob", 25))
```

A) `Hello, Bob! You are 25 years old.`
B) `Hello, {}! You are {} years old.`
C) `Hello, Bob! You are {} years old.`
D) Error

**Answer: A**

**Explanation:**
`.format()` replaces `{}` placeholders with arguments in order. Named placeholders: `"{name} is {age}".format(name="Bob", age=25)`. Positional: `"{0} {1}".format("a", "b")`. More flexible than `%`.

---

**Q7.17: Basic - [f-strings]**

What is the output?
```python
name = "Charlie"
age = 35
print(f"Name: {name}, Age: {age}")
```

A) `Name: Charlie, Age: 35`
B) `Name: {name}, Age: {age}`
C) `f"Name: Charlie, Age: 35"`
D) Error

**Answer: A**

**Explanation:**
F-strings (Python 3.6+): prefix with `f`, embed expressions in `{}`. Variables and expressions are evaluated at runtime. Most readable and often fastest formatting method. `f"{2+2}"` = "4".

---

**Q7.18: Intermediate - [f-string Expressions]**

What is the output?
```python
x = 10
print(f"{x * 2 = }")
```

A) `x * 2 = 20`
B) `20`
C) `x * 2 = `
D) Error

**Answer: A**

**Explanation:**
🐍 Python 3.8+: `=` in f-strings shows the expression AND its value. `f"{x * 2 = }"` outputs "x * 2 = 20". Great for debugging. Works with any expression. The spaces around `=` are preserved.

---

**Q7.19: Intermediate - [f-string Formatting]**

What is the output?
```python
value = 3.14159
print(f"{value:.2f}")
```

A) `3.14`
B) `3.14159`
C) `.2f`
D) `3.15`

**Answer: A**

**Explanation:**
Format specs after `:` in f-strings. `.2f` = 2 decimal places, float format. Other formats: `:>10` (right-align, width 10), `:,` (thousand separators), `:%` (percentage). Rounds 3.14159 to 3.14.

---

**Q7.20: Intermediate - [f-string Alignment]**

What is the output?
```python
s = "Hi"
print(f"[{s:>10}]")
print(f"[{s:<10}]")
print(f"[{s:^10}]")
```

A) Right, left, center aligned within 10 chars
B) All same
C) Error
D) `[Hi]` three times

**Answer: A**

**Explanation:**
`>` right-aligns, `<` left-aligns, `^` centers. Number is the width. `[{s:>10}]` = `[        Hi]`. `[{s:<10}]` = `[Hi        ]`. `[{s:^10}]` = `[    Hi    ]`. Fill character can precede: `{s:*^10}`.

---

**Q7.21: Basic - [Raw Strings]**

What is the output?
```python
print(r"Hello\nWorld")
```

A) `Hello` (newline) `World`
B) `Hello\nWorld`
C) `rHello\nWorld`
D) Error

**Answer: B**

**Explanation:**
Raw strings (prefix `r`) treat backslashes as literal characters, not escape sequences. `r"Hello\nWorld"` keeps `\n` as two characters. Essential for regex patterns and Windows paths: `r"C:\Users\name"`.

---

**Q7.22: Basic - [Escape Sequences]**

What is the output?
```python
print("Line1\nLine2\tTabbed")
```

A) `Line1\nLine2\tTabbed`
B) Line1, then Line2 with a tab before Tabbed
C) `Line1 Line2 Tabbed`
D) Error

**Answer: B**

**Explanation:**
Escape sequences: `\n` = newline, `\t` = tab, `\\` = literal backslash, `\'` = single quote, `\"` = double quote. They're interpreted in regular strings but not in raw strings.

---

**Q7.23: Intermediate - [String Methods - isdigit, isalpha]**

What is the output?
```python
print("123".isdigit(), "abc".isalpha(), "abc123".isalnum())
```

A) `True, True, True`
B) `True, True, False`
C) `False, True, True`
D) `True, False, True`

**Answer: A**

**Explanation:**
`isdigit()` - all digits? `isalpha()` - all letters? `isalnum()` - all letters or digits? "123" is digits only, "abc" is letters only, "abc123" is alphanumeric. Also: `isnumeric()`, `isdecimal()` for number variants.

---

**Q7.24: Intermediate - [String Methods - title, capitalize, swapcase]**

What is the output?
```python
s = "hello WORLD"
print(s.title(), s.capitalize(), s.swapcase())
```

A) `Hello World, Hello world, HELLO world`
B) `HELLO WORLD, Hello world, Hello World`
C) `Hello World, Hello WORLD, HELLO world`
D) `Hello World, Hello world, HELLO world`

**Answer: A**

**Explanation:**
`title()` - capitalizes first letter of each word. `capitalize()` - capitalizes first character only, lowercases rest. `swapcase()` - swaps upper/lower case. All return new strings.

---

**Q7.25: Intermediate - [Bytes vs Strings]**

What is the output?
```python
s = "hello"
b = b"hello"
print(type(s), type(b))
```

A) `<class 'str'>, <class 'bytes'>`
B) `<class 'str'>, <class 'str'>`
C) `<class 'unicode'>, <class 'bytes'>`
D) Error

**Answer: A**

**Explanation:**
`"hello"` is a str (Unicode text). `b"hello"` is bytes (raw binary data). In Python 3, these are distinct types. Use `.encode()` to convert str→bytes, `.decode()` for bytes→str.

---

**Q7.26: Intermediate - [Encoding]**

What is the output?
```python
s = "café"
b = s.encode('utf-8')
print(len(s), len(b))
```

A) `4, 4`
B) `4, 5`
C) `5, 5`
D) `5, 4`

**Answer: B**

**Explanation:**
`len(s)` = 4 characters. In UTF-8, 'é' requires 2 bytes (non-ASCII). So `len(b)` = 5 bytes. UTF-8 is variable-width: ASCII chars = 1 byte, others = 2-4 bytes. Character count ≠ byte count.

---

**Q7.27: Intermediate - [Decoding]**

What is the output?
```python
b = b'caf\xc3\xa9'
s = b.decode('utf-8')
print(s)
```

A) `café`
B) `caf\xc3\xa9`
C) Error
D) `cafe`

**Answer: A**

**Explanation:**
`\xc3\xa9` is the UTF-8 encoding of 'é'. `.decode('utf-8')` interprets the bytes as UTF-8, producing "café". Using wrong encoding (e.g., 'latin-1') would give different result or error.

---

**Q7.28: Advanced - [Encoding Errors]**

What happens with `"café".encode('ascii')`?

A) Returns `b'cafe'`
B) UnicodeEncodeError
C) Returns `b'caf?'`
D) Silently drops 'é'

**Answer: B**

**Explanation:**
ASCII can't represent 'é' (non-ASCII). Default behavior raises UnicodeEncodeError. Handle with `errors` parameter: `.encode('ascii', errors='ignore')` drops it, `errors='replace'` uses '?', `errors='xmlcharrefreplace'` uses XML entities.

---

**Q7.29: Intermediate - [Regular Expressions - re.search]**

What is the output?
```python
import re
match = re.search(r'\d+', 'abc123def456')
print(match.group())
```

A) `123`
B) `123456`
C) `['123', '456']`
D) None

**Answer: A**

**Explanation:**
`re.search()` finds FIRST match. `\d+` matches one or more digits. First match is "123". `.group()` returns the matched text. Use `re.findall()` for all matches: `['123', '456']`.

---

**Q7.30: Intermediate - [Regular Expressions - re.findall]**

What is the output?
```python
import re
result = re.findall(r'\d+', 'abc123def456')
print(result)
```

A) `123`
B) `['123', '456']`
C) `['1', '2', '3', '4', '5', '6']`
D) `123456`

**Answer: B**

**Explanation:**
`findall()` returns list of ALL non-overlapping matches. `\d+` matches sequences of digits. Two matches: "123" and "456". Without `+`, it would match individual digits.

---

**Q7.31: Intermediate - [Regular Expressions - re.sub]**

What is the output?
```python
import re
result = re.sub(r'\d', '#', 'abc123')
print(result)
```

A) `abc###`
B) `abc#`
C) `###123`
D) `abc123`

**Answer: A**

**Explanation:**
`re.sub(pattern, replacement, string)` replaces all matches. `\d` matches each digit, replaced with '#'. Result: "abc###". Use `count=1` to limit replacements.

---

**Q7.32: Intermediate - [Regex Character Classes]**

What does `[a-zA-Z]` match in regex?

A) Only lowercase letters
B) Any single letter (upper or lower)
C) The string "a-zA-Z"
D) Any character except letters

**Answer: B**

**Explanation:**
Character classes `[]` match any one character inside. Ranges: `a-z` (lowercase), `A-Z` (uppercase). Combined: `[a-zA-Z]` matches any single letter. `[^a-z]` with `^` negates: any character EXCEPT a-z.

---

**Q7.33: Intermediate - [Regex Quantifiers]**

What do `*`, `+`, and `?` mean in regex?

A) Multiplication, addition, conditional
B) `*`=0+, `+`=1+, `?`=0 or 1 occurrences
C) Same thing, different syntax
D) Comments

**Answer: B**

**Explanation:**
Quantifiers: `*` = zero or more, `+` = one or more, `?` = zero or one. `a*` matches "", "a", "aa"... `a+` matches "a", "aa"... (not empty). `a?` matches "" or "a" only. Greedy by default.

---

**Q7.34: Advanced - [Regex Greedy vs Non-Greedy]**

What is the output?
```python
import re
s = "<tag>content</tag>"
print(re.search(r'<.*>', s).group())
print(re.search(r'<.*?>', s).group())
```

A) `<tag>content</tag>`, `<tag>`
B) `<tag>`, `<tag>`
C) `<tag>content</tag>`, `<tag>content</tag>`
D) Error

**Answer: A**

**Explanation:**
`.*` is greedy — matches as much as possible. `.*?` is non-greedy (lazy) — matches as little as possible. Greedy matches entire `<tag>content</tag>`. Non-greedy matches just `<tag>`.

---

**Q7.35: Intermediate - [Regex Groups]**

What is the output?
```python
import re
match = re.search(r'(\d+)-(\d+)', '123-456')
print(match.group(1), match.group(2))
```

A) `123-456, 123-456`
B) `123, 456`
C) `1, 4`
D) `(123), (456)`

**Answer: B**

**Explanation:**
Parentheses create capture groups. `group(0)` or `group()` = entire match. `group(1)` = first group, `group(2)` = second. Here: group 1 = "123", group 2 = "456". Also: `match.groups()` returns tuple.

---

**Q7.36: Advanced - [Named Groups]**

What is the output?
```python
import re
match = re.search(r'(?P<first>\d+)-(?P<second>\d+)', '123-456')
print(match.group('first'))
```

A) `123`
B) `first`
C) `(?P<first>\d+)`
D) Error

**Answer: A**

**Explanation:**
`(?P<name>pattern)` creates a named group. Access with `group('name')` or `match.groupdict()`. More readable than numbered groups. `match.group('first')` = "123".

---

**Q7.37: Intermediate - [Regex Anchors]**

What do `^` and `$` mean in regex?

A) Start and end of any line
B) Start and end of string
C) Exponent and dollar sign
D) Not and reference

**Answer: B**

**Explanation:**
Anchors: `^` = start of string, `$` = end of string. With `re.MULTILINE` flag, they match start/end of each LINE. `^hello$` matches only "hello" as entire string. Without anchors, pattern can match anywhere.

---

**Q7.38: Intermediate - [re.compile]**

What is the advantage of `re.compile(pattern)`?

A) Makes regex faster always
B) Pre-compiles pattern for reuse, avoiding recompilation overhead
C) Compiles to machine code
D) No advantage

**Answer: B**

**Explanation:**
`re.compile()` returns a pattern object. If using same pattern many times, compiling once is more efficient than passing string each time. Python caches recent patterns, but explicit compilation is clearer and guarantees efficiency.

---

**Q7.39: Advanced - [Regex Word Boundary]**

What does `\b` match?

A) A backspace character
B) A word boundary (between word and non-word character)
C) The letter 'b'
D) Any whitespace

**Answer: B**

**Explanation:**
`\b` is a word boundary (zero-width assertion). `\bword\b` matches "word" as complete word, not "password". In Python strings, use raw string `r'\bword\b'` or escape: `'\\bword\\b'`.

---

**Q7.40: Intermediate - [String translate]**

What does `str.maketrans()` with `translate()` do?

A) Translates to another language
B) Creates a translation table for character-by-character replacement
C) Moves string to another location
D) Encodes the string

**Answer: B**

**Explanation:**
`str.maketrans('abc', 'xyz')` creates a table mapping a→x, b→y, c→z. `s.translate(table)` applies it. Efficient for bulk character replacement. Can also specify characters to delete.

---

**Q7.41: Advanced - [translate with deletion]**

What is the output?
```python
s = "hello, world!"
table = str.maketrans('', '', ', !')
print(s.translate(table))
```

A) `helloworld`
B) `hello world`
C) `hello, world!`
D) Error

**Answer: A**

**Explanation:**
Third argument to `maketrans` specifies characters to DELETE. `', !'` are deleted from string. Result: "helloworld". More efficient than multiple `replace()` calls for removing multiple characters.

---

**Q7.42: Intermediate - [String zfill]**

What is the output?
```python
print("42".zfill(5))
print("-42".zfill(5))
```

A) `00042, 00-42`
B) `00042, -0042`
C) `42000, -4200`
D) `00042, -00042`

**Answer: B**

**Explanation:**
`zfill(width)` pads with zeros to specified width. For negative numbers, zeros go AFTER the minus sign: `-0042`. Useful for numeric strings that need fixed width (e.g., IDs, codes).

---

**Q7.43: Intermediate - [String partition]**

What is the output?
```python
s = "hello=world"
print(s.partition('='))
```

A) `['hello', 'world']`
B) `('hello', '=', 'world')`
C) `('hello', 'world')`
D) `'hello=world'`

**Answer: B**

**Explanation:**
`partition(sep)` splits at FIRST occurrence of separator, returns 3-tuple: (before, separator, after). Unlike `split()`, keeps the separator. `rpartition()` splits at LAST occurrence.

---

**Q7.44: Basic - [String Membership]**

What is the output?
```python
print('py' in 'python')
print('PY' in 'python')
```

A) `True, True`
B) `True, False`
C) `False, True`
D) `False, False`

**Answer: B**

**Explanation:**
`in` on strings checks for substring. 'py' is in 'python' (True). 'PY' is not — search is case-sensitive (False). For case-insensitive: `'py' in 'python'.lower()`.

---

**Q7.45: Intermediate - [String Formatting - Numbers]**

What is the output?
```python
num = 1234567
print(f"{num:,}")
print(f"{num:_}")
```

A) `1,234,567` and `1_234_567`
B) `1234567,` and `1234567_`
C) `,1234567` and `_1234567`
D) Error

**Answer: A**

**Explanation:**
Format specifier `,` uses comma as thousand separator. `_` uses underscore (Python 3.6+). These improve readability of large numbers: `1,234,567` is clearer than `1234567`.

---

**Q7.46: Intermediate - [String center, ljust, rjust]**

What do `center()`, `ljust()`, `rjust()` do?

A) Move text in a document
B) Pad string to specified width with optional fill character
C) Remove centering
D) Justify text like in word processors

**Answer: B**

**Explanation:**
`s.center(10)` centers in width 10 (pads both sides). `ljust(10)` left-justifies (pads right). `rjust(10)` right-justifies (pads left). Optional second arg is fill character: `s.center(10, '-')`.

---

**Q7.47: Advanced - [Regex Lookahead]**

What does `(?=pattern)` mean in regex?

A) Optional pattern
B) Positive lookahead — matches if pattern follows, but doesn't consume it
C) Named group
D) Non-capturing group

**Answer: B**

**Explanation:**
Lookahead assertions check what follows without including it in the match. `foo(?=bar)` matches "foo" only if followed by "bar", but "bar" isn't part of the match. `(?!pattern)` is negative lookahead.

---

**Q7.48: Expert - [Catastrophic Backtracking]**

What is "catastrophic backtracking" in regex?

A) A fast pattern matching technique
B) Exponential time complexity from nested quantifiers on overlapping patterns
C) Going back to previous regex versions
D) Memory leak in regex

**Answer: B**

**Explanation:**
Patterns like `(a+)+$` on input "aaaaaaaaaaaaaaab" cause exponential backtracking — regex engine tries all combinations. Can hang programs. Avoid nested quantifiers with overlapping matches. Use possessive quantifiers or atomic groups where available.

---

**Q7.49: Intermediate - [String isspace, isprintable]**

What is the output?
```python
print("   ".isspace())
print("\t\n".isspace())
print("hello".isprintable())
```

A) `True, True, True`
B) `True, False, True`
C) `False, True, True`
D) `True, True, False`

**Answer: A**

**Explanation:**
`isspace()` returns True if all characters are whitespace (space, tab, newline, etc.). `isprintable()` returns True if all characters are printable (or string is empty). Control characters are not printable.

---

**Q7.50: Expert - [String Interning]**

What is the output?
```python
a = "hello"
b = "hello"
c = "hel" + "lo"
d = "".join(['h','e','l','l','o'])
print(a is b, a is c, a is d)
```

A) `True, True, True`
B) `True, True, False`
C) `True, False, False`
D) Depends on implementation

**Answer: D**

**Explanation:**
⚠️ String interning behavior varies. Compile-time constants like `"hello"` and `"hel" + "lo"` are usually interned. Runtime-created strings may or may not be. Never rely on `is` for string comparison — use `==`.

---

**Q7.51: Intermediate - [re.split]**

What is the output?
```python
import re
result = re.split(r'\s+', 'hello   world\tfoo')
print(result)
```

A) `['hello', 'world', 'foo']`
B) `['hello', '', '', 'world', 'foo']`
C) `['hello   world\tfoo']`
D) Error

**Answer: A**

**Explanation:**
`re.split(pattern, string)` splits on pattern matches. `\s+` = one or more whitespace. Splits at whitespace sequences, not individual characters. Result: `['hello', 'world', 'foo']`. More flexible than `str.split()`.

---

**Q7.52: Intermediate - [Unicode Strings]**

What is the output?
```python
s = "\u0048\u0065\u006c\u006c\u006f"
print(s)
```

A) `\u0048\u0065\u006c\u006c\u006f`
B) `Hello`
C) `U0048U0065U006cU006cU006f`
D) Error

**Answer: B**

**Explanation:**
`\uXXXX` is Unicode escape for code point XXXX (hex). 0048='H', 0065='e', 006c='l', 006f='o'. Python interprets these escapes in regular strings, producing "Hello".

---

**Q7.53: Intermediate - [ord and chr]**

What is the output?
```python
print(ord('A'), chr(65))
```

A) `65, A`
B) `A, 65`
C) `1, A`
D) Error

**Answer: A**

**Explanation:**
`ord(char)` returns Unicode code point of character. `chr(num)` returns character for code point. `ord('A')` = 65. `chr(65)` = 'A'. These are inverses: `chr(ord(c)) == c`.

---

**Q7.54: Advanced - [Unicode Normalization]**

Why might two visually identical strings not be equal?

A) Different fonts
B) Different Unicode normalization forms (composed vs decomposed characters)
C) Invisible characters
D) Both B and C are possible

**Answer: D**

**Explanation:**
'é' can be represented as single character (U+00E9) or 'e' + combining accent (U+0065 U+0301). Visually same, different bytes. Also, invisible characters (zero-width spaces, RTL marks) can hide in strings. Use `unicodedata.normalize()` for comparison.

---

**Q7.55: Advanced - [textwrap Module]**

What does the `textwrap` module do?

A) Creates wrappers for functions
B) Wraps and fills text to specified width
C) Encrypts text
D) Compresses text

**Answer: B**

**Explanation:**
`textwrap.wrap(text, width)` breaks text into lines of specified width. `textwrap.fill()` returns single string with newlines. `textwrap.dedent()` removes common leading whitespace — useful for docstrings.

---

## Chapter Summary

**Total MCQs: 55**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 15 | 27% |
| Intermediate | 32 | 58% |
| Advanced | 6 | 11% |
| Expert | 2 | 4% |

**Key Topics Covered:**
- String methods (manipulation, searching, checking)
- String formatting (%, format(), f-strings)
- Slicing and indexing
- Raw strings and escape sequences
- Bytes vs strings, encoding/decoding
- Regular expressions (re module)
- Unicode handling
- String interning
