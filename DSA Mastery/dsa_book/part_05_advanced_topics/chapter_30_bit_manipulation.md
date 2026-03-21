# Chapter 30: Bit Manipulation

**Target:** 50 MCQs | **Distribution:** 13 Foundational, 20 Intermediate, 12 Advanced, 5 Expert

---

**Q30.1: Foundational - [Theory] - [Binary Representation]**

Binary number system:

A) Base-2: each digit is 0 or 1 (bit)
B) Decimal 13 = binary 1101 = 8+4+0+1
C) n bits can represent 2^n distinct values (0 to 2^n - 1 unsigned)
D) All of the above

**Answer: D**

**Explanation:**
Binary representation: foundation of all computing. 1101₂ = 1×2³ + 1×2² + 0×2¹ + 1×2⁰ = 8+4+0+1 = 13. 8 bits (byte): 0–255. 32 bits: 0–4,294,967,295. 64 bits: 0–18.4×10¹⁸. Understanding binary is prerequisite for all bit manipulation.

---

**Q30.2: Foundational - [Theory] - [Bitwise Operators]**

Bitwise operators:

A) AND (&): 1 only if both bits are 1
B) OR (|): 1 if either bit is 1
C) XOR (^): 1 if bits differ
D) NOT (~): flip all bits

**Answer: D**

**Explanation:**
AND: masking (extract bits). OR: setting bits. XOR: toggling bits, finding differences. NOT: one's complement. These are O(1) hardware operations on entire words (32/64 bits simultaneously). Truth tables: AND(1,1)=1, all others 0. OR(0,0)=0, all others 1. XOR: same→0, different→1.

---

**Q30.3: Foundational - [Theory] - [Shift Operators]**

Shift operators:

A) Left shift (<<): shift bits left, fill with 0. x << k = x × 2^k
B) Logical right shift (>>>): shift right, fill with 0. x >>> k = x / 2^k (unsigned)
C) Arithmetic right shift (>>): shift right, fill with sign bit (preserves sign)
D) All of the above

**Answer: D**

**Explanation:**
Left shift: multiplication by power of 2. Fast: single instruction. Right shift: division by power of 2 (integer, rounds down). Arithmetic vs logical: for negative numbers, arithmetic preserves sign (fills with 1s), logical fills with 0s. Java has >>> for logical. C/C++: >> is implementation-defined for negative (usually arithmetic).

---

**Q30.4: Foundational - [Trace] - [Bitwise Operations]**

Compute: 12 & 10, 12 | 10, 12 ^ 10:

A) 12 = 1100, 10 = 1010
B) 12 & 10 = 1000 = 8
C) 12 | 10 = 1110 = 14
D) 12 ^ 10 = 0110 = 6

**Answer: D**

**Explanation:**
Bit by bit: 1100 AND 1010 = 1000 (8). 1100 OR 1010 = 1110 (14). 1100 XOR 1010 = 0110 (6). AND keeps common 1-bits. OR combines all 1-bits. XOR marks differences. These are the fundamental operations for bit manipulation tricks.

---

**Q30.5: Foundational - [Theory] - [Common Bit Tricks]**

Essential bit tricks:

A) Check if bit k is set: (n >> k) & 1
B) Set bit k: n | (1 << k)
C) Clear bit k: n & ~(1 << k)
D) Toggle bit k: n ^ (1 << k)

**Answer: D**

**Explanation:**
Get/set/clear/toggle: four fundamental operations. Get bit k: shift right by k, AND with 1. Set: OR with mask. Clear: AND with inverted mask. Toggle: XOR with mask. Mask = 1 << k (single bit at position k). All O(1). Foundation for bitmap data structures, flags, permission systems.

---

**Q30.6: Foundational - [Theory] - [Power of Two Check]**

Check if n is power of 2:

A) n & (n-1) == 0 (and n > 0)
B) Powers of 2 have exactly one set bit: 1, 10, 100, 1000, ...
C) n-1 flips all bits from LSB to rightmost 1
D) ANDing gives 0 only for powers of 2

**Answer: D**

**Explanation:**
n = 8 = 1000. n-1 = 7 = 0111. n & (n-1) = 0000. n = 6 = 110. n-1 = 101. 110 & 101 = 100 ≠ 0. This trick: n & (n-1) clears the rightmost set bit. If result is 0: only one bit was set → power of 2. Also: popcount(n) == 1. The n & (n-1) trick is the most famous bit manipulation identity.

