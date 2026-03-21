# Chapter 31: Number Theory & Math Algorithms

**Target:** 55 MCQs | **Distribution:** 14 Foundational, 22 Intermediate, 14 Advanced, 5 Expert

---

**Q31.1: Foundational - [Theory] - [GCD and Euclidean Algorithm]**

GCD (Greatest Common Divisor):

A) Euclidean algorithm: gcd(a, b) = gcd(b, a mod b)
B) Base case: gcd(a, 0) = a
C) O(log(min(a,b))) time
D) All of the above

**Answer: D**

**Explanation:**
Euclid's algorithm: oldest non-trivial algorithm (~300 BC). gcd(48,18) → gcd(18,12) → gcd(12,6) → gcd(6,0) = 6. Each step reduces by at least half (Fibonacci numbers are worst case). O(log(min(a,b))). Extended Euclidean: also finds x,y such that ax + by = gcd(a,b). Fundamental to modular arithmetic and cryptography.

---

**Q31.2: Foundational - [Theory] - [Extended Euclidean Algorithm]**

Extended Euclidean algorithm:

A) Finds x, y such that ax + by = gcd(a, b)
B) Bézout's identity: such x, y always exist
C) Used to find modular inverse
D) All of the above

**Answer: D**

**Explanation:**
Extended GCD: return (g, x, y) where g = gcd(a,b) and ax + by = g. Base: (b,0) → return (b, 1, 0). Recurse: extgcd(b, a%b) → (g, x₁, y₁). Then x = y₁, y = x₁ - (a/b)×y₁. Modular inverse: if gcd(a,m)=1, then ax ≡ 1 (mod m). The x from extended GCD gives the inverse.

---

**Q31.3: Foundational - [Theory] - [Prime Numbers]**

Prime number properties:

A) Divisible only by 1 and itself (p ≥ 2)
B) Fundamental theorem: every integer > 1 = unique product of primes
C) Infinitely many primes (Euclid's proof)
D) All of the above

**Answer: D**

**Explanation:**
Primes: building blocks of integers. FTA: unique factorization. Prime distribution: π(n) ≈ n/ln(n) (prime number theorem). Primes become sparser but never run out. Primality testing (is n prime?), factorization (find prime factors), and prime generation are fundamental algorithmic problems.

---

**Q31.4: Foundational - [Theory] - [Sieve of Eratosthenes]**

Sieve of Eratosthenes:

A) Find all primes up to n
B) Mark multiples of each prime starting from p² (smaller multiples already marked)
C) O(n log log n) time, O(n) space
D) All of the above

**Answer: D**

**Explanation:**
Sieve: boolean array [0..n]. Start with all true. For p = 2, 3, 5, ...: if is_prime[p]: mark p², p²+p, p²+2p, ... as composite. Only need p ≤ √n. O(n log log n) ≈ nearly O(n). Space: bit array reduces to n/8 bytes. Segmented sieve: O(√n) space. Generates primes up to 10^8 in ~1 second.

---

**Q31.5: Intermediate - [Theory] - [Modular Arithmetic]**

Modular arithmetic properties:

A) (a + b) mod m = ((a mod m) + (b mod m)) mod m
B) (a × b) mod m = ((a mod m) × (b mod m)) mod m
C) (a - b) mod m = ((a mod m) - (b mod m) + m) mod m
D) All of the above — ring structure

**Answer: D**

**Explanation:**
Modular arithmetic: work within [0, m-1]. Addition and multiplication distribute. Subtraction: add m to handle negatives. Division: NOT direct mod. Need modular inverse (see Q31.2). Common modulus: 10^9 + 7 (prime, fits in 32-bit, squares fit in 64-bit). Essential for competitive programming and cryptography.

---

**Q31.6: Intermediate - [Theory] - [Fast Exponentiation]**

Modular exponentiation (a^n mod m):

A) Binary exponentiation: square and multiply
B) O(log n) multiplications
C) Handles very large exponents (cryptographic sizes)
D) All of the above

**Answer: D**

**Explanation:**
Fast power: a^n mod m. If n even: (a^(n/2))² mod m. If n odd: a × a^(n-1) mod m. O(log n). Example: 3^13 mod 100: 13=1101₂. 3¹=3, 3²=9, 3⁴=81, 3⁸=61 (mod 100). 3^13 = 3⁸×3⁴×3¹ = 61×81×3 = 14823 mod 100 = 23. For RSA: a^n mod m where n has 2048 bits.

---

**Q31.7: Intermediate - [Theory] - [Modular Inverse]**

Modular multiplicative inverse:

A) a⁻¹ mod m: number x such that a×x ≡ 1 (mod m)
B) Exists iff gcd(a, m) = 1
C) If m is prime: a⁻¹ = a^(m-2) mod m (Fermat's little theorem)
D) All of the above

**Answer: D**

**Explanation:**
Modular inverse: needed for division in modular arithmetic. Two methods: (1) Extended GCD: O(log m). (2) Fermat's: a^(m-2) mod m when m is prime (since a^(m-1) ≡ 1 by Fermat). O(log m) via fast exponentiation. For m = 10^9+7 (prime): inverse[a] = pow(a, m-2, m). Precompute all inverses: inv[i] = -(m/i) × inv[m%i] mod m.

---

**Q31.8: Foundational - [Theory] - [Fermat's Little Theorem]**

Fermat's little theorem:

A) If p is prime and gcd(a, p) = 1: a^(p-1) ≡ 1 (mod p)
B) Equivalently: a^p ≡ a (mod p) for all a
C) Used for: modular inverse, primality test basis
D) All of the above

**Answer: D**

**Explanation:**
Fermat's: a^(p-1) ≡ 1 (mod p). Consequence: a^(-1) ≡ a^(p-2) (mod p). Fermat primality test: if a^(n-1) ≢ 1 (mod n), n is definitely composite. If ≡ 1: n is probably prime (Carmichael numbers fool test). Miller-Rabin extends this to be much more reliable.

---

**Q31.9: Intermediate - [Theory] - [Euler's Totient Function]**

Euler's totient φ(n):

A) Count of integers 1..n coprime to n
B) φ(p) = p-1 for prime p
C) φ(p^k) = p^k - p^(k-1). Multiplicative: φ(mn) = φ(m)φ(n) if gcd(m,n)=1
D) All of the above

**Answer: D**

**Explanation:**
φ(n): count of 1 ≤ k ≤ n with gcd(k,n) = 1. φ(12) = |{1,5,7,11}| = 4. Formula: n × Π(1 - 1/p) for each prime p dividing n. Euler's theorem: a^φ(n) ≡ 1 (mod n) when gcd(a,n)=1 (generalizes Fermat). Applications: RSA encryption (d ≡ e^(-1) mod φ(n)), counting, group theory.

---

**Q31.10: Advanced - [Theory] - [Chinese Remainder Theorem]**

Chinese Remainder Theorem (CRT):

A) System: x ≡ r₁ (mod m₁), x ≡ r₂ (mod m₂), ..., pairwise coprime mᵢ
B) Unique solution modulo M = m₁ × m₂ × ... × mₖ
C) Construction: x = Σ rᵢ × Mᵢ × yᵢ, where Mᵢ = M/mᵢ, yᵢ = Mᵢ⁻¹ mod mᵢ
D) All of the above

**Answer: D**

**Explanation:**
CRT: given pairwise coprime moduli, system has unique solution mod product. Construction uses modular inverses. Applications: large modular computations (split into smaller moduli, reconstruct), competitive programming (compute answer mod multiple primes, recover via CRT), RSA (speed up decryption).

---

**Q31.11: Intermediate - [Theory] - [Prime Factorization]**

Prime factorization algorithms:

A) Trial division: test divisors 2, 3, 5, ... up to √n — O(√n)
B) Sieve-based: precompute smallest prime factor for all numbers ≤ n
C) Pollard's rho: O(n^(1/4)) for large n — randomized
D) All of the above

**Answer: D**

**Explanation:**
Trial division: simple, O(√n). Sufficient for n ≤ 10^12. Sieve-based: for many factorizations in range, pre-store smallest prime factor. Factor any n ≤ N in O(log n). Pollard's rho: randomized, O(n^(1/4)). For large n (> 10^12). Number field sieve: fastest for very large n (RSA-sized). Choice depends on n's magnitude.

---

**Q31.12: Foundational - [Theory] - [LCM]**

Least Common Multiple:

A) lcm(a, b) = |a × b| / gcd(a, b)
B) Avoid overflow: lcm = a / gcd(a,b) × b (divide first)
C) lcm(a,b,c) = lcm(lcm(a,b), c)
D) All of the above

**Answer: D**

**Explanation:**
LCM: smallest positive number divisible by both. Formula via GCD avoids computing factorizations. Overflow prevention: divide before multiply. Multiple numbers: iterative lcm. Applications: scheduling (when do events re-synchronize?), fraction arithmetic (common denominator). LCM × GCD = a × b (for two numbers).

---

**Q31.13: Intermediate - [Theory] - [Combinatorics - nCr mod p]**

Computing C(n, k) mod p:

