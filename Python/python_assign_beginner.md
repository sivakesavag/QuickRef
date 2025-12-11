# Python Beginner Level Assignments (1-50)

> **Level**: Beginner | **Total Assignments**: 150+ | **Focus**: Python Fundamentals & Syntax

---

## Section A: Variables, Data Types & Operators (A1-A20)

### A1: Variable Swap
**Domain**: Scripting | **Difficulty**: ★☆☆☆☆ | **Time**: 10 min

**Problem**: Swap two variables without using a third variable.

**Input**: `a = 5, b = 10`
**Output**: `a = 10, b = 5`

**Test Cases**:
1. `a=5, b=10` → `a=10, b=5`
2. `a=-3, b=7` → `a=7, b=-3`
3. `a=0, b=100` → `a=100, b=0`

**Hints**: Use tuple unpacking or arithmetic operations.
**Skills**: Variable assignment, tuple unpacking

---

### A2: Type Inspector
**Domain**: Scripting | **Difficulty**: ★☆☆☆☆ | **Time**: 15 min

**Problem**: Write a function that takes any value and returns its type name and memory size.

**Input**: `42`
**Output**: `Type: int, Size: 28 bytes`

**Test Cases**:
1. `42` → `Type: int, Size: 28 bytes`
2. `"hello"` → `Type: str, Size: 54 bytes`
3. `[1,2,3]` → `Type: list, Size: 88 bytes`

**Starter Code**:
```python
import sys
def type_inspector(value):
    # Your code here
    pass
```

**Skills**: type(), sys.getsizeof(), f-strings

---

### A3: Number Base Converter
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Convert a decimal number to binary, octal, and hexadecimal representations.

**Input**: `255`
**Output**: `Binary: 11111111, Octal: 377, Hex: ff`

**Test Cases**:
1. `255` → `Binary: 11111111, Octal: 377, Hex: ff`
2. `16` → `Binary: 10000, Octal: 20, Hex: 10`
3. `0` → `Binary: 0, Octal: 0, Hex: 0`

**Skills**: bin(), oct(), hex(), string slicing

---

### A4: Temperature Converter
**Domain**: Scripting | **Difficulty**: ★☆☆☆☆ | **Time**: 15 min

**Problem**: Create a converter between Celsius, Fahrenheit, and Kelvin.

**Input**: `celsius=100`
**Output**: `Fahrenheit: 212.0, Kelvin: 373.15`

**Formulas**: F = C × 9/5 + 32, K = C + 273.15

**Test Cases**:
1. `C=0` → `F=32.0, K=273.15`
2. `C=100` → `F=212.0, K=373.15`
3. `C=-40` → `F=-40.0, K=233.15`

**Skills**: Arithmetic operators, float precision

---

### A5: BMI Calculator
**Domain**: Data Science | **Difficulty**: ★☆☆☆☆ | **Time**: 20 min

**Problem**: Calculate BMI and return the category (Underweight/Normal/Overweight/Obese).

**Input**: `weight=70, height=1.75`
**Output**: `BMI: 22.86, Category: Normal`

**Formula**: BMI = weight / height²

**Test Cases**:
1. `w=70, h=1.75` → `BMI: 22.86, Normal`
2. `w=45, h=1.60` → `BMI: 17.58, Underweight`
3. `w=100, h=1.70` → `BMI: 34.60, Obese`

**Skills**: Math operations, conditionals, rounding

---

### A6: Compound Interest Calculator
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Calculate compound interest with principal, rate, time, and compounding frequency.

**Formula**: A = P(1 + r/n)^(nt)

**Input**: `P=10000, r=0.05, t=5, n=12`
**Output**: `Final Amount: 12833.59, Interest Earned: 2833.59`

**Test Cases**:
1. `P=10000, r=0.05, t=5, n=12` → `A=12833.59`
2. `P=5000, r=0.10, t=2, n=4` → `A=6077.53`
3. `P=1000, r=0.08, t=10, n=1` → `A=2158.92`

**Skills**: Power operator, financial calculations

---

### A7: Bitwise Operations Suite
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Implement functions for AND, OR, XOR, NOT, left shift, right shift on integers.

**Input**: `a=12, b=10`
**Output**: `AND: 8, OR: 14, XOR: 6, NOT_a: -13, a<<2: 48, b>>1: 5`

**Test Cases**:
1. `12 & 10` → `8`
2. `12 | 10` → `14`
3. `12 ^ 10` → `6`

**Skills**: Bitwise operators, binary representation

---

### A8: ASCII Art Generator
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Convert text to ASCII values and back. Display as formatted table.

**Input**: `"Hello"`
**Output**: 
```
H -> 72
e -> 101
l -> 108
l -> 108
o -> 111
```

**Skills**: ord(), chr(), string iteration