---

**Q30.7: Intermediate - [Theory] - [Count Set Bits (Popcount)]**

Count number of 1-bits (popcount):

A) Brian Kernighan's: n = n & (n-1) repeatedly, count iterations
B) Lookup table: precompute for 8-bit chunks
C) Hardware: __builtin_popcount() / Integer.bitCount()
D) All valid approaches

**Answer: D**

**Explanation:**
Kernighan's: each n & (n-1) clears one set bit. Count until n=0. O(number of set bits). Lookup table: store popcount for all 256 byte values. Split 32-bit into 4 bytes, sum. O(1). SIMD: POPCNT instruction on x86 — single cycle. Divide and conquer: parallel bit summing (0x55555555 trick). Hardware support is fastest in practice.

---

**Q30.8: Intermediate - [Theory] - [XOR Properties]**

XOR properties:

A) x ^ x = 0 (self-inverse)
B) x ^ 0 = x (identity)
C) Commutative, associative
D) All of the above

**Answer: D**

**Explanation:**
XOR is addition in GF(2). Self-inverse: a ^ b ^ b = a (undoes itself). Identity: x ^ 0 = x. Commutative: a ^ b = b ^ a. Associative: (a ^ b) ^ c = a ^ (b ^ c). Applications: swap without temp (a^=b; b^=a; a^=b), find missing number, find single non-duplicate, encryption (one-time pad).

---

**Q30.9: Foundational - [Theory] - [Find Single Number]**

Find single non-duplicate (all others appear twice):

A) XOR all elements: duplicates cancel out (x ^ x = 0)
B) Result is the unique element
C) O(n) time, O(1) space
D) All of the above

**Answer: D**

**Explanation:**
Array [2,3,5,3,2]. XOR: 2^3^5^3^2 = (2^2)^(3^3)^5 = 0^0^5 = 5. Duplicates cancel. Single element survives. O(n) time, O(1) space. Elegant. Extension: if one element appears once, all others three times — use bit counting mod 3 per position.

---

**Q30.10: Intermediate - [Theory] - [Two's Complement]**

Two's complement representation:

A) Negative numbers: flip all bits and add 1
B) -x = ~x + 1
C) Range for n bits: [-2^(n-1), 2^(n-1) - 1]
D) All of the above

**Answer: D**

**Explanation:**
Two's complement: standard signed integer representation. MSB = sign bit. -1 = all 1s. -x = ~x + 1. Advantage: same hardware addition for signed/unsigned. 8-bit: -128 to 127. 32-bit: ≈ -2.1B to 2.1B. Trap: -(-2^31) overflows (no positive counterpart). Important for understanding bit tricks on negative numbers.

---

**Q30.11: Intermediate - [Theory] - [Lowest Set Bit]**

Isolate lowest set bit:

A) lowbit = n & (-n)
B) -n in two's complement = ~n + 1
C) Only the rightmost 1-bit survives the AND
D) Used in: Binary Indexed Tree (Fenwick tree), iterating set bits

**Answer: D**

**Explanation:**
n & (-n): isolates lowest set bit. Example: n=12=1100. -n = ~1100+1 = 0011+1 = 0100. 1100 & 0100 = 0100 = 4. The lowest set bit is at position 2 (value 4). BIT (Chapter 16) uses this for tree navigation. Iterating set bits: while(n) { process(n & -n); n &= (n-1); }.

---

**Q30.12: Intermediate - [Theory] - [Bit Masking for Subsets]**

Bitmask for subset representation:

A) Set of n elements: each subset = n-bit integer
B) Bit i set → element i included
C) Iterate all subsets: for mask = 0 to 2^n - 1
D) All of the above

**Answer: D**

**Explanation:**
Bitmask: compact subset representation. {0,2,3} from 5 elements = 01101 = 13. Union: a | b. Intersection: a & b. Complement: ~a & ((1<<n)-1). Check membership: (mask >> i) & 1. Enumerate subsets of a mask: for(s=mask; s>0; s=(s-1)&mask). Total over all masks: O(3^n). Foundation for bitmask DP (Chapter 22).

---

