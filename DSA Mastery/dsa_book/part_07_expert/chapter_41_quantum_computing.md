# Chapter 41: Quantum Computing & Algorithmic Implications

**Target:** 20 MCQs | **Distribution:** 5 Foundational, 8 Intermediate, 5 Advanced, 2 Expert

---

**Q41.1: Foundational - [Theory] - [Qubit vs Bit]**

A qubit differs from a classical bit in that:

A) A qubit can only be 0 or 1
B) A qubit can exist in a superposition of 0 and 1 simultaneously
C) A qubit stores more than one classical bit of information
D) A qubit is always faster than a bit

**Answer: B**

**Explanation:**
Qubit: |ψ⟩ = α|0⟩ + β|1⟩ where |α|² + |β|² = 1. Superposition: qubit is in both states simultaneously until measured. Measurement collapses to |0⟩ with probability |α|² or |1⟩ with probability |β|². C is a common misconception — Holevo's theorem limits extractable info to 1 classical bit per qubit. Power comes from parallel computation on superposed states and interference, not from storing more info.

---

**Q41.2: Foundational - [Theory] - [Quantum Speedup]**

Grover's algorithm achieves what speedup for unstructured search in a database of N items?

A) O(1) — constant time
B) O(√N) queries — quadratic speedup over classical O(N)
C) O(log N) — exponential speedup
D) O(N) — no speedup

**Answer: B**

**Explanation:**
Classical unstructured search: must check each item, O(N) worst case. Grover's algorithm: uses quantum amplitude amplification, finds target in O(√N) oracle queries. For N=10⁶: classical needs ~10⁶ queries, Grover needs ~10³. This is provably optimal for quantum — no quantum algorithm can do better than Ω(√N) for unstructured search. Quadratic speedup is significant but less dramatic than Shor's exponential speedup for factoring.

---

**Q41.3: Intermediate - [Theory] - [Shor's Algorithm]**

Shor's algorithm factors an n-bit integer in:

A) O(2^n) time — same as classical
B) O(n³) time — exponential speedup over classical
C) O(n) time — linear
D) O(n² log n) time — polynomial but slower than classical

**Answer: B**

**Explanation:**
Best classical factoring: General Number Field Sieve, O(exp(n^(1/3) × (log n)^(2/3))) — sub-exponential but super-polynomial. Shor's algorithm: O(n³) using quantum Fourier transform to find period of modular exponentiation. Exponential speedup! Threatens RSA encryption (factoring N = p×q). Implications: post-quantum cryptography research (lattice-based, code-based, hash-based crypto). Shor's is THE motivating algorithm for quantum computing.

---

**Q41.4: Foundational - [Theory] - [Entanglement]**

Quantum entanglement means:

A) Qubits are physically connected by wires
B) Measurement of one entangled qubit instantly determines the state of another, regardless of distance
C) Qubits vibrate at the same frequency
D) Two qubits always have the same value

**Answer: B**

**Explanation:**
Entangled pair (e.g., Bell state): |Φ⟩ = (|00⟩ + |11⟩)/√2. Measuring first qubit as |0⟩ → second is instantly |0⟩ (and vice versa). No "communication" — can't send information faster than light. But correlations are stronger than classical. Used in: quantum teleportation, superdense coding, quantum key distribution (QKD). Entanglement is a resource for quantum algorithms — enables parallelism beyond classical capabilities.

---

**Q41.5: Intermediate - [Theory] - [Quantum Gates]**

Which quantum gate is the analog of the classical NOT gate?

A) Hadamard (H) gate
B) Pauli-X gate
C) CNOT gate
D) Toffoli gate

**Answer: B**

**Explanation:**
Pauli-X: flips |0⟩ ↔ |1⟩, exactly like classical NOT. Hadamard (H): creates superposition H|0⟩ = (|0⟩ + |1⟩)/√2. No classical analog — puts qubit into equal superposition. CNOT: controlled-NOT, flips target if control is |1⟩ (2-qubit gate). Toffoli: controlled-controlled-NOT (3-qubit gate, classically universal). Quantum circuits are built from these elementary gates, similar to classical logic gates but reversible.

---

**Q41.6: Intermediate - [Theory] - [BQP Complexity Class]**