---

### A9: Scientific Notation Converter
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 15 min

**Problem**: Convert between standard and scientific notation.

**Input**: `0.000000123`
**Output**: `1.23e-07`

**Test Cases**:
1. `0.000000123` → `1.23e-07`
2. `12345678` → `1.2345678e+07`
3. `1.5e-10` → `0.00000000015`

**Skills**: Float formatting, scientific notation

---

### A10: Percentage Calculator Suite
**Domain**: Data Science | **Difficulty**: ★☆☆☆☆ | **Time**: 20 min

**Problem**: Calculate percentage, percentage change, and percentage of total.

**Functions**:
- `percentage(part, whole)` → what % is part of whole
- `percentage_change(old, new)` → % increase/decrease
- `percentage_of(percent, number)` → X% of number

**Test Cases**:
1. `percentage(25, 100)` → `25.0%`
2. `percentage_change(50, 75)` → `50.0% increase`
3. `percentage_of(20, 150)` → `30.0`

**Skills**: Arithmetic, percentage formulas

---

### A11: Complex Number Operations
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Implement add, subtract, multiply, divide, and magnitude for complex numbers.

**Input**: `c1 = 3+4j, c2 = 1+2j`
**Output**: `Sum: 4+6j, Product: -5+10j, Magnitude of c1: 5.0`

**Test Cases**:
1. `(3+4j) + (1+2j)` → `4+6j`
2. `(3+4j) * (1+2j)` → `-5+10j`
3. `abs(3+4j)` → `5.0`

**Skills**: Complex numbers, cmath module

---

### A12: Unit Converter
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create converters for length (m/km/mi/ft), weight (kg/lb/oz), and volume (L/gal).

**Input**: `convert(100, 'km', 'mi')`
**Output**: `62.14 miles`

**Test Cases**:
1. `100 km → mi` → `62.14`
2. `5 kg → lb` → `11.02`
3. `10 L → gal` → `2.64`

**Skills**: Dictionary mappings, unit conversions

---

### A13: Boolean Logic Evaluator
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Create truth tables for AND, OR, NOT, XOR, NAND, NOR operations.

**Input**: `truth_table('AND')`
**Output**:
```
A     B     A AND B
True  True  True
True  False False
False True  False
False False False
```

**Skills**: Boolean operators, formatted output

---

### A14: Number Properties Checker
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Check if a number is prime, perfect, armstrong, palindrome, or fibonacci.

**Input**: `153`
**Output**: `Armstrong: True, Palindrome: True, Prime: False`

**Test Cases**:
1. `153` → Armstrong, Palindrome
2. `28` → Perfect number
3. `13` → Prime, Fibonacci

**Skills**: Number theory, loops, conditionals

---

### A15: Floating Point Precision
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Demonstrate floating-point precision issues and use Decimal for accurate calculations.

**Input**: `0.1 + 0.2`
**Output**: `Float result: 0.30000000000000004, Decimal result: 0.3`

**Skills**: decimal module, precision handling

---

### A16: Expression Evaluator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Safely evaluate mathematical expressions from strings (without eval).

**Input**: `"2 + 3 * 4"`
**Output**: `14`

**Test Cases**:
1. `"2 + 3 * 4"` → `14`
2. `"(2 + 3) * 4"` → `20`
3. `"10 / 2 - 3"` → `2.0`

**Skills**: String parsing, operator precedence, ast.literal_eval

---

### A17: Currency Formatter
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Format numbers as currency with proper separators and symbols.

**Input**: `format_currency(1234567.89, 'USD')`
**Output**: `$1,234,567.89`

**Test Cases**:
1. `1234567.89, USD` → `$1,234,567.89`
2. `1234567.89, EUR` → `€1.234.567,89`
3. `1234567.89, INR` → `₹12,34,567.89`

**Skills**: locale module, string formatting

---

### A18: Binary String Operations
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Add, subtract binary strings and check if a binary string is valid.

**Input**: `binary_add('1010', '1011')`
**Output**: `'10101'`

**Test Cases**:
1. `'1010' + '1011'` → `'10101'`
2. `'1111' + '1'` → `'10000'`
3. `is_valid('10102')` → `False`

**Skills**: Binary arithmetic, string manipulation

---

### A19: Statistics Calculator
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Calculate mean, median, mode, range, variance, and standard deviation from a list.

**Input**: `[1, 2, 2, 3, 4, 5, 5, 5, 6]`
**Output**: `Mean: 3.67, Median: 4, Mode: 5, StdDev: 1.70`

**Skills**: statistics module, mathematical formulas

---

### A20: Data Type Coercion Suite
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Create safe conversion functions that handle errors gracefully.

**Functions**: `safe_int()`, `safe_float()`, `safe_bool()`, `safe_list()`

