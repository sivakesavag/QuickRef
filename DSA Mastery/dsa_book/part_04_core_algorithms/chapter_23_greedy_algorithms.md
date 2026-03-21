# Chapter 23: Greedy Algorithms

**Target:** 55 MCQs | **Distribution:** 14 Foundational, 22 Intermediate, 14 Advanced, 5 Expert

---

**Q23.1: Foundational - [Theory] - [Greedy Definition]**

Greedy algorithm:

A) Make locally optimal choice at each step
B) Hope local optimum leads to global optimum
C) Correct only for problems with greedy-choice property + optimal substructure
D) All of the above

**Answer: D**

**Explanation:**
Greedy: at each step, choose what looks best now, never reconsider. Works when: (1) Greedy-choice property: locally optimal choice is part of some globally optimal solution. (2) Optimal substructure: optimal solution contains optimal sub-solutions. Not all problems satisfy these — must prove correctness for each problem.

---

**Q23.2: Foundational - [Theory] - [Activity Selection]**

Activity selection (max non-overlapping activities):

A) Sort by finish time ascending
B) Greedily select earliest finishing activity
C) Skip conflicting (overlapping) activities
D) All of the above — O(n log n)

**Answer: D**

**Explanation:**
Activity selection: classic greedy. Sort by end time. Select first activity. For remaining: if start ≥ last selected's end, select it. Greedy choice: earliest finish leaves maximum room for future activities. Proof by exchange argument: swapping any other choice with earliest-finish doesn't improve count. O(n log n) for sort + O(n) scan.

---

**Q23.3: Foundational - [Trace] - [Activity Selection]**

Activities: [(1,4), (3,5), (0,6), (5,7), (3,9), (5,9), (6,10), (8,11), (8,12), (2,14), (12,16)]:

A) Sort by finish: (1,4), (3,5), (0,6), (5,7), (3,9), (5,9), (6,10), (8,11), (8,12), (2,14), (12,16)
B) Select (1,4). Next non-overlap: (5,7). Next: (8,11). Next: (12,16)
C) 4 activities selected
D) Maximum possible — verified

**Answer: D**

**Explanation:**
Sorted by end: select (1,4). Skip (3,5): 3<4. Skip (0,6): 0<4. Select (5,7): 5≥4. Skip (3,9),(5,9),(6,10): all start before 7. Select (8,11): 8≥7. Select (12,16): 12≥11. Result: 4 activities. Optimal.

---

**Q23.4: Foundational - [Theory] - [Huffman Coding]**

Huffman coding:

A) Variable-length prefix codes for compression
B) Shorter codes for more frequent characters
C) Build bottom-up: merge two least frequent nodes
D) All of the above — optimal prefix code

**Answer: D**

**Explanation:**
Huffman: greedy optimal prefix-free encoding. Priority queue of frequencies. Merge two smallest → parent with sum. Repeat until one tree. Frequent chars: short codes. Infrequent: long codes. Prefix-free: no code is prefix of another (enables unambiguous decoding). O(n log n). Optimal among prefix codes. Used in ZIP, JPEG, MP3.

---

**Q23.5: Foundational - [Theory] - [Fractional Knapsack]**

Fractional knapsack:

A) Can take fractions of items (unlike 0/1 knapsack)
B) Sort by value/weight ratio descending, take greedily
C) O(n log n) — greedy is optimal
D) All of the above

**Answer: D**

**Explanation:**
Fractional knapsack: take fractions. Greedy: sort by value-to-weight ratio. Take most valuable per unit first. If item fits completely: take all. If not: take fraction to fill remaining capacity. Greedy works because any other choice wastes capacity on less valuable items. Contrast: 0/1 knapsack requires DP (greedy fails).

---

**Q23.6: Intermediate - [Theory] - [Prove Greedy Correctness]**

Common techniques to prove greedy correctness:

A) Exchange argument: swap non-greedy choice with greedy, show no worse
B) Stays ahead: show greedy solution dominates any other at each step
C) Structural argument: show greedy maintains invariant
D) All are valid proof techniques