BQP (Bounded-Error Quantum Polynomial Time) is believed to relate to classical complexity classes as:

A) BQP = P
B) P ⊆ BQP ⊆ PSPACE, with BQP probably strictly between P and NP
C) BQP = NP
D) BQP contains all problems

**Answer: B**

**Explanation:**
BQP: problems solvable by quantum computer in polynomial time with bounded error. P ⊆ BQP (quantum can simulate classical). BQP ⊆ PSPACE (quantum can be simulated classically in polynomial space). Unknown: BQP vs NP — probably incomparable (some BQP problems may not be in NP, some NP problems may not be in BQP). Factoring: in BQP but not known to be in P. NP-complete problems: no proven quantum speedup beyond Grover's quadratic.

---

**Q41.7: Advanced - [Theory] - [Quantum Fourier Transform]**

The Quantum Fourier Transform (QFT) on n qubits runs in:

A) O(2^n) gates — same as classical FFT
B) O(n²) gates — exponentially faster than classical FFT
C) O(n) gates
D) O(n log n) gates — same as classical FFT

**Answer: B**

**Explanation:**
Classical FFT: O(N log N) = O(n × 2^n) for N=2^n points. QFT: O(n²) gates on n qubits (represents 2^n amplitudes). Exponentially faster! But: result is in quantum amplitudes — can't directly read all 2^n values (measurement collapses to one). QFT is useful as a SUBROUTINE: Shor's algorithm uses QFT for period finding. Directly reading QFT output would require O(2^n) measurements, negating the speedup.

---

**Q41.8: Foundational - [Theory] - [No-Cloning Theorem]**

The no-cloning theorem states that:

A) Quantum computers can clone any data
B) An arbitrary unknown quantum state cannot be exactly copied
C) Classical bits cannot be cloned
D) Quantum computers are unreliable

**Answer: B**

**Explanation:**
No-cloning: there's no quantum operation that creates a copy of an arbitrary unknown state |ψ⟩ → |ψ⟩|ψ⟩. Proof: linearity of quantum mechanics makes exact cloning impossible (would violate unitarity). Classical bits CAN be copied freely. Implications: (1) Quantum error correction is fundamentally different from classical, (2) Quantum cryptography (QKD) works because eavesdropping disturbs the state, (3) Can't "back up" quantum computations mid-way.

---

**Q41.9: Intermediate - [Theory] - [Quantum Cryptography Impact]**

Shor's algorithm breaks which classical cryptographic schemes?

A) All symmetric encryption (AES)
B) Public-key cryptography based on factoring and discrete logarithms (RSA, ECC, DH)
C) Hash functions (SHA-256)
D) One-time pads

**Answer: B**

**Explanation:**
Shor's: polynomial-time factoring and discrete log. Breaks: RSA (relies on factoring N=pq), Diffie-Hellman (discrete log), ECC (elliptic curve discrete log). AES: Grover gives only quadratic speedup → AES-256 retains 128-bit security (still secure). SHA-256: Grover gives √ speedup for collision finding, but still computationally hard. One-time pad: information-theoretically secure regardless. Post-quantum crypto: lattice-based (CRYSTALS-Kyber), hash-based (SPHINCS+) are NIST standards.

---

**Q41.10: Intermediate - [Theory] - [Quantum Error Correction]**

Why is quantum error correction harder than classical error correction?

A) Quantum computers don't have errors
B) Measurement destroys quantum states, and errors are continuous (not just bit-flips)
C) Classical error correction is impossible
D) Quantum errors only affect speed, not correctness

**Answer: B**

**Explanation:**
Classical: copy bit, majority vote. Simple. Quantum: (1) Can't copy (no-cloning), (2) Measurement destroys superposition, (3) Errors are continuous (arbitrary rotations, not just 0↔1), (4) Phase errors (no classical analog). Quantum error correction: encode logical qubit into many physical qubits. Surface codes, Shor code. Error threshold theorem: if physical error rate < threshold (~1%), arbitrarily long computation possible. Current hardware: approaching but not consistently below threshold.

---

**Q41.11: Advanced - [Theory] - [Amplitude Amplification]**

Grover's amplitude amplification works by:

A) Measuring repeatedly until the right answer appears
B) Iteratively reflecting amplitudes about the marked state and mean, amplifying the target's probability
C) Cloning the qubit state multiple times
D) Using classical search in parallel

**Answer: B**

**Explanation:**
Grover iteration: (1) Apply oracle O: flips sign of target state |x⟩ → -|x⟩. (2) Apply diffusion: reflect about mean amplitude (Grover diffuser). Each iteration: target amplitude increases by ~2/√N. After ~π√N/4 iterations: target probability ≈ 1. Geometric interpretation: rotation in 2D subspace (marked vs unmarked) by angle ~2/√N per step. Over-iteration: probability decreases again (must stop at right time).

---

**Q41.12: Intermediate - [Theory] - [Quantum Annealing]**

Quantum annealing (used by D-Wave systems) is designed to solve:

A) Any quantum computation
B) Optimization problems by finding low-energy states of an Ising model
C) Factoring integers
D) Database queries

**Answer: B**

**Explanation:**
Quantum annealing: start in ground state of simple Hamiltonian, slowly morph to problem Hamiltonian. System "tunnels" through energy barriers to find minimum energy state = optimal solution. Maps combinatorial optimization to Ising spin models. D-Wave: 5000+ qubits but limited connectivity and not universal quantum computer. Best for: specific optimization, sampling, QUBO problems. Debated whether it achieves genuine quantum speedup over classical simulated annealing.

---

**Q41.13: Advanced - [Theory] - [Quantum Walk]**

Quantum walks are the quantum analog of random walks and provide speedup for:

A) All graph algorithms
B) Element distinctness (from O(n log n) classically to O(n^(2/3)) quantumly)
C) Shortest path in O(1)
D) Graph coloring in O(1)

**Answer: B**

**Explanation:**
Quantum walk: superposition of walker positions, evolves via quantum rules (interference). Element distinctness: given n elements, are any two equal? Classical: sort O(n log n). Quantum walk algorithm (Ambainis): O(n^(2/3)) queries. Quadratic improvement uses walk on Johnson graph of subsets. Also: quantum walk spatial search on graphs, triangle finding. Quantum walks provide a general framework for quantum speedups on graph problems.

---

**Q41.14: Foundational - [Theory] - [Current Limitations]**

The main practical limitation of current quantum computers (NISQ era) is:

A) They can only process classical data
B) High error rates, limited qubit counts, and short coherence times
C) They are too fast to control
D) They use too much electricity

**Answer: B**

**Explanation:**
NISQ (Noisy Intermediate-Scale Quantum): 50-1000+ qubits, but error rates ~0.1-1% per gate. Coherence time: microseconds to milliseconds. Errors accumulate → limits circuit depth to ~100-1000 gates before noise overwhelms signal. Shor's algorithm on practical key sizes needs ~4000 logical qubits → millions of physical qubits (for error correction). Current: ~1000 physical qubits. "Quantum advantage" demonstrated for narrow tasks, not general-purpose computation.

---

**Q41.15: Expert - [Theory] - [Quantum Complexity Theory]**

The quantum query complexity of the OR function on n bits is:

A) O(1) — constant queries
B) Θ(√n) — proven by Grover's lower bound
C) Θ(n) — same as classical
D) Θ(log n)

**Answer: B**

**Explanation:**
OR(x₁,...,xₙ): is any xᵢ = 1? Classically: must check all n bits (adversary can place the 1 last) → Θ(n). Quantumly: Grover gives O(√n). Lower bound (BBBV theorem): Ω(√n) for any quantum algorithm. So quantum query complexity is Θ(√n). Quadratic speedup is the best possible for unstructured problems. Polynomial method and adversary method prove these lower bounds. Fundamental result in quantum complexity.

---

**Q41.16: Intermediate - [Theory] - [Post-Quantum Cryptography]**

Which mathematical problem is the basis for most NIST-selected post-quantum cryptographic standards?

A) Factoring large integers
B) Lattice problems (Learning With Errors, Module-LWE)
C) Discrete logarithm
D) Graph isomorphism

**Answer: B**

