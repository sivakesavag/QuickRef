# 🎯 DSA Mastery: Complete Curriculum

> **240+ Assignments | Beginner → Expert | Self-Contained Learning Path**

---

## 📚 Table of Contents

1. [Beginner Level (1-60)](#-beginner-level)
2. [Intermediate Level (61-120)](#-intermediate-level)
3. [Advanced Level (121-180)](#-advanced-level)
4. [Expert Level (181-240+)](#-expert-level)

---

## 📖 How to Use This Curriculum

- **Difficulty Scale**: ★☆☆☆☆ (Easy) to ★★★★★ (Very Hard)
- **Complete in order** for optimal learning progression
- **Time estimates** are for first-time solving; aim to improve speed on revisits
- **Test all edge cases** provided before moving forward

---

# 🟢 BEGINNER LEVEL
## Foundational Concepts and Basic Operations (Assignments 1-60)

---

## Section A: Arrays Fundamentals (1-15)

---

### Assignment 1: Array Traversal and Sum
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Arrays - Basics

#### Problem Statement
Given an array of `n` integers, calculate the sum of all elements.

**Constraints:**
- 1 ≤ n ≤ 10^5
- -10^9 ≤ arr[i] ≤ 10^9

#### Input/Output Format
- **Input**: First line: integer `n`. Second line: `n` space-separated integers.
- **Output**: Single integer representing the sum.

#### Examples
```
Input:
5
1 2 3 4 5

Output:
15
```

#### Learning Objectives
- Understand array indexing (0-based vs 1-based)
- Implement basic iteration
- Handle integer overflow considerations

#### Hints
1. Use a loop to iterate through each element
2. Consider using `long long` for sum to prevent overflow

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `1` `[5]` | `5` | Single element |
| `3` `[-1, 0, 1]` | `0` | Negative numbers |
| `5` `[1000000000, 1000000000, 1000000000, 1000000000, 1000000000]` | `5000000000` | Large numbers |

#### Common Mistakes
- Using `int` instead of `long long` for sum
- Off-by-one errors in loop bounds

---

### Assignment 2: Find Maximum and Minimum
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Arrays - Basics

#### Problem Statement
Find both the maximum and minimum elements in an array in a single traversal.

**Constraints:**
- 1 ≤ n ≤ 10^5
- -10^9 ≤ arr[i] ≤ 10^9

#### Input/Output Format
- **Input**: First line: `n`. Second line: `n` integers.
- **Output**: Two integers: max and min, space-separated.

#### Examples
```
Input:
5
3 1 4 1 5

Output:
5 1
```

#### Learning Objectives
- Compare elements efficiently
- Initialize variables with appropriate boundary values

#### Hints
1. Initialize max to smallest possible value, min to largest
2. Alternative: Initialize with first element

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `1` `[42]` | `42 42` | Single element |
| `3` `[-5, -1, -10]` | `-1 -10` | All negative |
| `4` `[7, 7, 7, 7]` | `7 7` | All same |

#### Common Mistakes
- Initializing max to 0 (fails for negative arrays)
- Making two separate loops (inefficient)

---

### Assignment 3: Reverse an Array
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Arrays - Manipulation

#### Problem Statement
Reverse an array in-place without using extra space.

**Constraints:**
- 1 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: First line: `n`. Second line: `n` integers.
- **Output**: Reversed array.

#### Examples
```
Input:
5
1 2 3 4 5

Output:
5 4 3 2 1
```

#### Learning Objectives
- Two-pointer technique introduction
- In-place array modification
- Swap operations

#### Hints
1. Use two pointers: one at start, one at end
2. Swap elements and move pointers toward center

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `1` `[1]` | `1` | Single element |
| `2` `[1, 2]` | `2 1` | Two elements |
| `4` `[1, 2, 3, 4]` | `4 3 2 1` | Even length |

---

### Assignment 4: Linear Search
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Arrays - Searching

#### Problem Statement
Find the first occurrence of a target element in an array. Return its index or -1 if not found.

**Constraints:**
- 1 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: `n`, array of `n` elements, target `t`
- **Output**: Index of first occurrence or -1

#### Examples
```
Input:
5
1 2 3 2 5
2

Output:
1
```

#### Learning Objectives
- Sequential search algorithm
- Early termination optimization
- Return value handling

#### Hints
1. Iterate and compare each element
2. Return immediately when found

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1]` target=`1` | `0` | Found at first |
| `[1,2,3]` target=`3` | `2` | Found at last |
| `[1,2,3]` target=`5` | `-1` | Not found |

---

### Assignment 5: Count Element Occurrences
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Arrays - Basics

#### Problem Statement
Count how many times a specific element appears in an array.

**Constraints:**
- 1 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: Array and target element
- **Output**: Count of occurrences

#### Examples
```
Input:
7
1 2 2 3 2 4 2
2

Output:
4
```

#### Learning Objectives
- Counter pattern
- Conditional counting

#### Hints
1. Maintain a count variable
2. Increment when element matches

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1,1,1]` target=`1` | `3` | All match |
| `[1,2,3]` target=`5` | `0` | None match |

---

### Assignment 6: Second Largest Element
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Arrays - Logic

#### Problem Statement
Find the second largest element in an array. If no second largest exists, return -1.

**Constraints:**
- 1 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: Array of integers
- **Output**: Second largest or -1

#### Examples
```
Input:
5
12 35 1 10 34

Output:
34
```

#### Learning Objectives
- Tracking multiple values
- Edge case handling

#### Hints
1. Track both largest and second largest
2. Handle duplicates correctly

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[5, 5, 5]` | `-1` | All same |
| `[1, 2]` | `1` | Two elements |
| `[10]` | `-1` | Single element |

---

### Assignment 7: Remove Duplicates from Sorted Array
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Arrays - Two Pointers

#### Problem Statement
Remove duplicates from a sorted array in-place. Return the new length.

**Constraints:**
- Array is sorted in non-decreasing order
- 0 ≤ n ≤ 10^4

#### Input/Output Format
- **Input**: Sorted array
- **Output**: New length, modified array

#### Examples
```
Input:
[1, 1, 2, 2, 3]

Output:
3, [1, 2, 3, _, _]
```

#### Learning Objectives
- Two-pointer technique
- In-place modification with write pointer

#### Hints
1. Use a "write" pointer that tracks where to place next unique element
2. Array being sorted means duplicates are adjacent

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[]` | `0` | Empty array |
| `[1, 1, 1]` | `1` | All duplicates |
| `[1, 2, 3]` | `3` | No duplicates |

---

### Assignment 8: Move Zeros to End
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Arrays - Two Pointers

#### Problem Statement
Move all zeros in an array to the end while maintaining relative order of non-zero elements.

**Constraints:**
- 1 ≤ n ≤ 10^4

#### Input/Output Format
- **Input**: Array with zeros and non-zeros
- **Output**: Modified array

#### Examples
```
Input:
[0, 1, 0, 3, 12]

Output:
[1, 3, 12, 0, 0]
```

#### Learning Objectives
- Order-preserving rearrangement
- Two-pointer approach variant

#### Hints
1. Use a pointer to track position for next non-zero
2. Swap when non-zero is found

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[0, 0, 0]` | `[0, 0, 0]` | All zeros |
| `[1, 2, 3]` | `[1, 2, 3]` | No zeros |
| `[0]` | `[0]` | Single zero |

---

### Assignment 9: Rotate Array Left by K
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Arrays - Rotation

#### Problem Statement
Rotate an array to the left by K positions.

**Constraints:**
- 1 ≤ n ≤ 10^5
- 0 ≤ k ≤ 10^9

#### Input/Output Format
- **Input**: Array and K
- **Output**: Rotated array

#### Examples
```
Input:
[1, 2, 3, 4, 5], k=2

Output:
[3, 4, 5, 1, 2]
```

#### Learning Objectives
- Modular arithmetic with array indices
- Reversal algorithm technique

#### Hints
1. k = k % n (handle k > n)
2. Try: reverse first k, reverse rest, reverse all

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1,2,3]` k=`0` | `[1,2,3]` | No rotation |
| `[1,2,3]` k=`3` | `[1,2,3]` | Full rotation |
| `[1,2,3]` k=`5` | `[3,1,2]` | k > n |

---

### Assignment 10: Rotate Array Right by K
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Arrays - Rotation

#### Problem Statement
Rotate an array to the right by K positions.

**Constraints:**
- 1 ≤ n ≤ 10^5
- 0 ≤ k ≤ 10^9

#### Input/Output Format
- **Input**: Array and K
- **Output**: Rotated array

#### Examples
```
Input:
[1, 2, 3, 4, 5], k=2

Output:
[4, 5, 1, 2, 3]
```

#### Learning Objectives
- Right rotation vs left rotation relationship
- Efficient O(n) solution

#### Hints
1. Right rotate by k = Left rotate by (n-k)
2. Alternatively: reverse all, reverse first k, reverse rest

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1]` k=`100` | `[1]` | Single element |
| `[1,2]` k=`1` | `[2,1]` | Two elements |

---

### Assignment 11: Check if Array is Sorted
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Arrays - Validation

#### Problem Statement
Check if an array is sorted in non-decreasing order.

**Constraints:**
- 1 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: Array
- **Output**: "YES" or "NO"

#### Examples
```
Input:
[1, 2, 2, 3, 4]

Output:
YES
```

#### Learning Objectives
- Pairwise comparison
- Early termination

#### Hints
1. Compare each adjacent pair
2. Return false immediately if violation found

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1]` | `YES` | Single element |
| `[2, 1]` | `NO` | Simple violation |
| `[1, 1, 1]` | `YES` | All equal |

---

### Assignment 12: Union of Two Sorted Arrays
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Arrays - Merge

#### Problem Statement
Find the union of two sorted arrays (all unique elements from both).

**Constraints:**
- Arrays are sorted
- 1 ≤ n, m ≤ 10^5

#### Input/Output Format
- **Input**: Two sorted arrays
- **Output**: Sorted union array

#### Examples
```
Input:
[1, 2, 3, 4, 5]
[2, 3, 4, 4, 5]

Output:
[1, 2, 3, 4, 5]
```

#### Learning Objectives
- Two-pointer merge technique
- Duplicate handling

#### Hints
1. Use two pointers, one for each array
2. Skip duplicates in result

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1,2]` `[3,4]` | `[1,2,3,4]` | No overlap |
| `[1,2]` `[1,2]` | `[1,2]` | Identical arrays |
| `[]` `[1,2]` | `[1,2]` | One empty |

---

### Assignment 13: Intersection of Two Sorted Arrays
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Arrays - Merge

#### Problem Statement
Find common elements between two sorted arrays.

**Constraints:**
- Arrays are sorted
- 1 ≤ n, m ≤ 10^5

#### Input/Output Format
- **Input**: Two sorted arrays
- **Output**: Sorted intersection array

#### Examples
```
Input:
[1, 2, 2, 3, 4]
[2, 2, 4, 6]

Output:
[2, 2, 4]
```

#### Learning Objectives
- Two-pointer technique for finding common elements
- Understanding intersection vs union

#### Hints
1. Advance pointer of smaller element
2. Add to result when elements match

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1,2]` `[3,4]` | `[]` | No common |
| `[1,1,1]` `[1,1]` | `[1,1]` | Handle duplicates |

---

### Assignment 14: Find Missing Number
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Arrays - Math

#### Problem Statement
Given an array containing n distinct numbers from 0 to n, find the missing number.

**Constraints:**
- 0 ≤ arr[i] ≤ n
- All numbers are unique

#### Input/Output Format
- **Input**: Array of n numbers
- **Output**: Missing number

#### Examples
```
Input:
[3, 0, 1]

Output:
2
```

#### Learning Objectives
- Sum formula technique
- XOR technique for finding missing

#### Hints
1. Sum of 0 to n = n*(n+1)/2
2. Alternative: XOR all numbers with 0 to n

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[0]` | `1` | Missing last |
| `[1]` | `0` | Missing first |
| `[0,1]` | `2` | Missing at end |

---

### Assignment 15: Find Single Number
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Arrays - Bit Manipulation Intro

#### Problem Statement
Every element appears twice except one. Find that single element.

**Constraints:**
- Array has odd length
- Except one, each appears exactly twice

#### Input/Output Format
- **Input**: Array
- **Output**: Single number

#### Examples
```
Input:
[2, 2, 1]

Output:
1
```

#### Learning Objectives
- XOR property: a ⊕ a = 0, a ⊕ 0 = a
- Bit manipulation basics

#### Hints
1. XOR all elements together
2. Pairs cancel out, leaving the single number

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1]` | `1` | Single element |
| `[4,1,2,1,2]` | `4` | Multiple pairs |

---

## Section B: String Fundamentals (16-25)

---

### Assignment 16: Reverse a String
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Strings - Basics

#### Problem Statement
Reverse a string in-place.

**Constraints:**
- 1 ≤ len ≤ 10^5

#### Input/Output Format
- **Input**: String
- **Output**: Reversed string

#### Examples
```
Input: "hello"
Output: "olleh"
```

#### Learning Objectives
- String as character array
- Two-pointer technique on strings

#### Hints
1. Swap characters from both ends

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `"a"` | `"a"` | Single char |
| `"ab"` | `"ba"` | Two chars |
| `""` | `""` | Empty string |

---

### Assignment 17: Check Palindrome
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Strings - Validation

#### Problem Statement
Check if a string is a palindrome (reads same forwards and backwards).

**Constraints:**
- Consider only alphanumeric characters
- Ignore case

#### Input/Output Format
- **Input**: String
- **Output**: "YES" or "NO"

#### Examples
```
Input: "A man, a plan, a canal: Panama"
Output: YES
```

#### Learning Objectives
- Two-pointer comparison
- Character filtering and case handling

#### Hints
1. Use two pointers from both ends
2. Skip non-alphanumeric characters

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `""` | `YES` | Empty |
| `"a"` | `YES` | Single |
| `"race a car"` | `NO` | Not palindrome |

---

### Assignment 18: Count Vowels and Consonants
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Strings - Counting

#### Problem Statement
Count the number of vowels and consonants in a string.

**Constraints:**
- String contains only alphabets

#### Input/Output Format
- **Input**: String
- **Output**: Two integers: vowel count, consonant count

#### Examples
```
Input: "Hello World"
Output: 3 7
```

#### Learning Objectives
- Character classification
- Set membership check

#### Hints
1. Define vowels set: {a, e, i, o, u}
2. Handle both cases

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `"aeiou"` | `5 0` | All vowels |
| `"xyz"` | `0 3` | All consonants |

---

### Assignment 19: Check Anagram
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Strings - Comparison

#### Problem Statement
Check if two strings are anagrams (same characters, different order).

**Constraints:**
- 1 ≤ len ≤ 10^5
- Lowercase letters only

#### Input/Output Format
- **Input**: Two strings
- **Output**: "YES" or "NO"

#### Examples
```
Input: "listen", "silent"
Output: YES
```

#### Learning Objectives
- Character frequency counting
- Array as frequency map

#### Hints
1. Count frequency of each character in both strings
2. Compare frequency arrays

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `"a"` `"a"` | `YES` | Single char |
| `"ab"` `"ba"` | `YES` | Simple anagram |
| `"ab"` `"abc"` | `NO` | Different lengths |

---

### Assignment 20: First Non-Repeating Character
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Strings - Frequency

#### Problem Statement
Find the first character that appears only once in a string.

**Constraints:**
- 1 ≤ len ≤ 10^5

#### Input/Output Format
- **Input**: String
- **Output**: First non-repeating character or '-1'

#### Examples
```
Input: "leetcode"
Output: 'l'
```

#### Learning Objectives
- Two-pass frequency counting
- Order preservation

#### Hints
1. First pass: count frequencies
2. Second pass: find first with count 1

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `"aabb"` | `-1` | All repeat |
| `"ab"` | `'a'` | First is unique |

---

### Assignment 21: Remove All Occurrences of Substring
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Strings - Manipulation

#### Problem Statement
Remove all occurrences of a substring from a string.

**Constraints:**
- 1 ≤ len(s), len(part) ≤ 1000

#### Input/Output Format
- **Input**: String s, substring part
- **Output**: String after removals

#### Examples
```
Input: s = "daabcbaabcbc", part = "abc"
Output: "dab"
```

#### Learning Objectives
- Iterative removal pattern
- String searching

#### Hints
1. Repeatedly find and remove until no occurrence left
2. Be careful: removal may create new occurrences

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `"aaa"` `"a"` | `""` | Remove all |
| `"abc"` `"d"` | `"abc"` | Not found |

---

### Assignment 22: Longest Common Prefix
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Strings - Comparison

#### Problem Statement
Find the longest common prefix among an array of strings.

**Constraints:**
- 1 ≤ n ≤ 200
- 0 ≤ len ≤ 200

#### Input/Output Format
- **Input**: Array of strings
- **Output**: Longest common prefix

#### Examples
```
Input: ["flower", "flow", "flight"]
Output: "fl"
```

#### Learning Objectives
- Vertical scanning approach
- Early termination

#### Hints
1. Compare characters at same position across all strings
2. Stop when mismatch found

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `["a"]` | `"a"` | Single string |
| `["dog","racecar"]` | `""` | No common |
| `["","abc"]` | `""` | Empty string present |

---

### Assignment 23: String Compression
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Strings - Run-Length Encoding

#### Problem Statement
Compress a string using counts of repeated characters. If compressed not smaller, return original.

**Constraints:**
- Only uppercase/lowercase letters

#### Input/Output Format
- **Input**: String
- **Output**: Compressed string or original

#### Examples
```
Input: "aabcccccaaa"
Output: "a2b1c5a3"
```

#### Learning Objectives
- Run-length encoding concept
- Counting consecutive characters

#### Hints
1. Use a counter for consecutive identical characters
2. Build result string incrementally

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `"abc"` | `"abc"` | Each once (compressed longer) |
| `"aa"` | `"a2"` | Simple compression |

---

### Assignment 24: Valid Parentheses (Intro)
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Strings - Matching

#### Problem Statement
Check if a string containing only '(' and ')' is valid (properly matched).

**Constraints:**
- 1 ≤ len ≤ 10^4

#### Input/Output Format
- **Input**: String of parentheses
- **Output**: "YES" or "NO"

#### Examples
```
Input: "(())"
Output: YES
```

#### Learning Objectives
- Counter approach for single type parentheses
- Balance checking

#### Hints
1. Increment for '(', decrement for ')'
2. Counter should never go negative
3. Final counter should be 0

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `""` | `YES` | Empty |
| `"("` | `NO` | Unmatched open |
| `")("` | `NO` | Wrong order |

---

### Assignment 25: Isomorphic Strings
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Strings - Mapping

#### Problem Statement
Check if two strings are isomorphic (each character can be mapped to another uniquely).

**Constraints:**
- len(s) == len(t)

#### Input/Output Format
- **Input**: Two strings s and t
- **Output**: "YES" or "NO"

#### Examples
```
Input: s = "egg", t = "add"
Output: YES (e->a, g->d)
```

#### Learning Objectives
- Bijective mapping concept
- Two-way mapping validation

#### Hints
1. Map characters from s to t and verify consistency
2. Also ensure no two characters map to same character

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `"foo"` `"bar"` | `NO` | Two chars map to same |
| `"paper"` `"title"` | `YES` | Valid mapping |

---

## Section C: Linked Lists Basics (26-35)

---

### Assignment 26: Implement Singly Linked List
**Difficulty**: ★★☆☆☆ | **Time**: 30 mins | **Category**: Linked Lists - Implementation

#### Problem Statement
Implement a singly linked list with operations: insert at head, insert at tail, delete by value, display.

**Constraints:**
- Values are integers

#### Input/Output Format
- **Input**: Series of operations
- **Output**: Result of each operation

#### Examples
```
insertHead(1), insertTail(2), insertHead(0), display()
Output: 0 -> 1 -> 2 -> NULL
```

#### Learning Objectives
- Node structure with data and next pointer
- Head pointer management
- Traversal pattern

#### Hints
1. Handle empty list case for each operation
2. For tail insert, traverse to last node first

#### Test Cases
| Operations | Output | Edge Case |
|------------|--------|-----------|
| `insertHead(1), deleteByValue(1)` | empty list | Delete only element |
| `insertTail(1)` on empty | `1 -> NULL` | First element |

#### Common Mistakes
- Forgetting to update head when deleting first node
- Not handling empty list case

---

### Assignment 27: Find Length of Linked List
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Linked Lists - Traversal

#### Problem Statement
Count the number of nodes in a linked list.

#### Input/Output Format
- **Input**: Head of linked list
- **Output**: Number of nodes

#### Examples
```
1 -> 2 -> 3 -> NULL
Output: 3
```

#### Learning Objectives
- Basic traversal with counter

#### Hints
1. Traverse while current is not NULL
2. Increment counter each step

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `NULL` | `0` | Empty list |
| `1 -> NULL` | `1` | Single node |

---

### Assignment 28: Search in Linked List
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Linked Lists - Searching

#### Problem Statement
Search for a value in linked list. Return its position (1-indexed) or -1.

#### Input/Output Format
- **Input**: Head, target value
- **Output**: Position or -1

#### Examples
```
List: 1 -> 2 -> 3, Target: 2
Output: 2
```

#### Learning Objectives
- Linear search in linked structure
- Position tracking during traversal

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| Empty list, any target | `-1` | Empty |
| `1->2->3`, target=1 | `1` | Found at head |
| `1->2->3`, target=3 | `3` | Found at tail |

---

### Assignment 29: Insert at Position
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Linked Lists - Insertion

#### Problem Statement
Insert a node at a given position in linked list (1-indexed).

**Constraints:**
- Position is valid (1 ≤ pos ≤ length + 1)

#### Input/Output Format
- **Input**: Head, position, value
- **Output**: Modified list

#### Examples
```
List: 1 -> 3, Insert 2 at position 2
Output: 1 -> 2 -> 3
```

#### Learning Objectives
- Finding position in linked list
- Pointer manipulation for insertion

#### Hints
1. Special case: position = 1 (insert at head)
2. Navigate to node before insertion point

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| Empty, pos=1 | New node as head | Insert into empty |
| `1->2`, pos=3 | `1->2->new` | Insert at end |

---

### Assignment 30: Delete at Position
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Linked Lists - Deletion

#### Problem Statement
Delete node at given position (1-indexed).

**Constraints:**
- Position is valid

#### Input/Output Format
- **Input**: Head, position
- **Output**: Modified list

#### Examples
```
List: 1 -> 2 -> 3, Delete at position 2
Output: 1 -> 3
```

#### Learning Objectives
- Pointer manipulation for deletion
- Memory considerations

#### Hints
1. Special case: position = 1 (delete head)
2. Keep track of previous node

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `1`, delete pos=1 | Empty | Delete only node |
| `1->2->3`, pos=3 | `1->2` | Delete tail |

---

### Assignment 31: Reverse Linked List
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Linked Lists - Fundamentals

#### Problem Statement
Reverse a singly linked list iteratively.

#### Input/Output Format
- **Input**: Head
- **Output**: New head (of reversed list)

#### Examples
```
Input: 1 -> 2 -> 3 -> NULL
Output: 3 -> 2 -> 1 -> NULL
```

#### Learning Objectives
- Three-pointer technique
- In-place reversal

#### Hints
1. Use three pointers: prev, current, next
2. Change each node's next to point to previous

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `NULL` | `NULL` | Empty |
| `1` | `1` | Single node |

#### Common Mistakes
- Losing reference to next node before updating

---

### Assignment 32: Find Middle of Linked List
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Linked Lists - Two Pointers

#### Problem Statement
Find the middle node. For even length, return second middle.

#### Input/Output Format
- **Input**: Head
- **Output**: Middle node value

#### Examples
```
1 -> 2 -> 3 -> 4 -> 5
Output: 3

1 -> 2 -> 3 -> 4
Output: 3
```

#### Learning Objectives
- Fast and slow pointer technique
- Single-pass solution

#### Hints
1. Fast pointer moves 2 steps, slow moves 1
2. When fast reaches end, slow is at middle

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `1` | `1` | Single node |
| `1->2` | `2` | Two nodes |

---

### Assignment 33: Detect Cycle in Linked List
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Linked Lists - Cycle Detection

#### Problem Statement
Detect if a linked list has a cycle.

#### Input/Output Format
- **Input**: Head
- **Output**: True/False

#### Examples
```
1 -> 2 -> 3 -> 4 -> 2 (cycle to node 2)
Output: True
```

#### Learning Objectives
- Floyd's Cycle Detection (Tortoise and Hare)
- Space-efficient detection

#### Hints
1. Use fast and slow pointers
2. If they meet, cycle exists
3. If fast reaches NULL, no cycle

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `NULL` | `False` | Empty |
| `1` | `False` | Single, no cycle |
| `1->1` (self loop) | `True` | Self cycle |

---

### Assignment 34: Remove Nth Node from End
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Linked Lists - Two Pointers

#### Problem Statement
Remove the nth node from the end in one pass.

**Constraints:**
- n is valid (1 ≤ n ≤ length)

#### Input/Output Format
- **Input**: Head, n
- **Output**: Modified list

#### Examples
```
List: 1 -> 2 -> 3 -> 4 -> 5, n=2
Output: 1 -> 2 -> 3 -> 5
```

#### Learning Objectives
- Two-pointer with gap technique
- Dummy node usage

#### Hints
1. Advance first pointer n steps
2. Move both pointers until first reaches end
3. Use dummy node to handle edge cases

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `1->2`, n=2 | `2` | Remove head |
| `1`, n=1 | Empty | Remove only node |

---

### Assignment 35: Merge Two Sorted Linked Lists
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Linked Lists - Merging

#### Problem Statement
Merge two sorted linked lists into one sorted list.

#### Input/Output Format
- **Input**: Two sorted list heads
- **Output**: Merged sorted list head

#### Examples
```
List1: 1 -> 3 -> 5
List2: 2 -> 4 -> 6
Output: 1 -> 2 -> 3 -> 4 -> 5 -> 6
```

#### Learning Objectives
- Two-pointer merge technique on lists
- Dummy node pattern

#### Hints
1. Use dummy node to simplify head handling
2. Compare and link smaller node, advance that pointer

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| Empty, `1->2` | `1->2` | One empty |
| Empty, Empty | Empty | Both empty |
| `1->1`, `1->1` | `1->1->1->1` | Duplicates |

---

## Section D: Stacks and Queues (36-45)

---

### Assignment 36: Implement Stack using Array
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Stacks - Implementation

#### Problem Statement
Implement a stack with push, pop, peek, isEmpty operations using an array.

**Constraints:**
- Fixed maximum size

#### Input/Output Format
- **Input**: Operations
- **Output**: Results

#### Examples
```
push(1), push(2), pop(), peek()
Output: 2, 1
```

#### Learning Objectives
- LIFO principle
- Top pointer management

#### Hints
1. Use top = -1 for empty stack
2. Check overflow before push, underflow before pop

#### Test Cases
| Operations | Output | Edge Case |
|------------|--------|-----------|
| pop on empty | Error/underflow | Underflow |
| push to full | Error/overflow | Overflow |

---

### Assignment 37: Implement Stack using Linked List
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Stacks - Implementation

#### Problem Statement
Implement stack with push, pop, peek using linked list.

#### Input/Output Format
- **Input**: Operations
- **Output**: Results

#### Learning Objectives
- Dynamic stack size
- Head as top

#### Hints
1. Push = insert at head
2. Pop = remove from head

#### Test Cases
| Operations | Expected | Edge Case |
|------------|----------|-----------|
| push(1), pop() | 1 | Single element |
| Multiple pushes | Stack grows | Dynamic size |

---

### Assignment 38: Implement Queue using Array
**Difficulty**: ★★☆☆☆ | **Time**: 25 mins | **Category**: Queues - Implementation

#### Problem Statement
Implement a circular queue with enqueue, dequeue, front, isEmpty operations.

**Constraints:**
- Fixed maximum size

#### Input/Output Format
- **Input**: Operations
- **Output**: Results

#### Examples
```
enqueue(1), enqueue(2), dequeue(), front()
Output: 1, 2
```

#### Learning Objectives
- FIFO principle
- Circular array technique
- Front and rear pointer management

#### Hints
1. Use modulo for circular indexing
2. Track size or use (rear + 1) % n == front for full

#### Test Cases
| Operations | Output | Edge Case |
|------------|--------|-----------|
| dequeue on empty | Error | Underflow |
| Circular wrap-around | Correct values | Wrap test |

---

### Assignment 39: Implement Queue using Linked List
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Queues - Implementation

#### Problem Statement
Implement queue using linked list.

#### Learning Objectives
- Maintaining front and rear pointers
- O(1) enqueue and dequeue

#### Hints
1. Enqueue at rear (tail)
2. Dequeue from front (head)

---

### Assignment 40: Implement Queue using Two Stacks
**Difficulty**: ★★☆☆☆ | **Time**: 25 mins | **Category**: Queues - Advanced Implementation

#### Problem Statement
Implement a queue using two stacks.

#### Input/Output Format
- **Input**: Queue operations
- **Output**: Queue behavior

#### Learning Objectives
- Stack-based queue simulation
- Amortized analysis concept

#### Hints
1. stack1 for enqueue (push)
2. stack2 for dequeue (if empty, transfer all from stack1)

#### Test Cases
| Operations | Output | Notes |
|------------|--------|-------|
| enq(1), enq(2), deq() | 1 | FIFO order |
| interleaved operations | FIFO maintained | Various patterns |

---

### Assignment 41: Implement Stack using Two Queues
**Difficulty**: ★★☆☆☆ | **Time**: 25 mins | **Category**: Stacks - Advanced Implementation

#### Problem Statement
Implement a stack using two queues.

#### Learning Objectives
- Queue-based stack simulation
- Push or pop heavy approaches

#### Hints
1. Push-heavy: push to q1, O(1)
2. Pop: transfer n-1 elements to q2, dequeue last

---

### Assignment 42: Valid Parentheses (Multiple Types)
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Stacks - Application

#### Problem Statement
Check if string with '()', '[]', '{}' is valid.

**Constraints:**
- 1 ≤ len ≤ 10^4

#### Input/Output Format
- **Input**: String
- **Output**: True/False

#### Examples
```
Input: "([{}])"
Output: True

Input: "([)]"
Output: False
```

#### Learning Objectives
- Stack for matching problems
- Character pairing

#### Hints
1. Push opening brackets onto stack
2. For closing, check if top matches

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `""` | True | Empty |
| `"["` | False | Unmatched |
| `"]"` | False | No opening |

---

### Assignment 43: Next Greater Element
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Stacks - Monotonic Stack

#### Problem Statement
For each element, find the next greater element to its right. Return -1 if none.

**Constraints:**
- 1 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: Array
- **Output**: Array of next greater elements

#### Examples
```
Input: [4, 5, 2, 25]
Output: [5, 25, 25, -1]
```

#### Learning Objectives
- Monotonic stack concept
- Right-to-left processing

#### Hints
1. Process from right to left
2. Maintain stack of candidates (monotonically decreasing)
3. Pop smaller elements

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[1, 2, 3]` | `[2, 3, -1]` | Increasing |
| `[3, 2, 1]` | `[-1, -1, -1]` | Decreasing |

---

### Assignment 44: Stock Span Problem
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Stacks - Monotonic Stack

#### Problem Statement
Calculate span for each day (consecutive days before with price ≤ current, including current).

**Constraints:**
- 1 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: Array of prices
- **Output**: Array of spans

#### Examples
```
Input: [100, 80, 60, 70, 60, 75, 85]
Output: [1, 1, 1, 2, 1, 4, 6]
```

#### Learning Objectives
- Stack storing indices
- Previous greater element pattern

#### Hints
1. Stack stores indices of previous greater elements
2. Span = current index - index at stack top

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[10, 20, 30]` | `[1, 2, 3]` | Increasing |
| `[30, 20, 10]` | `[1, 1, 1]` | Decreasing |

---

### Assignment 45: Evaluate Postfix Expression
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Stacks - Expression Evaluation

#### Problem Statement
Evaluate a postfix (Reverse Polish Notation) expression.

**Constraints:**
- Valid expression
- Operators: +, -, *, /

#### Input/Output Format
- **Input**: Postfix expression (tokens)
- **Output**: Integer result

#### Examples
```
Input: ["2", "1", "+", "3", "*"]
Output: 9  (i.e., (2+1)*3)
```

#### Learning Objectives
- Stack for expression evaluation
- Operator precedence elimination

#### Hints
1. Push operands to stack
2. On operator: pop two, compute, push result

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `["2", "3", "+"]` | `5` | Simple |
| `["4", "13", "5", "/", "+"]` | `6` | Division |

---

## Section E: Basic Sorting Algorithms (46-50)

---

### Assignment 46: Bubble Sort
**Difficulty**: ★☆☆☆☆ | **Time**: 15 mins | **Category**: Sorting - Basic

#### Problem Statement
Implement Bubble Sort algorithm.

**Constraints:**
- 1 ≤ n ≤ 10^4

#### Input/Output Format
- **Input**: Array
- **Output**: Sorted array

#### Examples
```
Input: [64, 34, 25, 12, 22]
Output: [12, 22, 25, 34, 64]
```

#### Learning Objectives
- Adjacent element comparison
- Optimized version with early termination

#### Hints
1. Repeatedly swap adjacent elements if in wrong order
2. Add flag to detect already sorted array

#### Test Cases
| Input | Output | Time Complexity |
|-------|--------|-----------------|
| Sorted | Same | O(n) with optimization |
| Reverse | Sorted | O(n²) |
| All same | Same | O(n) |

---

### Assignment 47: Selection Sort
**Difficulty**: ★☆☆☆☆ | **Time**: 15 mins | **Category**: Sorting - Basic

#### Problem Statement
Implement Selection Sort algorithm.

#### Learning Objectives
- Finding minimum in unsorted portion
- Minimizing swaps

#### Hints
1. Find minimum in remaining array
2. Swap with first unsorted position

#### Test Cases
| Input | Output | Notes |
|-------|--------|-------|
| Any array | Sorted | Always O(n²) |

---

### Assignment 48: Insertion Sort
**Difficulty**: ★☆☆☆☆ | **Time**: 15 mins | **Category**: Sorting - Basic

#### Problem Statement
Implement Insertion Sort algorithm.

#### Learning Objectives
- Building sorted portion incrementally
- Shifting elements

#### Hints
1. Insert each element into correct position in sorted portion
2. Shift larger elements right

#### Test Cases
| Input | Output | Notes |
|-------|--------|-------|
| Nearly sorted | Sorted | O(n) best case |
| Reverse sorted | Sorted | O(n²) worst case |

---

### Assignment 49: Counting Inversions (Using Bubble Sort)
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Sorting - Applications

#### Problem Statement
Count the number of inversions (pairs where i < j but arr[i] > arr[j]).

#### Input/Output Format
- **Input**: Array
- **Output**: Number of inversions

#### Examples
```
Input: [2, 4, 1, 3, 5]
Output: 3 (inversions: (2,1), (4,1), (4,3))
```

#### Learning Objectives
- Understanding inversions
- Relationship with sorting

#### Hints
1. Count swaps in bubble sort = inversions
2. This is O(n²), efficient solution uses merge sort (intermediate)

---

### Assignment 50: Sort Array of 0s, 1s, 2s (Dutch National Flag)
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Sorting - Special

#### Problem Statement
Sort an array containing only 0s, 1s, and 2s in O(n) time, O(1) space.

#### Input/Output Format
- **Input**: Array of 0s, 1s, 2s
- **Output**: Sorted array

#### Examples
```
Input: [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]
```

#### Learning Objectives
- Three-way partitioning
- Dutch National Flag algorithm

#### Hints
1. Use three pointers: low, mid, high
2. 0s before low, 1s between low-high, 2s after high

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| `[0,0,0]` | `[0,0,0]` | All same |
| `[2,1,0]` | `[0,1,2]` | One of each |

---

## Section F: Recursion Basics (51-60)

---

### Assignment 51: Factorial Using Recursion
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Recursion - Basics

#### Problem Statement
Calculate factorial of n using recursion.

**Constraints:**
- 0 ≤ n ≤ 20

#### Input/Output Format
- **Input**: n
- **Output**: n!

#### Examples
```
Input: 5
Output: 120
```

#### Learning Objectives
- Base case and recursive case
- Stack memory visualization

#### Hints
1. Base: 0! = 1
2. Recursive: n! = n * (n-1)!

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| 0 | 1 | Base case |
| 1 | 1 | Base case |
| 20 | 2432902008176640000 | Large |

---

### Assignment 52: Fibonacci Using Recursion
**Difficulty**: ★☆☆☆☆ | **Time**: 15 mins | **Category**: Recursion - Basics

#### Problem Statement
Calculate nth Fibonacci number using recursion.

**Constraints:**
- 0 ≤ n ≤ 30 (naive recursion)

#### Input/Output Format
- **Input**: n
- **Output**: F(n)

#### Examples
```
Input: 6
Output: 8 (sequence: 0,1,1,2,3,5,8)
```

#### Learning Objectives
- Double recursion
- Exponential time complexity awareness

#### Hints
1. Base: F(0)=0, F(1)=1
2. Recursive: F(n) = F(n-1) + F(n-2)

#### Common Mistakes
- Ignoring exponential time complexity (solve with DP later)

---

### Assignment 53: Sum of Array Using Recursion
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Recursion - Array

#### Problem Statement
Find sum of array elements using recursion.

#### Learning Objectives
- Reducing problem size
- Head vs tail recursion

#### Hints
1. Base: empty array → 0
2. Recursive: first element + sum of rest

---

### Assignment 54: Reverse String Using Recursion
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Recursion - String

#### Problem Statement
Reverse a string using recursion.

#### Learning Objectives
- String manipulation with recursion
- Character at boundary

#### Hints
1. Base: empty or single char
2. Recursive: last char + reverse(rest)

---

### Assignment 55: Power Function (Exponentiation)
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Recursion - Math

#### Problem Statement
Calculate x^n using recursion.

**Constraints:**
- Handle negative exponents

#### Input/Output Format
- **Input**: x (float), n (int)
- **Output**: x^n

#### Examples
```
Input: x=2.0, n=10
Output: 1024.0
```

#### Learning Objectives
- Efficient exponentiation
- Binary exponentiation concept

#### Hints
1. x^n = x^(n/2) * x^(n/2) if n even
2. x^n = x * x^(n-1) if n odd
3. x^(-n) = 1 / x^n

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| 2.0, 0 | 1.0 | Zero exponent |
| 2.0, -2 | 0.25 | Negative exp |

---

### Assignment 56: Check Palindrome Using Recursion
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Recursion - String

#### Problem Statement
Check if string is palindrome using recursion.

#### Learning Objectives
- Two-end recursive comparison
- Index management in recursion

#### Hints
1. Compare first and last characters
2. Recursively check substring without first and last

---

### Assignment 57: Print All Subsequences
**Difficulty**: ★★☆☆☆ | **Time**: 25 mins | **Category**: Recursion - Enumeration

#### Problem Statement
Print all possible subsequences of a string.

**Constraints:**
- 1 ≤ len ≤ 15

#### Input/Output Format
- **Input**: String
- **Output**: All subsequences

#### Examples
```
Input: "abc"
Output: "", "a", "b", "c", "ab", "ac", "bc", "abc"
```

#### Learning Objectives
- Include/exclude pattern
- Backtracking introduction

#### Hints
1. For each character: include it or exclude it
2. Total subsequences = 2^n

#### Test Cases
| Input | Output Count | Notes |
|-------|--------------|-------|
| "ab" | 4 | "", "a", "b", "ab" |
| "aaa" | 8 | Duplicates possible |

---

### Assignment 58: Tower of Hanoi
**Difficulty**: ★★☆☆☆ | **Time**: 25 mins | **Category**: Recursion - Classic

#### Problem Statement
Solve Tower of Hanoi for n disks. Print all moves.

**Constraints:**
- 1 ≤ n ≤ 20

#### Input/Output Format
- **Input**: n
- **Output**: Sequence of moves

#### Examples
```
Input: 2
Output:
Move disk 1 from A to B
Move disk 2 from A to C
Move disk 1 from B to C
```

#### Learning Objectives
- Classic recursive problem
- Breaking into subproblems

#### Hints
1. Move n-1 disks from source to auxiliary
2. Move largest disk from source to destination
3. Move n-1 disks from auxiliary to destination

#### Test Cases
| n | Number of Moves | Formula |
|---|-----------------|---------|
| 1 | 1 | 2^n - 1 |
| 3 | 7 | |
| 4 | 15 | |

---

### Assignment 59: Generate All Permutations
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Recursion - Backtracking

#### Problem Statement
Generate all permutations of a string.

**Constraints:**
- 1 ≤ len ≤ 8

#### Input/Output Format
- **Input**: String with unique characters
- **Output**: All permutations

#### Examples
```
Input: "abc"
Output: "abc", "acb", "bac", "bca", "cab", "cba"
```

#### Learning Objectives
- Backtracking pattern
- Swapping technique

#### Hints
1. Fix one character, recursively permute rest
2. Swap to place each character at each position

#### Test Cases
| Input | Output Count | Formula |
|-------|--------------|---------|
| "ab" | 2 | n! |
| "abc" | 6 | |

---

### Assignment 60: Binary Search Using Recursion
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Recursion - Searching

#### Problem Statement
Implement binary search recursively.

**Constraints:**
- Array is sorted

#### Input/Output Format
- **Input**: Sorted array, target
- **Output**: Index or -1

#### Examples
```
Input: [1, 2, 3, 4, 5], target=4
Output: 3
```

#### Learning Objectives
- Divide and conquer concept
- Recursive vs iterative binary search

#### Hints
1. Compare with middle element
2. Recurse on left or right half

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| Empty array | -1 | No elements |
| [1], target=1 | 0 | Single element |
---

# 🟡 INTERMEDIATE LEVEL
## Standard Algorithms and Problem-Solving Patterns (Assignments 61-120)

---

## Section G: Hash Tables and Maps (61-70)

---

### Assignment 61: Implement Hash Map
**Difficulty**: ★★★☆☆ | **Time**: 40 mins | **Category**: Hash Tables - Implementation

#### Problem Statement
Implement a hash map with put(key, value), get(key), remove(key) operations using chaining.

**Constraints:**
- Keys are strings, values are integers
- Handle collisions with chaining

#### Input/Output Format
- **Input**: Operations
- **Output**: Results of get operations

#### Examples
```
put("apple", 5), put("banana", 3), get("apple"), remove("apple"), get("apple")
Output: 5, -1
```

#### Learning Objectives
- Hash function design
- Collision resolution (chaining)
- Load factor concept

#### Hints
1. Use array of linked lists
2. Hash = sum of ASCII values % table_size (simple hash)
3. Search in chain for correct key

#### Test Cases
| Operations | Output | Edge Case |
|------------|--------|-----------|
| put then update | New value | Overwrite |
| get missing key | -1 | Not found |
| remove then get | -1 | Deleted key |

---

### Assignment 62: Two Sum
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Hash Tables - Application

#### Problem Statement
Find indices of two numbers that add up to target.

**Constraints:**
- Exactly one solution exists
- Cannot use same element twice

#### Input/Output Format
- **Input**: Array, target
- **Output**: Two indices

#### Examples
```
Input: [2, 7, 11, 15], target=9
Output: [0, 1]
```

#### Learning Objectives
- Complement lookup pattern
- Hash map for O(1) lookup

#### Hints
1. For each num, check if (target - num) exists in map
2. Store number → index mapping

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| [3,3], target=6 | [0,1] | Duplicates |
| [1,2,3], target=5 | [1,2] | End of array |

---

### Assignment 63: First Unique Character in String
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Hash Tables - Frequency

#### Problem Statement
Find index of first non-repeating character. Return -1 if none.

#### Input/Output Format
- **Input**: String
- **Output**: Index or -1

#### Examples
```
Input: "loveleetcode"
Output: 2 ('v' is first unique)
```

#### Learning Objectives
- Two-pass with hash map
- Order preservation

---

### Assignment 64: Group Anagrams
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Hash Tables - Grouping

#### Problem Statement
Group strings that are anagrams of each other.

**Constraints:**
- 1 ≤ n ≤ 10^4
- Lowercase letters only

#### Input/Output Format
- **Input**: Array of strings
- **Output**: Grouped anagrams

#### Examples
```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"]
Output: [["eat","tea","ate"], ["tan","nat"], ["bat"]]
```

#### Learning Objectives
- Sorted string as key
- Map of lists pattern

#### Hints
1. Sort each string → use as map key
2. Append original string to that key's list

---

### Assignment 65: Subarray Sum Equals K
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Hash Tables - Prefix Sum

#### Problem Statement
Count subarrays whose sum equals K.

**Constraints:**
- -10^9 ≤ nums[i] ≤ 10^9

#### Input/Output Format
- **Input**: Array, K
- **Output**: Count

#### Examples
```
Input: [1, 1, 1], k=2
Output: 2 ([1,1] at indices 0-1 and 1-2)
```

#### Learning Objectives
- Prefix sum technique
- Hash map for sum frequency

#### Hints
1. prefixSum[j] - prefixSum[i] = k means subarray [i+1...j] sums to k
2. Store frequency of each prefix sum

#### Test Cases
| Input | Output | Edge Case |
|-------|--------|-----------|
| [1,-1,0], k=0 | 3 | Zero sum |
| [1], k=0 | 0 | No valid |

---

### Assignment 66: Longest Consecutive Sequence
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Hash Tables - Sequences

#### Problem Statement
Find the length of longest consecutive elements sequence in O(n) time.

**Constraints:**
- 0 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: Unsorted array
- **Output**: Length of longest consecutive sequence

#### Examples
```
Input: [100, 4, 200, 1, 3, 2]
Output: 4 (sequence: 1,2,3,4)
```

#### Learning Objectives
- HashSet for O(1) lookup
- Starting point identification

#### Hints
1. Add all to HashSet
2. For each num, if num-1 not in set, it's a sequence start
3. Count consecutive numbers from each start

---

### Assignment 67: Contains Duplicate II
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Hash Tables - Window

#### Problem Statement
Check if array has duplicates within distance k.

**Constraints:**
- 1 ≤ n ≤ 10^5

#### Input/Output Format
- **Input**: Array, k
- **Output**: True/False

#### Examples
```
Input: [1,2,3,1], k=3
Output: True (indices 0 and 3)
```

#### Learning Objectives
- Sliding window with hash map
- Index tracking

#### Hints
1. Map value to its most recent index
2. Check if difference ≤ k

---

### Assignment 68: Valid Sudoku
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Hash Tables - Validation

#### Problem Statement
Check if a 9x9 Sudoku board is valid (no repeats in rows, columns, 3x3 boxes).

#### Input/Output Format
- **Input**: 9x9 board
- **Output**: True/False

#### Learning Objectives
- Multiple hash sets for validation
- 3x3 box index calculation

#### Hints
1. Use sets for each row, column, and box
2. Box index = (row/3)*3 + col/3

---

### Assignment 69: Intersection of Two Arrays II
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Hash Tables - Counting

#### Problem Statement
Find intersection including duplicates.

#### Examples
```
Input: [1,2,2,1], [2,2]
Output: [2,2]
```

#### Learning Objectives
- Frequency counting with maps
- Decrementing count pattern

---

### Assignment 70: Top K Frequent Elements
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Hash Tables + Sorting

#### Problem Statement
Return k most frequent elements.

**Constraints:**
- Answer is unique

#### Examples
```
Input: [1,1,1,2,2,3], k=2
Output: [1,2]
```

#### Learning Objectives
- Frequency counting
- Bucket sort or heap approach

#### Hints
1. Count frequencies with map
2. Use bucket sort: array of lists where index = frequency

---

## Section H: Binary Trees (71-82)

---

### Assignment 71: Binary Tree Node Implementation
**Difficulty**: ★☆☆☆☆ | **Time**: 15 mins | **Category**: Trees - Implementation

#### Problem Statement
Implement binary tree node with insert, and basic traversals structure.

#### Learning Objectives
- Node structure: data, left, right
- Root pointer management

---

### Assignment 72: Inorder Traversal (Recursive)
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Trees - Traversal

#### Problem Statement
Implement inorder traversal (Left → Root → Right).

#### Examples
```
    1
   / \
  2   3
Output: [2, 1, 3]
```

#### Learning Objectives
- Recursive tree traversal
- Visit order significance

---

### Assignment 73: Preorder Traversal (Recursive)
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Trees - Traversal

#### Problem Statement
Implement preorder traversal (Root → Left → Right).

#### Examples
```
    1
   / \
  2   3
Output: [1, 2, 3]
```

---

### Assignment 74: Postorder Traversal (Recursive)
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Trees - Traversal

#### Problem Statement
Implement postorder traversal (Left → Right → Root).

#### Examples
```
    1
   / \
  2   3
Output: [2, 3, 1]
```

---

### Assignment 75: Level Order Traversal (BFS)
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Trees - BFS

#### Problem Statement
Traverse tree level by level using BFS.

#### Examples
```
    3
   / \
  9  20
    /  \
   15   7
Output: [[3], [9,20], [15,7]]
```

#### Learning Objectives
- Queue-based BFS
- Level separation

#### Hints
1. Use queue, process level by level
2. Track level size before processing

---

### Assignment 76: Maximum Depth of Binary Tree
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Trees - DFS

#### Problem Statement
Find maximum depth (root to deepest leaf).

#### Examples
```
    3
   / \
  9  20
    /  \
   15   7
Output: 3
```

#### Learning Objectives
- Recursive depth calculation
- Max of subtrees + 1

#### Hints
1. Base: null → 0
2. Recursive: 1 + max(left_depth, right_depth)

---

### Assignment 77: Check if Tree is Balanced
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Trees - DFS

#### Problem Statement
Check if height difference between left and right subtrees is at most 1 for every node.

#### Learning Objectives
- Balanced tree definition
- Bottom-up computation

#### Hints
1. Return -1 to indicate unbalanced subtree
2. Check balance at each node

---

### Assignment 78: Same Tree
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Trees - Comparison

#### Problem Statement
Check if two binary trees are identical.

#### Learning Objectives
- Simultaneous traversal of two trees
- Structural and value comparison

---

### Assignment 79: Symmetric Tree
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Trees - Comparison

#### Problem Statement
Check if a tree is symmetric around its center.

#### Examples
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
Output: True
```

#### Learning Objectives
- Mirror comparison
- Modified simultaneous traversal

#### Hints
1. Compare left subtree with right subtree
2. Left.left with Right.right, Left.right with Right.left

---

### Assignment 80: Invert Binary Tree
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Trees - Modification

#### Problem Statement
Mirror/invert a binary tree.

#### Learning Objectives
- Recursive tree modification
- Swapping children

#### Hints
1. Swap left and right children
2. Recursively invert subtrees

---

### Assignment 81: Path Sum
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Trees - DFS

#### Problem Statement
Check if root-to-leaf path exists with given sum.

#### Learning Objectives
- Root-to-leaf path tracking
- Sum accumulation in DFS

#### Hints
1. Subtract current value from target
2. Check if leaf with remaining = 0

---

### Assignment 82: Count Complete Tree Nodes
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Trees - Complete Tree

#### Problem Statement
Count nodes in complete binary tree in O(log²n) time.

#### Learning Objectives
- Complete tree properties
- Binary search on last level

#### Hints
1. If left height = right height, it's perfect: 2^h - 1 nodes
2. Otherwise, recurse on subtrees

---

## Section I: Binary Search Trees (83-90)

---

### Assignment 83: BST Insert Operation
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: BST - Operations

#### Problem Statement
Insert a value into BST maintaining BST property.

#### Learning Objectives
- BST property: left < root < right
- Recursive insertion

#### Hints
1. Compare with root to decide direction
2. Insert at null position

---

### Assignment 84: BST Search Operation
**Difficulty**: ★★☆☆☆ | **Time**: 10 mins | **Category**: BST - Operations

#### Problem Statement
Search for a value in BST.

#### Learning Objectives
- Efficient O(log n) search in BST
- Comparison-based navigation

---

### Assignment 85: BST Minimum and Maximum
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: BST - Operations

#### Problem Statement
Find minimum and maximum values in BST.

#### Learning Objectives
- Leftmost = minimum
- Rightmost = maximum

---

### Assignment 86: Validate BST
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: BST - Validation

#### Problem Statement
Check if binary tree is a valid BST.

#### Learning Objectives
- Range-based validation
- Passing bounds in recursion

#### Hints
1. Track valid range (min, max) for each node
2. Update bounds as you descend

#### Common Mistakes
- Only comparing with parent (must check all ancestors)

---

### Assignment 87: BST Delete Operation
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: BST - Operations

#### Problem Statement
Delete a node from BST maintaining BST property.

#### Learning Objectives
- Three cases: leaf, one child, two children
- Inorder successor/predecessor

#### Hints
1. Leaf: simply remove
2. One child: replace with child
3. Two children: replace with inorder successor, delete successor

---

### Assignment 88: Kth Smallest Element in BST
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: BST - Traversal

#### Problem Statement
Find kth smallest element in BST.

#### Learning Objectives
- Inorder traversal gives sorted order
- Early termination

#### Hints
1. Inorder traversal with counter
2. Stop when counter reaches k

---

### Assignment 89: Lowest Common Ancestor in BST
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: BST - LCA

#### Problem Statement
Find LCA of two nodes in BST.

#### Learning Objectives
- BST property for LCA
- Split point identification

#### Hints
1. If both values < root, LCA is in left subtree
2. If both values > root, LCA is in right subtree
3. Otherwise, root is LCA

---

### Assignment 90: Convert Sorted Array to BST
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: BST - Construction

#### Problem Statement
Convert sorted array to height-balanced BST.

#### Learning Objectives
- Divide and conquer for tree construction
- Middle element as root

#### Hints
1. Middle element becomes root
2. Left half → left subtree, Right half → right subtree

---

## Section J: Heaps and Priority Queues (91-98)

---

### Assignment 91: Implement Min Heap
**Difficulty**: ★★★☆☆ | **Time**: 40 mins | **Category**: Heaps - Implementation

#### Problem Statement
Implement min heap with insert, extractMin, peek operations.

#### Learning Objectives
- Heap property: parent ≤ children
- Array representation
- Heapify up and down

#### Hints
1. Parent of i = (i-1)/2
2. Children of i = 2i+1 and 2i+2
3. Insert: add at end, heapify up
4. Extract: remove root, move last to root, heapify down

---

### Assignment 92: Implement Max Heap
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Heaps - Implementation

#### Problem Statement
Implement max heap with insert, extractMax operations.

#### Learning Objectives
- Max heap property
- Same structure, different comparison

---

### Assignment 93: Heap Sort
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Heaps - Sorting

#### Problem Statement
Sort array using heap sort algorithm.

#### Learning Objectives
- Build heap in O(n)
- Extract elements one by one

#### Hints
1. Build max heap
2. Swap root with last, reduce heap size, heapify root

---

### Assignment 94: Kth Largest Element in Array
**Difficulty**: ★★★☆☆ | **Time**: 20 mins | **Category**: Heaps - Application

#### Problem Statement
Find kth largest element.

#### Examples
```
Input: [3,2,1,5,6,4], k=2
Output: 5
```

#### Learning Objectives
- Min heap of size k
- Stream processing pattern

#### Hints
1. Maintain min heap of size k
2. Process all elements, top of heap is kth largest

---

### Assignment 95: Merge K Sorted Lists
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: Heaps - Merging

#### Problem Statement
Merge k sorted linked lists into one sorted list.

#### Learning Objectives
- Heap for efficient minimum selection
- Multi-way merge

#### Hints
1. Add first element of each list to min heap
2. Extract min, add next element from that list

---

### Assignment 96: Find Median from Data Stream
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Heaps - Two Heaps

#### Problem Statement
Design data structure that supports addNum() and findMedian().

#### Learning Objectives
- Two heaps technique
- Balancing heaps

#### Hints
1. Max heap for lower half, min heap for upper half
2. Balance sizes: differ by at most 1
3. Median = top of larger heap or average of tops

---

### Assignment 97: Last Stone Weight
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Heaps - Simulation

#### Problem Statement
Smash heaviest two stones repeatedly. Return weight of last stone.

#### Learning Objectives
- Max heap for repeated maximum retrieval
- Simulation with heap

---

### Assignment 98: Reorganize String
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Heaps - Greedy

#### Problem Statement
Rearrange string so no two adjacent chars are same. Return "" if impossible.

#### Examples
```
Input: "aab"
Output: "aba"
```

#### Learning Objectives
- Greedy with heap
- Character frequency prioritization

#### Hints
1. Use max heap based on frequency
2. Place most frequent, then second most frequent, alternate

---

## Section K: Advanced Sorting (99-105)

---

### Assignment 99: Merge Sort
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Sorting - Divide & Conquer

#### Problem Statement
Implement merge sort algorithm.

#### Learning Objectives
- Divide and conquer paradigm
- Merging sorted halves
- O(n log n) guaranteed

#### Hints
1. Divide array into two halves
2. Recursively sort each half
3. Merge sorted halves

---

### Assignment 100: Quick Sort
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: Sorting - Divide & Conquer

#### Problem Statement
Implement quick sort with Lomuto or Hoare partition.

#### Learning Objectives
- Partition scheme
- Pivot selection
- Average O(n log n), worst O(n²)

#### Hints
1. Choose pivot (last element for Lomuto)
2. Partition: elements < pivot left, > pivot right
3. Recursively sort partitions

---

### Assignment 101: Counting Sort
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Sorting - Linear

#### Problem Statement
Implement counting sort for integers in known range.

**Constraints:**
- 0 ≤ arr[i] ≤ k

#### Learning Objectives
- Non-comparison based sorting
- O(n + k) time complexity

---

### Assignment 102: Radix Sort
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Sorting - Linear

#### Problem Statement
Implement radix sort for non-negative integers.

#### Learning Objectives
- Digit-by-digit sorting
- Stable sort requirement

---

### Assignment 103: Count Inversions (Merge Sort)
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Sorting - Applications

#### Problem Statement
Count inversions in O(n log n) using modified merge sort.

#### Learning Objectives
- Merge sort modification
- Counting during merge

#### Hints
1. When element from right is smaller, count += remaining elements in left

---

### Assignment 104: Sort Colors (Three-Way Partition)
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Sorting - Partitioning

#### Problem Statement
Sort array of 0s, 1s, 2s in-place.

#### Learning Objectives
- Dutch National Flag (revisited from beginner)
- Three-way partitioning

---

### Assignment 105: Merge Intervals
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Sorting - Intervals

#### Problem Statement
Merge overlapping intervals.

#### Examples
```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
```

#### Learning Objectives
- Interval problems
- Sort then merge pattern

#### Hints
1. Sort by start time
2. Merge if current start ≤ previous end

---

## Section L: Dynamic Programming Basics (106-115)

---

### Assignment 106: Climbing Stairs
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: DP - Introduction

#### Problem Statement
Count ways to climb n stairs (1 or 2 steps at a time).

#### Examples
```
Input: n=3
Output: 3 (1+1+1, 1+2, 2+1)
```

#### Learning Objectives
- Overlapping subproblems
- Fibonacci-like recurrence
- Memoization vs tabulation

#### Hints
1. dp[i] = dp[i-1] + dp[i-2]
2. Base: dp[1]=1, dp[2]=2

---

### Assignment 107: House Robber
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: DP - Linear

#### Problem Statement
Maximum sum of non-adjacent elements.

#### Examples
```
Input: [2,7,9,3,1]
Output: 12 (2+9+1)
```

#### Learning Objectives
- Include/exclude pattern
- State definition

#### Hints
1. dp[i] = max(dp[i-1], dp[i-2] + nums[i])

---

### Assignment 108: Maximum Subarray (Kadane's Algorithm)
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: DP - Classic

#### Problem Statement
Find contiguous subarray with largest sum.

#### Examples
```
Input: [-2,1,-3,4,-1,2,1,-5,4]
Output: 6 ([4,-1,2,1])
```

#### Learning Objectives
- Kadane's algorithm
- Current vs global maximum

#### Hints
1. currentMax = max(nums[i], currentMax + nums[i])
2. Track globalMax

---

### Assignment 109: Coin Change
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Unbounded Knapsack

#### Problem Statement
Minimum coins needed to make amount.

#### Examples
```
Input: coins=[1,2,5], amount=11
Output: 3 (5+5+1)
```

#### Learning Objectives
- Unbounded knapsack pattern
- Minimization DP

#### Hints
1. dp[i] = min(dp[i], dp[i-coin] + 1) for each coin
2. Initialize with infinity

---

### Assignment 110: Coin Change II (Count Ways)
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Counting

#### Problem Statement
Count ways to make amount using coins.

#### Learning Objectives
- Counting vs minimization
- Order of loops matters

#### Hints
1. dp[i] += dp[i-coin]
2. Outer loop on coins to avoid duplicates

---

### Assignment 111: Longest Increasing Subsequence
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: DP - Subsequence

#### Problem Statement
Find length of longest strictly increasing subsequence.

#### Examples
```
Input: [10,9,2,5,3,7,101,18]
Output: 4 ([2,3,7,101])
```

#### Learning Objectives
- O(n²) DP solution
- O(n log n) binary search optimization (advanced)

#### Hints
1. dp[i] = longest ending at index i
2. dp[i] = max(dp[j] + 1) for all j < i where nums[j] < nums[i]

---

### Assignment 112: 0/1 Knapsack Problem
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: DP - Classic

#### Problem Statement
Maximum value with weight constraint, each item used once.

#### Learning Objectives
- 2D DP: items × capacity
- Include/exclude decision

#### Hints
1. dp[i][w] = max(dp[i-1][w], dp[i-1][w-wt[i]] + val[i])
2. Can optimize to 1D

---

### Assignment 113: Unique Paths
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: DP - Grid

#### Problem Statement
Count paths from top-left to bottom-right in m×n grid (only right/down moves).

#### Examples
```
Input: m=3, n=7
Output: 28
```

#### Learning Objectives
- Grid DP
- Path counting

#### Hints
1. dp[i][j] = dp[i-1][j] + dp[i][j-1]
2. Base: first row and column = 1

---

### Assignment 114: Minimum Path Sum
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: DP - Grid

#### Problem Statement
Find path with minimum sum from top-left to bottom-right.

#### Learning Objectives
- Grid DP for minimization
- In-place optimization

#### Hints
1. dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])

---

### Assignment 115: Word Break
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Strings

#### Problem Statement
Check if string can be segmented into dictionary words.

#### Examples
```
Input: s="leetcode", wordDict=["leet","code"]
Output: True
```

#### Learning Objectives
- String segmentation DP
- Substring checking

#### Hints
1. dp[i] = true if s[0...i-1] can be segmented
2. dp[i] = any dp[j] && s[j...i-1] in dict

---

## Section M: Graph Fundamentals (116-120)

---

### Assignment 116: Graph Representation
**Difficulty**: ★★☆☆☆ | **Time**: 25 mins | **Category**: Graphs - Basics

#### Problem Statement
Implement graph using adjacency list and adjacency matrix.

#### Learning Objectives
- Graph terminology: vertices, edges, directed/undirected
- Space-time tradeoffs

#### Hints
1. Adjacency list: array of lists
2. Adjacency matrix: 2D array

---

### Assignment 117: BFS on Graph
**Difficulty**: ★★☆☆☆ | **Time**: 25 mins | **Category**: Graphs - Traversal

#### Problem Statement
Implement Breadth-First Search from a source vertex.

#### Learning Objectives
- Level-order traversal on graphs
- Shortest path in unweighted graph

#### Hints
1. Use queue
2. Mark visited before adding to queue

---

### Assignment 118: DFS on Graph
**Difficulty**: ★★☆☆☆ | **Time**: 25 mins | **Category**: Graphs - Traversal

#### Problem Statement
Implement Depth-First Search (recursive and iterative).

#### Learning Objectives
- Deep exploration pattern
- Recursive vs stack-based

---

### Assignment 119: Detect Cycle in Undirected Graph
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Graphs - Cycle Detection

#### Problem Statement
Check if undirected graph contains a cycle.

#### Learning Objectives
- Parent tracking in DFS
- Cycle back to non-parent ancestor

#### Hints
1. If visited neighbor is not parent, cycle exists
2. Handle disconnected components

---

### Assignment 120: Number of Connected Components
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Graphs - Components

#### Problem Statement
Count connected components in undirected graph.

#### Learning Objectives
- DFS/BFS from each unvisited node
- Component counting

#### Hints
1. Increment count for each new DFS/BFS started
2. Mark all reachable as visited

---

# 🟠 ADVANCED LEVEL
## Complex Algorithms and Optimization Techniques (Assignments 121-180)

---

## Section N: Advanced Tree Structures (121-130)

---

### Assignment 121: AVL Tree Rotations
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Trees - Balanced

#### Problem Statement
Implement left rotation, right rotation, left-right, and right-left rotations for AVL trees.

#### Learning Objectives
- Balance factor concept (height difference)
- Four rotation types
- When each rotation is needed

#### Hints
1. Single rotations: LL case → right rotate, RR case → left rotate
2. Double rotations: LR → left then right, RL → right then left

---

### Assignment 122: AVL Tree Insert with Balancing
**Difficulty**: ★★★★☆ | **Time**: 50 mins | **Category**: Trees - Balanced

#### Problem Statement
Implement insert operation in AVL tree with automatic balancing.

#### Learning Objectives
- Height update after insertion
- Balance check and rotation trigger

#### Hints
1. Standard BST insert
2. Update heights going up
3. Check balance factor, rotate if needed

---

### Assignment 123: Red-Black Tree Properties Validator
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Trees - Balanced

#### Problem Statement
Validate if a given tree satisfies Red-Black tree properties.

#### Learning Objectives
- Red-Black tree properties
- Black height validation
- Red-red violation check

#### Properties to Check
1. Root is black
2. Red nodes have black children
3. All paths have same black height
4. Leaves (NIL) are black

---

### Assignment 124: Lowest Common Ancestor in Binary Tree
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Trees - LCA

#### Problem Statement
Find LCA of two nodes in general binary tree (not BST).

#### Learning Objectives
- Recursive LCA without BST property
- Post-order approach

#### Hints
1. If current node is p or q, return it
2. Recurse on left and right
3. If both subtrees return non-null, current is LCA

---

### Assignment 125: Serialize and Deserialize Binary Tree
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Trees - Serialization

#### Problem Statement
Convert binary tree to string and back.

#### Learning Objectives
- Tree encoding strategies
- Null marker handling

#### Hints
1. Preorder with null markers
2. Use delimiter between values

---

### Assignment 126: Binary Tree Maximum Path Sum
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Trees - DP on Trees

#### Problem Statement
Find maximum sum path (any node to any node).

#### Examples
```
    -10
   /   \
  9    20
      /  \
     15   7
Output: 42 (15 + 20 + 7)
```

#### Learning Objectives
- DP on trees
- Path through node vs from node

#### Hints
1. For each node, calculate max single path going down
2. Update global max with path through current node

---

### Assignment 127: Vertical Order Traversal
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: Trees - Traversal Variants

#### Problem Statement
Print nodes in vertical order (column by column).

#### Learning Objectives
- Horizontal distance concept
- Map-based grouping

---

### Assignment 128: Construct Tree from Inorder and Preorder
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: Trees - Construction

#### Problem Statement
Build binary tree from inorder and preorder traversals.

#### Learning Objectives
- Root identification from preorder
- Subtree partition from inorder

#### Hints
1. First element of preorder is root
2. Find root in inorder → left of it is left subtree

---

### Assignment 129: Diameter of Binary Tree
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Trees - DFS

#### Problem Statement
Find diameter (longest path between any two nodes).

#### Learning Objectives
- Diameter may not pass through root
- Height calculation with side effect

#### Hints
1. Diameter at node = left_height + right_height
2. Track maximum diameter as you go

---

### Assignment 130: All Nodes at Distance K
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Trees - BFS/DFS

#### Problem Statement
Find all nodes at distance K from a target node.

#### Learning Objectives
- Bidirectional tree traversal
- Parent pointers or graph conversion

#### Hints
1. Add parent pointers to nodes OR
2. Convert tree to undirected graph, BFS from target

---

## Section O: Segment Trees and Range Queries (131-138)

---

### Assignment 131: Segment Tree Build (Sum)
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Segment Trees - Basics

#### Problem Statement
Build a segment tree for range sum queries.

#### Learning Objectives
- Segment tree structure
- Tree array representation
- Build O(n) complexity

#### Hints
1. Leaf nodes = array elements
2. Internal node = sum of children
3. Size of tree array = 4 * n (safe)

---

### Assignment 132: Segment Tree Point Update
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Segment Trees - Update

#### Problem Statement
Update a single element and propagate changes.

#### Learning Objectives
- O(log n) update
- Traversing to correct leaf

---

### Assignment 133: Segment Tree Range Query
**Difficulty**: ★★★★☆ | **Time**: 30 mins | **Category**: Segment Trees - Query

#### Problem Statement
Query sum of a range [l, r].

#### Learning Objectives
- Range decomposition
- Three cases: total overlap, no overlap, partial

---

### Assignment 134: Segment Tree for Range Minimum Query
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Segment Trees - Variants

#### Problem Statement
Build segment tree for minimum queries.

#### Learning Objectives
- Changing merge operation
- Min instead of sum

---

### Assignment 135: Lazy Propagation Introduction
**Difficulty**: ★★★★★ | **Time**: 50 mins | **Category**: Segment Trees - Advanced

#### Problem Statement
Implement range update with lazy propagation for addition.

#### Learning Objectives
- Lazy array for deferred updates
- Push down before query
- O(log n) range update

#### Hints
1. Store pending updates in lazy array
2. Push lazy value to children when visiting node
3. Update lazy value instead of all leaves

---

### Assignment 136: Range Update Range Query
**Difficulty**: ★★★★★ | **Time**: 55 mins | **Category**: Segment Trees - Advanced

#### Problem Statement
Support both range updates and range queries efficiently.

#### Learning Objectives
- Combining lazy propagation with queries
- Consistency maintenance

---

### Assignment 137: Fenwick Tree (Binary Indexed Tree) - Basics
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: BIT - Basics

#### Problem Statement
Implement Fenwick Tree for prefix sum and point update.

#### Learning Objectives
- BIT structure using bit manipulation
- LSB trick: i & (-i)
- O(log n) update and query

#### Hints
1. Update: add value, move to parent (i += i & (-i))
2. Query: sum from index, move to predecessor (i -= i & (-i))

---

### Assignment 138: Count Inversions using BIT
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: BIT - Applications

#### Problem Statement
Count inversions in O(n log n) using Fenwick Tree.

#### Learning Objectives
- BIT for counting
- Coordinate compression

#### Hints
1. Process from right to left
2. For each element, query count of smaller elements seen

---

## Section P: Advanced Dynamic Programming (139-153)

---

### Assignment 139: Longest Common Subsequence
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Strings

#### Problem Statement
Find length of LCS of two strings.

#### Examples
```
Input: "abcde", "ace"
Output: 3 ("ace")
```

#### Learning Objectives
- 2D DP on strings
- Match/mismatch recurrence

#### Hints
1. dp[i][j] = LCS of s1[0..i-1] and s2[0..j-1]
2. If match: dp[i-1][j-1] + 1, else max(dp[i-1][j], dp[i][j-1])

---

### Assignment 140: Edit Distance
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: DP - Strings

#### Problem Statement
Minimum operations (insert, delete, replace) to convert string A to B.

#### Learning Objectives
- Classic DP problem
- Three operations choice

#### Hints
1. If chars match: dp[i-1][j-1]
2. Else: 1 + min(insert, delete, replace costs)

---

### Assignment 141: Longest Palindromic Subsequence
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Strings

#### Problem Statement
Find length of longest palindromic subsequence.

#### Learning Objectives
- DP on single string
- Interval DP concept

#### Hints
1. LPS of string = LCS of string and its reverse
2. Or: dp[i][j] = LPS of s[i..j]

---

### Assignment 142: Palindrome Partitioning (Min Cuts)
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: DP - Partitioning

#### Problem Statement
Minimum cuts to partition string into palindromes.

#### Learning Objectives
- DP with preprocessing
- Cut optimization

#### Hints
1. Precompute isPalin[i][j]
2. dp[i] = min cuts for s[0..i]

---

### Assignment 143: Matrix Chain Multiplication
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: DP - Interval

#### Problem Statement
Minimum scalar multiplications to multiply chain of matrices.

#### Learning Objectives
- Interval DP classic
- Parenthesization problem

#### Hints
1. dp[i][j] = min cost to multiply matrices i to j
2. Try all split points k

---

### Assignment 144: Egg Drop Problem
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: DP - Decision Making

#### Problem Statement
Minimum trials to find critical floor with k eggs and n floors.

#### Learning Objectives
- Worst case optimization
- Binary search optimization

#### Hints
1. dp[eggs][floors] = min trials
2. Try dropping from each floor, take max of break/not break, minimize

---

### Assignment 145: Subset Sum Problem
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: DP - Subsets

#### Problem Statement
Check if subset exists with given sum.

#### Learning Objectives
- Boolean DP
- 0/1 Knapsack variant

---

### Assignment 146: Partition Equal Subset Sum
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Partitioning

#### Problem Statement
Check if array can be partitioned into two subsets with equal sum.

#### Learning Objectives
- Reduction to subset sum
- Sum/2 target

---

### Assignment 147: Target Sum (Ways to Make Target)
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Counting

#### Problem Statement
Count ways to assign + and - to make target sum.

#### Learning Objectives
- DP with offset for negative indices
- State representation

---

### Assignment 148: Longest Increasing Path in Matrix
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: DP - Grids

#### Problem Statement
Find longest strictly increasing path in matrix (4-directional moves).

#### Learning Objectives
- DFS with memoization on grid
- Topological order implicitly

---

### Assignment 149: Maximal Square
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Grids

#### Problem Statement
Find largest square containing only 1s in binary matrix.

#### Learning Objectives
- Grid DP for area maximization
- Elegant recurrence

#### Hints
1. dp[i][j] = side length of largest square with bottom-right at (i,j)
2. dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1 if matrix[i][j]=1

---

### Assignment 150: Rod Cutting Problem
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DP - Unbounded

#### Problem Statement
Maximum revenue from cutting rod into pieces with given prices.

#### Learning Objectives
- Unbounded knapsack pattern
- Length as capacity

---

### Assignment 151: Count Distinct Subsequences
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: DP - Counting

#### Problem Statement
Count distinct subsequences of T in S.

#### Learning Objectives
- Subsequence matching DP
- Counting paths

---

### Assignment 152: Burst Balloons
**Difficulty**: ★★★★★ | **Time**: 50 mins | **Category**: DP - Interval

#### Problem Statement
Maximum coins from bursting all balloons.

#### Learning Objectives
- Reverse thinking (last to first)
- Interval DP

#### Hints
1. Think: which balloon to burst LAST in range [i,j]
2. dp[i][j] = max coins from balloons i to j

---

### Assignment 153: Shortest Common Supersequence
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: DP - Strings

#### Problem Statement
Find shortest string that has both strings as subsequences.

#### Learning Objectives
- Inverse of LCS
- String reconstruction

#### Hints
1. SCS length = len(s1) + len(s2) - LCS length
2. Reconstruct by backtracking through LCS

---

## Section Q: Graph Algorithms (154-165)

---

### Assignment 154: Detect Cycle in Directed Graph
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Graphs - Cycles

#### Problem Statement
Check if directed graph has a cycle.

#### Learning Objectives
- Three-color DFS (white, gray, black)
- Back edge detection

#### Hints
1. Gray = currently in DFS stack
2. Edge to gray node = cycle

---

### Assignment 155: Topological Sort (Kahn's Algorithm)
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Graphs - DAG

#### Problem Statement
Find topological ordering using BFS (Kahn's algorithm).

#### Learning Objectives
- In-degree based approach
- Cycle detection integration

---

### Assignment 156: Topological Sort (DFS)
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Graphs - DAG

#### Problem Statement
Find topological ordering using DFS.

#### Learning Objectives
- Stack-based ordering
- Finish time ordering

---

### Assignment 157: Course Schedule
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Graphs - Application

#### Problem Statement
Check if courses can be completed given prerequisites.

#### Learning Objectives
- Cycle detection in prerequisite graph
- Topological sort applicability

---

### Assignment 158: Dijkstra's Algorithm
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Graphs - Shortest Path

#### Problem Statement
Find shortest paths from source to all vertices (positive weights).

#### Learning Objectives
- Priority queue based implementation
- Relaxation concept

#### Hints
1. Use min heap with (distance, vertex)
2. Skip if vertex already finalized

---

### Assignment 159: Bellman-Ford Algorithm
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Graphs - Shortest Path

#### Problem Statement
Find shortest paths (handles negative weights). Detect negative cycles.

#### Learning Objectives
- Edge relaxation V-1 times
- Negative cycle detection in Vth iteration

---

### Assignment 160: Floyd-Warshall Algorithm
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Graphs - All Pairs

#### Problem Statement
Find shortest paths between all pairs of vertices.

#### Learning Objectives
- DP approach for all-pairs shortest path
- O(V³) complexity

---

### Assignment 161: Minimum Spanning Tree - Prim's Algorithm
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Graphs - MST

#### Problem Statement
Find MST using Prim's algorithm.

#### Learning Objectives
- Greedy MST construction
- Priority queue for edge selection

---

### Assignment 162: Minimum Spanning Tree - Kruskal's Algorithm
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Graphs - MST

#### Problem Statement
Find MST using Kruskal's algorithm with Union-Find.

#### Learning Objectives
- Sort edges by weight
- Union-Find for cycle detection

---

### Assignment 163: Strongly Connected Components (Kosaraju's)
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Graphs - Components

#### Problem Statement
Find all strongly connected components in directed graph.

#### Learning Objectives
- Two-pass DFS algorithm
- Transpose graph concept

---

### Assignment 164: Bridges in Graph
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Graphs - Cuts

#### Problem Statement
Find all bridge edges (removal disconnects graph).

#### Learning Objectives
- Tarjan's algorithm
- Discovery and low values

---

### Assignment 165: Articulation Points
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Graphs - Cuts

#### Problem Statement
Find all articulation points (removal disconnects graph).

#### Learning Objectives
- DFS with discovery/low time
- Root handling (multiple children)

---

## Section R: String Algorithms (166-173)

---

### Assignment 166: KMP Pattern Matching
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Strings - Pattern Matching

#### Problem Statement
Find all occurrences of pattern in text using KMP algorithm.

#### Learning Objectives
- Failure function (LPS array)
- O(n+m) matching

#### Hints
1. Build LPS: longest proper prefix which is also suffix
2. On mismatch, use LPS to avoid re-checking

---

### Assignment 167: Rabin-Karp Algorithm
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Strings - Pattern Matching

#### Problem Statement
Find pattern using rolling hash.

#### Learning Objectives
- Polynomial hashing
- Rolling hash technique
- Spurious hit handling

---

### Assignment 168: Z-Algorithm
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Strings - Pattern Matching

#### Problem Statement
Compute Z-array and find pattern occurrences.

#### Learning Objectives
- Z-array: length of longest substring starting from i matching prefix
- O(n) construction

---

### Assignment 169: Longest Palindromic Substring
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Strings - Palindromes

#### Problem Statement
Find longest palindromic substring.

#### Learning Objectives
- Expand around center approach
- O(n²) vs O(n) Manacher's

#### Hints
1. Try each position (and gap) as center
2. Expand while characters match

---

### Assignment 170: Implement Trie
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: Tries - Implementation

#### Problem Statement
Implement Trie with insert, search, startsWith operations.

#### Learning Objectives
- Trie node structure
- Prefix-based operations

---

### Assignment 171: Trie - Word Search II
**Difficulty**: ★★★★☆ | **Time**: 50 mins | **Category**: Tries - Application

#### Problem Statement
Find all words from dictionary in a board using DFS + Trie.

#### Learning Objectives
- Trie for efficient prefix checking
- Backtracking on grid with Trie

---

### Assignment 172: Longest Common Prefix using Trie
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Tries - Application

#### Problem Statement
Find longest common prefix among words using Trie.

#### Learning Objectives
- Trie for common prefix
- Walk until branching or word end

---

### Assignment 173: Regular Expression Matching
**Difficulty**: ★★★★★ | **Time**: 50 mins | **Category**: Strings - DP

#### Problem Statement
Implement regex matching with '.' and '*'.

#### Learning Objectives
- Complex DP state
- Handling * for zero or more matches

---

## Section S: Backtracking (174-180)

---

### Assignment 174: N-Queens Problem
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Backtracking - Classic

#### Problem Statement
Place N queens on N×N board such that no two attack each other.

#### Learning Objectives
- Constraint-based search
- Efficient attack checking

#### Hints
1. Place row by row
2. Check column and diagonals using sets or arrays

---

### Assignment 175: Sudoku Solver
**Difficulty**: ★★★★☆ | **Time**: 50 mins | **Category**: Backtracking - Grid

#### Problem Statement
Solve a given Sudoku puzzle.

#### Learning Objectives
- Cell-by-cell filling
- Constraint validation

---

### Assignment 176: Word Search in Grid
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Backtracking - Grid

#### Problem Statement
Check if word exists in grid (adjacent cells, no reuse).

#### Learning Objectives
- DFS backtracking on grid
- Visited state management

---

### Assignment 177: Combination Sum
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Backtracking - Combinations

#### Problem Statement
Find all unique combinations that sum to target (can reuse elements).

#### Learning Objectives
- Unbounded combination generation
- Avoiding duplicates

---

### Assignment 178: Subsets II (with Duplicates)
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Backtracking - Subsets

#### Problem Statement
Generate all subsets when input has duplicates.

#### Learning Objectives
- Handling duplicates
- Skip consecutive equal elements at same level

---

### Assignment 179: Permutations II (with Duplicates)
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Backtracking - Permutations

#### Problem Statement
Generate all unique permutations when input has duplicates.

#### Learning Objectives
- Swap-based with duplicate handling
- Used array approach

---

### Assignment 180: Hamiltonian Path
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Backtracking - Graphs

#### Problem Statement
Find a Hamiltonian path if one exists.

#### Learning Objectives
- Graph backtracking
- Visiting all nodes exactly once

---

# 🔴 EXPERT LEVEL
## Competitive Programming and System Design Problems (Assignments 181-240+)

---

## Section T: Union-Find (Disjoint Set Union) (181-188)

---

### Assignment 181: Basic Union-Find Implementation
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DSU - Basics

#### Problem Statement
Implement Union-Find with find() and union() operations.

#### Learning Objectives
- Parent array representation
- Find with path compression
- Union by rank/size

#### Hints
1. find(x): if parent[x] != x, parent[x] = find(parent[x])
2. union(x,y): attach smaller tree under larger

---

### Assignment 182: Union by Rank
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: DSU - Optimization

#### Problem Statement
Implement union by rank to keep trees balanced.

#### Learning Objectives
- Rank vs Size
- Amortized O(α(n)) complexity

---

### Assignment 183: Path Compression
**Difficulty**: ★★★☆☆ | **Time**: 20 mins | **Category**: DSU - Optimization

#### Problem Statement
Implement path compression in find operation.

#### Learning Objectives
- Flattening tree during find
- Combined with union by rank

---

### Assignment 184: Number of Islands using DSU
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: DSU - Applications

#### Problem Statement
Count islands in grid using Union-Find instead of DFS.

#### Learning Objectives
- 2D to 1D index mapping
- Alternative to DFS/BFS

---

### Assignment 185: Redundant Connection
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: DSU - Cycle Detection

#### Problem Statement
Find the edge that creates a cycle in an undirected graph.

#### Learning Objectives
- DSU for cycle detection
- Return first cycle-forming edge

---

### Assignment 186: Accounts Merge
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: DSU - Applications

#### Problem Statement
Merge accounts that share common emails.

#### Learning Objectives
- DSU for grouping
- String-based union-find

---

### Assignment 187: Number of Provinces
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: DSU - Components

#### Problem Statement
Count connected components using Union-Find.

#### Learning Objectives
- Component counting with DSU
- Final roots count

---

### Assignment 188: Making a Large Island
**Difficulty**: ★★★★★ | **Time**: 50 mins | **Category**: DSU - Advanced

#### Problem Statement
Flip one 0 to 1 to maximize island size.

#### Learning Objectives
- Precompute island sizes with DSU
- Check adjacent islands for each 0

---

## Section U: Bit Manipulation Advanced (189-196)

---

### Assignment 189: Count Set Bits (Kernighan's Algorithm)
**Difficulty**: ★★☆☆☆ | **Time**: 15 mins | **Category**: Bits - Counting

#### Problem Statement
Count set bits in O(number of set bits).

#### Learning Objectives
- n & (n-1) removes rightmost set bit
- Brian Kernighan's algorithm

---

### Assignment 190: Power of Two Check
**Difficulty**: ★☆☆☆☆ | **Time**: 10 mins | **Category**: Bits - Properties

#### Problem Statement
Check if number is power of 2 using bit manipulation.

#### Learning Objectives
- Single bit set property
- n & (n-1) == 0 for power of 2

---

### Assignment 191: Single Number II (Every Element Thrice)
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Bits - Advanced

#### Problem Statement
Every element appears 3 times except one. Find it.

#### Learning Objectives
- Bit counting modulo 3
- Generalized XOR approach

---

### Assignment 192: Single Number III (Two Unique)
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Bits - Advanced

#### Problem Statement
Two elements appear once, others twice. Find both.

#### Learning Objectives
- XOR gives a⊕b
- Partitioning by rightmost set bit

---

### Assignment 193: Maximum XOR of Two Numbers
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Bits - Trie

#### Problem Statement
Find maximum XOR of any two numbers in array.

#### Learning Objectives
- Binary Trie for XOR
- Greedy bit selection

---

### Assignment 194: Divide Two Integers without Division
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Bits - Arithmetic

#### Problem Statement
Divide without using /, *, or %.

#### Learning Objectives
- Bit shifting for division
- Subtraction-based approach

---

### Assignment 195: Reverse Bits
**Difficulty**: ★★☆☆☆ | **Time**: 20 mins | **Category**: Bits - Manipulation

#### Problem Statement
Reverse all 32 bits of a number.

#### Learning Objectives
- Bit extraction and placement
- Shift and OR

---

### Assignment 196: Bitwise AND of Range
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Bits - Range

#### Problem Statement
Find bitwise AND of all numbers in range [m, n].

#### Learning Objectives
- Common prefix concept
- Right shift until equal

---

## Section V: Computational Geometry (197-206)

---

### Assignment 197: Line Intersection
**Difficulty**: ★★★☆☆ | **Time**: 30 mins | **Category**: Geometry - Basics

#### Problem Statement
Check if two line segments intersect.

#### Learning Objectives
- Cross product for orientation
- Collinear overlap handling

---

### Assignment 198: Point in Polygon
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: Geometry - Point Location

#### Problem Statement
Check if a point lies inside a polygon.

#### Learning Objectives
- Ray casting algorithm
- Winding number method

---

### Assignment 199: Convex Hull (Graham Scan)
**Difficulty**: ★★★★☆ | **Time**: 50 mins | **Category**: Geometry - Hull

#### Problem Statement
Find convex hull of a set of points.

#### Learning Objectives
- Sorting by polar angle
- Stack-based construction

---

### Assignment 200: Convex Hull (Jarvis March)
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Geometry - Hull

#### Problem Statement
Find convex hull using gift wrapping method.

#### Learning Objectives
- Leftmost point start
- O(nh) complexity

---

### Assignment 201: Closest Pair of Points
**Difficulty**: ★★★★★ | **Time**: 60 mins | **Category**: Geometry - Divide & Conquer

#### Problem Statement
Find closest pair in O(n log n) time.

#### Learning Objectives
- Divide and conquer approach
- Strip optimization

---

### Assignment 202: Area of Polygon
**Difficulty**: ★★★☆☆ | **Time**: 25 mins | **Category**: Geometry - Area

#### Problem Statement
Calculate area of simple polygon given vertices.

#### Learning Objectives
- Shoelace formula
- Cross product sum

---

### Assignment 203: Circle-Line Intersection
**Difficulty**: ★★★☆☆ | **Time**: 35 mins | **Category**: Geometry - Intersection

#### Problem Statement
Find intersection points of circle and line.

#### Learning Objectives
- Quadratic equation solving
- Discriminant for intersection count

---

### Assignment 204: Rotating Calipers (Diameter of Polygon)
**Difficulty**: ★★★★★ | **Time**: 55 mins | **Category**: Geometry - Advanced

#### Problem Statement
Find diameter of convex polygon (farthest pair).

#### Learning Objectives
- Rotating calipers technique
- Antipodal pairs

---

### Assignment 205: Minimum Enclosing Circle
**Difficulty**: ★★★★★ | **Time**: 55 mins | **Category**: Geometry - Optimization

#### Problem Statement
Find smallest circle enclosing all points.

#### Learning Objectives
- Welzl's algorithm
- Randomized approach

---

### Assignment 206: Sweep Line Algorithm
**Difficulty**: ★★★★☆ | **Time**: 50 mins | **Category**: Geometry - Sweep

#### Problem Statement
Find all intersection points among n line segments.

#### Learning Objectives
- Event-based processing
- Active set maintenance

---

## Section W: Advanced Data Structures (207-218)

---

### Assignment 207: B-Tree Implementation
**Difficulty**: ★★★★★ | **Time**: 90 mins | **Category**: Trees - B-Tree

#### Problem Statement
Implement B-Tree with insert, search, and split operations.

#### Learning Objectives
- Multi-way search tree
- Node splitting on overflow
- Disk-efficient structure

---

### Assignment 208: Skip List Implementation
**Difficulty**: ★★★★☆ | **Time**: 60 mins | **Category**: Lists - Skip List

#### Problem Statement
Implement Skip List with insert, search, delete.

#### Learning Objectives
- Probabilistic data structure
- Multi-level linked list
- Expected O(log n) operations

---

### Assignment 209: Persistent Segment Tree
**Difficulty**: ★★★★★ | **Time**: 70 mins | **Category**: Segment Trees - Persistence

#### Problem Statement
Implement segment tree that preserves all versions.

#### Learning Objectives
- Path copying technique
- Version array
- O(log n) per update/query

---

### Assignment 210: Suffix Array Construction
**Difficulty**: ★★★★★ | **Time**: 60 mins | **Category**: Strings - Suffix Structures

#### Problem Statement
Build suffix array in O(n log n) time.

#### Learning Objectives
- Doubling technique
- Rank-based sorting

---

### Assignment 211: LCP Array from Suffix Array
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Strings - Suffix Structures

#### Problem Statement
Build LCP array in O(n) using Kasai's algorithm.

#### Learning Objectives
- LCP relationship with sorted suffixes
- Linear time construction

---

### Assignment 212: Suffix Tree (Ukkonen's Algorithm)
**Difficulty**: ★★★★★ | **Time**: 90 mins | **Category**: Strings - Suffix Structures

#### Problem Statement
Build suffix tree using Ukkonen's online algorithm.

#### Learning Objectives
- Implicit to explicit suffix tree
- Suffix links
- O(n) construction

---

### Assignment 213: Heavy-Light Decomposition
**Difficulty**: ★★★★★ | **Time**: 75 mins | **Category**: Trees - Path Queries

#### Problem Statement
Implement HLD for path queries on trees.

#### Learning Objectives
- Tree decomposition into chains
- Combining with segment tree
- O(log²n) path queries

---

### Assignment 214: Centroid Decomposition
**Difficulty**: ★★★★★ | **Time**: 60 mins | **Category**: Trees - Decomposition

#### Problem Statement
Implement centroid decomposition for tree queries.

#### Learning Objectives
- Centroid finding
- Divide and conquer on trees
- O(n log n) preprocessing

---

### Assignment 215: LCA with Binary Lifting
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Trees - LCA

#### Problem Statement
Answer LCA queries in O(log n) after O(n log n) preprocessing.

#### Learning Objectives
- Sparse table for ancestors
- 2^k jumping technique

---

### Assignment 216: LCA with Euler Tour + RMQ
**Difficulty**: ★★★★☆ | **Time**: 50 mins | **Category**: Trees - LCA

#### Problem Statement
Answer LCA queries using Euler tour and Range Minimum Query.

#### Learning Objectives
- Euler tour linearization
- Reduction to RMQ

---

### Assignment 217: Sparse Table for RMQ
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Range Queries - Static

#### Problem Statement
Build sparse table for O(1) range minimum queries.

#### Learning Objectives
- O(n log n) preprocessing
- Overlapping subarray technique

---

### Assignment 218: Sqrt Decomposition
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Range Queries - Decomposition

#### Problem Statement
Implement sqrt decomposition for range queries.

#### Learning Objectives
- Block division concept
- O(√n) query time
- Balance between preprocessing and query

---

## Section X: Network Flow and Matching (219-225)

---

### Assignment 219: Ford-Fulkerson Algorithm
**Difficulty**: ★★★★★ | **Time**: 60 mins | **Category**: Graphs - Flow

#### Problem Statement
Implement Ford-Fulkerson for maximum flow using DFS.

#### Learning Objectives
- Augmenting paths
- Residual graph
- Max flow min cut theorem

---

### Assignment 220: Edmonds-Karp Algorithm
**Difficulty**: ★★★★★ | **Time**: 55 mins | **Category**: Graphs - Flow

#### Problem Statement
Implement BFS-based Ford-Fulkerson for O(VE²) complexity.

#### Learning Objectives
- Shortest augmenting path
- Polynomial time guarantee

---

### Assignment 221: Dinic's Algorithm
**Difficulty**: ★★★★★ | **Time**: 70 mins | **Category**: Graphs - Flow

#### Problem Statement
Implement Dinic's algorithm for O(V²E) maximum flow.

#### Learning Objectives
- Level graph construction
- Blocking flow concept

---

### Assignment 222: Bipartite Matching
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Graphs - Matching

#### Problem Statement
Find maximum matching in bipartite graph.

#### Learning Objectives
- Augmenting path in bipartite
- Hungarian algorithm variant

---

### Assignment 223: Min Cost Max Flow
**Difficulty**: ★★★★★ | **Time**: 75 mins | **Category**: Graphs - Flow

#### Problem Statement
Find maximum flow with minimum cost.

#### Learning Objectives
- Cost on edges
- Shortest path for augmentation

---

### Assignment 224: Assignment Problem
**Difficulty**: ★★★★★ | **Time**: 60 mins | **Category**: Matching - Optimization

#### Problem Statement
Minimum cost assignment of n workers to n jobs.

#### Learning Objectives
- Hungarian algorithm
- Optimal matching

---

### Assignment 225: Maximum Bipartite Matching (Hopcroft-Karp)
**Difficulty**: ★★★★★ | **Time**: 65 mins | **Category**: Graphs - Matching

#### Problem Statement
O(√V × E) maximum bipartite matching.

#### Learning Objectives
- Phase-based augmentation
- BFS for shortest paths

---

## Section Y: Competitive Programming Problems (226-240)

---

### Assignment 226: Sliding Window Maximum
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Competitive - Deque

#### Problem Statement
Find maximum in each sliding window of size k.

#### Learning Objectives
- Monotonic deque
- O(n) solution

---

### Assignment 227: Trapping Rain Water
**Difficulty**: ★★★★☆ | **Time**: 30 mins | **Category**: Competitive - Two Pointers

#### Problem Statement
Calculate water trapped between bars.

#### Learning Objectives
- Precompute left and right max
- Two pointer optimization

---

### Assignment 228: LRU Cache
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Design - Cache

#### Problem Statement
Implement LRU Cache with O(1) get and put.

#### Learning Objectives
- Doubly linked list + hash map
- Order maintenance

---

### Assignment 229: LFU Cache
**Difficulty**: ★★★★★ | **Time**: 55 mins | **Category**: Design - Cache

#### Problem Statement
Implement LFU Cache with O(1) operations.

#### Learning Objectives
- Frequency-based eviction
- Multiple linked lists

---

### Assignment 230: Design Twitter
**Difficulty**: ★★★★☆ | **Time**: 50 mins | **Category**: Design - System

#### Problem Statement
Design a simplified Twitter with postTweet, getNewsFeed, follow, unfollow.

#### Learning Objectives
- Merge K sorted lists for feed
- User relationship management

---

### Assignment 231: Skyline Problem
**Difficulty**: ★★★★★ | **Time**: 55 mins | **Category**: Competitive - Sweep

#### Problem Statement
Compute building skyline from rectangles.

#### Learning Objectives
- Event-based sweep
- Max heap for active heights

---

### Assignment 232: Median of Two Sorted Arrays
**Difficulty**: ★★★★★ | **Time**: 45 mins | **Category**: Competitive - Binary Search

#### Problem Statement
Find median of two sorted arrays in O(log(m+n)).

#### Learning Objectives
- Binary search on partition
- Handling edge cases

---

### Assignment 233: Regular Expression Matching with Wildcard
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Competitive - DP

#### Problem Statement
Implement matching with '?' and '*' (wildcard).

#### Learning Objectives
- Different from regex *
- DP state transitions

---

### Assignment 234: Longest Valid Parentheses
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Competitive - Stack/DP

#### Problem Statement
Find length of longest valid parentheses substring.

#### Learning Objectives
- Stack-based solution
- DP alternative

---

### Assignment 235: Candy Distribution
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Competitive - Greedy

#### Problem Statement
Minimum candies to give n children with rating constraints.

#### Learning Objectives
- Two-pass greedy
- Left-right sweep

---

### Assignment 236: First Missing Positive
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Competitive - Arrays

#### Problem Statement
Find first missing positive integer in O(n) time, O(1) space.

#### Learning Objectives
- Index as hash
- Cyclic sort concept

---

### Assignment 237: Count of Range Sum
**Difficulty**: ★★★★★ | **Time**: 55 mins | **Category**: Competitive - Merge Sort

#### Problem Statement
Count range sums that lie in [lower, upper].

#### Learning Objectives
- Merge sort with counting
- Prefix sum transformation

---

### Assignment 238: Reverse Pairs
**Difficulty**: ★★★★★ | **Time**: 50 mins | **Category**: Competitive - Merge Sort

#### Problem Statement
Count pairs where i < j and nums[i] > 2*nums[j].

#### Learning Objectives
- Modified merge sort
- Two-pointer during merge

---

### Assignment 239: Russian Doll Envelopes
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Competitive - LIS

#### Problem Statement
Maximum envelopes that can be nested.

#### Learning Objectives
- Sort + LIS
- 2D to 1D reduction

---

### Assignment 240: Maximal Rectangle
**Difficulty**: ★★★★★ | **Time**: 50 mins | **Category**: Competitive - Stack

#### Problem Statement
Find largest rectangle containing only 1s in binary matrix.

#### Learning Objectives
- Histogram per row
- Largest rectangle in histogram

---

## Section Z: Additional Expert Problems (241-250)

---

### Assignment 241: Longest Substring with At Most K Distinct Characters
**Difficulty**: ★★★★☆ | **Time**: 30 mins | **Category**: Sliding Window

#### Problem Statement
Find longest substring with at most K distinct characters.

#### Learning Objectives
- Variable size sliding window
- Frequency map with window

---

### Assignment 242: Alien Dictionary
**Difficulty**: ★★★★☆ | **Time**: 45 mins | **Category**: Graphs - Topological

#### Problem Statement
Derive character ordering from sorted alien dictionary.

#### Learning Objectives
- Graph construction from constraints
- Topological sort for ordering

---

### Assignment 243: Word Ladder II
**Difficulty**: ★★★★★ | **Time**: 60 mins | **Category**: Graphs - BFS

#### Problem Statement
Find all shortest transformation sequences.

#### Learning Objectives
- BFS for shortest path
- DFS for path reconstruction

---

### Assignment 244: Number of Ways to Arrive at Destination
**Difficulty**: ★★★★☆ | **Time**: 40 mins | **Category**: Graphs - Dijkstra

#### Problem Statement
Count paths with minimum travel time.

#### Learning Objectives
- Dijkstra with path counting
- Modular arithmetic

---

### Assignment 245: Minimum Cost to Hire K Workers
**Difficulty**: ★★★★★ | **Time**: 50 mins | **Category**: Greedy + Heap

#### Problem Statement
Hire K workers with minimum total cost based on quality and wage ratio.

#### Learning Objectives
- Sort by wage/quality ratio
- Max heap for quality selection

---

### Assignment 246: Split Array Largest Sum
**Difficulty**: ★★★★★ | **Time**: 45 mins | **Category**: Binary Search

#### Problem Statement
Split array into m subarrays to minimize largest sum.

#### Learning Objectives
- Binary search on answer
- Greedy validation

---

### Assignment 247: Kth Smallest in Sorted Matrix
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Heap/Binary Search

#### Problem Statement
Find kth smallest element in row-wise and column-wise sorted matrix.

#### Learning Objectives
- Min heap with pointers
- Binary search on value

---

### Assignment 248: Smallest Range Covering Elements from K Lists
**Difficulty**: ★★★★★ | **Time**: 50 mins | **Category**: Heap

#### Problem Statement
Find smallest range that includes at least one number from each list.

#### Learning Objectives
- K-way merge with tracking
- Min and max maintenance

---

### Assignment 249: Find K Pairs with Smallest Sums
**Difficulty**: ★★★★☆ | **Time**: 35 mins | **Category**: Heap

#### Problem Statement
Find k pairs with smallest sums from two sorted arrays.

#### Learning Objectives
- Min heap for pair selection
- Avoiding duplicates

---

### Assignment 250: Design Search Autocomplete System
**Difficulty**: ★★★★★ | **Time**: 70 mins | **Category**: Design - Trie

#### Problem Statement
Implement autocomplete with frequency-based suggestions.

#### Learning Objectives
- Trie for prefix storage
- Priority queue for top suggestions

---

# 📊 Curriculum Summary

| Level | Assignments | Key Topics |
|-------|-------------|------------|
| 🟢 Beginner | 1-60 | Arrays, Strings, Linked Lists, Stacks, Queues, Basic Sorting, Recursion |
| 🟡 Intermediate | 61-120 | Hash Tables, Trees, Heaps, Advanced Sorting, DP Basics, Graph Basics |
| 🟠 Advanced | 121-180 | Balanced Trees, Segment Trees, BIT, Advanced DP, Graph Algorithms, String Algorithms, Backtracking |
| 🔴 Expert | 181-250 | Union-Find, Bit Manipulation, Computational Geometry, Advanced Structures, Network Flow, Competitive Problems |

---

## Time Investment Estimate

| Level | Avg Time/Assignment | Total Time |
|-------|---------------------|------------|
| Beginner | 15 mins | ~15 hours |
| Intermediate | 25 mins | ~25 hours |
| Advanced | 40 mins | ~40 hours |
| Expert | 50 mins | ~60 hours |
| **Total** | | **~140 hours** |

---

## Mastery Milestones

- **After Beginner**: Ready for basic coding interviews
- **After Intermediate**: Ready for standard SDE interviews
- **After Advanced**: Ready for competitive programming and top-tier interviews
- **After Expert**: Ready for FAANG/MAANG and competitive programming contests

---

*This curriculum is designed to be self-contained. Each assignment builds upon previous concepts, creating a comprehensive learning path for DSA mastery.*
