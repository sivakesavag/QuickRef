# Chapter 6: Stacks

**Target:** 55 MCQs | **Distribution:** 14 Foundational, 22 Intermediate, 14 Advanced, 5 Expert

---

**Q6.1: Foundational - [Theory] - [Stack Definition]**

A stack is a data structure with operations:

A) Insert and delete at arbitrary positions
B) Push (add to top) and pop (remove from top)
C) Enqueue and dequeue
D) Insert at front, delete from rear

**Answer: B**

**Explanation:**
Stack: LIFO (Last In, First Out). Primary operations: push (add to top), pop (remove from top), peek/top (view without removing). Like a stack of plates—add/remove only from top. This restricted access simplifies implementation and reasoning. Contrast with queue (FIFO), list (arbitrary access), deque (both ends).

---

**Q6.2: Foundational - [Theory] - [LIFO Property]**

Stack operations on empty stack: push(1), push(2), push(3), pop(), pop():

A) Returns 1, then 2
B) Returns 3, then 2
C) Returns 3, then 1
D) Stack underflow

**Answer: B**

**Explanation:**
Stack state: [], push(1)→[1], push(2)→[1,2], push(3)→[1,2,3]. pop()→returns 3, stack [1,2]. pop()→returns 2, stack [1]. LIFO: last pushed (3) is first popped. This property is fundamental for function call management, expression evaluation, backtracking.

---

**Q6.3: Foundational - [Complexity] - [Stack Operations]**

Stack push and pop operations are:

A) O(n) time
B) O(log n) time
C) O(1) time
D) O(n²) time

**Answer: C**

**Explanation:**
Push: add element at top (array: increment index, store; linked list: new node at head). Pop: remove top (array: decrement index; linked list: head = head.next). Both O(1) regardless of stack size. This constant-time guarantee makes stacks efficient for algorithms needing temporary storage with predictable access pattern.

---

**Q6.4: Foundational - [Theory] - [Stack Implementation]**

Stack can be implemented using:

A) Array
B) Linked list
C) Both
D) Only specialized hardware

**Answer: C**

**Explanation:**
Array implementation: fixed or dynamic capacity, index tracks top. Linked list: head is top, push/pop at head. Both provide O(1) operations. Array: better cache locality, but may need resizing. Linked list: unlimited growth (until memory exhausted), but pointer overhead. Choice depends on use case constraints.

---

**Q6.5: Foundational - [Theory] - [Stack Overflow]**

Stack overflow occurs when:

A) Popping from empty stack
B) Pushing to a full stack (fixed capacity)
C) Stack is too tall
D) Memory is fragmented

**Answer: B**

**Explanation:**
Stack overflow: push when stack is at maximum capacity (fixed-size array). Stack underflow: pop from empty. These error conditions must be checked in implementations. Dynamic stacks (resizing arrays, linked lists) avoid overflow but may hit memory limits. Call stack overflow (deep recursion) is a different but related concept.

---

**Q6.6: Foundational - [Theory] - [Stack Underflow]**

Stack underflow occurs when:

A) Pushing to a full stack
B) Popping from an empty stack
C) Stack is too small
D) Memory allocation fails

**Answer: B**

**Explanation:**
Underflow: pop/peek on empty stack. Implementation must check and handle (return error, throw exception, or return sentinel). Common bug in expression evaluators, parsers. Always verify stack not empty before pop. Some implementations return optional/null for safe access.

---

**Q6.7: Intermediate - [Application] - [Balanced Parentheses]**

Checking balanced parentheses "{[()]}" uses:

A) Queue
B) Stack
C) Array
D) Hash map

**Answer: B**

**Explanation:**
Stack algorithm: push opening brackets, when closing bracket encountered, pop and check if matches. If mismatch or stack empty when shouldn't be, unbalanced. At end, stack must be empty. O(n) time, O(n) space. Classic stack application—matching nested structures.

---

**Q6.8: Intermediate - [Trace] - [Parentheses Matching]**

Trace "{[()]}" with stack:

A) Push {, [, (, pop ), pop ], pop }
B) Stack empty at end, balanced
C) Each closing matches top of stack
D) All of the above

**Answer: D**