**Test Cases**:
1. `safe_int("42")` → `42`
2. `safe_int("hello")` → `None`
3. `safe_float("3.14abc")` → `None`

**Skills**: Type conversion, exception handling basics

---

## Section B: String Operations (B1-B15)

### B1: Palindrome Checker
**Domain**: Scripting | **Difficulty**: ★☆☆☆☆ | **Time**: 15 min

**Problem**: Check if a string is a palindrome (ignore case and non-alphanumeric).

**Input**: `"A man, a plan, a canal: Panama"`
**Output**: `True`

**Test Cases**:
1. `"racecar"` → `True`
2. `"A man, a plan, a canal: Panama"` → `True`
3. `"hello"` → `False`

**Skills**: String methods, slicing

---

### B2: Word Counter
**Domain**: Data Science | **Difficulty**: ★☆☆☆☆ | **Time**: 20 min

**Problem**: Count words, characters, sentences, and paragraphs in text.

**Input**: `"Hello world. This is a test."`
**Output**: `Words: 6, Chars: 28, Sentences: 2`

**Skills**: String splitting, counting

---

### B3: String Compression
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Compress string using run-length encoding.

**Input**: `"aaabbbccccaaa"`
**Output**: `"a3b3c4a3"`

**Test Cases**:
1. `"aaabbbcccc"` → `"a3b3c4"`
2. `"abc"` → `"a1b1c1"`
3. `"aaa"` → `"a3"`

**Skills**: String iteration, counting consecutive chars

---

### B4: Anagram Checker
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Check if two strings are anagrams of each other.

**Input**: `"listen", "silent"`
**Output**: `True`

**Test Cases**:
1. `"listen", "silent"` → `True`
2. `"hello", "world"` → `False`
3. `"Dormitory", "Dirty room"` → `True`

**Skills**: sorted(), Counter, string normalization

---

### B5: Caesar Cipher
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Implement Caesar cipher encryption and decryption.

**Input**: `encrypt("HELLO", 3)`
**Output**: `"KHOOR"`

**Test Cases**:
1. `encrypt("HELLO", 3)` → `"KHOOR"`
2. `decrypt("KHOOR", 3)` → `"HELLO"`
3. `encrypt("xyz", 3)` → `"abc"`

**Skills**: Character manipulation, modular arithmetic

---

### B6: Title Case Converter
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Convert text to title case with proper handling of articles and prepositions.

**Input**: `"the quick brown fox jumps over the lazy dog"`
**Output**: `"The Quick Brown Fox Jumps over the Lazy Dog"`

**Skills**: String methods, word lists, edge cases

---

### B7: Phone Number Formatter
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Validate and format phone numbers to standard format.

**Input**: `"1234567890"`
**Output**: `"(123) 456-7890"`

**Test Cases**:
1. `"1234567890"` → `"(123) 456-7890"`
2. `"123-456-7890"` → `"(123) 456-7890"`
3. `"+1 (123) 456-7890"` → `"+1 (123) 456-7890"`

**Skills**: String manipulation, formatting

---

### B8: Email Validator
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Validate email format using basic string operations (no regex yet).

**Input**: `"user@example.com"`
**Output**: `Valid: True`

**Validation Rules**: One @, domain has dot, no spaces, alphanumeric username

**Skills**: String parsing, validation logic

---

### B9: Text Reversal Suite
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Reverse words, sentences, and characters in different ways.

**Functions**:
- `reverse_chars("hello")` → `"olleh"`
- `reverse_words("hello world")` → `"world hello"`
- `reverse_each_word("hello world")` → `"olleh dlrow"`

**Skills**: Slicing, split/join

---

### B10: Password Strength Checker
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Rate password strength based on length, character variety, and patterns.

**Input**: `"MyP@ssw0rd123"`
**Output**: `Strength: Strong (Score: 85/100)`

**Criteria**: Length, uppercase, lowercase, numbers, special chars, no common patterns

**Skills**: String analysis, scoring algorithms

---

### B11: Slug Generator
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Convert titles to URL-friendly slugs.

**Input**: `"Hello World! This is a Test."`
**Output**: `"hello-world-this-is-a-test"`

**Test Cases**:
1. `"Hello World!"` → `"hello-world"`
2. `"Python 3.9 Features"` → `"python-3-9-features"`
3. `"  Multiple   Spaces  "` → `"multiple-spaces"`

**Skills**: String cleaning, normalization

---

### B12: Text Alignment Formatter
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Left, right, center align text and justify paragraphs.

**Input**: `justify("Lorem ipsum dolor sit amet", width=30)`
**Output**: Justified text with even spacing

**Skills**: String formatting, ljust, rjust, center

---

### B13: Find and Replace Engine
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Case-insensitive find/replace with whole word matching option.

