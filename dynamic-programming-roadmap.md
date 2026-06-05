# Dynamic Programming Roadmap

Refined, study-ordered roadmap for interview preparation. This version is organized for navigation, not just reference.

## Index

- [Module Files](#module-files)
- [How to Use](#how-to-use)
- [Priority Legend](#priority-legend)
- [Quick Mental Index](#quick-mental-index)
- [1. Foundations and Warmup](#1-foundations-and-warmup)
- [2. 1D Linear and Prefix DP](#2-1d-linear-and-prefix-dp)
- [3. Decision and Take-or-Skip DP](#3-decision-and-take-or-skip-dp)
- [4. Target Knapsack and Counting DP](#4-target-knapsack-and-counting-dp)
- [5. Grid DP](#5-grid-dp)
- [6. Two-Sequence String DP](#6-two-sequence-string-dp)
- [7. Interval and Palindrome DP](#7-interval-and-palindrome-dp)
- [8. LIS and Transition-Heavy DP](#8-lis-and-transition-heavy-dp)
- [9. State-Machine DP](#9-state-machine-dp)
- [10. Tree DP](#10-tree-dp)
- [11. DAG and Graph DP](#11-dag-and-graph-dp)
- [12. Optional Mastery Layer](#12-optional-mastery-layer)
- [High-ROI Order for MAANG Prep](#high-roi-order-for-maang-prep)

## Module Files

- [Module 1 - Foundations and Warmup](modules/01-foundations-and-warmup.md)
- [Module 2 - 1D Linear and Prefix DP](modules/02-1d-linear-and-prefix-dp.md)
- [Module 3 - Decision and Take-or-Skip DP](modules/03-decision-and-take-or-skip-dp.md)
- [Module 4 - Target Knapsack and Counting DP](modules/04-target-knapsack-and-counting-dp.md)
- [Module 5 - Grid DP](modules/05-grid-dp.md)
- [Module 6 - Two-Sequence String DP](modules/06-two-sequence-string-dp.md)
- [Module 7 - Interval and Palindrome DP](modules/07-interval-and-palindrome-dp.md)
- [Module 8 - LIS and Transition-Heavy DP](modules/08-lis-and-transition-heavy-dp.md)
- [Module 9 - State-Machine DP](modules/09-state-machine-dp.md)
- [Module 10 - Tree DP](modules/10-tree-dp.md)
- [Module 11 - DAG and Graph DP](modules/11-dag-and-graph-dp.md)
- [Module 12 - Optional Mastery Layer](modules/12-optional-mastery-layer.md)

## How to Use

- Study the sections from top to bottom.
- Each problem has one primary home to reduce repetition.
- For every problem, write these five lines before coding: state, transition, base case, iteration order, final answer location.
- Solve in this order whenever possible: recursion, memoization, tabulation, space optimization.
- Move on only when you can explain the section's state shape without looking at notes.

## Priority Legend

- `Must do`: core interview coverage.
- `Good to do`: broadens pattern fluency.
- `Stretch`: harder or less frequent, but valuable.

## Quick Mental Index

| State shape | Typical meaning | Main buckets |
| --- | --- | --- |
| `dp[i]` | best answer up to index or prefix `i` | foundations, 1D DP, decision DP |
| `dp[target]` or `dp[i][cap]` | answer for a target sum or capacity | knapsack, subset, counting |
| `dp[r][c]` | answer at grid cell `(r, c)` | grid DP |
| `dp[i][j]` | answer for two prefixes or two sequences | two-sequence string DP |
| `dp[l][r]` | answer for interval `[l, r]` | interval and palindrome DP |
| `dp[i][state]` | answer at index or day `i` with a mode | state-machine DP |
| `dp[node][state]` | answer in a subtree with a condition | tree DP |
| `memo(node)` or topo order | answer for a DAG node or graph state | DAG and graph DP |

## 1. Foundations and Warmup

**Focus:** build the DP workflow and learn to translate brute force recursion into reusable states.

**Subtopics**

- Recursion basics
- Overlapping subproblems
- Optimal substructure
- Memoization with arrays or maps
- Tabulation order
- Base cases and boundary handling
- Time and space complexity awareness

**Core pattern**

Start with brute force recursion, identify repeated states, cache them, then convert the same recurrence into bottom-up computation.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 70 - Climbing Stairs | first clean recurrence and memo-to-tabulation conversion |
| Must do | LC 746 - Min Cost Climbing Stairs | introduces min-cost transitions |
| Good to do | LC 509 - Fibonacci Number | smallest possible DP state model |
| Good to do | LC 1137 - N-th Tribonacci Number | adds wider lookback without changing the idea |

**Ready to move on when**

- You can explain what overlapping subproblems and optimal substructure mean in your own words.
- You can derive `dp[i]` and write both memoized and tabulated versions for a simple recurrence.

## 2. 1D Linear and Prefix DP

**Focus:** solve problems where one linear state captures the answer for a prefix, suffix, or position.

**Subtopics**

- Prefix DP
- Count, min, max, and boolean forms
- Fixed-lookback transitions
- Variable jump or window transitions
- Prefix segmentation on strings
- Rolling-state optimization

**Core pattern**

`dp[i]` stores the answer for position or prefix `i`, and transitions come from a small set of earlier positions or valid cuts.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 91 - Decode Ways | classic prefix counting DP |
| Must do | LC 139 - Word Break | prefix validity and cut-based transitions |
| Must do | LC 983 - Minimum Cost For Tickets | variable jump transitions over days |
| Must do | LC 2140 - Solving Questions With Brainpower | skip-ahead recurrence on one dimension |

**Ready to move on when**

- You can tell whether the problem is asking for count, min/max, or feasibility.
- You can decide whether a transition comes from `i - 1`, `i - 2`, or from all valid earlier cuts.

## 3. Decision and Take-or-Skip DP

**Focus:** learn the inclusion-exclusion style of DP where each step is a choice between taking the current option or skipping it.

**Subtopics**

- Take vs skip
- Inclusion and exclusion
- Non-adjacent constraints
- Circular array handling
- Frequency transformation into linear DP

**Core pattern**

At each state, compute the best result for taking the current option and compare it with skipping the current option.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 198 - House Robber | the canonical take-or-skip problem |
| Must do | LC 213 - House Robber II | same pattern with circular constraint |
| Must do | LC 740 - Delete and Earn | transforms values into house-robber style DP |

**Ready to move on when**

- You can write `take` and `skip` states without confusion.
- You can recognize when a problem is secretly a transformed House Robber variant.

## 4. Target Knapsack and Counting DP

**Focus:** build DP over target sums, capacities, and feasibility states.

**Subtopics**

- 0/1 knapsack
- Unbounded knapsack
- Subset sum
- Partition DP
- Min-coin DP
- Count-ways DP
- Boolean feasibility DP
- Order matters vs order does not matter
- Forward vs reverse loop order

**Core pattern**

`dp[target]` or `dp[i][cap]` tracks whether a target is reachable, the minimum or maximum value for it, or the number of ways to build it.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 322 - Coin Change | unbounded knapsack for minimization |
| Must do | LC 518 - Coin Change II | unbounded knapsack for combinations |
| Must do | LC 416 - Partition Equal Subset Sum | 0/1 feasibility DP |
| Must do | LC 494 - Target Sum | subset transformation and counting |
| Good to do | LC 377 - Combination Sum IV | order-sensitive counting |
| Good to do | LC 279 - Perfect Squares | unbounded knapsack in disguise |
| Good to do | LC 474 - Ones and Zeroes | two-dimensional capacity DP |
| Good to do | LC 1049 - Last Stone Weight II | subset partition optimization |
| Stretch | LC 1155 - Number of Dice Rolls With Target Sum | count DP with modulo arithmetic |
| Stretch | LC 879 - Profitable Schemes | multidimensional counting DP |

**Ready to move on when**

- You can tell when to use reverse iteration for 0/1 choices and forward iteration for unbounded reuse.
- You can separate feasibility, minimization, and counting versions of the same target DP idea.

## 5. Grid DP

**Focus:** solve path and cell-based problems where each state belongs to a matrix position.

**Subtopics**

- Path counting
- Minimum or maximum path sum
- Obstacles and blocked cells
- Right and down traversal
- Reverse traversal when required
- Falling-path transitions
- Square-building DP
- Boundary initialization and padding

**Core pattern**

`dp[r][c]` stores the answer for cell `(r, c)`, using information from allowed predecessor cells.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 62 - Unique Paths | pure counting on a grid |
| Must do | LC 63 - Unique Paths II | same pattern with blocked cells |
| Must do | LC 64 - Minimum Path Sum | path optimization on a grid |
| Must do | LC 120 - Triangle | compact grid DP with bottom-up option |
| Good to do | LC 931 - Minimum Falling Path Sum | multiple predecessor choices per cell |
| Good to do | LC 221 - Maximal Square | local square-building recurrence |
| Good to do | LC 1277 - Count Square Submatrices with All Ones | counting extension of maximal square |
| Stretch | LC 174 - Dungeon Game | reverse-direction DP with health constraints |

**Ready to move on when**

- You can initialize first row and first column correctly without trial and error.
- You can tell when forward traversal works and when reverse traversal is cleaner.

## 6. Two-Sequence String DP

**Focus:** solve problems where the answer depends on prefixes of two strings or two sequences.

**Subtopics**

- Prefix-vs-prefix state
- Match vs mismatch transitions
- Longest common subsequence pattern
- Edit-distance pattern
- Subsequence counting
- Interleaving and alignment
- Base row and base column setup

**Core pattern**

`dp[i][j]` represents the answer for the first `i` characters or elements of one sequence and the first `j` of another.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 1143 - Longest Common Subsequence | the core two-sequence DP pattern |
| Must do | LC 72 - Edit Distance | insert, delete, replace transitions |
| Must do | LC 115 - Distinct Subsequences | counting subsequences across two strings |
| Must do | LC 97 - Interleaving String | boolean DP on two prefixes |
| Good to do | LC 1035 - Uncrossed Lines | LCS in array form |
| Good to do | LC 712 - Minimum ASCII Delete Sum for Two Strings | weighted edit-style DP |
| Good to do | LC 1092 - Shortest Common Supersequence | reconstruction after LCS reasoning |
| Good to do | LC 718 - Maximum Length of Repeated Subarray | substring-style recurrence in 2D |

**Ready to move on when**

- You can define whether `i` and `j` mean indices or prefix lengths and stay consistent.
- You can fill the base row and base column correctly before coding the recurrence.

## 7. Interval and Palindrome DP

**Focus:** solve problems where the answer is defined on a subarray or substring range.

**Subtopics**

- Interval state `dp[l][r]`
- Solve by increasing length
- Split-at-`k` transitions
- Shrink-from-both-ends transitions
- Merge-cost DP
- Palindrome interval DP

**Core pattern**

`dp[l][r]` stores the answer for interval `[l, r]`, and transitions depend on smaller intervals inside it.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 647 - Palindromic Substrings | interval reasoning on string ranges |
| Must do | LC 516 - Longest Palindromic Subsequence | classic shrink-from-both-ends DP |
| Must do | LC 312 - Burst Balloons | split-at-last-choice interval DP |
| Good to do | LC 5 - Longest Palindromic Substring | interval thinking, even if center expansion is also valid |
| Good to do | LC 1130 - Minimum Cost Tree From Leaf Values | partition-based interval DP |
| Good to do | LC 664 - Strange Printer | interval compression and merging |
| Stretch | LC 1000 - Minimum Cost to Merge Stones | hard merge-cost DP |
| Stretch | LC 1690 - Stone Game VII | score-difference interval DP |

**Ready to move on when**

- You can decide whether to iterate by interval length or by left boundary first.
- You can spot when the right state is a range instead of a prefix.

## 8. LIS and Transition-Heavy DP

**Focus:** handle problems where each state may transition from many earlier valid states instead of a fixed number of predecessors.

**Subtopics**

- Transition from all previous valid states
- `O(n^2)` LIS reasoning
- Counting LIS variants
- Chain-building DP
- Partition DP with variable previous cut
- LIS optimization with binary search

**Core pattern**

`dp[i]` stores the best answer ending at index `i`, and transitions may come from every earlier index `j` that satisfies a validity condition.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 300 - Longest Increasing Subsequence | the base pattern for all-previous transitions |
| Must do | LC 673 - Number of Longest Increasing Subsequence | adds counting on top of LIS |
| Must do | LC 1048 - Longest String Chain | chain-building with predecessor relation |
| Good to do | LC 1043 - Partition Array for Maximum Sum | variable-length partition transitions |
| Good to do | LC 1105 - Filling Bookcase Shelves | segmented transitions with layout constraints |
| Good to do | LC 813 - Largest Sum of Averages | partition optimization over prefixes |
| Good to do | LC 1395 - Count Number of Teams | counting from previous valid states |

**Ready to move on when**

- You can recognize when `dp[i]` depends on all earlier valid `j`, not just `i - 1` or `i - 2`.
- You understand that `O(n log n)` LIS is an optimization for LIS itself, not a replacement for general DP reasoning.

## 9. State-Machine DP

**Focus:** model each index or day with a small number of modes such as holding, not holding, cooling down, or having limited transactions left.

**Subtopics**

- Multiple states per day or index
- Holding vs not holding
- Cooldown states
- Transaction fee states
- Transaction-limit states
- State compression

**Core pattern**

`dp[i][state]` stores the best answer on day or index `i` while being in a specific mode, and transitions switch between modes based on the action taken.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 121 - Best Time to Buy and Sell Stock | simplest hold/not-hold model |
| Must do | LC 122 - Best Time to Buy and Sell Stock II | repeated transactions with simple states |
| Must do | LC 309 - Best Time to Buy and Sell Stock with Cooldown | adds a cooldown state |
| Must do | LC 714 - Best Time to Buy and Sell Stock with Transaction Fee | adds a fee to transitions |
| Good to do | LC 123 - Best Time to Buy and Sell Stock III | limited-transaction state expansion |
| Stretch | LC 188 - Best Time to Buy and Sell Stock IV | generalized transaction count DP |

**Ready to move on when**

- You can draw the states and transitions before coding.
- You understand why stock problems are better viewed as finite-state DP than as ad hoc formulas.

## 10. Tree DP

**Focus:** compute answers over subtrees where the parent decision changes what children are allowed to do.

**Subtopics**

- Subtree answers
- Postorder traversal
- Include or exclude node logic
- Parent-child dependency handling
- Two-state node DP

**Core pattern**

`dp[node][state]` stores the answer for the subtree rooted at `node` under a condition such as taking or not taking the node.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 337 - House Robber III | house-robber logic lifted to trees |
| Must do | LC 968 - Binary Tree Cameras | multi-state postorder DP on a tree |
| Stretch | LC 834 - Sum of Distances in Tree | introduces rerooting-style tree DP |

**Ready to move on when**

- You can explain why postorder traversal is usually the natural direction for tree DP.
- You can define child-to-parent return values cleanly.

## 11. DAG and Graph DP

**Focus:** solve problems where states form an acyclic dependency graph and each state should be computed once.

**Subtopics**

- Memoized DFS on DAG-like states
- Topological-order DP
- Longest path on acyclic dependencies
- Matrix path problems that behave like DAGs
- Graph states as DP states

**Core pattern**

Compute each state once using DFS plus memoization or topological order, depending on whether the dependency graph is implicit or explicit.

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Must do | LC 329 - Longest Increasing Path in a Matrix | classic DFS plus memoization on an implicit DAG |
| Good to do | LC 2328 - Number of Increasing Paths in a Grid | counting version of graph-flavored DP |
| Good to do | LC 2684 - Maximum Number of Moves in a Grid | path maximization on acyclic moves |
| Stretch | LC 1857 - Largest Color Value in a Directed Graph | topo-DP on an explicit graph |

**Ready to move on when**

- You can explain why DFS plus memoization is still DP when the state graph is acyclic.
- You can recognize when a matrix problem is really a DAG problem in disguise.

## 12. Optional Mastery Layer

**Focus:** advanced DP families that are valuable for deeper mastery but lower priority for mainstream interview prep.

**Subtopics**

- Bitmask DP
- Digit DP
- Probability DP
- Game DP
- Rerooting DP
- State compression DP
- Profile DP

**Representative problems**

| Priority | Problem | Why it belongs here |
| --- | --- | --- |
| Good to do | LC 688 - Knight Probability in Chessboard | probability DP |
| Good to do | LC 1140 - Stone Game II | game-theory flavored interval DP |
| Stretch | LC 847 - Shortest Path Visiting All Nodes | bitmask state compression |
| Stretch | LC 902 - Numbers At Most N Given Digit Set | digit-DP style counting |
| Stretch | LC 834 - Sum of Distances in Tree | rerooting transition on trees |

**When to study this layer**

- Only after you are comfortable with sections 1 through 11.
- Treat these as mastery topics, not prerequisites.

## High-ROI Order for MAANG Prep

1. Foundations and Warmup
2. 1D Linear and Prefix DP
3. Decision and Take-or-Skip DP
4. Target Knapsack and Counting DP
5. Grid DP
6. Two-Sequence String DP
7. Interval and Palindrome DP
8. LIS and Transition-Heavy DP
9. State-Machine DP
10. Tree DP
11. DAG and Graph DP
12. Optional Mastery Layer

If you want a minimal high-return core, finish sections 1 through 10 before spending serious time on section 12.