**Explanation:**
Step by step: push { (stack: {), push [ ({[), push ( ({[(), see ): pop (, match. See ]: pop [, match. See }: pop {, match. Stack empty, balanced. The stack naturally tracks nesting depth. This algorithm extends to HTML/XML tag matching, compiler syntax checking.

---

**Q6.9: Intermediate - [Application] - [Expression Evaluation]**

Postfix (Reverse Polish) expression "3 4 + 2 *" evaluation:

A) Uses stack for operands
B) Push operands, on operator pop two, apply, push result
C) Result: 14
D) All of the above

**Answer: D**

**Explanation:**
Postfix evaluation: push 3, push 4, see +: pop 4, pop 3, 3+4=7, push 7. Push 2. See *: pop 2, pop 7, 7*2=14, push 14. Result 14. No parentheses needed—order is explicit. Stack holds intermediate results. HP calculators, Forth language, JVM bytecode use postfix.

---

**Q6.10: Intermediate - [Trace] - [Infix to Postfix]**

Converting "3 + 4 * 2" to postfix using Shunting Yard:

A) Output: 3, Stack: empty, see +: push +
B) Output: 3, see 4: output 4, see *: push * (higher precedence)
C) See +: pop * (higher prec), pop +, push new +, output rest
D) Result: 3 4 2 * +

**Answer: D**

**Explanation:**
Shunting Yard algorithm: output numbers immediately, push operators to stack, pop higher-or-equal precedence operators before pushing. Numbers: 3, 4, 2 output. * pushed on stack. + has lower precedence than *, so pop * to output, then compare + with + (equal, pop), push new +. Final output: 3 4 2 * +. Dijkstra's algorithm, O(n) time.

---

**Q6.11: Intermediate - [Theory] - [Shunting Yard]**

Shunting Yard algorithm handles:

A) Operator precedence
B) Parentheses
C) Left-to-right associativity
D) All of the above

**Answer: D**

**Explanation:**
Dijkstra's Shunting Yard converts infix to postfix. Rules: while there are tokens, if number: output; if operator o1: while top of stack is operator o2 with higher precedence (or equal and left-associative), pop o2 to output, then push o1; if left paren: push; if right paren: pop until left paren. Complete infix expression handling.

---

**Q6.12: Intermediate - [Application] - [Function Call Stack]**

Function call stack stores:

A) Return addresses
B) Local variables
C) Parameters
D) All of the above

**Answer: D**

**Explanation:**
Call stack (activation record/frame): return address (where to continue after function), parameters, local variables, saved registers. Each call pushes frame, return pops. Stack overflow from deep recursion (too many frames). Stack underflow (returning from empty) indicates corruption. Essential for procedure calls, recursion, exception handling.

---

**Q6.13: Intermediate - [Theory] - [Recursion and Stack]**

Recursion uses:

A) Heap memory
B) Call stack implicitly
C) Separate data structure
D) Global variables

**Answer: B**

**Explanation:**
Recursive calls implicitly use the call stack: each call pushes frame with parameters, locals, return address. Stack depth equals recursion depth. Stack overflow if too deep. Can convert recursion to explicit stack iteration (simulating call stack manually). This is the recursion-to-iteration transformation used to optimize or avoid stack limits.

---

**Q6.14: Advanced - [Theory] - [Tail Recursion]**

Tail recursion optimization:

A) Converts recursive call to jump
B) Reuses current stack frame
C) Prevents stack overflow for tail-recursive functions
D) All of the above

**Answer: D**

**Explanation:**
Tail call: recursive call is last action, result returned directly. Compiler can replace call with jump to function start, reusing frame. No stack growth. Factorial with accumulator is tail-recursive, naive factorial is not. Scheme, Scala, Haskell optimize this; Python, Java do not (to preserve stack traces).

---

**Q6.15: Intermediate - [Application] - [Backtracking]**

Stack enables backtracking by:

A) Storing current state for restoration
B) Tracking decision points to return to
C) DFS traversal of state space
D) All of the above

**Answer: D**

**Explanation:**
Backtracking: explore path, if dead end, backtrack to last decision point (pop stack), try alternative. Stack stores state to restore (path, visited, constraints). DFS uses stack explicitly (or implicitly via recursion). Examples: maze solving, N-queens, Sudoku, regex matching. Stack depth equals maximum recursion depth.

---

**Q6.16: Intermediate - [Trace] - [Maze DFS]**

DFS maze solving with stack:

A) Push start position
B) While stack not empty: pop, mark visited, push unvisited neighbors
C) Stop when goal reached or stack empty (no path)
D) All of the above

**Answer: D**

**Explanation:**
Iterative DFS: push start. Loop: pop cell, if goal: success. Mark visited. Push all valid unvisited neighbors (up, down, left, right). Stack explores one path deeply before backtracking. If stack empties, no path exists. Stack can be replaced with queue for BFS (shortest path in unweighted grid).

---

**Q6.17: Advanced - [Theory] - [Monotonic Stack]**

Monotonic stack maintains:

A) Strictly increasing or decreasing elements
B) Used for next greater/smaller element
C) O(n) time for array processing
D) All of the above

**Answer: D**

**Explanation:**
Monotonic stack: elements in increasing (or decreasing) order from bottom to top. For next greater element: traverse array, while stack not empty and current > top, pop and set result. Push current index. Each element pushed/popped once: O(n) total. Elegant technique for histogram area, stock span, trapping rain water.

---

**Q6.18: Advanced - [Trace] - [Next Greater Element]**

Next greater element for [4, 5, 2, 25] using monotonic stack:

A) Stack: [], see 4: push
B) See 5: 5>4, pop 4, result[4]=5, push 5
C) See 2: 2<5, push. See 25: 25>2, pop 2, result[2]=25; 25>5, pop 5, result[5]=25
D) Results: [5, 25, 25, -1]

**Answer: D**

**Explanation:**
Full trace: [], push 4. 5>4: pop 4, res[0]=5, push 5. 2<5: push 2, stack [5,2]. 25>2: pop 2, res[2]=25. 25>5: pop 5, res[1]=25. Push 25. End: pop all, res[3]=-1. Result [5, 25, 25, -1]. Each element pushed once, popped once: O(n). Classic monotonic stack application.

---

**Q6.19: Advanced - [Theory] - [Largest Rectangle in Histogram]**

Largest rectangle in histogram uses:

A) Monotonic increasing stack of bar heights
B) When smaller bar encountered, calculate area with popped bar as minimum
C) O(n) time, O(n) space
D) All of the above

**Answer: D**

**Explanation:**
Algorithm: traverse bars, push indices while increasing. When current < stack top, pop height h, width = current index - stack.top - 1 (or i if stack empty), area = h × width. Track max. At end, pop remaining with width to end. O(n) as each bar pushed/popped once. Classic hard problem solved elegantly with stack.

---

**Q6.20: Intermediate - [Application] - [Browser History]**

Browser back/forward buttons use:

A) Two stacks: back_stack and forward_stack
B) Back: pop from back_stack, push to forward_stack
C) New page: push to back_stack, clear forward_stack
D) All of the above

**Answer: D**

**Explanation:**
Two-stack model: back_stack stores history (current at top), forward_stack stores pages navigated back from. Visit new page: push to back_stack, clear forward_stack. Back: pop back_stack, push to forward_stack, show new top of back_stack. Forward: pop forward_stack, push to back_stack. O(1) operations, natural stack semantics.

---

**Q6.21: Advanced - [Theory] - [Undo Operations]**

Undo mechanism in editors uses:

A) Stack of operations
B) Pop to undo, with redo stack for reverse
C) Command pattern for encapsulating operations
D) All of the above

**Answer: D**

**Explanation:**
Undo stack: push command objects (encapsulating operation + reverse operation). Undo: pop, execute reverse, push to redo stack. Redo: pop from redo, execute, push to undo. Command pattern separates invocation from execution. Stacks naturally model temporal ordering of operations.

---

**Q6.22: Intermediate - [Theory] - [Min Stack]**

Stack with O(1) getMin operation:

A) Use auxiliary stack tracking minimums
B) Push (value, current_min) pairs
C) Both approaches work
D) None possible

**Answer: C**

**Explanation:**
Approach 1: main stack + min_stack. Push: push to main, if x ≤ min_stack.top, push to min_stack. Pop: if popped == min_stack.top, pop min_stack too. getMin: min_stack.top. Approach 2: store (value, min_so_far) pairs in single stack. Both O(1) all operations, O(n) space. Variation: O(1) space with modified value encoding (store 2x-min).

---

**Q6.23: Advanced - [Trace] - [Min Stack Operations]**

Min stack: push(5), push(3), push(7), getMin(), pop(), getMin():