**Input**: `replace_all("The cat sat on the mat", "cat", "dog")`
**Output**: `"The dog sat on the mat"`

**Skills**: String methods, case handling

---

### B14: Substring Finder
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Find all occurrences of substring with their positions.

**Input**: `find_all("abcabcabc", "abc")`
**Output**: `[0, 3, 6]`

**Test Cases**:
1. `"abcabcabc", "abc"` → `[0, 3, 6]`
2. `"hello", "ll"` → `[2]`
3. `"aaaa", "aa"` → `[0, 1, 2]` (overlapping)

**Skills**: String searching, index tracking

---

### B15: Lorem Ipsum Generator
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Generate placeholder text with specified word/sentence/paragraph count.

**Input**: `generate_lorem(words=50)`
**Output**: 50 words of Lorem Ipsum text

**Skills**: Random selection, text generation

---

## Section C: Lists, Tuples, Sets, Dictionaries (C1-C25)

### C1: List Flattener
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Flatten a nested list of arbitrary depth.

**Input**: `[[1, [2, 3]], [4, [5, [6]]]]`
**Output**: `[1, 2, 3, 4, 5, 6]`

**Skills**: Recursion, list manipulation

---

### C2: Duplicate Remover
**Domain**: Data Science | **Difficulty**: ★☆☆☆☆ | **Time**: 15 min

**Problem**: Remove duplicates while preserving order.

**Input**: `[1, 2, 2, 3, 1, 4, 3, 5]`
**Output**: `[1, 2, 3, 4, 5]`

**Skills**: Sets, order preservation

---

### C3: List Rotation
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Rotate list left or right by k positions.

**Input**: `rotate([1,2,3,4,5], 2, 'right')`
**Output**: `[4, 5, 1, 2, 3]`

**Skills**: Slicing, deque

---

### C4: Matrix Operations
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 35 min

**Problem**: Add, multiply, and transpose matrices using nested lists.

**Input**: Two 2x2 matrices
**Output**: Sum, product, transpose

**Skills**: Nested loops, matrix math

---

### C5: Set Operations Visualizer
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Perform and visualize union, intersection, difference, symmetric difference.

**Input**: `{1,2,3,4}, {3,4,5,6}`
**Output**: Visual representation of all set operations

**Skills**: Set operations, formatted output

---

### C6: Dictionary Merger
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Deep merge nested dictionaries with conflict resolution.

**Input**: `{'a': 1, 'b': {'c': 2}}, {'b': {'d': 3}, 'e': 4}`
**Output**: `{'a': 1, 'b': {'c': 2, 'd': 3}, 'e': 4}`

**Skills**: Recursion, dictionary operations

---

### C7: Frequency Counter
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Count frequency of elements and return top N most common.

**Input**: `[1,1,1,2,2,3,3,3,3,4]`
**Output**: `{3: 4, 1: 3, 2: 2, 4: 1}`

**Skills**: Counter, sorting

---

### C8: List Chunker
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Split list into chunks of specified size.

**Input**: `chunk([1,2,3,4,5,6,7], 3)`
**Output**: `[[1,2,3], [4,5,6], [7]]`

**Skills**: Slicing, iteration

---

### C9: Tuple Unpacking Master
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Demonstrate advanced tuple unpacking with *, nested unpacking.

**Exercises**:
1. `a, *b, c = [1,2,3,4,5]` → a=1, b=[2,3,4], c=5
2. `((a, b), c) = ((1, 2), 3)` → a=1, b=2, c=3

**Skills**: Extended unpacking, destructuring

---

### C10: Inventory Management System
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Create inventory system with add, remove, update, search, low stock alerts.

**Features**: Product CRUD, stock tracking, value calculation

**Skills**: Dictionary operations, CRUD logic

---

### C11: Named Tuple Database
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Create a simple database using named tuples for records.

**Input**: Student records with name, age, grade, gpa
**Output**: Query and filter operations

**Skills**: Named tuples, data organization

---

### C12: Sparse Matrix
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement sparse matrix using dictionary for memory efficiency.

**Input**: Large matrix with many zeros
**Output**: Operations on sparse representation

**Skills**: Dictionary-based data structures

---

### C13: Shopping Cart
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 35 min

**Problem**: Implement shopping cart with add, remove, quantity update, discount codes.

**Features**: Item management, total calculation, discount application

**Skills**: Dictionary manipulation, business logic

---

### C14: Stack and Queue
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Implement stack (LIFO) and queue (FIFO) using lists.

**Operations**: push, pop, peek, isEmpty, size

**Skills**: List as data structure, collections.deque

---

### C15: Two Sum Problem
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Find two numbers that add up to target. Return indices.