**Answer: D**

**Explanation:**
Exchange argument: assume optimal solution that differs from greedy. Swap one choice to match greedy. Show result ≥ original. "Stays ahead": inductively show greedy's partial solution ≥ any alternative's at each step. These are the standard proof techniques. Without proof: greedy may seem right but give wrong answer. Always verify.

---

**Q23.7: Intermediate - [Theory] - [When Greedy Fails]**

Greedy fails for:

A) 0/1 knapsack: taking best ratio item may prevent optimal combination
B) Coin change with arbitrary denominations: greedy may not minimize coins
C) Longest path in general graph: greedy doesn't find optimal
D) All of the above

**Answer: D**

**Explanation:**
0/1 knapsack: items {(w=10,v=60),(w=20,v=100),(w=30,v=120)}, capacity 50. Greedy (ratio): takes item 1 (6.0/unit) + item 2 (5.0). Value=160. DP optimal: items 2+3=220. Coin change: coins {1,3,4}, amount 6. Greedy: 4+1+1=3 coins. Optimal: 3+3=2 coins. Must use DP for these.

---

**Q23.8: Intermediate - [Theory] - [Interval Scheduling Maximization]**

Interval scheduling maximization:

A) Select maximum number of non-overlapping intervals
B) Greedy: sort by end time, select greedily
C) Same as activity selection
D) O(n log n)

**Answer: D**

**Explanation:**
Interval scheduling maximization = activity selection. Sort by end time, greedily select. Optimal. If instead sort by start time or duration: not optimal. End time Sort key insight: earliest finish creates most room. Weighted version (each interval has weight): DP needed (greedy doesn't handle weights).

---

**Q23.9: Intermediate - [Theory] - [Interval Partitioning]**

Interval partitioning (minimum rooms/resources):

A) Minimum resources to schedule all intervals
B) Sort by start time, assign to available resource
C) Equals maximum overlapping intervals at any point
D) O(n log n)

**Answer: D**

**Explanation:**
Interval partitioning: schedule all (can't skip), minimize resources. Sort by start time. Assign interval to any resource free at its start. PQ of resource end times. Need new resource when all busy. Answer = max concurrent intervals = max depth of overlap. Proof: need ≥ max overlap (obvious), greedy achieves exactly max overlap.

---

**Q23.10: Intermediate - [Theory] - [Job Scheduling with Deadlines]**

Job scheduling to minimize lateness:

A) Each job has duration and deadline
B) Sort by deadline (earliest deadline first)
C) Greedy: process in deadline order
D) Minimizes maximum lateness — O(n log n)

**Answer: D**

**Explanation:**
Minimize max lateness: EDF (Earliest Deadline First). Sort by deadline. Process in order. Proof by exchange: swapping two adjacent jobs where later deadline is processed first can only reduce max lateness. No idle time between jobs. Related: EDF scheduling in real-time operating systems guarantees schedulability.

---

**Q23.11: Intermediate - [Theory] - [Huffman Coding Detail]**

Huffman coding optimality:

A) Optimal among prefix-free binary codes
B) Two least frequent symbols are siblings at deepest level
C) Removing these two and adding parent doesn't change optimality structure
D) All of the above — greedy + optimal substructure

**Answer: D**

**Explanation:**
Huffman optimality proof: (1) Greedy choice: two rarest symbols must be at deepest level (swapping rarer to shallower level reduces cost). (2) Optimal substructure: replacing two deepest symbols with combined parent gives sub-instance; optimal sub-instance + greedy choice = optimal. Full proof by induction on alphabet size.

---

**Q23.12: Advanced - [Theory] - [Matroids and Greedy]**

Matroid theory and greedy algorithms:

A) Matroid: set system where greedy finds optimal weighted base
B) Independent sets satisfy: subset closed, exchange property
C) Greedy on matroid: sort by weight, add if stays independent
D) All of the above

**Answer: D**