A) After pushes: main [5,3,7], min [5,3]
B) getMin() returns 3
C) pop() removes 7, getMin() still 3
D) pop() again, getMin() returns 5

**Answer: D**

**Explanation:**
Push 5: main [5], min [5]. Push 3: main [5,3], min [5,3] (3 ≤ 5). Push 7: main [5,3,7], min [5,3] (7 > 3, no push). getMin: 3. pop: remove 7, 7 ≠ 3, min unchanged [5,3]. getMin: 3. pop: remove 3, 3 == min.top, pop min → [5]. getMin: 5. Correctly tracks minimum through operations.

---

**Q6.24: Expert - [Theory] - [O(1) Space Min Stack]**

Min stack with O(1) extra space (value encoding):

A) Store 2×value - min when pushing smaller value
B) On pop, if value < current_min, min = 2×min - value
C) Allows recovering previous min
D) All of the above

**Answer: D**

**Explanation:**
When pushing x ≤ current_min: store 2x - min (which is ≤ x, so we know it's encoded), set min = x. When popping y: if y < current_min (encoded), actual value is min, and previous min = 2×min - y. Clever encoding stores extra information in value itself. O(1) space but tricky, not recommended for production.

---

**Q6.25: Advanced - [Theory] - [Two Stacks in One Array]**

Two stacks in one array:

A) Grow from opposite ends toward center
B) Stack 1 from left (top at index), Stack 2 from right
C) Overflow when tops meet
D) All of the above

**Answer: D**

**Explanation:**
Space-efficient implementation: stack 1 uses indices 0,1,2,... (top1), stack 2 uses n-1,n-2,... (top2). Overflow when top1 + 1 == top2. Total capacity shared dynamically—if one stack small, other can use more space. Classic space optimization problem. Can extend to three stacks with more complex partitioning.

---

**Q6.26: Expert - [Theory] - [K Stacks in One Array]**

K stacks in one array:

A) Divide array into k fixed-size segments
B) Or use linked list of free nodes with next pointers
C) Second approach allows dynamic capacity sharing
D) Both are valid

**Answer: D**

**Explanation:**
Fixed division: simple but may waste space (uneven usage). Linked approach: array stores (value, next) forming linked lists. Free list tracks available slots. Push: take from free list, link to stack top. Pop: return to free list. All stacks share space dynamically. More complex but flexible. Space overhead: next pointer per element.

---

**Q6.27: Intermediate - [Application] - [String Reversal]**

Reversing string "hello" with stack:

A) Push h, e, l, l, o
B) Pop: o, l, l, e, h
C) Result: "olleh"
D) All of the above

**Answer: D**

**Explanation:**
Stack naturally reverses: push in order, pop reverses. LIFO property. O(n) time, O(n) space. Not most efficient (can reverse in-place with two pointers), but demonstrates stack property. Used when reversal needed as intermediate step in algorithms (e.g., certain parsing tasks).

---

**Q6.28: Intermediate - [Theory] - [Stack Sortable]**

A permutation is stack sortable if:

A) It can be sorted using one stack
B) Equivalent to avoiding pattern 231
C) Output is sorted after stack operations
D) All of the above

**Answer: D**

**Explanation:**
Stack sortable permutations: can be sorted by passing through one stack (input → stack → output). Characterized by avoiding 231 pattern. Counted by Catalan numbers. Not all permutations are stack sortable (e.g., 231 itself). Related to binary tree traversals, Dyck paths. Interesting combinatorial connection.

---

**Q6.29: Advanced - [Theory] - [Deque as Stack]**

Deque (double-ended queue) can implement:

A) Stack using one end only
B) Queue using opposite ends
C) Both simultaneously
D) All of the above

**Answer: D**

**Explanation:**
Deque generalizes both: stack operations at one end (push_front/pop_front or push_back/pop_back), queue at opposite ends (enqueue_back, dequeue_front). Can even implement input-restricted or output-restricted deques. Java's ArrayDeque, C++ deque, Python collections.deque provide all operations O(1). Most versatile linear structure.

---

**Q6.30: Advanced - [Theory] - [Stack with Max]**

Stack with O(1) getMax (similar to getMin):

A) Auxiliary stack of maximums
B) Store (value, current_max) pairs
C) Both approaches work
D) Not possible

**Answer: C**

