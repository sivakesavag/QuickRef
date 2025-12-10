# 📖 DSA Mastery Cheatsheet
## Complete Reference Guide for 250 Assignments

---

## 📋 Quick Coverage Reference

| Section | Topics Covered |
|---------|----------------|
| Complexity Analysis | Big-O Notation, Time/Space Analysis, Master Theorem |
| Arrays & Strings | Two Pointers, Sliding Window, Prefix Sum, Dutch Flag |
| Linked Lists | Reversal, Fast-Slow Pointers, Cycle Detection, Merge |
| Stacks & Queues | Monotonic Stack, Expression Parsing, Sliding Window Max |
| Hash Tables | Frequency Counting, Two Sum Pattern, Grouping |
| Trees | DFS/BFS Traversals, BST Operations, LCA, Diameter |
| Heaps | Priority Queue, Two Heaps Pattern, K-way Merge |
| Graphs | BFS, DFS, Dijkstra, Bellman-Ford, Union-Find, MST |
| Sorting | Merge Sort, Quick Sort, Heap Sort, Counting Sort |
| Binary Search | Standard, Lower/Upper Bound, Rotated Array Search |
| Recursion & Backtracking | Subsets, Permutations, N-Queens, Sudoku |
| Dynamic Programming | Knapsack, LCS, LIS, Edit Distance, Grid DP |
| Greedy | Activity Selection, Interval Scheduling, Jump Game |
| String Algorithms | KMP, Rabin-Karp, Trie Implementation |
| Bit Manipulation | Common Operations, Single Number Patterns |
| Advanced DS | Segment Tree, Fenwick Tree (BIT) |
| Computational Geometry | Cross Product, Convex Hull, Polygon Area |
| Common Patterns | Problem-Solving Checklist, Pattern Recognition |

---

# 📚 Table of Contents

