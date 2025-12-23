# 📚 Arrays and Strings - Complete Cheatsheet

> **Goal**: Master all array and string concepts, patterns, and algorithms for DSA interviews.

---

## 📋 Quick Reference

| Section | Key Contents |
|---------|--------------|
| **Array Fundamentals** | Operations, complexity table, Python snippets |
| **Dynamic Arrays** | Implementation, amortized analysis |
| **Matrices** | Traversals, spiral order, rotation, sorted search |
| **String Fundamentals** | Immutability, character ops, palindrome, anagram |
| **Two Pointers** | 4 patterns with templates (opposite, same-dir, fast-slow, 3-sum) |
| **Sliding Window** | Fixed-size, variable-size, with hash map templates |
| **Prefix Sum** | 1D/2D prefix, subarray sum = K, product except self |
| **Kadane's Algorithm** | Max subarray, with indices, circular, product variants |
| **String Matching** | KMP, Rabin-Karp, Z-Algorithm (full implementations) |
| **Subarray Problems** | Count, longest, distinct elements patterns |
| **Common Patterns** | Dutch flag, merge intervals, binary search on answer |
| **Time Complexity** | Quick reference table |

---

## Table of Contents
1. [Array Fundamentals](#1-array-fundamentals)
2. [Dynamic Arrays](#2-dynamic-arrays)
3. [Multidimensional Arrays & Matrices](#3-multidimensional-arrays--matrices)
4. [String Fundamentals](#4-string-fundamentals)
5. [Two Pointer Technique](#5-two-pointer-technique)
6. [Sliding Window Technique](#6-sliding-window-technique)
7. [Prefix Sum](#7-prefix-sum)
8. [Kadane's Algorithm](#8-kadanes-algorithm)
9. [String Matching Algorithms](#9-string-matching-algorithms)
10. [Subarray Problems](#10-subarray-problems)
11. [Common Patterns & Templates](#11-common-patterns--templates)
12. [Time Complexity Reference](#12-time-complexity-reference)

---

## 1. Array Fundamentals

### What is an Array?
A contiguous block of memory storing elements of the same type, accessed by index.

### Basic Operations & Complexity

| Operation | Static Array | Dynamic Array |
|-----------|-------------|---------------|
| Access by index | O(1) | O(1) |
| Search (unsorted) | O(n) | O(n) |
| Search (sorted) | O(log n) | O(log n) |
| Insert at end | N/A | O(1) amortized |
| Insert at position | O(n) | O(n) |
| Delete at end | N/A | O(1) |
| Delete at position | O(n) | O(n) |

### Python Array Operations

```python
# Array declaration and initialization
arr = [1, 2, 3, 4, 5]           # List (dynamic array)
arr = [0] * 10                   # Array of 10 zeros
arr = list(range(1, 11))         # [1, 2, ..., 10]

# Access
first = arr[0]                   # First element
last = arr[-1]                   # Last element
sub = arr[1:4]                   # Subarray [1:4) - elements at index 1,2,3

# Modification
arr[0] = 10                      # Update element
arr.append(6)                    # Add to end - O(1) amortized
arr.insert(0, 0)                 # Insert at position - O(n)
arr.pop()                        # Remove from end - O(1)
arr.pop(0)                       # Remove from position - O(n)

# Common operations
len(arr)                         # Length
min(arr), max(arr)               # Min/Max - O(n)
sum(arr)                         # Sum - O(n)
arr.reverse()                    # In-place reverse - O(n)
arr[::-1]                        # Returns reversed copy - O(n)
sorted(arr)                      # Returns sorted copy - O(n log n)
arr.sort()                       # In-place sort - O(n log n)

# Searching
3 in arr                         # Check existence - O(n)
arr.index(3)                     # Find index (raises error if not found)
arr.count(3)                     # Count occurrences - O(n)
```

### Key Patterns for Array Problems

1. **In-place modification** - Swap elements to avoid extra space
2. **Sorting first** - Many problems become easier after sorting
3. **Hash map auxiliary** - O(n) lookup for frequency, duplicates
4. **Multiple passes** - Sometimes 2-3 passes are cleaner than one

---

## 2. Dynamic Arrays

### How They Work
- Start with initial capacity
- When full, allocate new array (typically 2x size)
- Copy elements to new array
- Amortized O(1) insertion

### Implementation Concept

```python
class DynamicArray:
    def __init__(self):
        self.capacity = 1
        self.size = 0
        self.arr = [None] * self.capacity
    
    def append(self, val):
        if self.size == self.capacity:
            self._resize(2 * self.capacity)
        self.arr[self.size] = val
        self.size += 1
    
    def _resize(self, new_capacity):
        new_arr = [None] * new_capacity
        for i in range(self.size):
            new_arr[i] = self.arr[i]
        self.arr = new_arr
        self.capacity = new_capacity
    
    def get(self, index):
        if 0 <= index < self.size:
            return self.arr[index]
        raise IndexError("Index out of bounds")
    
    def pop(self):
        if self.size == 0:
            raise IndexError("Array is empty")
        val = self.arr[self.size - 1]
        self.size -= 1
        # Optional: shrink if too empty
        if self.size < self.capacity // 4:
            self._resize(self.capacity // 2)
        return val
```

### Amortized Analysis
- Individual worst case: O(n) when resizing
- Amortized over n operations: O(1) per operation
- Total cost for n insertions: O(n)

---

## 3. Multidimensional Arrays & Matrices

### 2D Array Creation

```python
# Create m x n matrix
rows, cols = 3, 4
matrix = [[0] * cols for _ in range(rows)]  # ✅ Correct
# matrix = [[0] * cols] * rows  # ❌ Wrong! Creates references

# From input
matrix = [[int(x) for x in input().split()] for _ in range(rows)]
```

### Matrix Traversals

```python
# Row-wise traversal
for i in range(rows):
    for j in range(cols):
        print(matrix[i][j])

# Column-wise traversal
for j in range(cols):
    for i in range(rows):
        print(matrix[i][j])

# Diagonal traversal (main diagonal)
for i in range(min(rows, cols)):
    print(matrix[i][i])

# Anti-diagonal
for i in range(min(rows, cols)):
    print(matrix[i][cols - 1 - i])
```

### Spiral Order Traversal

```python
def spiral_order(matrix):
    if not matrix:
        return []
    
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    
    while top <= bottom and left <= right:
        # Left to right
        for col in range(left, right + 1):
            result.append(matrix[top][col])
        top += 1
        
        # Top to bottom
        for row in range(top, bottom + 1):
            result.append(matrix[row][right])
        right -= 1
        
        # Right to left
        if top <= bottom:
            for col in range(right, left - 1, -1):
                result.append(matrix[bottom][col])
            bottom -= 1
        
        # Bottom to top
        if left <= right:
            for row in range(bottom, top - 1, -1):
                result.append(matrix[row][left])
            left += 1
    
    return result
```

### Matrix Rotation (90° Clockwise)

```python
def rotate_90_clockwise(matrix):
    n = len(matrix)
    # Transpose
    for i in range(n):
        for j in range(i + 1, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    # Reverse each row
    for row in matrix:
        row.reverse()
```

### Search in Sorted Matrix

```python
# Matrix sorted row-wise and column-wise
def search_matrix(matrix, target):
    if not matrix:
        return False
    
    rows, cols = len(matrix), len(matrix[0])
    row, col = 0, cols - 1  # Start from top-right
    
    while row < rows and col >= 0:
        if matrix[row][col] == target:
            return True
        elif matrix[row][col] > target:
            col -= 1
        else:
            row += 1
    return False
# Time: O(m + n)
```

### 4 Directional Movement

```python
# For grid problems (BFS/DFS)
directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]  # right, left, down, up

# 8 directions (including diagonals)
directions_8 = [(0,1), (0,-1), (1,0), (-1,0), (1,1), (1,-1), (-1,1), (-1,-1)]

def is_valid(row, col, rows, cols):
    return 0 <= row < rows and 0 <= col < cols
```

---

## 4. String Fundamentals

### Python String Basics

```python
s = "hello world"

# Strings are IMMUTABLE in Python
# s[0] = 'H'  # ❌ Error!

# Common operations
len(s)                          # Length
s[0], s[-1]                     # First, last character
s[1:5]                          # Substring [1:5)
s.upper(), s.lower()            # Case conversion
s.strip()                       # Remove whitespace
s.split()                       # Split by whitespace
s.split(',')                    # Split by delimiter
'-'.join(['a', 'b', 'c'])       # Join: "a-b-c"
s.replace('l', 'L')             # Replace all occurrences
s.find('world')                 # Find index (-1 if not found)
s.count('l')                    # Count occurrences
s.startswith('hello')           # Prefix check
s.endswith('world')             # Suffix check
s.isalpha()                     # All alphabetic?
s.isdigit()                     # All digits?
s.isalnum()                     # All alphanumeric?

# String building (use list for efficiency)
chars = []
for c in s:
    chars.append(c.upper())
result = ''.join(chars)         # O(n) instead of O(n²)
```

### Character Operations

```python
# ASCII conversions
ord('a')                        # 97 (character to ASCII)
chr(97)                         # 'a' (ASCII to character)

# Alphabet index (0-25)
index = ord('c') - ord('a')     # 2

# Check character type
c.isalpha()                     # Is letter?
c.isdigit()                     # Is digit?
c.isspace()                     # Is whitespace?
c.islower(), c.isupper()        # Case check
```

### String Reversal Techniques

```python
s = "hello"

# Method 1: Slicing
reversed_s = s[::-1]

# Method 2: reversed() function
reversed_s = ''.join(reversed(s))

# Method 3: Two pointers (for lists)
chars = list(s)
left, right = 0, len(chars) - 1
while left < right:
    chars[left], chars[right] = chars[right], chars[left]
    left += 1
    right -= 1
reversed_s = ''.join(chars)
```

### Palindrome Check

```python
def is_palindrome(s):
    # Simple check
    return s == s[::-1]

def is_palindrome_two_pointer(s):
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True

# Ignore non-alphanumeric
def is_palindrome_clean(s):
    cleaned = ''.join(c.lower() for c in s if c.isalnum())
    return cleaned == cleaned[::-1]
```

### Anagram Check

```python
from collections import Counter

def is_anagram(s1, s2):
    return Counter(s1) == Counter(s2)

# Or using sorting
def is_anagram_sort(s1, s2):
    return sorted(s1) == sorted(s2)
```

---

## 5. Two Pointer Technique

### When to Use
- Sorted arrays
- Finding pairs with certain sum
- Removing duplicates
- Comparing elements from both ends
- Fast and slow pointer scenarios

### Pattern 1: Opposite Ends

```python
# Two Sum on Sorted Array
def two_sum_sorted(arr, target):
    left, right = 0, len(arr) - 1
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return []
# Time: O(n), Space: O(1)
```

### Pattern 2: Same Direction

```python
# Remove Duplicates from Sorted Array
def remove_duplicates(arr):
    if not arr:
        return 0
    
    write_idx = 1
    for read_idx in range(1, len(arr)):
        if arr[read_idx] != arr[read_idx - 1]:
            arr[write_idx] = arr[read_idx]
            write_idx += 1
    return write_idx
# Time: O(n), Space: O(1)
```

### Pattern 3: Fast and Slow (Floyd's)

```python
# Find Middle of Array
def find_middle(arr):
    slow = fast = 0
    while fast < len(arr) - 1 and fast + 1 < len(arr):
        slow += 1
        fast += 2
    return slow

# Detect Cycle in Linked List (concept)
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

### Three Pointers / Three Sum

```python
def three_sum(nums, target=0):
    nums.sort()
    result = []
    
    for i in range(len(nums) - 2):
        # Skip duplicates for i
        if i > 0 and nums[i] == nums[i-1]:
            continue
        
        left, right = i + 1, len(nums) - 1
        while left < right:
            total = nums[i] + nums[left] + nums[right]
            if total == target:
                result.append([nums[i], nums[left], nums[right]])
                # Skip duplicates
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                left += 1
                right -= 1
            elif total < target:
                left += 1
            else:
                right -= 1
    
    return result
# Time: O(n²), Space: O(1) excluding result
```

### Container With Most Water

```python
def max_area(heights):
    left, right = 0, len(heights) - 1
    max_water = 0
    
    while left < right:
        width = right - left
        height = min(heights[left], heights[right])
        max_water = max(max_water, width * height)
        
        # Move the shorter line
        if heights[left] < heights[right]:
            left += 1
        else:
            right -= 1
    
    return max_water
# Time: O(n), Space: O(1)
```

### Trapping Rain Water

```python
def trap_water(heights):
    if not heights:
        return 0
    
    left, right = 0, len(heights) - 1
    left_max, right_max = heights[left], heights[right]
    water = 0
    
    while left < right:
        if left_max < right_max:
            left += 1
            left_max = max(left_max, heights[left])
            water += left_max - heights[left]
        else:
            right -= 1
            right_max = max(right_max, heights[right])
            water += right_max - heights[right]
    
    return water
# Time: O(n), Space: O(1)
```

---

## 6. Sliding Window Technique

### When to Use
- Contiguous subarray/substring problems
- Finding max/min in subarrays
- Problems involving "window" of elements
- Optimization problems with constraints

### Pattern 1: Fixed Size Window

```python
# Maximum Sum Subarray of Size K
def max_sum_subarray(arr, k):
    if len(arr) < k:
        return -1
    
    # Calculate first window
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Slide the window
    for i in range(k, len(arr)):
        window_sum += arr[i] - arr[i - k]  # Add new, remove old
        max_sum = max(max_sum, window_sum)
    
    return max_sum
# Time: O(n), Space: O(1)
```

### Pattern 2: Variable Size Window (Expand + Shrink)

```python
# Minimum Size Subarray Sum >= Target
def min_subarray_len(target, nums):
    left = 0
    current_sum = 0
    min_len = float('inf')
    
    for right in range(len(nums)):
        current_sum += nums[right]
        
        # Shrink window while valid
        while current_sum >= target:
            min_len = min(min_len, right - left + 1)
            current_sum -= nums[left]
            left += 1
    
    return min_len if min_len != float('inf') else 0
# Time: O(n), Space: O(1)
```

### Pattern 3: Window with Hash Map

```python
# Longest Substring Without Repeating Characters
def longest_unique_substring(s):
    char_index = {}  # char -> last seen index
    left = 0
    max_len = 0
    
    for right, char in enumerate(s):
        if char in char_index and char_index[char] >= left:
            left = char_index[char] + 1
        char_index[char] = right
        max_len = max(max_len, right - left + 1)
    
    return max_len
# Time: O(n), Space: O(min(n, alphabet_size))
```

### Pattern 4: Window with Frequency Count

```python
from collections import Counter

# Find All Anagrams in String
def find_anagrams(s, p):
    if len(p) > len(s):
        return []
    
    p_count = Counter(p)
    window_count = Counter(s[:len(p)])
    result = []
    
    if window_count == p_count:
        result.append(0)
    
    for i in range(len(p), len(s)):
        # Add new character
        window_count[s[i]] += 1
        # Remove old character
        old_char = s[i - len(p)]
        window_count[old_char] -= 1
        if window_count[old_char] == 0:
            del window_count[old_char]
        
        if window_count == p_count:
            result.append(i - len(p) + 1)
    
    return result
# Time: O(n), Space: O(1) - fixed alphabet size
```

### Minimum Window Substring

```python
from collections import Counter

def min_window(s, t):
    if not t or not s:
        return ""
    
    t_count = Counter(t)
    required = len(t_count)
    formed = 0
    window_count = {}
    
    left = 0
    min_len = float('inf')
    result = (0, 0)
    
    for right, char in enumerate(s):
        window_count[char] = window_count.get(char, 0) + 1
        
        if char in t_count and window_count[char] == t_count[char]:
            formed += 1
        
        # Shrink window
        while formed == required:
            if right - left + 1 < min_len:
                min_len = right - left + 1
                result = (left, right)
            
            left_char = s[left]
            window_count[left_char] -= 1
            if left_char in t_count and window_count[left_char] < t_count[left_char]:
                formed -= 1
            left += 1
    
    return s[result[0]:result[1]+1] if min_len != float('inf') else ""
# Time: O(|s| + |t|), Space: O(|s| + |t|)
```

---

## 7. Prefix Sum

### Concept
Precompute cumulative sums to answer range queries in O(1).

```
Array:      [3, 1, 2, 5, 4]
Prefix Sum: [3, 4, 6, 11, 15]

Sum from index i to j = prefix[j] - prefix[i-1]
Sum from index 1 to 3 = prefix[3] - prefix[0] = 11 - 3 = 8
```

### Basic Implementation

```python
def build_prefix_sum(arr):
    n = len(arr)
    prefix = [0] * (n + 1)  # Extra element for easier calculations
    for i in range(n):
        prefix[i + 1] = prefix[i] + arr[i]
    return prefix

def range_sum(prefix, left, right):
    """Sum of elements from index left to right (inclusive)"""
    return prefix[right + 1] - prefix[left]

# Example
arr = [3, 1, 2, 5, 4]
prefix = build_prefix_sum(arr)  # [0, 3, 4, 6, 11, 15]
print(range_sum(prefix, 1, 3))  # 1 + 2 + 5 = 8
```

### Subarray Sum Equals K

```python
from collections import defaultdict

def subarray_sum_k(nums, k):
    count = 0
    prefix_sum = 0
    prefix_count = defaultdict(int)
    prefix_count[0] = 1  # Empty prefix
    
    for num in nums:
        prefix_sum += num
        # If prefix_sum - k exists, we found subarrays
        count += prefix_count[prefix_sum - k]
        prefix_count[prefix_sum] += 1
    
    return count
# Time: O(n), Space: O(n)
```

### 2D Prefix Sum

```python
def build_2d_prefix(matrix):
    if not matrix:
        return []
    
    rows, cols = len(matrix), len(matrix[0])
    prefix = [[0] * (cols + 1) for _ in range(rows + 1)]
    
    for i in range(rows):
        for j in range(cols):
            prefix[i+1][j+1] = (matrix[i][j] + prefix[i][j+1] + 
                                prefix[i+1][j] - prefix[i][j])
    return prefix

def region_sum(prefix, r1, c1, r2, c2):
    """Sum of rectangle from (r1,c1) to (r2,c2) inclusive"""
    return (prefix[r2+1][c2+1] - prefix[r1][c2+1] - 
            prefix[r2+1][c1] + prefix[r1][c1])
```

### Product Array Except Self

```python
def product_except_self(nums):
    n = len(nums)
    result = [1] * n
    
    # Left products
    left_product = 1
    for i in range(n):
        result[i] = left_product
        left_product *= nums[i]
    
    # Right products
    right_product = 1
    for i in range(n - 1, -1, -1):
        result[i] *= right_product
        right_product *= nums[i]
    
    return result
# Time: O(n), Space: O(1) excluding result
```

---

## 8. Kadane's Algorithm

### Problem: Maximum Subarray Sum
Find the contiguous subarray with the largest sum.

### Core Idea
At each position, decide: start fresh or extend the previous subarray.

```python
def max_subarray_sum(nums):
    if not nums:
        return 0
    
    max_sum = nums[0]
    current_sum = nums[0]
    
    for i in range(1, len(nums)):
        current_sum = max(nums[i], current_sum + nums[i])
        max_sum = max(max_sum, current_sum)
    
    return max_sum
# Time: O(n), Space: O(1)
```

### Kadane's with Indices

```python
def max_subarray_with_indices(nums):
    max_sum = current_sum = nums[0]
    start = end = temp_start = 0
    
    for i in range(1, len(nums)):
        if nums[i] > current_sum + nums[i]:
            current_sum = nums[i]
            temp_start = i
        else:
            current_sum = current_sum + nums[i]
        
        if current_sum > max_sum:
            max_sum = current_sum
            start = temp_start
            end = i
    
    return max_sum, start, end
```

### Minimum Subarray Sum

```python
def min_subarray_sum(nums):
    min_sum = current_sum = nums[0]
    for i in range(1, len(nums)):
        current_sum = min(nums[i], current_sum + nums[i])
        min_sum = min(min_sum, current_sum)
    return min_sum
```

### Maximum Circular Subarray Sum

```python
def max_circular_subarray(nums):
    # Case 1: Max subarray doesn't wrap
    max_kadane = kadane_max(nums)
    
    # Case 2: Max subarray wraps around
    # Equivalent to: total_sum - min_subarray
    total_sum = sum(nums)
    min_kadane = kadane_min(nums)
    
    # If all negative, max_kadane handles it
    if min_kadane == total_sum:
        return max_kadane
    
    return max(max_kadane, total_sum - min_kadane)

def kadane_max(nums):
    max_sum = current = nums[0]
    for num in nums[1:]:
        current = max(num, current + num)
        max_sum = max(max_sum, current)
    return max_sum

def kadane_min(nums):
    min_sum = current = nums[0]
    for num in nums[1:]:
        current = min(num, current + num)
        min_sum = min(min_sum, current)
    return min_sum
```

### Maximum Product Subarray

```python
def max_product_subarray(nums):
    if not nums:
        return 0
    
    max_prod = min_prod = result = nums[0]
    
    for i in range(1, len(nums)):
        num = nums[i]
        # When multiplying by negative, min becomes max
        if num < 0:
            max_prod, min_prod = min_prod, max_prod
        
        max_prod = max(num, max_prod * num)
        min_prod = min(num, min_prod * num)
        result = max(result, max_prod)
    
    return result
# Time: O(n), Space: O(1)
```

---

## 9. String Matching Algorithms

### Brute Force

```python
def brute_force_search(text, pattern):
    n, m = len(text), len(pattern)
    matches = []
    
    for i in range(n - m + 1):
        match = True
        for j in range(m):
            if text[i + j] != pattern[j]:
                match = False
                break
        if match:
            matches.append(i)
    
    return matches
# Time: O(n * m), Space: O(1)
```

### KMP Algorithm (Knuth-Morris-Pratt)

```python
def kmp_search(text, pattern):
    def build_lps(pattern):
        """Longest Proper Prefix which is also Suffix"""
        m = len(pattern)
        lps = [0] * m
        length = 0
        i = 1
        
        while i < m:
            if pattern[i] == pattern[length]:
                length += 1
                lps[i] = length
                i += 1
            else:
                if length != 0:
                    length = lps[length - 1]
                else:
                    lps[i] = 0
                    i += 1
        return lps
    
    n, m = len(text), len(pattern)
    lps = build_lps(pattern)
    matches = []
    
    i = j = 0  # i for text, j for pattern
    while i < n:
        if text[i] == pattern[j]:
            i += 1
            j += 1
            if j == m:
                matches.append(i - j)
                j = lps[j - 1]
        else:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1
    
    return matches
# Time: O(n + m), Space: O(m)
```

### Rabin-Karp Algorithm

```python
def rabin_karp(text, pattern):
    n, m = len(text), len(pattern)
    if m > n:
        return []
    
    base = 26
    mod = 10**9 + 7
    matches = []
    
    # Calculate hash of pattern and first window
    pattern_hash = 0
    text_hash = 0
    h = 1  # base^(m-1)
    
    for i in range(m - 1):
        h = (h * base) % mod
    
    for i in range(m):
        pattern_hash = (base * pattern_hash + ord(pattern[i])) % mod
        text_hash = (base * text_hash + ord(text[i])) % mod
    
    # Slide the window
    for i in range(n - m + 1):
        if pattern_hash == text_hash:
            # Verify character by character
            if text[i:i+m] == pattern:
                matches.append(i)
        
        if i < n - m:
            # Remove first char, add next char
            text_hash = (base * (text_hash - ord(text[i]) * h) + 
                        ord(text[i + m])) % mod
            if text_hash < 0:
                text_hash += mod
    
    return matches
# Time: O(n + m) average, O(n * m) worst case, Space: O(1)
```

### Z-Algorithm

```python
def z_algorithm(s):
    """Z[i] = length of longest substring starting at i which is also a prefix"""
    n = len(s)
    z = [0] * n
    left = right = 0
    
    for i in range(1, n):
        if i > right:
            left = right = i
            while right < n and s[right - left] == s[right]:
                right += 1
            z[i] = right - left
            right -= 1
        else:
            k = i - left
            if z[k] < right - i + 1:
                z[i] = z[k]
            else:
                left = i
                while right < n and s[right - left] == s[right]:
                    right += 1
                z[i] = right - left
                right -= 1
    return z

def z_search(text, pattern):
    combined = pattern + "$" + text
    z = z_algorithm(combined)
    m = len(pattern)
    return [i - m - 1 for i in range(m + 1, len(combined)) if z[i] == m]
# Time: O(n + m), Space: O(n + m)
```

---

## 10. Subarray Problems

### Common Subarray Problem Types

1. **Find subarray with given sum**
2. **Maximum/Minimum sum subarray**
3. **Longest subarray with constraint**
4. **Count subarrays with property**
5. **Subarray with distinct elements**

### Count Subarrays with Sum K

```python
from collections import defaultdict

def count_subarrays_sum_k(nums, k):
    count = 0
    prefix_sum = 0
    prefix_counts = defaultdict(int)
    prefix_counts[0] = 1
    
    for num in nums:
        prefix_sum += num
        count += prefix_counts[prefix_sum - k]
        prefix_counts[prefix_sum] += 1
    
    return count
```

### Longest Subarray with Sum K

```python
def longest_subarray_sum_k(nums, k):
    prefix_sum = 0
    first_occurrence = {0: -1}  # prefix_sum -> first index
    max_len = 0
    
    for i, num in enumerate(nums):
        prefix_sum += num
        
        if prefix_sum - k in first_occurrence:
            max_len = max(max_len, i - first_occurrence[prefix_sum - k])
        
        if prefix_sum not in first_occurrence:
            first_occurrence[prefix_sum] = i
    
    return max_len
```

### Subarray with Given Sum (Positive Numbers)

```python
def subarray_sum_positive(arr, target):
    left = 0
    current_sum = 0
    
    for right in range(len(arr)):
        current_sum += arr[right]
        
        while current_sum > target and left <= right:
            current_sum -= arr[left]
            left += 1
        
        if current_sum == target:
            return (left, right)
    
    return (-1, -1)
```

### Count Subarrays with At Most K Distinct Elements

```python
from collections import defaultdict

def at_most_k_distinct(nums, k):
    count = 0
    left = 0
    freq = defaultdict(int)
    distinct = 0
    
    for right, num in enumerate(nums):
        if freq[num] == 0:
            distinct += 1
        freq[num] += 1
        
        while distinct > k:
            freq[nums[left]] -= 1
            if freq[nums[left]] == 0:
                distinct -= 1
            left += 1
        
        count += right - left + 1  # All subarrays ending at right
    
    return count

def exactly_k_distinct(nums, k):
    return at_most_k_distinct(nums, k) - at_most_k_distinct(nums, k - 1)
```

---

## 11. Common Patterns & Templates

### Pattern 1: In-Place Array Modification

```python
# Move Zeros to End
def move_zeros(nums):
    write_idx = 0
    for read_idx in range(len(nums)):
        if nums[read_idx] != 0:
            nums[write_idx], nums[read_idx] = nums[read_idx], nums[write_idx]
            write_idx += 1
```

### Pattern 2: Dutch National Flag (3-way partition)

```python
def sort_colors(nums):  # 0, 1, 2
    low, mid, high = 0, 0, len(nums) - 1
    
    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1
```

### Pattern 3: Merge Intervals

```python
def merge_intervals(intervals):
    if not intervals:
        return []
    
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    
    for start, end in intervals[1:]:
        if start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])
    
    return merged
```

### Pattern 4: Binary Search on Answer

```python
def find_kth_smallest(matrix, k):
    def count_less_equal(mid):
        count = 0
        row, col = len(matrix) - 1, 0
        while row >= 0 and col < len(matrix[0]):
            if matrix[row][col] <= mid:
                count += row + 1
                col += 1
            else:
                row -= 1
        return count
    
    lo, hi = matrix[0][0], matrix[-1][-1]
    while lo < hi:
        mid = (lo + hi) // 2
        if count_less_equal(mid) < k:
            lo = mid + 1
        else:
            hi = mid
    return lo
```

### Pattern 5: Frequency Counter

```python
from collections import Counter

def find_majority_element(nums):
    counts = Counter(nums)
    return max(counts.keys(), key=counts.get)

# Boyer-Moore Voting (O(1) space)
def majority_element_optimal(nums):
    candidate = count = 0
    for num in nums:
        if count == 0:
            candidate = num
        count += 1 if num == candidate else -1
    return candidate
```

---

## 12. Time Complexity Reference

### Array Operations
| Operation | Time | Notes |
|-----------|------|-------|
| Access | O(1) | Direct index access |
| Linear Search | O(n) | Check each element |
| Binary Search | O(log n) | Sorted array only |
| Insert/Delete (end) | O(1)* | *Amortized for dynamic |
| Insert/Delete (middle) | O(n) | Shift elements |
| Sort | O(n log n) | Comparison-based |

### String Operations (Python)
| Operation | Time | Notes |
|-----------|------|-------|
| Length | O(1) | Cached |
| Access char | O(1) | Direct index |
| Slice | O(k) | k = slice length |
| Concatenate | O(n + m) | Creates new string |
| Find/Index | O(n * m) | Worst case |
| Replace | O(n) | Creates new string |
| Split/Join | O(n) | Linear in length |

### Algorithm Complexities
| Algorithm | Time | Space |
|-----------|------|-------|
| Kadane's | O(n) | O(1) |
| Prefix Sum (build) | O(n) | O(n) |
| Prefix Sum (query) | O(1) | - |
| Two Pointers | O(n) | O(1) |
| Sliding Window | O(n) | O(1) to O(k) |
| KMP | O(n + m) | O(m) |
| Rabin-Karp | O(n + m) avg | O(1) |
| Z-Algorithm | O(n + m) | O(n + m) |

---

## Quick Problem-Solving Checklist

```
□ Is the array sorted? → Consider Two Pointers, Binary Search
□ Finding subarray with constraint? → Sliding Window or Prefix Sum
□ Maximum/Minimum subarray? → Kadane's Algorithm
□ Need O(n) with O(1) space? → Two Pointers or In-place modification
□ Range queries? → Prefix Sum or Segment Tree
□ Pattern matching? → KMP/Rabin-Karp/Z-Algorithm
□ Frequency counting? → Hash Map
□ Need to maintain order? → Preserve indices with hash map
□ Matrix problem? → Think about rows, cols, diagonals separately
□ Subarray count? → Often uses prefix sum with hash map
```

---

## Practice Problems by Topic

### Beginner
1. Two Sum
2. Reverse String
3. Valid Palindrome
4. Merge Sorted Array
5. Remove Duplicates from Sorted Array

### Intermediate
1. 3Sum
2. Container With Most Water
3. Longest Substring Without Repeating Characters
4. Maximum Subarray (Kadane's)
5. Product of Array Except Self

### Advanced
1. Trapping Rain Water
2. Minimum Window Substring
3. Longest Consecutive Sequence
4. Subarray Sum Equals K
5. Implement strStr() (KMP)

### Expert
1. Median of Two Sorted Arrays
2. Sliding Window Maximum (Deque)
3. Maximum Product Subarray
4. Longest Palindromic Substring
5. Regular Expression Matching

---

> 💡 **Study Tip**: Master the patterns, not just the problems. Each pattern can solve dozens of variations!