**Explanation:**
Matroid: (E, I) where I = independent sets. Properties: ∅ ∈ I. A ⊂ B ∈ I → A ∈ I. |A| < |B|, both ∈ I → ∃x ∈ B\A: A∪{x} ∈ I. Weighted matroid optimization: greedy (sort, add max weight if independent) finds optimal. Graphic matroid (forests), partition matroid, transversal matroid. Explains WHY greedy works for some problems.

---

**Q23.13: Foundational - [Theory] - [Greedy vs DP vs Brute Force]**

Algorithmic paradigm comparison:

A) Brute force: try all, O(exponential)
B) DP: try all subproblems, O(polynomial usually)
C) Greedy: try one choice per step, O(n log n typically)
D) Greedy fastest but most restrictive

**Answer: D**

**Explanation:**
Brute force: always correct, impractical for large n. DP: correct for problems with optimal substructure + overlapping subproblems. Greedy: correct only with greedy-choice property. Speed: greedy > DP > brute force. Applicability: brute force > DP > greedy. Use greedy when provably correct; DP when greedy fails; brute force as baseline.

---

**Q23.14: Intermediate - [Theory] - [Optimal Merge Pattern]**

Optimal merge pattern (merge files):

A) Merge n sorted files — order affects total cost
B) Like Huffman: always merge two smallest first
C) Minimum total merge cost
D) O(n log n) using priority queue

**Answer: D**

**Explanation:**
Merging sorted files: cost = sum of merged sizes. Merging large files early = more cost (they're part of more subsequent merges). Merge two smallest: largest files merged last (fewest times). Identical to Huffman coding structure. PQ: extract two smallest, merge, insert result. Total: O(n log n). Optimal by Huffman's proof.

---

**Q23.15: Intermediate - [Theory] - [Minimum Platforms]**

Minimum platforms at railway station:

A) Given arrival and departure times
B) Sort events, sweep: +1 for arrival, -1 for departure
C) Maximum concurrent trains = minimum platforms
D) O(n log n) — same as interval partitioning

**Answer: D**

**Explanation:**
Event sweep: create events (time, type). Sort by time (departure before arrival on tie — leaving frees platform before arriving needs one). Sweep: track current concurrent. Max concurrent = answer. O(n log n). Alternative: sort arrivals and departures separately, two-pointer merge.

---

**Q23.16: Advanced - [Theory] - [Greedy for Graph Coloring]**

Greedy graph coloring:

A) Process vertices in some order, assign smallest available color
B) Uses at most Δ+1 colors (Δ = max degree)
C) Not optimal in general (optimal coloring is NP-hard)
D) All of the above

**Answer: D**

**Explanation:**
Greedy coloring: for each vertex in order, use smallest color not used by neighbors. At most Δ+1 colors (each vertex has ≤ Δ neighbors, at most Δ colors used). Vertex ordering matters: good orderings give fewer colors. Optimal chromatic number: NP-hard. Greedy is heuristic. Perfect for 2-colorable (bipartite) graphs.

---

**Q23.17: Advanced - [Theory] - [Scheduling with Penalties]**

Job scheduling with deadlines and penalties:

A) Each job: deadline, penalty if missed
B) Schedule to minimize total penalty (or maximize total profit)
C) Sort by penalty/profit descending, greedily assign to latest available slot
D) O(n²) or O(n log n) with DSU

**Answer: D**

**Explanation:**
Weighted job scheduling: each job takes unit time, has deadline and profit. Sort by profit descending. For each job: assign to latest available slot ≤ deadline. O(n²) with linear scan for slot. O(n log n) with DSU: parent of slot points to next available slot. Matroid-based greedy works because job scheduling forms a matroid.

---

**Q23.18: Expert - [Theory] - [Online Greedy Algorithms]**

Online greedy (decisions before seeing all input):

A) Competitive ratio: online/optimal
B) Secretary problem: 1/e ≈ 37% success rate
C) Ski rental: buy vs rent, competitive ratio 2
D) All of the above

**Answer: D**