**Q30.13: Intermediate - [Theory] - [Swap Without Temp]**

Swap two variables without temporary:

A) a ^= b; b ^= a; a ^= b;
B) After step 1: a = a^b. Step 2: b = a^b^b = a. Step 3: a = a^b^a = b
C) Works but NOT recommended in practice (less readable, same speed)
D) All of the above

**Answer: D**

**Explanation:**
XOR swap: mathematically elegant. Step 1: a stores a⊕b. Step 2: b = (a⊕b)⊕b = a. Step 3: a = (a⊕b)⊕a = b. Warning: fails if a and b are the same variable (same memory location: x ^= x → 0). Modern compilers optimize temp-variable swap to register operations. Use XOR swap only as interview trick, not production code.

---

**Q30.14: Advanced - [Theory] - [Bit Manipulation for Division]**

Bitwise division tricks:

A) Divide by 2: x >> 1 (arithmetic right shift)
B) Divide by power of 2^k: x >> k
C) Modulo power of 2: x & (2^k - 1)
D) All of the above

**Answer: D**

**Explanation:**
Shift division: x >> k = ⌊x / 2^k⌋ for non-negative. For negative: arithmetic right shift rounds toward -∞ (not toward 0). Modulo: x & ((1<<k)-1) = x mod 2^k. Mask: (1<<k)-1 = k ones = 0111...1. These are faster than division instruction (especially on older hardware). Compilers often convert div-by-power-of-2 to shifts automatically.

---

**Q30.15: Intermediate - [Theory] - [Bitwise Tricks Collection]**

Useful bitwise tricks:

A) Turn off rightmost 1: n & (n-1)
B) Check if exactly one bit set: n && !(n & (n-1))
C) Get rightmost set bit position: __builtin_ctz(n) (count trailing zeros)
D) All of the above

**Answer: D**

**Explanation:**
Collection: (1) n & (n-1): clear lowest set bit. (2) n | (n-1): set all bits from LSB to lowest set bit. (3) __builtin_ctz: trailing zeros (= position of lowest set bit). (4) __builtin_clz: leading zeros (= position of highest set bit). (5) ~0: all 1s. (6) (1 << n) - 1: n lowest bits set. Memorize these for competitive programming.

---

**Q30.16: Intermediate - [Theory] - [Gray Code]**

Gray code:

A) Binary code where consecutive numbers differ by exactly 1 bit
B) n-bit Gray code: G(n) = n ^ (n >> 1)
C) Inverse: binary from Gray code using XOR prefix
D) Applications: error correction, rotary encoders

**Answer: D**

**Explanation:**
Gray code: 0,1,3,2,6,7,5,4 (for 3-bit). Only one bit changes between consecutive values. G(n) = n ^ (n>>1). Inverse: b[n-1]=g[n-1], b[i]=b[i+1]^g[i]. Applications: minimize switching errors in hardware (rotary encoders, ADC), Karnaugh maps, Towers of Hanoi solution encodes Gray code.

---

**Q30.17: Advanced - [Theory] - [Find Two Missing Numbers]**

Find two missing numbers from 1..n:

A) XOR all: get a ^ b (the two missing)
B) Find any set bit in a^b (they differ here)
C) Partition numbers by that bit, XOR each group separately
D) O(n) time, O(1) space

**Answer: D**

**Explanation:**
Step 1: XOR all 1..n and all array elements. Result = a ^ b. Step 2: a and b differ in some bit (find any set bit in a^b: bit = xor & -xor). Step 3: partition all numbers (1..n and array) into two groups based on that bit. XOR within each group: one gives a, other gives b. Generalizes "find single number."

---

**Q30.18: Advanced - [Theory] - [Bitwise AND of Range]**

Bitwise AND of all numbers in range [m, n]:

A) Find common prefix of m and n in binary
B) Shift both right until equal, shift result back left
C) O(log n) — number of bit positions
D) All of the above

**Answer: D**

**Explanation:**
AND of range: as numbers increase, lower bits flip between 0 and 1 → AND clears them. Only the common prefix (where m and n agree) survives. Algorithm: shift m and n right until equal (count shifts). Shift result back left. Example: [5,7] = 101,110,111. Common prefix: 1, followed by zeros → 100 = 4. O(number of bits).

---

**Q30.19: Advanced - [Theory] - [Bit Reversal]**