**Input**: `[2, 7, 11, 15], target=9`
**Output**: `[0, 1]`

**Skills**: Dictionary lookup, algorithm optimization

---

### C16: Group Anagrams
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Group list of words by their anagram groups.

**Input**: `["eat", "tea", "tan", "ate", "nat", "bat"]`
**Output**: `[["eat","tea","ate"], ["tan","nat"], ["bat"]]`

**Skills**: Dictionary grouping, sorted tuple keys

---

### C17: Nested Dictionary Navigator
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Access nested dictionary with dot notation path.

**Input**: `get_nested(data, "user.address.city")`
**Output**: Value at that path or default

**Skills**: String splitting, recursive access

---

### C18: Set Cover Problem
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Find minimum sets that cover all elements (greedy approach).

**Input**: Universe and collection of sets
**Output**: Minimum sets needed for coverage

**Skills**: Set operations, greedy algorithms

---

### C19: Dictionary Inversion
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Invert dictionary (handle duplicate values as lists).

**Input**: `{'a': 1, 'b': 2, 'c': 1}`
**Output**: `{1: ['a', 'c'], 2: ['b']}`

**Skills**: Dictionary manipulation, defaultdict

---

### C20: Moving Average
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Calculate moving average with configurable window size.

**Input**: `[1, 2, 3, 4, 5], window=3`
**Output**: `[2.0, 3.0, 4.0]`

**Skills**: List slicing, windowed calculations

---

### C21: Priority Queue
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement priority queue with insert, extract_min, peek.

**Input**: Items with priorities
**Output**: Items extracted in priority order

**Skills**: heapq module, tuple ordering

---

### C22: LRU Cache
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Implement Least Recently Used cache with get/put operations.

**Features**: Capacity limit, O(1) operations

**Skills**: OrderedDict, cache concepts

---

### C23: Zip and Unzip
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Transpose list of lists, zip multiple lists, handle unequal lengths.

**Input**: `[[1,2,3], [4,5,6]]`
**Output**: `[(1,4), (2,5), (3,6)]`

**Skills**: zip, itertools.zip_longest

---

### C24: All Pairs Distance
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Calculate all pairwise distances for list of points.

**Input**: `[(0,0), (3,0), (0,4)]`
**Output**: Distance matrix

**Skills**: Nested iteration, math functions

---

### C25: Data Validation Framework
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Create validators for different data types with constraints.

**Features**: Type checking, range validation, pattern matching

**Skills**: Dictionary schemas, validation logic

---

## Section D: Control Structures (D1-D20)

### D1: FizzBuzz Extended
**Domain**: Scripting | **Difficulty**: ★☆☆☆☆ | **Time**: 20 min

**Problem**: Classic FizzBuzz with configurable rules.

**Input**: `fizzbuzz(15, {3: "Fizz", 5: "Buzz", 7: "Bazz"})`
**Output**: Numbers 1-15 with substitutions for multiples

**Skills**: Conditionals, modular arithmetic

---

### D2: Number Pyramid
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Generate various number patterns (pyramid, diamond, spiral).

**Input**: `pyramid(5)`
**Output**:
```
    1
   121
  12321
 1234321
123454321
```

**Skills**: Nested loops, string formatting

---

### D3: Collatz Conjecture
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Generate Collatz sequence and analyze stopping times.

**Input**: `collatz(27)`
**Output**: Full sequence, length, max value

**Skills**: While loops, sequence analysis

---

### D4: Prime Sieve
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Implement Sieve of Eratosthenes for finding primes.

**Input**: `sieve(100)`
**Output**: All primes up to 100

**Skills**: Algorithm implementation, boolean arrays

---

### D5: Binary Search
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Implement binary search with iterative and recursive versions.

**Input**: `binary_search([1,3,5,7,9,11], 7)`
**Output**: `3` (index)

**Skills**: Search algorithms, loop vs recursion

---

### D6: Sorting Algorithms
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 45 min

**Problem**: Implement bubble, selection, insertion sort with step visualization.

**Input**: `bubble_sort([64, 34, 25, 12, 22, 11, 90])`
**Output**: Sorted list with each step shown

**Skills**: Sorting algorithms, visualization

---

### D7: Nested Loop Patterns
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Generate star patterns (right triangle, inverted, diamond, hollow).

**Input**: `pattern("diamond", 5)`
**Output**: Diamond shape with stars

**Skills**: Nested loops, pattern recognition

---

### D8: List Comprehension Master
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Convert 10 loop-based operations to list comprehensions.

**Examples**:
1. Filter even numbers
2. Square of odds
3. Flatten nested list
4. Conditional transformation
5. Multiple iterables

**Skills**: List comprehensions, generator expressions

---

### D9: Dictionary Comprehension
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Create dictionaries using comprehensions.