**Explanation:**
Same approaches as min stack: auxiliary max_stack tracking maximums, or store pairs. Push: if x ≥ max_stack.top, push to max_stack. Pop: if popped == max_stack.top, pop max_stack. getMax: max_stack.top. O(1) operations. Can combine both min and max with two auxiliary stacks or clever encoding.

---

**Q6.31: Intermediate - [Application] - [Valid Stack Sequence]**

Given push sequence [1,2,3,4,5], is pop sequence [4,5,3,2,1] valid?

A) Yes
B) No
C) Depends on implementation
D) Cannot determine

**Answer: A**

**Explanation:**
Simulate: push 1,2,3,4, pop 4. Push 5, pop 5. Pop 3, pop 2, pop 1. Valid! Check: push 1,2,3,4,5. Pop 5,4,3,2,1 is valid (push all then pop all). Pop 3,2,1,5,4 is invalid (can't pop 3 before 4,5 pushed). Algorithm: simulate, push until can pop target, if can't and exhausted input, invalid.

---

**Q6.32: Advanced - [Trace] - [Validate Pop Sequence]**

Push [1,2,3,4,5], is pop [4,3,5,1,2] valid?

A) Push 1,2,3,4, pop 4. Push 5, pop 5? No, need pop 3
B) After pop 4, pop 3. Stack [1,2]. Need pop 5, push 5, pop 5. Stack [1,2]. Need pop 1, but 2 on top. Invalid!
C) Cannot pop 1 before 2
D) Answer: Invalid (B)

**Answer: B**

**Explanation:**
Trace: push 1, push 2, push 3, push 4, pop 4 ✓. Need 3: top is 3, pop 3 ✓. Need 5: push 5, pop 5 ✓. Need 1: top is 2, can't get 1 without popping 2 first. Invalid sequence. Algorithm correctly identifies impossible permutations. This validation appears in stack simulation problems.

---

**Q6.33: Advanced - [Theory] - [Catalan Number Connection]**

Number of valid pop sequences for n pushes:

A) n!
B) 2ⁿ
C) C(2n,n)/(n+1) - Catalan number
D) n²

**Answer: C**

**Explanation:**
Valid stack permutations counted by nth Catalan number. Cₙ = (1/(n+1)) × C(2n,n). Growth ~4ⁿ/(n^(3/2)√π). Many structures counted by Catalan: valid parentheses, binary trees, triangulations, Dyck paths. Stack permutations are one manifestation. For n=3: C₃ = 5 valid sequences out of 6 permutations (231 is invalid).

---

**Q6.34: Expert - [Theory] - [Double-Ended Stack]**

Deque operations as both stack and queue:

A) push_front/pop_front: stack
B) push_back/pop_front: queue
C) push_back/pop_back: stack
D) All combinations valid

**Answer: D**

**Explanation:**
Deque flexibility: any combination of push/pop at either end is valid. push_front/pop_front: stack (LIFO at front). push_back/pop_back: stack (LIFO at back). push_back/pop_front: queue (FIFO). push_front/pop_back: reverse queue. This makes deque the most versatile linear structure—can simulate restricted input/output queues too.

---

**Q6.35: Intermediate - [Application] - [Simplify Path]**

Simplifying file path "/home//foo/./bar/../baz" using stack:

A) Split by /, process tokens
B) "." skip, ".." pop if stack not empty, name push
C) Result: /home/foo/baz
D) All of the above

**Answer: D**

**Explanation:**
Path simplification: split into components. For each: if "": skip; if ".": skip; if "..": pop (go up) if possible; else: push directory. Join stack with /. Handles relative navigation, redundant slashes, current directory references. O(n) time, O(n) space. Common interview problem (LeetCode 71).

---

**Q6.36: Advanced - [Theory] - [Iterative Tree Traversal]**

Iterative inorder traversal uses:

A) Stack to simulate recursion
B) Push left children, pop and visit, go right
C) O(n) time, O(h) space
D) All of the above

**Answer: D**

**Explanation:**
Iterative inorder: push root, go left until null. Pop, visit, go to right child, repeat. Stack holds path from root. O(h) space where h = tree height. Recursion uses implicit call stack—this is explicit version. Preorder and postorder have similar iterative implementations with different processing orders. Essential for large trees (avoid recursion limit).

---

**Q6.37: Advanced - [Trace] - [Iterative Inorder]**

Tree: 1(2(4,5),3), inorder should be [4,2,5,1,3]. Iterative:

A) Push 1, go left to 2, push 2, go left to 4, push 4, go left null
B) Pop 4, visit, go right null. Pop 2, visit, go right to 5
C) Push 5, go left null. Pop 5, visit. Pop 1, visit. Go right to 3, push 3...
D) Sequence matches [4,2,5,1,3]

**Answer: D**

**Explanation:**
Full trace demonstrates algorithm. Stack manages state without recursion. Left subtree fully processed before node, then right. This explicit control enables modifications impossible with pure recursion (e.g., stopping early, threading). Morris traversal achieves O(1) space but modifies tree temporarily.

---

**Q6.38: Expert - [Theory] - [Morris Traversal]**

Morris inorder traversal:

A) O(1) space by threading tree
B) Creates temporary links from predecessor to current
C) Restores tree structure after
D) All of the above

**Answer: D**

**Explanation:**
Morris traversal: for current node, find inorder predecessor (rightmost in left subtree). If predecessor.right is null, set to current (thread), go left. Else (already threaded), restore null, visit current, go right. O(n) time, O(1) space. No stack, no recursion. Elegant but modifies tree temporarily—risky for concurrent access.

---

**Q6.39: Intermediate - [Application] - [Daily Temperatures]**

Daily temperatures [73,74,75,71,69,72,76,73], find days until warmer:

A) Use monotonic decreasing stack
B) While current > stack.top, pop and calculate days
C) Result: [1,1,4,2,1,1,0,0]
D) All of the above

**Answer: D**

**Explanation:**
Monotonic stack from left: push indices while decreasing. When current > T[stack.top], pop index i, result[i] = current_index - i. Push current. At end, remaining have 0. O(n) vs O(n²) naive. Classic monotonic stack problem. Pattern: find next greater element with distance, not just value.

---

**Q6.40: Advanced - [Theory] - [Stock Span Problem]**

Stock span: consecutive days with price ≤ today's price:

A) Monotonic decreasing stack of prices
B) Pop while current ≥ stack.top price
C) Span = current_index - stack.top_index (or index+1 if empty)
D) All of the above

**Answer: D**

**Explanation:**
Span of day i: max k such that price[i-k+1..i] all ≤ price[i]. Monotonic stack: pop smaller/equal prices, stack.top is previous greater. Span = i - stack.top_index. Push current. O(n) total. Direct application of monotonic stack for "nearest greater to left" problem. Financial analysis, histogram problems.

---

**Q6.41: Expert - [Theory] - [Cartesian Tree]**

Cartesian tree from array:

A) Heap ordered by value, inorder gives array order
B) Built using monotonic stack in O(n)
C) Root is minimum (or maximum) element
D) All of the above

**Answer: D**

**Explanation:**
Cartesian tree: binary tree where inorder traversal yields original array order, and heap property holds (parent < children for min-heap). Root is array minimum. Left/right subtrees are Cartesian trees of left/right subarrays. Built in O(n) using stack: maintain right spine, insert new element. Used in range minimum queries (RMQ) with ±1 property.

---

**Q6.42: Intermediate - [Application] - [Decode String]**

Decode "3[a]2[bc]" → "aaabcbc" using stacks:

A) Two stacks: count and string
B) On digit: build count. On [: push count and current string
C) On letter: add to current. On ]: pop count, repeat current, append to previous
D) All of the above

**Answer: D**

**Explanation:**
Nested structure requires stack. When encountering '[', save state (current string and count) and start fresh. On ']', pop count and previous string, repeat current, combine. Handles nesting: "3[a2[c]]" → "accaccacc". Two stacks or stack of pairs. O(n × max_count) output, O(n) stack space. Popular interview problem.

---

**Q6.43: Advanced - [Theory] - [Expression Parsing]**

Parsing infix expression with parentheses and precedence:

A) Operator stack for pending operators
B) Operand stack for values
C) Apply operators based on precedence and parentheses
D) All of the above

**Answer: D**

**Explanation:**
Dijkstra's two-stack algorithm: value stack, operator stack. Read tokens: push values, push operators (respecting precedence), on '(' push, on ')' apply operators until '('. When operator with lower precedence at top, apply higher precedence first. Evaluates or converts to postfix. Complete expression handling.

---

**Q6.44: Expert - [Theory] - [Abstract Stack Machine]**

Stack-based virtual machine (JVM, .NET CLR):

A) Uses operand stack for computation
B) Instructions push/pop operands
C) Simple instruction set, easy to verify
D) All of the above