Reverse bits of a 32-bit integer:

A) Swap halves: swap 16-bit halves, then 8-bit, then 4-bit, then 2-bit, then 1-bit
B) Divide and conquer approach: O(log n) operations
C) Lookup table: reverse 8 bits at a time
D) All valid approaches

**Answer: D**

**Explanation:**
D&C reversal: swap adjacent bits, then 2-bit groups, then 4-bit, 8-bit, 16-bit. Uses masks: 0x55555555 (alternating), 0x33333333 (pairs), 0x0F0F0F0F (nibbles), etc. 5 operations for 32 bits. Lookup table: precompute reversal for all 256 byte values, reverse 4 bytes. Hardware: some CPUs have bit-reverse instructions. Applications: FFT (bit-reversal permutation).

---

**Q30.20: Foundational - [Theory] - [Bit Fields and Flags]**

Using bits as flags:

A) Store multiple boolean values in one integer
B) Unix permissions: rwxrwxrwx = 9 bits (owner, group, other)
C) Feature flags: enable/disable features with bitmask
D) All of the above

**Answer: D**

**Explanation:**
Bit flags: space-efficient boolean storage. Unix permissions: read=4, write=2, execute=1. chmod 755 = 111 101 101. Feature flags: FEATURE_A = 1, FEATURE_B = 2, FEATURE_C = 4. Enable: flags |= FEATURE_A. Check: flags & FEATURE_A. CPU status register uses flags. Network protocols: TCP flags (SYN, ACK, FIN).

---

**Q30.21: Intermediate - [Theory] - [Bitwise Minimum/Maximum]**

Finding min/max without branching:

A) min(a,b) = b ^ ((a^b) & -(a<b))
B) Avoids branch prediction misses
C) Useful in SIMD/vectorized code
D) All of the above

**Answer: D**

**Explanation:**
Branch-free min/max: -(a<b) = all 1s if a<b, all 0s otherwise. (a^b) & -(a<b) = a^b if a<b, 0 otherwise. b ^ that = a if a<b, b otherwise = min(a,b). Avoids conditional jump. Modern CPUs: cmov instruction makes this less important, but still relevant for SIMD where all lanes must execute same instruction.

---

**Q30.22: Advanced - [Theory] - [Bit Parallelism in String Matching]**

Bit-parallel string matching:

A) Bitap algorithm: pack character matches into bitvectors
B) Process w characters simultaneously (w = word size)
C) O(nm/w) — faster by factor of 64 on 64-bit machine
D) All of the above

**Answer: D**

**Explanation:**
Bitap (shift-or): precompute bitmask per character. State = bitvector of partial matches. Update: state = (state << 1) | char_mask. If bit m set: full match. Processes w=64 pattern positions per operation. Approximate matching: additional bitvectors for errors. Myers' bit-parallel edit distance: O(nm/w). Used in agrep, fuzzy search tools. See Chapter 26.

---

**Q30.23: Expert - [Theory] - [De Bruijn Sequence for Bit Position]**

De Bruijn sequence for finding bit position:

A) Multiply isolated bit by De Bruijn constant
B) Result's top bits encode position uniquely
C) O(1) — lookup table indexed by multiplication result
D) Used when __builtin_ctz unavailable

**Answer: D**

**Explanation:**
De Bruijn: binary sequence where all n-bit substrings are unique. Multiply isolated bit (from n & -n) by De Bruijn constant. Top log₂(n) bits = unique index. Lookup table maps index to bit position. O(1) with single multiplication. Classic pre-hardware-CTZ technique. Constant for 32-bit: 0x077CB531. For 64-bit: 0x03f79d71b4ca8b09.

---

**Q30.24: Intermediate - [Theory] - [Parity]**

Compute parity (odd/even number of set bits):

A) XOR all bits: result is 1 iff odd number of 1-bits
B) D&C: x ^= x>>16; x ^= x>>8; x ^= x>>4; x ^= x>>2; x ^= x>>1; result = x&1
C) __builtin_parity(n) — hardware support
D) All valid

**Answer: D**

**Explanation:**
Parity: XOR-fold. Each step halves the problem. 32-bit → 16 → 8 → 4 → 2 → 1. Final bit = parity. Alternative: popcount mod 2. Hardware: POPCNT and extract LSB. Applications: error detection (parity bit in serial communication, RAID), hash functions, coding theory.