**Explanation:**
NIST Post-Quantum standards (2024): CRYSTALS-Kyber (key encapsulation) and CRYSTALS-Dilithium (signatures) — both lattice-based (Module-LWE). Lattice problems: finding short vectors in high-dimensional lattices. No known quantum algorithm provides more than polynomial speedup. Also selected: SPHINCS+ (hash-based signatures, no lattice). Lattice crypto: efficient, compact keys, versatile (supports fully homomorphic encryption). Replaces RSA/ECC in quantum-threatened world.

---

**Q41.17: Advanced - [Theory] - [Quantum Supremacy]**

"Quantum supremacy" (quantum computational advantage) means:

A) Quantum computers are superior for all tasks
B) A quantum device performed a specific computation faster than any classical computer feasibly could
C) Classical computers are obsolete
D) Quantum computers can solve NP-complete problems efficiently

**Answer: B**

**Explanation:**
Google's Sycamore (2019): random circuit sampling in 200 seconds, estimated 10,000 years classically. IBM contested the classical estimate. Strictly: performing ANY task faster than classical (not a useful one necessarily). Random circuit sampling has no practical application. "Quantum advantage": performing a USEFUL task faster. Distinction matters: supremacy is proven for narrow tasks, general advantage for practical problems remains future goal. Caveat: doesn't imply NP-hard problems are easy.

---

**Q41.18: Expert - [Theory] - [VQE and QAOA]**

Variational Quantum Eigensolver (VQE) and QAOA are NISQ-era algorithms designed for:

A) Exact factoring of integers
B) Finding approximate solutions to optimization and chemistry problems using shallow circuits
C) Breaking encryption
D) Sorting large datasets

**Answer: B**

**Explanation:**
VQE: parameterized quantum circuit + classical optimizer loop. Estimates ground state energy of molecules (quantum chemistry). QAOA (Quantum Approximate Optimization Algorithm): variational approach to combinatorial optimization. Both use shallow circuits → compatible with NISQ hardware. Hybrid quantum-classical: quantum evaluates cost function, classical optimizes parameters. No proven exponential speedup, but may give practical advantages for specific problems. Active research area.

---

**Q41.19: Advanced - [Theory] - [Quantum Simulation]**

Why is quantum simulation considered the most promising near-term application of quantum computing?

A) It's the simplest quantum algorithm
B) Quantum systems naturally simulate other quantum systems — exponentially hard classically
C) It requires the fewest qubits
D) It's already commercially available

**Answer: B**

**Explanation:**
Feynman's insight (1982): simulating n-particle quantum system classically: state space ~ 2^n dimensions → exponential memory. Quantum computer with n qubits: naturally represents n-qubit state. Simulating molecules, materials, chemical reactions: directly map physics to quantum hardware. Applications: drug discovery, catalyst design, materials science. Even 100-200 qubits could simulate molecules beyond classical reach. Near-term quantum advantage likely here before general computation.

---

**Q41.20: Intermediate - [Theory] - [Classical vs Quantum Complexity]**

For which type of problem does quantum computing offer NO speedup over classical?

A) Unstructured search
B) Problems already solvable in O(1) time (trivial problems)
C) Integer factoring
D) Simulation of quantum systems

**Answer: B**

**Explanation:**
Trivial problems (O(1) classical): quantum offers zero speedup — already instantaneous. For meaningful problems: unstructured search: √N speedup (Grover). Factoring: exponential speedup (Shor). Simulation: exponential speedup. BUT: not all hard problems get speedup. NP-complete problems: only Grover's quadratic speedup known (no exponential). BPP problems: quantum gives at most polynomial speedup. Quantum speedups are problem-specific, not universal.

---

## Chapter 41 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 5 | Qubit, Grover overview, entanglement, no-cloning, NISQ limitations |
| Intermediate | 8 | Shor, quantum gates, BQP, QFT, error correction, annealing, post-quantum, classical vs quantum |
| Advanced | 5 | Amplitude amplification, quantum walk, supremacy, simulation, QFT detail |
| Expert | 2 | Query complexity lower bounds, VQE/QAOA |

**Total MCQs: 20**

**Answer Distribution: A=2, B=17, C=0, D=1**

**Next:** Chapter 42 - Comprehensive Review & Mixed Problems