**Explanation:**
Online algorithms: make irrevocable decisions as input arrives. Secretary problem: observe first n/e candidates, then pick next one better than all seen. 1/e probability of selecting best. Ski rental: rent costs $1/day, buy costs $B. Strategy: rent B-1 days then buy. Competitive ratio: 2-1/B. Online algorithms: fundamental in theoretical CS and real-world (caching, paging).

---

**Q23.19: Intermediate - [Theory] - [Task Scheduling with Profits]**

Weighted activity selection (intervals with weights):

A) Select non-overlapping intervals maximizing total weight
B) Greedy doesn't work (must consider weights)
C) DP: sort by finish, binary search for last compatible
D) O(n log n) DP, not pure greedy

**Answer: D**

**Explanation:**
Weighted: greedy (earliest finish) ignores weights. May skip heavy interval for two light ones. DP: dp[i] = max(dp[i-1], profit[i] + dp[p(i)]) where p(i) = last compatible with i. Binary search for p(i). O(n log n). Shows boundary where greedy fails and DP is needed. Unweighted: greedy suffices.

---

**Q23.20: Foundational - [Theory] - [Coin Change Greedy]**

Greedy for coin change (specific denominations):

A) US coins (1,5,10,25): greedy works (use largest first)
B) Not all denominations: {1,3,4} amount 6, greedy=4+1+1=3 coins, optimal=3+3=2
C) Greedy works when denomination system is canonical
D) All of the above

**Answer: D**

**Explanation:**
Canonical coin systems: greedy gives minimum coins. US coins, Euro coins: canonical. Test: for non-canonical systems, greedy fails for some amount. Characterizing canonical systems is itself a research problem. When in doubt: use DP for coin change. Greedy for standard currency systems.

---

**Q23.21: Advanced - [Theory] - [Set Cover Greedy]**

Greedy approximation for set cover:

A) NP-hard to solve optimally
B) Greedy: pick set covering most uncovered elements
C) O(log n)-approximation ratio (provably near-best possible)
D) All of the above

**Answer: D**

**Explanation:**
Set cover: cover universe with minimum sets from collection. NP-hard. Greedy: iteratively pick set covering most uncovered elements. Approximation ratio: H_n = ln(n) + 1 ≈ O(log n). Provably near-optimal: unless P=NP, no polynomial algorithm achieves (1-ε)ln(n). Greedy is both practical and theoretically justified.

---

**Q23.22: Intermediate - [Theory] - [Minimum Spanning Tree as Greedy]**

MST algorithms are greedy:

A) Kruskal's: greedily add lightest safe edge
B) Prim's: greedily extend with cheapest neighboring edge
C) Both: locally optimal choices lead to global optimum
D) Correctness: cut property provides greedy-choice property

**Answer: D**

**Explanation:**
MST algorithms: textbook greedy examples. Cut property: lightest edge crossing any cut is in MST (greedy choice). Optimal substructure: MST of contracted graph is part of overall MST. Kruskal's and Prim's both exploit this. See Chapter 21 for details. MST is the classic "greedy works" example.

---

**Q23.23: Advanced - [Theory] - [Greedy for Scheduling to Minimize Completion Time]**

Minimize average completion time (single machine):

A) Sort by processing time ascending (Shortest Job First)
B) SJF minimizes average (and total) completion time
C) Weighted: sort by p_i / w_i ascending (Smith's rule)
D) All of the above

**Answer: D**

**Explanation:**
SJF: shortest job first. Total completion = sum of finish times. Short jobs first: each job's start delayed minimally. Proof by exchange: swapping longer job before shorter only increases total. Weighted: each job has weight w_i (importance). Minimize weighted completion: sort by processing_time/weight. Smith's rule (1956). Elegant greedy result.

---

**Q23.24: Expert - [Theory] - [Greedy Randomized Adaptive Search]**

GRASP (Greedy Randomized Adaptive Search Procedure):

A) Metaheuristic combining greedy construction with local search
B) Construction: build solution using randomized greedy choices
C) Improvement: local search to refine
D) Repeat, keep best — no optimality guarantee but practical