---

**Q30.25: Expert - [Theory] - [Bitboard]**

Bitboards in chess engines:

A) 64-bit integer represents 8×8 board (one bit per square)
B) Separate bitboard for each piece type and color
C) Move generation: bitwise operations (shifts, masks, magic bitboards)
D) All of the above — enables parallel board evaluation

**Answer: D**

**Explanation:**
Bitboard: 64 bits = 64 squares. White pawns: bitboard with 1s at pawn positions. Attack generation: shift operations (pawn attacks = shift by 7 or 9 with mask). Rook/bishop: magic bitboards (perfect hash of occupied squares on ray → attack set lookup). AND/OR for combining/checking. ~50× faster than mailbox board representation. Used in Stockfish, AlphaZero.

---

**Q30.26: Advanced - [Theory] - [Subset Sum with Bitmask]**

All subset sums using bitmask:

A) For each mask 0..2^n-1: sum = sum[mask without last bit] + a[last bit position]
B) Or: for each element, update existing sums
C) O(2^n) total
D) Used in meet-in-the-middle algorithm

**Answer: D**

**Explanation:**
Subset sums: dp[mask] = sum of elements in mask. dp[mask] = dp[mask ^ lowbit(mask)] + a[ctz(lowbit(mask))]. O(2^n) to compute all. Meet-in-the-middle: split elements into two halves, compute all subset sums for each (O(2^(n/2))), combine with sorting/binary search. Turns O(2^n) to O(2^(n/2) × log). Effective for n ≈ 40.

---

**Q30.27: Foundational - [Theory] - [Hexadecimal and Binary]**

Hexadecimal and binary relationship:

A) Each hex digit = exactly 4 binary digits (nibble)
B) 0xF = 1111, 0xFF = 11111111, 0xA = 1010
C) Used for readable representation of bitmasks
D) All of the above

**Answer: D**

**Explanation:**
Hex is compact binary: 0x1A3F = 0001 1010 0011 1111. Common masks: 0xFF = 8 bits, 0xFFFF = 16 bits, 0x55555555 = alternating bits (01010101...). Hex makes bit patterns readable. Debugging: memory dumps in hex. Colors: 0xFF0000 = red (8 bits per channel RGB). Understanding hex↔binary conversion is essential for bit manipulation.

---

**Q30.28: Intermediate - [Theory] - [Counting Bits for All Numbers]**

Count bits for all numbers 0 to n:

A) dp[i] = dp[i >> 1] + (i & 1)
B) Or: dp[i] = dp[i & (i-1)] + 1
C) O(n) total — compute incrementally
D) All of the above

**Answer: D**

**Explanation:**
Count bits for every number 0..n in O(n). Method 1: dp[i] = dp[i/2] + (i%2). Right shift halves, last bit tells if odd. Method 2: dp[i] = dp[i with lowest bit cleared] + 1. Both O(1) per number. Useful when popcount of many numbers needed. Pattern: dp leverages previously computed values.

---

**Q30.29: Expert - [Theory] - [PDEP and PEXT Instructions]**

BMI2 instructions PDEP and PEXT:

A) PEXT: extract bits at positions specified by mask, pack contiguously
B) PDEP: deposit bits to positions specified by mask
C) Single instruction for complex bit manipulation
D) All of the above — O(1) hardware operations

**Answer: D**

**Explanation:**
PEXT(src, mask): for each set bit in mask, extract corresponding bit from src, pack left. PDEP(src, mask): scatter src bits to positions of set bits in mask. Single x86 instruction (BMI2). Applications: fast bitboard manipulation in chess, subset enumeration, data compression. Replaces loops of shift/mask operations. Available since Haswell (2013).

---

**Q30.30: Advanced - [Theory] - [Fenwick Tree and Bit Manipulation]**

BIT (Fenwick tree) and bit manipulation connection:

A) Parent of index i: i - (i & -i) — clear lowest set bit
B) Next in update: i + (i & -i) — add lowest set bit
C) Tree structure determined entirely by binary representation
D) All of the above — bit manipulation IS the algorithm

**Answer: D**