**Examples**:
1. Word length mapping
2. Filtered key-value pairs
3. Swapped keys/values
4. Computed values

**Skills**: Dictionary comprehensions

---

### D10: Set Comprehension
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Use set comprehensions for unique value extraction.

**Examples**:
1. Unique vowels in text
2. Common elements
3. Transformed unique values

**Skills**: Set comprehensions

---

### D11: Nested Comprehensions
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Matrix operations using nested comprehensions.

**Examples**:
1. Matrix transpose
2. Matrix multiplication
3. Filtering 2D arrays

**Skills**: Nested comprehensions

---

### D12: Control Flow Refactoring
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 35 min

**Problem**: Refactor complex if-else chains to cleaner patterns.

**Input**: Deeply nested conditionals
**Output**: Flat, readable code using early returns, dictionaries

**Skills**: Code refactoring, clean code

---

### D13: Loop Optimization
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Optimize slow loops using built-in functions.

**Examples**:
1. Replace loops with map/filter
2. Use enumerate instead of range
3. Use zip for parallel iteration

**Skills**: Performance optimization

---

### D14: Walrus Operator
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Demonstrate assignment expressions (:=) in various contexts.

**Examples**:
1. In while conditions
2. In comprehensions
3. To avoid repeated calculations

**Skills**: Python 3.8+ features

---

### D15: Match Statement
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Use structural pattern matching (match-case) for complex conditions.

**Examples**:
1. Type matching
2. Sequence patterns
3. Guard conditions

**Skills**: Python 3.10+ features

---

### D16: Short-Circuit Evaluation
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 20 min

**Problem**: Demonstrate and use short-circuit evaluation effectively.

**Examples**:
1. Default values with `or`
2. Guard clauses with `and`
3. Conditional execution

**Skills**: Boolean operators, performance

---

### D17: Loop Control Mastery
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use break, continue, else clause effectively.

**Examples**:
1. Search with early exit
2. Skip invalid items
3. For-else pattern

**Skills**: Loop control statements

---

### D18: Recursive vs Iterative
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Implement factorial, fibonacci, tree traversal both ways.

**Compare**: Time complexity, stack usage, readability

**Skills**: Recursion, call stack understanding

---

### D19: Tail Recursion
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Convert recursive functions to tail-recursive form.

**Examples**: Factorial, sum, fibonacci with accumulators

**Skills**: Tail recursion, optimization

---

### D20: Memoization
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement memoization to optimize recursive functions.

**Input**: Fibonacci with memoization
**Output**: O(n) instead of O(2^n)

**Skills**: Caching, functools.lru_cache

---

## Section E: Functions (E1-E25)

### E1: Function Basics
**Domain**: Scripting | **Difficulty**: ★☆☆☆☆ | **Time**: 20 min

**Problem**: Create functions with positional, keyword, default arguments.

**Skills**: Function definition, parameters

---

### E2: *args and **kwargs
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Create flexible functions accepting variable arguments.

**Examples**:
1. Sum of arbitrary numbers
2. Merge dictionaries
3. Format string with options

**Skills**: Variable arguments

---

### E3: Lambda Functions
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use lambdas with map, filter, sorted, reduce.

**Examples**:
1. Sort by second element
2. Filter by condition
3. Chain transformations

**Skills**: Lambda expressions, functional programming

---

### E4: Higher-Order Functions
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create functions that accept or return functions.

**Examples**:
1. Custom filter function
2. Function composer
3. Retry wrapper

**Skills**: Higher-order functions

---

### E5: Closures
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement counters, accumulators, rate limiters using closures.

**Examples**:
1. Counter function
2. Running average
3. Memoized function

**Skills**: Closures, encapsulation

---

### E6: Partial Functions
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use functools.partial for pre-configured functions.

**Examples**:
1. Pre-filled logging
2. Bound methods
3. Default configurations

**Skills**: functools.partial

---

### E7: Currying
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement function currying for mathematical operations.

**Input**: `add = curry(lambda a, b, c: a + b + c)`
**Output**: `add(1)(2)(3)` → `6`

**Skills**: Currying, functional programming

---

### E8: Function Composition
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Implement compose and pipe for function chaining.

**Input**: `compose(f, g, h)(x)` = `f(g(h(x)))`
**Output**: Chained result

**Skills**: Composition, reduce

---

### E9: Operator Module
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use operator module functions with higher-order functions.

**Examples**:
1. Sort by attribute
2. Item getter
3. Method caller

**Skills**: operator module

---

### E10: Docstrings
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Write comprehensive docstrings with examples and doctests.

**Format**: Google/NumPy style docstrings

**Skills**: Documentation, doctest

---

### E11: Type Hints
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Add type hints to functions, use Optional, Union, List, Dict.