**Answer: D**

**Explanation:**
GRASP: for NP-hard optimization problems. Phase 1: greedily build feasible solution with randomness (don't always pick best, pick from top-k candidates randomly). Phase 2: local search to improve. Repeat many times. No worst-case guarantee but effective in practice for scheduling, facility location, graph optimization.

---

**Q23.25: Foundational - [Theory] - [Greedy Applications Summary]**

Greedy algorithm applications:

A) Scheduling: activity selection, EDF, SJF
B) Graph: MST (Kruskal/Prim), Dijkstra
C) Coding: Huffman, prefix-free codes
D) All of the above — plus fractional knapsack, set cover approx

**Answer: D**

**Explanation:**
Greedy succeeds in many areas: scheduling (earliest deadline/shortest job), graphs (MST, Dijkstra), compression (Huffman), resource allocation (fractional knapsack). For NP-hard problems: greedy gives good approximations (set cover, vertex cover). Key skill: recognizing when greedy works, proving it, and knowing when to switch to DP.

---

**Q23.26: Foundational - [Theory] - [Greedy Proof Technique: Exchange Argument]**

Exchange argument for greedy correctness:

A) Assume optimal solution O differs from greedy solution G
B) Show you can transform O to be "more like G" without increasing cost
C) By induction: G is optimal
D) All of the above

**Answer: D**

**Explanation:**
Exchange argument: powerful proof technique. Start with any optimal solution. If it differs from greedy at some step, swap that choice to match greedy. Show swap doesn't worsen solution. Repeat until optimal = greedy. Used for: activity selection, Huffman, scheduling. Alternative proof technique: "greedy stays ahead" — at each step, greedy is at least as good.

---

**Q23.27: Intermediate - [Theory] - [Task Scheduling with Deadlines and Penalties]**

Schedule tasks on single machine to minimize late penalties:

A) Each task has deadline and penalty for missing it
B) Greedy: sort by penalty (highest first), schedule as late as possible before deadline
C) Use Union-Find to find latest available slot efficiently
D) O(n log n) with sorting + Union-Find

**Answer: D**

**Explanation:**
Task scheduling with penalties: maximize total penalty of on-time tasks (equivalently minimize late penalties). Sort by penalty descending. For each task: find latest free slot ≤ deadline (Union-Find: find(d) gives latest available slot before d). Schedule there. O(n α(n)) per query. Total: O(n log n) sort + O(n α(n)) scheduling. Matroid-based proof of correctness.

---

**Q23.28: Foundational - [Theory] - [MST as Greedy (Review)]**

Why MST algorithms are greedy:

A) Kruskal's: always add cheapest edge that doesn't form cycle
B) Prim's: always add cheapest edge connecting MST to non-MST vertex
C) Both make locally optimal choices that lead to global optimum
D) Correctness guaranteed by cut property (Chapter 21)

**Answer: D**

**Explanation:**
MST algorithms: quintessential greedy success. Kruskal's: greedy on globally sorted edges. Prim's: greedy on local frontier. Both proven optimal via cut property. Contrast with shortest path Dijkstra (also greedy — always relax nearest vertex). MST/Dijkstra share structure: greedy choice + optimality proof. See Chapter 21 for detailed MST coverage.

---

**Q23.29: Intermediate - [Trace] - [Gas Station / Circular Route]**

Gas station problem: n stations in circle, gas[i] and cost[i] to next:

A) Greedy: track cumulative surplus (gas - cost)
B) If total gas ≥ total cost: solution exists
C) Start at station after the point of minimum cumulative surplus
D) O(n) solution

**Answer: D**

**Explanation:**
Circular route: if total gas ≥ total cost, feasible. Find starting point: compute cumulative surplus. Point of minimum cumulative surplus: starting just after it guarantees you never run out. Proof: starting there means you begin with maximum deficit already behind you. One pass O(n). Classic greedy problem — local information (surplus) determines global strategy.

---

**Q23.30: Foundational - [Theory] - [Jump Game]**