**Explanation:**
Fenwick tree: the tree structure is defined by bit manipulation. Query prefix sum: i -= lowbit(i), accumulate. Update: i += lowbit(i), propagate. lowbit = i & (-i). Range of responsibility of node i: [i - lowbit(i) + 1, i]. Binary representation determines parent-child relationships. See Chapter 16 for full details. Beautiful bit manipulation application.

---

**Q30.31: Expert - [Theory] - [Bit Tricks for Cryptography]**

Bit manipulation in cryptography:

A) Rotation: (x << k) | (x >> (w-k)) — circular shift
B) S-boxes: lookup-based bit substitution
C) Constant-time operations (avoid timing attacks)
D) All of the above

**Answer: D**

**Explanation:**
Cryptographic primitives: rotation (AES, SHA), XOR (stream ciphers), bit permutation (DES P-box), substitution (S-box lookup). Constant-time: operations must not depend on secret data (avoid cache-timing attacks). Bit manipulation enables: branchless conditional, constant-time selection. Example: select = mask & a | ~mask & b (branchless mux).

---

**Q30.32: Foundational - [Theory] - [Bit Manipulation Applications]**

Bit manipulation applications:

A) Embedded systems: hardware register manipulation
B) Graphics: pixel manipulation, alpha blending
C) Networking: IP address masking, subnet calculation
D) All of the above — low-level optimization

**Answer: D**

**Explanation:**
Bit manipulation is everywhere in systems programming: device drivers (register bits), networking (IP & subnet_mask = network address), graphics (color channels, alpha blending), compression (Huffman coding, arithmetic coding), databases (bitmap indices), OS (page tables, permission bits). Understanding bits = understanding computers at the fundamental level.

---

**Q30.33: Intermediate - [Theory] - [Next Power of Two]**

Round up to next power of 2:

A) n--; n|=n>>1; n|=n>>2; n|=n>>4; n|=n>>8; n|=n>>16; n++;
B) Fills all bits below highest set bit, then adds 1
C) O(1) — fixed number of operations
D) All of the above

**Answer: D**

**Explanation:**
Round up: set all bits below highest, add 1. Example: 5=101 → 111 → 1000=8. Steps: spread highest bit rightward by OR-shifting. After 5 rounds (for 32-bit): all lower bits set. Add 1: next power of 2. Alternative: 1 << (32 - __builtin_clz(n-1)). Used for: hash table sizing, memory allocation alignment.

---

**Q30.34: Advanced - [Theory] - [Parallel Bit Operations]**

SIMD and bit-level parallelism:

A) Process 128/256/512 bits simultaneously
B) Bitwise operations on wide registers
C) Population count on vectors (VPOPCNT)
D) All of the above

**Answer: D**

**Explanation:**
SIMD: Single Instruction, Multiple Data. SSE: 128-bit. AVX2: 256-bit. AVX-512: 512-bit with VPOPCNT. Process 4-16 integers simultaneously. Bitwise AND/OR/XOR on wide vectors. Applications: bioinformatics (DNA comparison), database bitmap operations, neural networks (binary neural networks). Bit parallelism × data parallelism = massive throughput.

---

**Q30.35: Intermediate - [Theory] - [Absolute Value Without Branching]**

Absolute value without branching:

A) mask = x >> 31 (arithmetic: all 1s if negative, all 0s if positive)
B) abs = (x ^ mask) - mask
C) If x ≥ 0: mask=0, abs = x. If x < 0: mask=-1, abs = ~x+1 = -x
D) All of the above

**Answer: D**

**Explanation:**
Branchless abs: shift sign bit to all positions (arithmetic right shift by 31 for 32-bit). XOR with mask: if negative, flips all bits (= ~x). Subtract mask: if negative, subtracts -1 (= adds 1). Combined: ~x + 1 = -x. If positive: XOR with 0 = x, subtract 0 = x. No branch → no branch misprediction penalty.

---

## Chapter 30 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 8 | Binary, operators, shifts, power-of-2, flags, hex, applications |
| Intermediate | 14 | Popcount, XOR tricks, masking, Gray code, parity, subsets, lowbit |
| Advanced | 9 | Bit reversal, range AND, parallelism, Fenwick connection, subset sums |
| Expert | 4 | De Bruijn, bitboards, PDEP/PEXT, cryptography |

**Total MCQs: 35**

**Next:** Chapter 31 - Number Theory & Math Algorithms