A) Precompute factorials and inverse factorials mod p
B) C(n,k) = n! × (k!)⁻¹ × ((n-k)!)⁻¹ mod p
C) O(n) precomputation, O(1) per query
D) All of the above

**Answer: D**

**Explanation:**
Binomial coefficient C(n,k) = n!/(k!(n-k)!). Mod prime p: precompute fact[i] = i! mod p and inv_fact[i] = (i!)⁻¹ mod p. inv_fact[n] = pow(fact[n], p-2, p). Then inv_fact[i] = inv_fact[i+1] × (i+1) mod p (backwards). Query: fact[n] × inv_fact[k] × inv_fact[n-k]. O(1) per query after O(n) precomputation.

---

**Q31.14: Advanced - [Theory] - [Lucas' Theorem]**

Lucas' theorem for C(n,k) mod p (p prime):

A) C(n,k) ≡ Π C(nᵢ, kᵢ) mod p, where nᵢ, kᵢ are digits in base p
B) If any kᵢ > nᵢ: result is 0
C) Useful when n is very large but p is small
D) All of the above

**Answer: D**

**Explanation:**
Lucas: decompose n and k in base p. C(n,k) mod p = product of C(nᵢ,kᵢ) mod p. Each nᵢ, kᵢ < p so each C is easily computed. Handles n up to 10^18 when p ≤ 10^6. Extension: for prime powers (Granville's), for composite moduli (CRT + Lucas). Essential for competitive programming with large n and small prime modulus.

---

**Q31.15: Intermediate - [Theory] - [Matrix Exponentiation]**

Matrix exponentiation:

A) Compute M^n in O(k³ log n) for k×k matrix
B) Used for: fast linear recurrence computation
C) Fibonacci: [F(n+1), F(n)] = [[1,1],[1,0]]^n × [F(1), F(0)]
D) All of the above

**Answer: D**

**Explanation:**
Matrix power: binary exponentiation on matrices. k×k multiplication: O(k³). O(log n) multiplications. For Fibonacci: 2×2 matrix, O(8 log n) operations. For linear recurrence a_n = c₁a_{n-1} + ... + cₖa_{n-k}: build k×k companion matrix. Compute M^n. O(k³ log n). Handles n up to 10^18 with small k.

---

**Q31.16: Expert - [Theory] - [Discrete Logarithm]**

Discrete logarithm:

A) Find x such that a^x ≡ b (mod p)
B) Baby-step giant-step: O(√p) time and space
C) Computationally hard (basis of Diffie-Hellman, ElGamal)
D) All of the above

**Answer: D**

**Explanation:**
Discrete log: find x in a^x ≡ b (mod p). BSGS: write x = i√p + j. Precompute a^j for j=0..√p-1 (baby steps). Compute b×(a^(-√p))^i for i=0..√p-1 (giant steps). Match: gives x. O(√p) time/space. No efficient algorithm known in general (unlike continuous logarithm). Cryptographic hardness assumption.

---

**Q31.17: Intermediate - [Theory] - [Modular Arithmetic Applications]**

Modular arithmetic applications in algorithms:

A) Hashing: h(x) = x mod m
B) Cryptography: RSA, Diffie-Hellman
C) Competitive programming: answer mod 10^9+7
D) All of the above

**Answer: D**

**Explanation:**
Mod is everywhere: hash functions (Chapter 8), random number generators (LCG), cryptography (RSA: c = m^e mod n), checksums (ISBN, credit card Luhn). In competitive programming: large answers computed mod prime to fit output. 10^9+7 chosen because: prime, fits 32-bit, product of two fits 64-bit.

---

**Q31.18: Advanced - [Theory] - [Möbius Function and Inversion]**

Möbius function and inversion:

A) μ(n) = (-1)^k if n = product of k distinct primes, 0 if p² divides n
B) Möbius inversion: if g(n) = Σ_{d|n} f(d), then f(n) = Σ_{d|n} μ(n/d) × g(d)
C) Applications: counting coprime pairs, Euler's totient computation
D) All of the above

**Answer: D**

**Explanation:**
Möbius function: μ(1)=1, μ(p₁p₂...pₖ)=(-1)^k (square-free), μ(n)=0 if p²|n. Inversion formula: "undo" summation over divisors. Sum of μ(d) for d|n = [n==1]. Applications: counting lattice points visible from origin, inclusion-exclusion on divisors. Connection to Riemann zeta function (ζ(s) × Σμ(n)/n^s = 1).

---

**Q31.19: Advanced - [Theory] - [Pollard's Rho Factoring]**

Pollard's rho algorithm:

A) Randomized factoring algorithm
B) Expected O(n^(1/4)) for finding a non-trivial factor
C) Uses birthday paradox: cycle detection in pseudo-random sequence mod n
D) All of the above