**Skills**: typing module, mypy compatibility

---

### E12: Callback Functions
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Implement callback pattern for async-style operations.

**Examples**:
1. Event handlers
2. Progress reporting
3. Completion callbacks

**Skills**: Callbacks, functional patterns

---

### E13: Pure Functions
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Convert impure functions to pure functions.

**Principles**: No side effects, deterministic output

**Skills**: Functional programming principles

---

### E14: Recursive Data Processing
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Process recursive data structures (trees, nested dicts).

**Examples**:
1. Tree traversal
2. JSON flattening
3. Nested sum

**Skills**: Recursion, data structures

---

### E15: Function Factories
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Create factories that generate specialized functions.

**Examples**:
1. Validator factory
2. Formatter factory
3. Logger factory

**Skills**: Function generation, closures

---

### E16: Reduce Operations
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Implement various aggregations using reduce.

**Examples**:
1. Product of list
2. Longest string
3. Nested merge

**Skills**: functools.reduce

---

### E17: Itertools Functions
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Master itertools for efficient iteration.

**Functions**: chain, cycle, repeat, combinations, permutations, groupby

**Skills**: itertools module

---

### E18: Function Signature
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 30 min

**Problem**: Inspect and modify function signatures dynamically.

**Skills**: inspect module, signature manipulation

---

### E19: Default Argument Gotcha
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 25 min

**Problem**: Demonstrate and fix mutable default argument bug.

**Anti-pattern**: `def func(lst=[]):`
**Fix**: `def func(lst=None):`

**Skills**: Python gotchas, defensive coding

---

### E20: Unpacking in Functions
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Use * and ** for argument unpacking.

**Examples**:
1. Spread lists as args
2. Spread dicts as kwargs
3. Combine both

**Skills**: Argument unpacking

---

### E21: Built-in Functions Master
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 35 min

**Problem**: Master all important built-in functions.

**Functions**: all, any, enumerate, filter, map, zip, sorted, min, max, sum

**Skills**: Built-in function mastery

---

### E22: Math Functions
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Use math module for scientific calculations.

**Functions**: ceil, floor, trunc, pow, sqrt, log, sin, cos, factorial

**Skills**: math module

---

### E23: String Functions
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Master all string methods through practical examples.

**Categories**: Search, transform, validate, split/join

**Skills**: String methods mastery

---

### E24: Functools Module
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Use functools utilities effectively.

**Functions**: cache, lru_cache, partial, reduce, wraps, total_ordering

**Skills**: functools module

---

### E25: Custom Sorting
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Implement complex sorting with multiple criteria.

**Examples**:
1. Multi-key sorting
2. Natural sorting
3. Custom comparator

**Skills**: Sorting, key functions

---

## Section F: File I/O & Basic NumPy (F1-F25)

### F1: Text File Reader
**Domain**: Scripting | **Difficulty**: ★☆☆☆☆ | **Time**: 20 min

**Problem**: Read text file, count lines, words, characters.

**Skills**: open(), read modes, with statement

---

### F2: Line-by-Line Processing
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Process large files line by line efficiently.

**Skills**: File iteration, memory efficiency

---

### F3: Write Operations
**Domain**: Scripting | **Difficulty**: ★☆☆☆☆ | **Time**: 20 min

**Problem**: Write, append, overwrite text files.

**Skills**: write modes (w, a, x)

---

### F4: Binary Files
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Read and write binary files.

**Skills**: Binary mode (rb, wb)

---

### F5: File Search
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Search for pattern in files, report line numbers.

**Skills**: String searching, file processing

---

### F6: Log File Analyzer
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 40 min

**Problem**: Parse log files, extract timestamps, count errors.

**Skills**: Text parsing, date handling

---

### F7: Configuration Files
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Read/write INI-style configuration files.

**Skills**: configparser module

---

### F8: File Path Operations
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Use pathlib for path manipulation.

**Skills**: pathlib module, os.path

---

### F9: Directory Listing
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: List files recursively with filtering.

**Skills**: glob, Path.glob, os.walk

---

### F10: File Statistics
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Get file metadata (size, dates, permissions).

**Skills**: os.stat, pathlib properties

---

### F11: NumPy Array Creation
**Domain**: Data Science | **Difficulty**: ★☆☆☆☆ | **Time**: 25 min

**Problem**: Create arrays using various methods.

**Functions**: array, zeros, ones, arange, linspace, random

**Skills**: NumPy basics

---

### F12: Array Indexing
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Master slicing, boolean indexing, fancy indexing.

**Skills**: NumPy indexing

---

### F13: Array Operations
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Perform vectorized arithmetic operations.

**Skills**: Broadcasting, vectorization

---

### F14: Array Reshaping
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Reshape, flatten, stack, split arrays.