1. [Complexity Analysis](#1-complexity-analysis)
2. [Arrays & Strings](#2-arrays--strings)
3. [Linked Lists](#3-linked-lists)
4. [Stacks & Queues](#4-stacks--queues)
5. [Hash Tables](#5-hash-tables)
6. [Trees](#6-trees)
7. [Heaps](#7-heaps)
8. [Graphs](#8-graphs)
9. [Sorting Algorithms](#9-sorting-algorithms)
10. [Searching Algorithms](#10-searching-algorithms)
11. [Recursion & Backtracking](#11-recursion--backtracking)
12. [Dynamic Programming](#12-dynamic-programming)
13. [Greedy Algorithms](#13-greedy-algorithms)
14. [String Algorithms](#14-string-algorithms)
15. [Bit Manipulation](#15-bit-manipulation)
16. [Advanced Data Structures](#16-advanced-data-structures)
17. [Computational Geometry](#17-computational-geometry)
18. [Common Patterns](#18-common-patterns)

---

# 1. Complexity Analysis

## Time Complexity Quick Reference

| Complexity | Name | Example Operations |
|------------|------|-------------------|
| O(1) | Constant | Array access, hash lookup |
| O(log n) | Logarithmic | Binary search, balanced tree ops |
| O(n) | Linear | Array traversal, linear search |
| O(n log n) | Linearithmic | Merge sort, heap sort |
| O(n²) | Quadratic | Nested loops, bubble sort |
| O(n³) | Cubic | Floyd-Warshall, matrix mult |
| O(2ⁿ) | Exponential | All subsets, recursive fib |
| O(n!) | Factorial | All permutations |

## Space Complexity Tips
```
In-place: O(1) extra space
Recursive: O(depth) for call stack
Auxiliary array: O(n)
2D DP: O(n*m), optimize to O(min(n,m))
```

## Master Theorem (Divide & Conquer)
```
T(n) = aT(n/b) + f(n)

If f(n) = O(n^c):
  - c < log_b(a) → T(n) = O(n^log_b(a))
  - c = log_b(a) → T(n) = O(n^c * log n)
  - c > log_b(a) → T(n) = O(f(n))
```

---

# 2. Arrays & Strings

## Essential Techniques

### Two Pointer Pattern
```python
# Same direction (fast-slow)
def remove_duplicates(arr):
    write = 0
    for read in range(len(arr)):
        if read == 0 or arr[read] != arr[read-1]:
            arr[write] = arr[read]
            write += 1
    return write

# Opposite direction
def two_sum_sorted(arr, target):
    left, right = 0, len(arr) - 1
    while left < right:
        total = arr[left] + arr[right]
        if total == target: return [left, right]
        elif total < target: left += 1
        else: right -= 1
```

### Sliding Window Pattern
```python
# Fixed size window
def max_sum_subarray(arr, k):
    window_sum = sum(arr[:k])
    max_sum = window_sum
    for i in range(k, len(arr)):
        window_sum += arr[i] - arr[i-k]
        max_sum = max(max_sum, window_sum)
    return max_sum

# Variable size window
def longest_substring_k_distinct(s, k):
    left = 0
    freq = {}
    max_len = 0
    for right in range(len(s)):
        freq[s[right]] = freq.get(s[right], 0) + 1
        while len(freq) > k:
            freq[s[left]] -= 1
            if freq[s[left]] == 0:
                del freq[s[left]]
            left += 1
        max_len = max(max_len, right - left + 1)
    return max_len
```

### Prefix Sum Pattern
```python
# Build prefix sum
prefix = [0] * (len(arr) + 1)
for i in range(len(arr)):
    prefix[i+1] = prefix[i] + arr[i]

# Range sum query [l, r]
range_sum = prefix[r+1] - prefix[l]

# Count subarrays with sum = k
def subarray_sum(arr, k):
    prefix_count = {0: 1}
    curr_sum = 0
    count = 0
    for num in arr:
        curr_sum += num
        count += prefix_count.get(curr_sum - k, 0)
        prefix_count[curr_sum] = prefix_count.get(curr_sum, 0) + 1
    return count
```

### Array Rotation (Reversal Algorithm)
```python
def rotate_left(arr, k):
    k = k % len(arr)
    reverse(arr, 0, k-1)
    reverse(arr, k, len(arr)-1)
    reverse(arr, 0, len(arr)-1)

def rotate_right(arr, k):
    k = k % len(arr)
    reverse(arr, 0, len(arr)-1)
    reverse(arr, 0, k-1)
    reverse(arr, k, len(arr)-1)
```

### Dutch National Flag (3-way partition)
```python
def sort_colors(arr):
    low, mid, high = 0, 0, len(arr) - 1
    while mid <= high:
        if arr[mid] == 0:
            arr[low], arr[mid] = arr[mid], arr[low]
            low += 1
            mid += 1
        elif arr[mid] == 1:
            mid += 1
        else:
            arr[mid], arr[high] = arr[high], arr[mid]
            high -= 1
```

## String Operations

### Common String Patterns
```python
# Check palindrome
def is_palindrome(s):
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True

# Check anagram
def is_anagram(s1, s2):
    return sorted(s1) == sorted(s2)
    # OR use frequency count
    
# Longest common prefix
def longest_common_prefix(strs):
    if not strs: return ""
    prefix = strs[0]
    for s in strs[1:]:
        while not s.startswith(prefix):
            prefix = prefix[:-1]
    return prefix
```

---

# 3. Linked Lists

## Node Structure
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class DoublyListNode:
    def __init__(self, val=0, prev=None, next=None):
        self.val = val
        self.prev = prev
        self.next = next
```

## Essential Operations

### Reversal
```python
def reverse_list(head):
    prev, curr = None, head
    while curr:
        next_temp = curr.next
        curr.next = prev
        prev = curr
        curr = next_temp
    return prev
```

### Find Middle (Fast-Slow Pointer)
```python
def find_middle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow  # For even length, returns 2nd middle
```

### Detect Cycle (Floyd's Algorithm)
```python
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False

def find_cycle_start(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            slow = head
            while slow != fast:
                slow = slow.next
                fast = fast.next
            return slow
    return None
```

### Merge Two Sorted Lists
```python
def merge_lists(l1, l2):
    dummy = ListNode(0)
    curr = dummy
    while l1 and l2:
        if l1.val <= l2.val:
            curr.next = l1
            l1 = l1.next
        else:
            curr.next = l2
            l2 = l2.next
        curr = curr.next
    curr.next = l1 or l2
    return dummy.next
```

### Remove Nth from End
```python
def remove_nth_from_end(head, n):
    dummy = ListNode(0, head)
    first = second = dummy
    for _ in range(n + 1):
        first = first.next
    while first:
        first = first.next
        second = second.next
    second.next = second.next.next
    return dummy.next
```

---

# 4. Stacks & Queues

## Stack Templates

### Basic Stack Operations
```python
stack = []
stack.append(x)      # Push
top = stack[-1]      # Peek
stack.pop()          # Pop
len(stack) == 0      # isEmpty
```

### Monotonic Stack Pattern
```python
# Next Greater Element
def next_greater(arr):
    n = len(arr)
    result = [-1] * n
    stack = []  # indices
    for i in range(n - 1, -1, -1):
        while stack and arr[stack[-1]] <= arr[i]:
            stack.pop()
        if stack:
            result[i] = arr[stack[-1]]
        stack.append(i)
    return result

# Largest Rectangle in Histogram
def largest_rectangle(heights):
    stack = []
    max_area = 0
    for i, h in enumerate(heights + [0]):
        while stack and heights[stack[-1]] > h:
            height = heights[stack.pop()]
            width = i if not stack else i - stack[-1] - 1
            max_area = max(max_area, height * width)
        stack.append(i)
    return max_area
```

### Parentheses Matching
```python
def is_valid_parentheses(s):
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    for char in s:
        if char in mapping:
            if not stack or stack.pop() != mapping[char]:
                return False
        else:
            stack.append(char)
    return len(stack) == 0
```

### Expression Evaluation
```python
def eval_postfix(tokens):
    stack = []
    ops = {'+': lambda a,b: a+b, '-': lambda a,b: a-b,
           '*': lambda a,b: a*b, '/': lambda a,b: int(a/b)}
    for t in tokens:
        if t in ops:
            b, a = stack.pop(), stack.pop()
            stack.append(ops[t](a, b))
        else:
            stack.append(int(t))
    return stack[0]
```

## Queue Templates

### Basic Queue with Deque
```python
from collections import deque
queue = deque()
queue.append(x)      # Enqueue
front = queue[0]     # Front
queue.popleft()      # Dequeue
```

### Sliding Window Maximum (Monotonic Deque)
```python
def max_sliding_window(nums, k):
    dq = deque()  # indices
    result = []
    for i, num in enumerate(nums):
        while dq and nums[dq[-1]] < num:
            dq.pop()
        dq.append(i)
        if dq[0] <= i - k:
            dq.popleft()
        if i >= k - 1:
            result.append(nums[dq[0]])
    return result
```

---

# 5. Hash Tables

## Common Patterns

### Frequency Counting
```python
from collections import Counter
freq = Counter(arr)
# OR
freq = {}
for x in arr:
    freq[x] = freq.get(x, 0) + 1
```

### Two Sum Pattern
```python
def two_sum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []
```

### Group By Key
```python
from collections import defaultdict

# Group anagrams
def group_anagrams(strs):
    groups = defaultdict(list)
    for s in strs:
        key = tuple(sorted(s))
        groups[key].append(s)
    return list(groups.values())
```

### Longest Consecutive Sequence
```python
def longest_consecutive(nums):
    num_set = set(nums)
    max_len = 0
    for num in num_set:
        if num - 1 not in num_set:  # Start of sequence
            curr = num
            length = 1
            while curr + 1 in num_set:
                curr += 1
                length += 1
            max_len = max(max_len, length)
    return max_len
```

---

# 6. Trees

## Tree Node Structure
```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```

## Traversals

### Recursive Traversals
```python
def inorder(root):    # Left → Root → Right
    if root:
        inorder(root.left)
        print(root.val)
        inorder(root.right)

def preorder(root):   # Root → Left → Right
    if root:
        print(root.val)
        preorder(root.left)
        preorder(root.right)

def postorder(root):  # Left → Right → Root
    if root:
        postorder(root.left)
        postorder(root.right)
        print(root.val)
```

### Iterative Traversals
```python
def inorder_iterative(root):
    stack, result = [], []
    curr = root
    while stack or curr:
        while curr:
            stack.append(curr)
            curr = curr.left
        curr = stack.pop()
        result.append(curr.val)
        curr = curr.right
    return result
```

### Level Order (BFS)
```python
def level_order(root):
    if not root: return []
    result = []
    queue = deque([root])
    while queue:
        level = []
        for _ in range(len(queue)):
            node = queue.popleft()
            level.append(node.val)
            if node.left: queue.append(node.left)
            if node.right: queue.append(node.right)
        result.append(level)
    return result
```

## Common Tree Problems

### Height/Depth
```python
def max_depth(root):
    if not root: return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))
```

### Balanced Check
```python
def is_balanced(root):
    def check(node):
        if not node: return 0
        left = check(node.left)
        right = check(node.right)
        if left == -1 or right == -1 or abs(left - right) > 1:
            return -1
        return 1 + max(left, right)
    return check(root) != -1
```

### Validate BST
```python
def is_valid_bst(root, min_val=float('-inf'), max_val=float('inf')):
    if not root: return True
    if root.val <= min_val or root.val >= max_val:
        return False
    return (is_valid_bst(root.left, min_val, root.val) and
            is_valid_bst(root.right, root.val, max_val))
```

### Lowest Common Ancestor
```python
# Binary Tree
def lca_bt(root, p, q):
    if not root or root == p or root == q:
        return root
    left = lca_bt(root.left, p, q)
    right = lca_bt(root.right, p, q)
    if left and right: return root
    return left or right

# BST
def lca_bst(root, p, q):
    while root:
        if p.val < root.val and q.val < root.val:
            root = root.left
        elif p.val > root.val and q.val > root.val:
            root = root.right
        else:
            return root
```

### Diameter of Tree
```python
def diameter(root):
    max_diameter = [0]
    def height(node):
        if not node: return 0
        left = height(node.left)
        right = height(node.right)
        max_diameter[0] = max(max_diameter[0], left + right)
        return 1 + max(left, right)
    height(root)
    return max_diameter[0]
```

---

# 7. Heaps

## Heap Operations
```python
import heapq

# Min Heap (default in Python)
heap = []
heapq.heappush(heap, x)
min_val = heapq.heappop(heap)
min_val = heap[0]  # Peek

# Max Heap (negate values)
heapq.heappush(heap, -x)
max_val = -heapq.heappop(heap)

# Heapify array
heapq.heapify(arr)

# K largest/smallest
k_smallest = heapq.nsmallest(k, arr)
k_largest = heapq.nlargest(k, arr)
```

## Common Patterns

### Kth Largest Element
```python
def kth_largest(nums, k):
    heap = []
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)
    return heap[0]
```

### Merge K Sorted Lists
```python
def merge_k_lists(lists):
    heap = []
    for i, lst in enumerate(lists):
        if lst:
            heapq.heappush(heap, (lst.val, i, lst))
    
    dummy = ListNode(0)
    curr = dummy
    while heap:
        val, i, node = heapq.heappop(heap)
        curr.next = node
        curr = curr.next
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))
    return dummy.next
```

### Running Median (Two Heaps)
```python
class MedianFinder:
    def __init__(self):
        self.small = []  # Max heap (negated)
        self.large = []  # Min heap
    
    def addNum(self, num):
        heapq.heappush(self.small, -num)
        heapq.heappush(self.large, -heapq.heappop(self.small))
        if len(self.large) > len(self.small):
            heapq.heappush(self.small, -heapq.heappop(self.large))
    
    def findMedian(self):
        if len(self.small) > len(self.large):
            return -self.small[0]
        return (-self.small[0] + self.large[0]) / 2
```

---

# 8. Graphs

## Representations
```python
# Adjacency List
graph = defaultdict(list)
graph[u].append(v)  # Add edge u → v

# Adjacency Matrix
graph = [[0] * n for _ in range(n)]
graph[u][v] = 1  # Add edge

# Edge List
edges = [(u, v, weight), ...]
```

## Traversals

### BFS
```python
def bfs(graph, start):
    visited = {start}
    queue = deque([start])
    while queue:
        node = queue.popleft()
        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

### DFS (Iterative)
```python
def dfs(graph, start):
    visited = set()
    stack = [start]
    while stack:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            for neighbor in graph[node]:
                stack.append(neighbor)
```

### DFS (Recursive)
```python
def dfs(graph, node, visited):
    visited.add(node)
    for neighbor in graph[node]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

## Common Algorithms

### Cycle Detection
```python
# Undirected Graph
def has_cycle_undirected(graph, n):
    visited = set()
    def dfs(node, parent):
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                if dfs(neighbor, node):
                    return True
            elif neighbor != parent:
                return True
        return False
    
    for i in range(n):
        if i not in visited:
            if dfs(i, -1):
                return True
    return False

# Directed Graph (3-color DFS)
def has_cycle_directed(graph, n):
    WHITE, GRAY, BLACK = 0, 1, 2
    color = [WHITE] * n
    
    def dfs(node):
        color[node] = GRAY
        for neighbor in graph[node]:
            if color[neighbor] == GRAY:
                return True
            if color[neighbor] == WHITE and dfs(neighbor):
                return True
        color[node] = BLACK
        return False
    
    for i in range(n):
        if color[i] == WHITE:
            if dfs(i):
                return True
    return False
```

### Topological Sort
```python
# Kahn's Algorithm (BFS)
def topological_sort(graph, n):
    in_degree = [0] * n
    for u in graph:
        for v in graph[u]:
            in_degree[v] += 1
    
    queue = deque([i for i in range(n) if in_degree[i] == 0])
    result = []
    
    while queue:
        node = queue.popleft()
        result.append(node)
        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    return result if len(result) == n else []  # Empty if cycle
```

### Dijkstra's Algorithm
```python
def dijkstra(graph, start, n):
    dist = [float('inf')] * n
    dist[start] = 0
    heap = [(0, start)]
    
    while heap:
        d, u = heapq.heappop(heap)
        if d > dist[u]:
            continue
        for v, weight in graph[u]:
            if dist[u] + weight < dist[v]:
                dist[v] = dist[u] + weight
                heapq.heappush(heap, (dist[v], v))
    
    return dist
```

### Bellman-Ford
```python
def bellman_ford(edges, n, start):
    dist = [float('inf')] * n
    dist[start] = 0
    
    for _ in range(n - 1):
        for u, v, w in edges:
            if dist[u] != float('inf') and dist[u] + w < dist[v]:
                dist[v] = dist[u] + w
    
    # Check negative cycle
    for u, v, w in edges:
        if dist[u] != float('inf') and dist[u] + w < dist[v]:
            return None  # Negative cycle
    
    return dist
```

### Floyd-Warshall
```python
def floyd_warshall(graph, n):
    dist = [[float('inf')] * n for _ in range(n)]
    for i in range(n):
        dist[i][i] = 0
    for u in range(n):
        for v, w in graph[u]:
            dist[u][v] = w
    
    for k in range(n):
        for i in range(n):
            for j in range(n):
                dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])
    
    return dist
```

### Union-Find (Disjoint Set)
```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
    
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # Path compression
        return self.parent[x]
    
    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py:
            return False  # Already connected
        if self.rank[px] < self.rank[py]:
            px, py = py, px
        self.parent[py] = px
        if self.rank[px] == self.rank[py]:
            self.rank[px] += 1
        return True
```

### Kruskal's MST
```python
def kruskal(edges, n):
    edges.sort(key=lambda x: x[2])  # Sort by weight
    uf = UnionFind(n)
    mst = []
    total_weight = 0
    
    for u, v, w in edges:
        if uf.union(u, v):
            mst.append((u, v, w))
            total_weight += w
            if len(mst) == n - 1:
                break
    
    return mst, total_weight
```

---

# 9. Sorting Algorithms

## Algorithm Comparison

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Heap | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Counting | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes |
| Radix | O(nk) | O(nk) | O(nk) | O(n+k) | Yes |

## Implementations

### Merge Sort
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result
```

### Quick Sort
```python
def quick_sort(arr, low, high):
    if low < high:
        pivot_idx = partition(arr, low, high)
        quick_sort(arr, low, pivot_idx - 1)
        quick_sort(arr, pivot_idx + 1, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] < pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1
```

### Heap Sort
```python
def heap_sort(arr):
    n = len(arr)
    # Build max heap
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)
    # Extract elements
    for i in range(n - 1, 0, -1):
        arr[0], arr[i] = arr[i], arr[0]
        heapify(arr, i, 0)

def heapify(arr, n, i):
    largest = i
    left, right = 2 * i + 1, 2 * i + 2
    if left < n and arr[left] > arr[largest]:
        largest = left
    if right < n and arr[right] > arr[largest]:
        largest = right
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)
```

---

# 10. Searching Algorithms

### Binary Search Variants
```python
# Standard binary search
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# First occurrence (lower bound)
def lower_bound(arr, target):
    left, right = 0, len(arr)
    while left < right:
        mid = (left + right) // 2
        if arr[mid] < target:
            left = mid + 1
        else:
            right = mid
    return left

# Last occurrence (upper bound - 1)
def upper_bound(arr, target):
    left, right = 0, len(arr)
    while left < right:
        mid = (left + right) // 2
        if arr[mid] <= target:
            left = mid + 1
        else:
            right = mid
    return left

# Search in rotated sorted array
def search_rotated(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        # Left half is sorted
        if arr[left] <= arr[mid]:
            if arr[left] <= target < arr[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # Right half is sorted
        else:
            if arr[mid] < target <= arr[right]:
                left = mid + 1
            else:
                right = mid - 1
    return -1
```

---

# 11. Recursion & Backtracking

## Recursion Template
```python
def recursive_function(params):
    # Base case
    if base_condition:
        return base_result
    
    # Recursive case
    result = recursive_function(modified_params)
    return process(result)
```

## Backtracking Template
```python
def backtrack(state, choices):
    if is_goal(state):
        result.append(state.copy())
        return
    
    for choice in choices:
        if is_valid(choice):
            make_choice(state, choice)
            backtrack(state, remaining_choices)
            undo_choice(state, choice)  # Backtrack
```

## Common Problems

### Subsets
```python
def subsets(nums):
    result = []
    def backtrack(start, path):
        result.append(path[:])
        for i in range(start, len(nums)):
            path.append(nums[i])
            backtrack(i + 1, path)
            path.pop()
    backtrack(0, [])
    return result
```

### Permutations
```python
def permutations(nums):
    result = []
    def backtrack(path, remaining):
        if not remaining:
            result.append(path[:])
            return
        for i in range(len(remaining)):
            path.append(remaining[i])
            backtrack(path, remaining[:i] + remaining[i+1:])
            path.pop()
    backtrack([], nums)
    return result
```

### Combinations
```python
def combinations(n, k):
    result = []
    def backtrack(start, path):
        if len(path) == k:
            result.append(path[:])
            return
        for i in range(start, n + 1):
            path.append(i)
            backtrack(i + 1, path)
            path.pop()
    backtrack(1, [])
    return result
```

### N-Queens
```python
def solve_n_queens(n):
    result = []
    board = [['.'] * n for _ in range(n)]
    cols = set()
    diag1 = set()  # row - col
    diag2 = set()  # row + col
    
    def backtrack(row):
        if row == n:
            result.append([''.join(row) for row in board])
            return
        for col in range(n):
            if col in cols or (row-col) in diag1 or (row+col) in diag2:
                continue
            board[row][col] = 'Q'
            cols.add(col)
            diag1.add(row - col)
            diag2.add(row + col)
            backtrack(row + 1)
            board[row][col] = '.'
            cols.remove(col)
            diag1.remove(row - col)
            diag2.remove(row + col)
    
    backtrack(0)
    return result
```

---

# 12. Dynamic Programming

## DP Approach
```
1. Define state: dp[i] = ?
2. Base case: dp[0] = ?
3. Recurrence relation: dp[i] = f(dp[i-1], dp[i-2], ...)
4. Build order: bottom-up or top-down
5. Optimize space if possible
```

## Common Patterns

### Linear DP
```python
# Fibonacci
def fib(n):
    if n <= 1: return n
    dp = [0] * (n + 1)
    dp[1] = 1
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

# House Robber (non-adjacent max sum)
def rob(nums):
    if not nums: return 0
    if len(nums) == 1: return nums[0]
    dp = [0] * len(nums)
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])
    for i in range(2, len(nums)):
        dp[i] = max(dp[i-1], dp[i-2] + nums[i])
    return dp[-1]
```

### Kadane's Algorithm (Maximum Subarray)
```python
def max_subarray(nums):
    max_sum = curr_sum = nums[0]
    for num in nums[1:]:
        curr_sum = max(num, curr_sum + num)
        max_sum = max(max_sum, curr_sum)
    return max_sum
```

### 0/1 Knapsack
```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]
    
    for i in range(1, n + 1):
        for w in range(capacity + 1):
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i-1][w], 
                              dp[i-1][w-weights[i-1]] + values[i-1])
            else:
                dp[i][w] = dp[i-1][w]
    
    return dp[n][capacity]

# Space optimized (1D)
def knapsack_optimized(weights, values, capacity):
    dp = [0] * (capacity + 1)
    for i in range(len(weights)):
        for w in range(capacity, weights[i] - 1, -1):  # Reverse!
            dp[w] = max(dp[w], dp[w - weights[i]] + values[i])
    return dp[capacity]
```

### Unbounded Knapsack (Coin Change)
```python
def coin_change(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    for coin in coins:
        for x in range(coin, amount + 1):
            dp[x] = min(dp[x], dp[x - coin] + 1)
    return dp[amount] if dp[amount] != float('inf') else -1
```

### Longest Common Subsequence
```python
def lcs(s1, s2):
    m, n = len(s1), len(s2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s1[i-1] == s2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[m][n]
```

### Longest Increasing Subsequence
```python
# O(n²) DP
def lis_dp(nums):
    n = len(nums)
    dp = [1] * n
    for i in range(1, n):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)
    return max(dp)

# O(n log n) Binary Search
def lis_binary(nums):
    tails = []
    for num in nums:
        idx = bisect.bisect_left(tails, num)
        if idx == len(tails):
            tails.append(num)
        else:
            tails[idx] = num
    return len(tails)
```

### Edit Distance
```python
def edit_distance(s1, s2):
    m, n = len(s1), len(s2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(m + 1):
        dp[i][0] = i
    for j in range(n + 1):
        dp[0][j] = j
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s1[i-1] == s2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(dp[i-1][j],    # Delete
                                  dp[i][j-1],     # Insert
                                  dp[i-1][j-1])   # Replace
    
    return dp[m][n]
```

### Grid DP
```python
# Unique Paths
def unique_paths(m, n):
    dp = [[1] * n for _ in range(m)]
    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
    return dp[m-1][n-1]

# Minimum Path Sum
def min_path_sum(grid):
    m, n = len(grid), len(grid[0])
    for i in range(m):
        for j in range(n):
            if i == 0 and j == 0:
                continue
            elif i == 0:
                grid[i][j] += grid[i][j-1]
            elif j == 0:
                grid[i][j] += grid[i-1][j]
            else:
                grid[i][j] += min(grid[i-1][j], grid[i][j-1])
    return grid[m-1][n-1]
```

---

# 13. Greedy Algorithms

## When to Use Greedy
- Local optimal leads to global optimal
- Optimal substructure + greedy choice property
- Cannot revisit choices

## Common Problems

### Activity Selection / Meeting Rooms
```python
def max_meetings(intervals):
    intervals.sort(key=lambda x: x[1])  # Sort by end time
    count = 0
    last_end = 0
    for start, end in intervals:
        if start >= last_end:
            count += 1
            last_end = end
    return count
```

### Merge Intervals
```python
def merge_intervals(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    for start, end in intervals[1:]:
        if start <= merged[-1][1]:
            merged[-1][1] = max(merged[-1][1], end)
        else:
            merged.append([start, end])
    return merged
```

### Jump Game
```python
def can_jump(nums):
    max_reach = 0
    for i, jump in enumerate(nums):
        if i > max_reach:
            return False
        max_reach = max(max_reach, i + jump)
    return True
```

---

# 14. String Algorithms

### KMP Pattern Matching
```python
def kmp_search(text, pattern):
    def build_lps(pattern):
        lps = [0] * len(pattern)
        length = 0
        i = 1
        while i < len(pattern):
            if pattern[i] == pattern[length]:
                length += 1
                lps[i] = length
                i += 1
            elif length != 0:
                length = lps[length - 1]
            else:
                lps[i] = 0
                i += 1
        return lps
    
    lps = build_lps(pattern)
    i = j = 0
    result = []
    while i < len(text):
        if pattern[j] == text[i]:
            i += 1
            j += 1
        if j == len(pattern):
            result.append(i - j)
            j = lps[j - 1]
        elif i < len(text) and pattern[j] != text[i]:
            if j != 0:
                j = lps[j - 1]
            else:
                i += 1
    return result
```

### Rabin-Karp (Rolling Hash)
```python
def rabin_karp(text, pattern):
    d = 256  # Number of characters
    q = 101  # Prime number
    m, n = len(pattern), len(text)
    p = t = 0  # Hash values
    h = pow(d, m - 1) % q
    result = []
    
    # Calculate initial hash
    for i in range(m):
        p = (d * p + ord(pattern[i])) % q
        t = (d * t + ord(text[i])) % q
    
    # Slide pattern
    for i in range(n - m + 1):
        if p == t:
            if text[i:i+m] == pattern:
                result.append(i)
        if i < n - m:
            t = (d * (t - ord(text[i]) * h) + ord(text[i + m])) % q
            t = (t + q) % q  # Ensure positive
    
    return result
```

### Trie Implementation
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end
    
    def starts_with(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True
```

---

# 15. Bit Manipulation

## Common Operations
```python
# Check if bit is set
(n >> i) & 1

# Set bit
n | (1 << i)

# Clear bit
n & ~(1 << i)

# Toggle bit
n ^ (1 << i)

# Count set bits
bin(n).count('1')
# OR Brian Kernighan's
def count_bits(n):
    count = 0
    while n:
        n &= (n - 1)  # Clear rightmost set bit
        count += 1
    return count

# Check power of 2
n > 0 and (n & (n - 1)) == 0

# Get rightmost set bit
n & (-n)

# Clear rightmost set bit
n & (n - 1)
```

## Common Problems
```python
# Single Number (XOR all)
def single_number(nums):
    result = 0
    for num in nums:
        result ^= num
    return result

# Missing number (XOR with indices)
def missing_number(nums):
    result = len(nums)
    for i, num in enumerate(nums):
        result ^= i ^ num
    return result
```

---

# 16. Advanced Data Structures

### Segment Tree
```python
class SegmentTree:
    def __init__(self, arr):
        self.n = len(arr)
        self.tree = [0] * (4 * self.n)
        self.build(arr, 0, 0, self.n - 1)
    
    def build(self, arr, node, start, end):
        if start == end:
            self.tree[node] = arr[start]
        else:
            mid = (start + end) // 2
            self.build(arr, 2*node+1, start, mid)
            self.build(arr, 2*node+2, mid+1, end)
            self.tree[node] = self.tree[2*node+1] + self.tree[2*node+2]
    
    def update(self, node, start, end, idx, val):
        if start == end:
            self.tree[node] = val
        else:
            mid = (start + end) // 2
            if idx <= mid:
                self.update(2*node+1, start, mid, idx, val)
            else:
                self.update(2*node+2, mid+1, end, idx, val)
            self.tree[node] = self.tree[2*node+1] + self.tree[2*node+2]
    
    def query(self, node, start, end, l, r):
        if r < start or l > end:
            return 0
        if l <= start and end <= r:
            return self.tree[node]
        mid = (start + end) // 2
        left = self.query(2*node+1, start, mid, l, r)
        right = self.query(2*node+2, mid+1, end, l, r)
        return left + right
```

### Fenwick Tree (BIT)
```python
class FenwickTree:
    def __init__(self, n):
        self.n = n
        self.tree = [0] * (n + 1)
    
    def update(self, i, delta):
        i += 1
        while i <= self.n:
            self.tree[i] += delta
            i += i & (-i)
    
    def query(self, i):
        i += 1
        total = 0
        while i > 0:
            total += self.tree[i]
            i -= i & (-i)
        return total
    
    def range_query(self, l, r):
        return self.query(r) - self.query(l - 1)
```

---

# 17. Computational Geometry

### Basic Operations
```python
# Cross product (for orientation)
def cross(o, a, b):
    return (a[0] - o[0]) * (b[1] - o[1]) - (a[1] - o[1]) * (b[0] - o[0])

# > 0: counter-clockwise, < 0: clockwise, = 0: collinear

# Distance between points
def distance(p1, p2):
    return ((p1[0] - p2[0])**2 + (p1[1] - p2[1])**2) ** 0.5

# Area of polygon (Shoelace formula)
def polygon_area(points):
    n = len(points)
    area = 0
    for i in range(n):
        j = (i + 1) % n
        area += points[i][0] * points[j][1]
        area -= points[j][0] * points[i][1]
    return abs(area) / 2
```

### Convex Hull (Graham Scan)
```python
def convex_hull(points):
    points = sorted(set(points))
    if len(points) <= 1:
        return points
    
    # Build lower hull
    lower = []
    for p in points:
        while len(lower) >= 2 and cross(lower[-2], lower[-1], p) <= 0:
            lower.pop()
        lower.append(p)
    
    # Build upper hull
    upper = []
    for p in reversed(points):
        while len(upper) >= 2 and cross(upper[-2], upper[-1], p) <= 0:
            upper.pop()
        upper.append(p)
    
    return lower[:-1] + upper[:-1]
```

---

# 18. Common Patterns

## Problem-Solving Checklist

1. **Understand the problem**
   - Read carefully, note constraints
   - Work through examples
   - Identify edge cases

2. **Identify pattern**
   - What data structure fits?
   - What algorithm paradigm?
   - Similar problems solved before?

3. **Design solution**
   - Start with brute force
   - Optimize step by step
   - Consider time/space tradeoffs

4. **Implement**
   - Write clean code
   - Handle edge cases
   - Test with examples

5. **Analyze**
   - Time complexity
   - Space complexity
   - Can it be optimized further?

## Pattern Recognition Guide

| Problem Characteristics | Likely Pattern |
|------------------------|----------------|
| Find pair with sum/diff | Two pointers, Hash map |
| Subarray/substring with property | Sliding window |
| Sorted array search | Binary search |
| Tree traversal | DFS (recursion/stack), BFS (queue) |
| Graph connectivity | BFS, DFS, Union-Find |
| Shortest path | BFS (unweighted), Dijkstra (weighted) |
| Optimal solution with choices | DP or Greedy |
| All combinations/permutations | Backtracking |
| Range queries | Segment Tree, BIT |
| Prefix-based strings | Trie |
| Top/Bottom K elements | Heap |
| Stream of data | Heap, Sliding window |
| Cycle detection | Floyd's, DFS coloring |
| Interval scheduling | Sort + Greedy |

## Edge Cases to Always Consider

- Empty input
- Single element
- All same elements
- Sorted/reverse sorted
- Negative numbers
- Integer overflow
- Very large inputs
- Duplicates

---

*Use this cheatsheet as a quick reference while solving the 250 DSA assignments. Each section provides the key concepts and code templates needed to tackle problems in that category.*