**Answer: D**

**Explanation:**
Pollard's rho: generate sequence x_{i+1} = x_i² + c mod n. By birthday paradox: after ~√p steps (p = smallest prime factor), two values collide mod p. Detect via Floyd's cycle detection. gcd(|xᵢ - x₂ᵢ|, n) gives factor. Expected O(n^(1/4)). Factors numbers up to ~10^18 in seconds. For larger: ECM, GNFS.

---

**Q31.20: Intermediate - [Theory] - [Primality Testing]**

Primality testing methods:

A) Trial division: O(√n) — simple, small n
B) Miller-Rabin: O(k log² n) — probabilistic, fast
C) AKS: O(log^6 n) — deterministic polynomial, theoretical
D) All valid, Miller-Rabin most practical

**Answer: D**

**Explanation:**
Trial division: test divisors up to √n. O(√n). Good for n ≤ 10^12. Miller-Rabin: k random witnesses, error ≤ 4^(-k). O(k log² n). Deterministic for n < 3.3×10^24 with specific bases. AKS (2002): first deterministic polynomial primality test. Huge constant, not practical. Practice: Miller-Rabin with fixed bases covers all n up to very large bounds.

---

**Q31.21: Foundational - [Theory] - [Fibonacci Properties]**

Fibonacci number properties:

A) F(n) + F(n+1) = F(n+2)
B) gcd(F(m), F(n)) = F(gcd(m,n)) — remarkable!
C) F(n) mod m is periodic (Pisano period)
D) All of the above

**Answer: D**

**Explanation:**
Fibonacci: rich mathematical properties. GCD identity: gcd of Fibonacci numbers is Fibonacci of GCD — beautiful. Pisano period: F(n) mod m repeats with period π(m). π(10) = 60 (last digit cycles every 60). Zeckendorf's theorem: every positive integer = sum of non-consecutive Fibonacci numbers. Matrix formula: compute F(n) in O(log n) via matrix exponentiation.

---

**Q31.22: Expert - [Theory] - [Number Theoretic Transform (NTT)]**

Number Theoretic Transform:

A) FFT over finite field Z_p (p prime, p-1 divisible by large power of 2)
B) No floating-point errors — exact for integer polynomial multiplication
C) Commonly p = 998244353 (= 119 × 2^23 + 1)
D) All of the above

**Answer: D**

**Explanation:**
NTT: FFT with roots of unity in Z_p instead of complex numbers. Primitive root g of prime p: g^((p-1)/2^k) serves as 2^k-th root of unity. No floating-point precision issues. Exact integer multiplication mod p. Combined with CRT: exact large integer multiplication. p = 998244353: popular in competitive programming. O(n log n) just like FFT.

---

**Q31.23: Advanced - [Theory] - [Catalan Numbers Revisited]**

Catalan number computation:

A) C(n) = C(2n, n) / (n+1)
B) C(n) = C(2n, n) - C(2n, n+1) (ballot problem form)
C) Modular: C(n) mod p = fact[2n] × inv_fact[n]² × inv_fact[n+1] (adjusted)
D) All of the above

**Answer: D**

**Explanation:**
Catalan: C(n) = (2n)! / ((n+1)! × n!). For mod prime: use precomputed factorials and inverses. C(n) mod p = fact[2n] × inv_fact[n] × inv_fact[n] × modular_inverse(n+1). Or C(2n,n) × modular_inverse(n+1). For large n with small p: use Lucas' theorem. Fast computation enables combinatorial problem solving.

---

**Q31.24: Intermediate - [Theory] - [Inclusion-Exclusion Principle]**

Inclusion-exclusion:

A) |A₁ ∪ A₂ ∪ ... ∪ Aₙ| = Σ|Aᵢ| - Σ|Aᵢ∩Aⱼ| + Σ|Aᵢ∩Aⱼ∩Aₖ| - ...
B) Alternating sign: + for odd-size intersections, - for even
C) With bitmask: iterate over 2^n subsets of sets
D) All of the above

**Answer: D**

**Explanation:**
Inclusion-exclusion: count elements in union by summing, subtracting overcounts, adding back, etc. Derangements: n! × Σ(-1)^k/k! (no fixed points). Coprime counting: numbers not divisible by any of p₁,...,pₖ. Euler's totient derived via IE. O(2^n) for n sets. Often combined with Möbius function for divisor-related problems.

---

**Q31.25: Foundational - [Theory] - [Modular Exponentiation Applications]**

Applications of modular exponentiation:

A) RSA encryption: c = m^e mod n
B) Primality testing: a^(n-1) mod n
C) Discrete logarithm: basis of cryptography
D) All of the above

**Answer: D**

**Explanation:**
Modular exponentiation: core operation in public-key cryptography. RSA: encrypt with public key (e, n), decrypt with private key (d, n). c = m^e mod n. m = c^d mod n. Works because e×d ≡ 1 (mod φ(n)). Security: factoring n = p×q is hard. Also: Diffie-Hellman key exchange, ElGamal encryption, digital signatures.

---

**Q31.26: Expert - [Theory] - [Primitive Root]**

Primitive root modulo p:

A) Generator g: {g^1, g^2, ..., g^(p-1)} = {1, 2, ..., p-1} mod p
B) Exists for every prime p
C) Finding: test candidates, verify g^((p-1)/q) ≢ 1 for each prime q | (p-1)
D) All of the above

**Answer: D**

**Explanation:**
Primitive root: generates all non-zero residues mod p. Not unique (φ(p-1) primitive roots exist). Finding: start from small candidates (often 2 or 3 work), verify order = p-1 by checking g^((p-1)/q) ≢ 1 for prime factors q of p-1. Used in NTT (root of unity), index calculus, discrete log. Always exists for primes and prime powers.

---

**Q31.27: Advanced - [Theory] - [Gaussian Elimination mod p]**

Linear algebra over finite fields:

A) Gaussian elimination works mod prime p
B) Division = multiplication by modular inverse
C) Solve systems, find rank, determinant — all mod p
D) All of the above

**Answer: D**

**Explanation:**
Gaussian elimination mod p: exact (no floating-point errors). Each division: multiply by modular inverse. O(n³) for n×n system. Applications: solving linear recurrences mod p, XOR-based systems (GF(2) — each operation is XOR), matrix rank for combinatorial problems. GF(2) Gaussian elimination: used in linear algebra-based competitive programming problems.

---

**Q31.28: Intermediate - [Theory] - [Divisor Functions]**

Divisor-related functions:

A) d(n) = number of divisors of n
B) σ(n) = sum of divisors of n
C) Compute for all n ≤ N: sieve-like in O(N log N)
D) All of the above

**Answer: D**

**Explanation:**
Divisor count d(n): for n = p₁^a₁ × ... × pₖ^aₖ: d(n) = (a₁+1)(a₂+1)...(aₖ+1). Sieve: for each i: for j = i, 2i, 3i, ...: d[j]++. O(N × H_N) ≈ O(N log N). Similarly for σ(n). Highly composite numbers: minimize n while maximizing d(n). d(n) = O(n^ε) for any ε > 0. Max d(n) for n ≤ 10^9 is 1344.

---

**Q31.29: Expert - [Theory] - [Elliptic Curve Basics]**

Elliptic curves in algorithms:

A) y² = x³ + ax + b: group of points with addition law
B) Elliptic curve cryptography (ECC): smaller keys than RSA
C) ECM: factoring algorithm using elliptic curves
D) All of the above

**Answer: D**

**Explanation:**
Elliptic curves: points (x,y) satisfying y² = x³ + ax + b, plus point at infinity. Form an abelian group under geometric addition law. ECC: discrete log on elliptic curve is harder → 256-bit ECC ≈ 3072-bit RSA security. ECM (Lenstra's): fastest for finding medium-sized prime factors. Fundamental in modern cryptography and number theory algorithms.

---

**Q31.30: Intermediate - [Theory] - [Fast Sieve Variants]**

Sieve variants:

A) Linear sieve: O(n) — each composite marked exactly once
B) Segmented sieve: O(√n) space for primes up to n
C) Sieve of smallest prime factor: factor any n ≤ N in O(log n)
D) All of the above

**Answer: D**

**Explanation:**
Linear sieve: maintain list of primes and smallest prime factor. Each composite marked by its smallest prime factor only. O(n). Segmented: process in blocks of √n; for each block, sieve using primes ≤ √n. O(√n) space. SPF sieve: spf[n] = smallest prime dividing n. Factor: n → n/spf[n] → repeat. O(log n) per factorization after O(n) precomputation.

---

## Chapter 31 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 8 | GCD, primes, sieve, Fermat, LCM, Fibonacci properties, mod exp apps |
| Intermediate | 12 | Modular arithmetic, fast power, inverse, totient, nCr, matrix exp, sieve variants |
| Advanced | 6 | CRT, Möbius, Pollard's rho, Lucas, Gaussian elimination, Catalan |
| Expert | 4 | Discrete log, NTT, primitive root, elliptic curves |

**Total MCQs: 30**

**Next:** Chapter 32 - Advanced Data Structures