**Skills**: reshape, ravel, vstack, hstack

---

### F15: Statistical Functions
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Calculate statistics on arrays.

**Functions**: mean, std, var, min, max, sum, cumsum

**Skills**: NumPy statistics

---

### F16: Array Comparison
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Compare arrays, find elements meeting conditions.

**Skills**: Comparison operators, where, argmax

---

### F17: Linear Algebra Basics
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Matrix multiplication, transpose, inverse, determinant.

**Skills**: numpy.linalg, dot product

---

### F18: Random Number Generation
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Generate random numbers with various distributions.

**Skills**: numpy.random, seeding

---

### F19: Data Type Handling
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Work with different dtypes, type conversion.

**Skills**: dtype, astype, memory considerations

---

### F20: Saving/Loading Arrays
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 25 min

**Problem**: Save and load arrays to/from files.

**Skills**: np.save, np.load, np.savetxt

---

### F21: Array Filtering
**Domain**: Data Science | **Difficulty**: ★★☆☆☆ | **Time**: 30 min

**Problem**: Filter arrays by complex conditions.

**Skills**: Boolean masks, np.where

---

### F22: Aggregation by Groups
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Group data and calculate aggregate statistics.

**Skills**: np.unique, bincount, grouping

---

### F23: Time Series Basics
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Work with datetime arrays, time-based calculations.

**Skills**: numpy datetime64, timedelta64

---

### F24: Performance Comparison
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 35 min

**Problem**: Compare NumPy vs Python loops performance.

**Skills**: timeit, vectorization benefits

---

### F25: Mini Data Analysis Project
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 60 min

**Problem**: Analyze dataset using only NumPy operations.

**Dataset**: Array of student scores
**Tasks**: Clean, analyze, summarize, find patterns

**Skills**: End-to-end NumPy project

---

## Beginner Level Capstone Projects (CAP1-CAP10)

### CAP1: Personal Budget Tracker
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 3 hours

**Description**: Build CLI app to track income/expenses, categories, reports.

**Features**: Add transactions, view by category/date, monthly summary

**Skills Demonstrated**: File I/O, dictionaries, functions, loops

---

### CAP2: Quiz Game
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 2 hours

**Description**: Create interactive quiz with scoring and categories.

**Features**: Multiple choice, score tracking, high scores

**Skills Demonstrated**: Control flow, user input, data structures

---

### CAP3: Grade Calculator
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 2 hours

**Description**: Calculate weighted grades, GPA, class statistics.

**Features**: Weighted averages, letter grades, ranking

**Skills Demonstrated**: NumPy, statistics, functions

---

### CAP4: Contact Manager
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 3 hours

**Description**: Store and manage contacts with search and export.

**Features**: CRUD operations, search, export to file

**Skills Demonstrated**: File I/O, dictionaries, string operations

---

### CAP5: Number Analysis Tool
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 2 hours

**Description**: Analyze sequences of numbers for statistics and patterns.

**Features**: Descriptive stats, distribution analysis, outlier detection

**Skills Demonstrated**: NumPy, math functions, list operations

---

### CAP6: Mad Libs Generator
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 1.5 hours

**Description**: Create story templates with placeholder replacement.

**Features**: Multiple templates, word categories, save stories

**Skills Demonstrated**: Strings, file I/O, user interaction

---

### CAP7: Expense Splitter
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 2 hours

**Description**: Split expenses among friends, track who owes whom.

**Features**: Add people, expenses, calculate balances

**Skills Demonstrated**: Dictionaries, math, functions

---

### CAP8: Hangman Game
**Domain**: Scripting | **Difficulty**: ★★☆☆☆ | **Time**: 2 hours

**Description**: Classic word guessing game with categories.

**Features**: Word categories, ASCII art, difficulty levels

**Skills Demonstrated**: Strings, loops, conditionals, sets

---

### CAP9: Data Analyzer
**Domain**: Data Science | **Difficulty**: ★★★☆☆ | **Time**: 3 hours

**Description**: Load and analyze CSV-like data using fundamental Python.

**Features**: Load data, filter, aggregate, simple visualizations (text-based)

**Skills Demonstrated**: File I/O, lists, dictionaries, NumPy

---

### CAP10: Text Adventure Game
**Domain**: Scripting | **Difficulty**: ★★★☆☆ | **Time**: 4 hours

**Description**: Interactive story with choices, inventory, save/load.

**Features**: Multiple paths, items, save game state

**Skills Demonstrated**: All beginner concepts combined

---

**Beginner Level Summary**:
- **Total Assignments**: 155
- **Scripting Focus**: ~75 assignments
- **Data Science Focus**: ~70 assignments
- **Capstone Projects**: 10

---

*Continue to Intermediate Level: `python_assign_intermediate.md`*