Jump game: array where arr[i] = max jump from position i. Can you reach the end?

A) Greedy: track farthest reachable position
B) For each position i ≤ farthest: update farthest = max(farthest, i + arr[i])
C) If farthest ≥ n-1: reachable
D) O(n) time, O(1) space

**Answer: D**

**Explanation:**
Jump game: maintain farthest reachable index. Scan left to right. At each reachable position: update farthest. If current position > farthest: unreachable (gap). If farthest ≥ last index: reachable. Simple greedy. Variant: minimum jumps to reach end — track current range end and next range end. Still O(n).

---

**Q23.31: Intermediate - [Theory] - [Minimum Deletions for Sorted Sequence]**

Minimum deletions to make array sorted:

A) Keep longest non-decreasing subsequence (LIS variant)
B) Delete n - LIS_length elements
C) Greedy with binary search gives O(n log n)
D) All of the above

**Answer: D**

**Explanation:**
Minimum deletions = n - LIS length. Finding LIS: patience sorting / binary search O(n log n). Keep sorted tails array, binary search for insertion position. Greedy: always extend LIS if possible, else replace smallest larger element. This "greedy within DP" approach is optimal. Chapter 22 covers LIS DP in detail.

---

**Q23.32: Intermediate - [Theory] - [Assign Cookies]**

Assign cookies: child i has greed g[i], cookie j has size s[j]:

A) Sort children by greed, cookies by size
B) Greedily give smallest sufficient cookie to least greedy child
C) Maximizes number of content children
D) O(n log n) sorting

**Answer: D**

**Explanation:**
Cookie assignment: match smallest adequate cookie to least demanding child. Proof by exchange: if you give a bigger cookie to a less greedy child, swapping can't decrease total. Two-pointer after sorting: advance child pointer when matched, always advance cookie pointer. Classic greedy matching problem.

---

**Q23.33: Intermediate - [Theory] - [Boats to Save People]**

Boats to save people: each boat holds max two people with weight limit:

A) Sort people by weight
B) Try pairing lightest with heaviest
C) If pair fits: both go, else heaviest goes alone
D) Two-pointer: O(n log n) total

**Answer: D**

**Explanation:**
Boat pairing: sort weights. Two pointers: lightest (left) and heaviest (right). If left + right ≤ limit: pair them (both pointers move). Else: heaviest goes alone (right moves). Each step uses one boat. Proof: pairing lightest with heaviest is never worse than any other pairing. Minimizes total boats.

---

**Q23.34: Intermediate - [Trace] - [Meeting Rooms II]**

Minimum meeting rooms needed: meetings [(0,30),(5,10),(15,20)]:

A) Sort by start time: (0,30),(5,10),(15,20)
B) Use min-heap of end times
C) (0,30): heap=[30]. (5,10): 5<30, new room, heap=[10,30]. (15,20): 15≥10, reuse, heap=[20,30]
D) Max heap size = 2 rooms needed

**Answer: D**

**Explanation:**
Meeting rooms: sweep line approach. Sort by start. Min-heap tracks earliest ending room. New meeting: if starts after earliest end → reuse that room (replace in heap). Else: new room (push to heap). Max heap size = answer. O(n log n). Alternative: sort all start/end events, sweep with counter. Same result.

---

**Q23.35: Intermediate - [Theory] - [Non-Overlapping Intervals]**

Maximum non-overlapping intervals (equivalently, minimum removals):

A) Sort by end time (earliest finish first)
B) Greedily pick next interval that doesn't overlap with last picked
C) Same as activity selection problem
D) All of the above — O(n log n)

**Answer: D**

**Explanation:**
Non-overlapping intervals = activity selection. Sort by end time. Greedily select: if current start ≥ last end, include it. Count included = max non-overlapping. Minimum removals = n - count. Proof: earliest ending leaves most room. Classic greedy. Variant: weighted interval scheduling needs DP.

---

**Q23.36: Intermediate - [Theory] - [Partition Labels]**

Partition string into maximum parts where each letter appears in at most one part:

A) Record last occurrence of each character
B) Greedily extend current partition to cover all last occurrences
C) When current position = partition end: cut
D) O(n) with one preprocessing pass

**Answer: D**

**Explanation:**
Partition labels: for each char, find last index. Scan left to right: extend partition end to max(end, last[char]). When i == end: partition boundary found. Start new partition. Greedy: extend as little as needed but as much as required. Each character contained in exactly one partition. O(n) time, O(1) space (26 letters).

---

**Q23.37: Intermediate - [Theory] - [Minimum Arrows to Burst Balloons]**

Minimum arrows to burst balloons (intervals on number line):

A) Each arrow at position x bursts all balloons containing x
B) Sort balloons by end coordinate
C) Shoot at first balloon's end — bursts all overlapping
D) Greedy: O(n log n), equivalent to interval partitioning

**Answer: D**

**Explanation:**
Balloon shooting = minimum points to hit all intervals. Sort by right endpoint. Shoot at first balloon's right end. All balloons containing this point: burst. Move to next un-burst balloon, repeat. Proof: shooting later can only miss more balloons. O(n log n). Same as "minimum number of intervals to cover all points" (dual problem).

---

**Q23.38: Advanced - [Theory] - [Reorganize String]**

Reorganize string so no two adjacent characters are same:

A) Count character frequencies
B) If any character has count > (n+1)/2: impossible
C) Greedy: always place most frequent remaining character (max-heap)
D) O(n log k) where k = alphabet size

**Answer: D**

**Explanation:**
Reorganize: max-heap of (count, char). Pop most frequent, place it. If previous char still has count > 0: push back. Ensures no two adjacent same. Impossible only if max_count > ⌈n/2⌉. Alternative: interleave positions (even indices first with most frequent). O(n log 26) = O(n). Related: task scheduler with cooldown.

---

**Q23.39: Foundational - [Theory] - [Container with Most Water]**

Container with most water: heights array, find two lines forming max area:

A) Two pointers: left=0, right=n-1
B) Area = min(h[left], h[right]) × (right-left)
C) Move the shorter pointer inward
D) O(n) — greedy shrinks width while seeking height gain

**Answer: D**

**Explanation:**
Two-pointer greedy: start with widest container. Area limited by shorter line. Moving shorter line inward: might find taller line (area could increase). Moving taller line: can only decrease (shorter stays same or decreases, width decreases). So always move shorter. O(n) scan. Proof: any container has both lines between or at our pointers at some point.

---

**Q23.40: Advanced - [Theory] - [Task Scheduler with Cooldown]**

Task scheduler: tasks with cooldown n between same tasks:

A) Most frequent task determines minimum time
B) Gaps between most frequent: (max_count - 1) × (cooldown + 1) + count_of_max_freq_tasks
C) Answer: max(len(tasks), formula above)
D) O(n) calculation after frequency count

**Answer: D**

**Explanation:**
Task scheduler: greedy/math. Most frequent task F appears f times. Must have ≥ (f-1) gaps of size (cooldown+1). Fill gaps with other tasks. If enough tasks: no idle time → answer = total tasks. If not enough: idle slots remain. Formula: max(total_tasks, (f-1)×(n+1) + count_of_tasks_with_freq_f). O(n) total.

---

**Q23.41: Intermediate - [Trace] - [Candy Distribution]**

Candy distribution: each child gets at least 1, higher-rated child gets more than neighbor:

A) Left pass: if rating[i] > rating[i-1]: candy[i] = candy[i-1] + 1, else 1
B) Right pass: if rating[i] > rating[i+1]: candy[i] = max(candy[i], candy[i+1] + 1)
C) Ratings [1,0,2]: Left pass [1,1,2], Right pass [2,1,2], total = 5
D) O(n) time, O(n) space

**Answer: D**

**Explanation:**
Candy: two-pass greedy. Left pass ensures right-neighbor constraint. Right pass ensures left-neighbor constraint. Take max to satisfy both. Ratings [1,0,2]: left [1,1,2], right [2,1,2] → total 5 candies. Minimum candies while satisfying all constraints. Single-pass solution exists using slope analysis but more complex.