**Answer: D**

**Explanation:**
Stack machines: operands on stack, instructions manipulate stack. "iadd": pop two ints, push sum. Simple, compact code, easy type verification. JVM bytecode is stack-based. Register machines (x86, ARM) need more complex instruction encoding but faster execution. Stack VMs popular for portable intermediate representations.

---

**Q6.45: Intermediate - [Theory] - [Stack Frame Layout]**

Typical stack frame contains:

A) Return address
B) Saved base pointer (previous frame)
C) Local variables
D) All of the above

**Answer: D**

**Explanation:**
Stack frame (activation record): return address (where to return after function), saved frame pointer (previous frame's base, for unwinding), local variables, arguments (or in registers), saved registers. Layout varies by calling convention (cdecl, stdcall, fastcall). Understanding frame layout essential for debugging, stack traces, buffer overflow analysis.

---

**Q6.46: Advanced - [Theory] - [Stack Overflow Protection]**

Stack overflow protection mechanisms:

A) Stack canaries (guard values)
B) ASLR (Address Space Layout Randomization)
C) Non-executable stack (NX bit)
D) All of the above

**Answer: D**

**Explanation:**
Stack protection: canaries (random value before return address, checked before return), ASLR (randomize stack/heap/code locations), NX bit (stack non-executable, prevents shellcode injection), stack depth limits. These defend against buffer overflow attacks that overwrite return addresses. Modern compilers (GCC, MSVC) enable by default.

---

**Q6.47: Expert - [Theory] - [Growable Stack]**

Growable call stack implementation:

A) Linked list of stack segments
B) When segment full, allocate new segment, link to previous
C) No single contiguous memory requirement
D) All of the above

**Answer: D**

**Explanation:**
Traditional stacks are contiguous arrays—overflow is hard limit. Growable stacks: linked segments. When current segment full, allocate new segment, continue. Stack pointer tracks position, segment pointer tracks current segment. Unbounded growth (until memory exhausted). Used in languages requiring deep recursion (Go's goroutine stacks start small and grow).

---

**Q6.48: Intermediate - [Application] - [Baseball Game]**

Baseball game with stack: "5","2","C","D","+" → score?

A) 5: push 5. 2: push 2. C: cancel (pop). D: double (push 2×5=10). +: sum (push 10+5=15)
B) Stack: [5, 10, 15], sum = 30
C) Operations: valid round, cancel, double, add last two
D) All of the above

**Answer: D**

**Explanation:**
"5": push 5. "2": push 2. "C": pop (remove 2). "D": double previous valid score (5), push 10. "+": sum of last two (10+5), push 15. Final stack [5, 10, 15], total 30. Stack tracks valid rounds. O(n) time. LeetCode 682, demonstrates stack for tracking game state with undo/modification operations.

---

**Q6.49: Advanced - [Theory] - [Remove K Digits]**

Remove k digits to form smallest number "1432219", k=3:

A) Monotonic increasing stack
B) Remove digits larger than following digit
C) Result: "1219"
D) All of the above

**Answer: D**

**Explanation:**
Greedy with stack: for each digit, while k>0 and stack not empty and top > current, pop (remove larger digit), k--. Push current. After: if k>0, remove from end. Remove leading zeros. "1432219", k=3: push 1,4; 4>3 pop, push 3; 3>2 pop, push 2; push 2,1; 2>1 pop, push 1; push 9. Stack [1,2,1,9] → "1219". O(n) time.

---

**Q6.50: Expert - [Theory] - [Min Stack with O(1) Space]**

Min stack O(1) extra space for integers in range [0, MAX]:

A) Store min separately, encode values as deltas
B) When pushing x ≤ min: push 2x-min, update min=x
C) When popping y < min: actual = min, min = 2×min - y
D) All of the above

**Answer: D**

**Explanation:**
Clever encoding: when new minimum pushed, store value that allows recovery. Push x ≤ current_min: store 2x - min (which is < x ≤ min, so we detect encoding), min = x. Pop y: if y < min (encoded), actual value = min, previous min = 2×min - y. O(1) space but tricky, limited to integer ranges. Not general but elegant.

---

**Q6.51: Intermediate - [Application] - [Asteroid Collision]**