---

**Q23.42: Intermediate - [Theory] - [Minimum Cost to Connect Sticks]**

Minimum cost to connect n sticks (cost = sum of two sticks joined):

A) Always join two shortest sticks first
B) Use min-heap to efficiently find shortest
C) Same as optimal merge pattern / Huffman
D) O(n log n)

**Answer: D**

**Explanation:**
Connect sticks: cost of joining two sticks = their combined length (paid once). Later joins: longer combined sticks contribute to future costs. Join shortest first to minimize total. Exactly the same problem as Huffman coding (merge two smallest) and optimal merge pattern. Min-heap: extract two smallest, push their sum, repeat. Total cost = sum of all intermediate merges.

---

**Q23.43: Foundational - [Theory] - [When Greedy Fails]**

When greedy algorithms fail:

A) 0/1 Knapsack: greedy by value/weight ratio doesn't give optimal
B) Longest path: greedy extension doesn't work
C) Traveling Salesman: nearest neighbor heuristic not optimal
D) All of the above — need DP or exhaustive search instead

**Answer: D**

**Explanation:**
Greedy fails when locally optimal ≠ globally optimal and no matroid structure exists. 0/1 knapsack: items {value:60,weight:10}, {value:100,weight:20}, {value:120,weight:30}, capacity 50. Greedy ratio: picks item 1(6) + item 2(5) = 160. Optimal: item 2 + item 3 = 220. Always verify greedy with counterexample or proof before trusting.

---

**Q23.44: Advanced - [Theory] - [Greedy Approximation Algorithms]**

Greedy as approximation for NP-hard problems:

A) Set cover: greedy gives O(log n) approximation
B) Vertex cover: pick both endpoints of any edge → 2-approximation
C) TSP: nearest neighbor → O(log n) approximation on metric instances
D) All provide guaranteed bounds

**Answer: D**

**Explanation:**
Greedy approximations: when optimal is NP-hard, greedy with provable bounds is valuable. Set cover greedy: O(ln n) factor — best possible unless P=NP for polynomial algorithms. Vertex cover 2-approx: simple and tight. TSP: nearest neighbor up to O(log n) factor, Christofides 1.5-factor (uses MST + matching). Greedy gives fast, bounded solutions.

---

**Q23.45: Expert - [Theory] - [Online Greedy and Secretary Problem]**

Secretary problem (optimal stopping):

A) Interview n candidates sequentially, hire/reject immediately
B) Optimal: reject first n/e candidates, then hire first one better than all seen
C) Probability of hiring best: ~1/e ≈ 36.8%
D) All of the above — foundation of online algorithm theory

**Answer: D**

**Explanation:**
Secretary problem: online decision-making under uncertainty. Optimal strategy: observe first ⌊n/e⌋ candidates (calibration phase), then hire first candidate better than all observed. Success probability → 1/e as n→∞. Generalizations: multiple hires (k-secretary), weighted choices, random order models. Foundation for: online auctions, prophet inequalities, streaming algorithms.

---

## Chapter 23 Summary

| Category | Count | Topics Covered |
|----------|-------|----------------|
| Foundational | 12 | Activity selection, Huffman, fractional knapsack, coin change, greedy vs DP, exchange argument, jump game, MST review, container, when greedy fails |
| Intermediate | 20 | Interval scheduling/partitioning, job scheduling, optimal merge, platforms, weighted selection, gas station, minimum deletions, assign cookies, boats, meeting rooms, non-overlapping, partition labels, balloons, candy, connect sticks, counting partitions |
| Advanced | 8 | Matroids, set cover, graph coloring, scheduling rules, reorganize string, task scheduler, greedy approximation |
| Expert | 5 | Online greedy, GRASP, competitive analysis, secretary problem |

**Total MCQs: 45** | **Target Met: ✓**

**Next:** Chapter 24 - Divide & Conquer