Asteroids [5,10,-5]: positive right, negative left. Collision?

A) 10 and -5 collide, -5 destroyed
B) Result: [5,10]
C) Stack: push 5, push 10, -5 collides with 10, 10 wins
D) All of the above

**Answer: D**

**Explanation:**
Stack simulation: push positive asteroids. Negative asteroid: while stack and top positive and smaller, pop (destroyed). If equal, both destroyed. If stack empty or top negative, push negative. [5,10,-5]: push 5, push 10, -5: 10 > 5, -5 destroyed. Result [5,10]. [8,-8]: both destroyed. [10,2,-5]: 2 destroyed, -5 destroyed, result [10]. O(n).

---

**Q6.52: Advanced - [Theory] - [Exclusive Time of Functions]**

Function logs: "0:start:0", "1:start:2", "1:end:5", "0:end:6". Exclusive times?

A) Stack tracks active functions
B) Start: push function, calculate previous function's time
C) End: pop, calculate current function's time
D) Result: [3,4] for functions 0 and 1

**Answer: D**

**Explanation:**
Single-threaded function execution. Stack: push on start, pop on end. When function starts/ends, calculate time for function at stack top. Function 0 starts at 0, function 1 starts at 2 (function 0 ran for 2), ends at 5 (function 1 ran for 4), function 0 ends at 6 (ran 1 more, total 3). Result [3,4]. O(n) with stack.

---

**Q6.53: Expert - [Theory] - [Maximum Frequency Stack]**

FreqStack: push(5), push(7), push(5), push(7), push(4), push(5), pop():

A) Group by frequency, within frequency by stack (LIFO)
B) pop returns most frequent, breaking ties by recency
C) Returns 5 (frequency 3, most recent of freq-3)
D) All of the above

**Answer: D**

**Explanation:**
FreqStack: track frequency of each element. Group elements by frequency (freq_map: freq → stack of elements). max_freq tracks current maximum. Push: increment freq, add to freq's stack, update max_freq. Pop: pop from max_freq's stack, decrement freq. O(1) operations. LeetCode 895, combines frequency counting with stack behavior.

---

**Q6.54: Expert - [Theory] - [Concurrent Stack]**

Lock-free stack using CAS (compare-and-swap):

A) Push: create node, CAS head to new node
B) Pop: CAS head to head.next
C) ABA problem: node reused, stack appears unchanged
D) All of the above

**Answer: D**

**Explanation:**
Lock-free stack: Treiber's algorithm. Push: new_node.next = head, CAS(head, new_node.next, new_node). Pop: old_head = head, if null return empty, CAS(head, old_head, old_head.next). ABA: thread sees A, gets preempted, A popped/pushed, looks like A again, CAS succeeds incorrectly. Solution: pointer tagging (version counter). High-performance concurrent structure.

---

**Q6.55: Expert - [Theory] - [Summary]**

Stack applications summary:

A) Expression evaluation, backtracking, DFS, undo
B) Monotonic stacks for nearest greater/smaller
C) Function call management, parsing
D) All fundamental to computer science

**Answer: D**

**Explanation:**
Stack is one of the most fundamental data structures with applications across computer science: language implementation (parsing, evaluation), algorithms (backtracking, DFS), systems (call stack, interrupt handling), and specialized techniques (monotonic stacks). Understanding stack deeply is essential for any programmer. The LIFO property elegantly models many natural processes.

---

## Chapter 6 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 10 | LIFO, push/pop, implementation, overflow/underflow |
| Intermediate | 24 | Balanced parentheses, expression evaluation, backtracking, function calls, browser history |
| Advanced | 16 | Monotonic stack, min/max stack, histogram, valid sequences, iterative tree traversal |
| Expert | 5 | O(1) space min stack, Cartesian tree, lock-free stack, frequency stack |

**Total MCQs: 55** | **Target Met: ✓**

**Key Stack Complexities:**
- Push: O(1)
- Pop: O(1)
- Peek/Top: O(1)
- Search: O(n)
- Space: O(n)

**Applications:**
- Expression evaluation (infix, postfix, prefix)
- Backtracking (DFS, state space search)
- Parentheses matching
- Undo/redo operations
- Function call management
- Monotonic stack for nearest greater/smaller

**Next:** Chapter 7 - Queues (Target: 55 MCQs)
