# AI Unit II – Search Strategies

A complete, exam-oriented study resource for **Artificial Intelligence – Unit II: Search Strategies**.

This single README contains the complete material for:

- State Space Search
- Tree Search and Graph Search
- Uninformed Search
- Breadth-First Search (BFS)
- Uniform-Cost Search (UCS)
- Depth-First Search (DFS)
- Depth-Limited Search (DLS)
- Iterative Deepening DFS (IDDFS)
- Bidirectional Search
- Informed Search
- Best-First Search
- Greedy Best-First Search
- A* Search
- Heuristic Functions
- Admissible Heuristics
- 8-Puzzle Heuristics
- Dominance
- Relaxed Problems
- Local Search
- Hill-Climbing Search
- Local Minima
- Ridge Problem
- Simulated Annealing
- Local Beam Search
- Genetic Algorithms
- Important formulas
- Algorithm comparisons
- Exam questions
- Quick revision

---

## Table of Contents

1. [Unit Overview](#unit-overview)
2. [State Space Search](#state-space-search)
3. [Tree Search and Graph Search](#tree-search-and-graph-search)
4. [Uninformed Search](#uninformed-search)
5. [BFS](#1-breadth-first-search-bfs)
6. [UCS](#2-uniform-cost-search-ucs)
7. [DFS](#3-depth-first-search-dfs)
8. [DLS](#4-depth-limited-search-dls)
9. [IDDFS](#5-iterative-deepening-depth-first-search-iddfs)
10. [Bidirectional Search](#6-bidirectional-search)
11. [Informed Search](#informed-search)
12. [Best-First Search](#best-first-search)
13. [Greedy Best-First Search](#greedy-best-first-search)
14. [A* Search](#a-search)
15. [Heuristics](#heuristic-functions)
16. [Admissible Heuristics](#admissible-heuristics)
17. [8-Puzzle Heuristics](#8-puzzle-heuristics)
18. [Dominance](#dominance-of-heuristics)
19. [Relaxed Problems](#relaxed-problems)
20. [Local Search](#local-search)
21. [Hill Climbing](#hill-climbing-search)
22. [Local Search Difficulties](#local-search-difficulties)
23. [Ridge Problem](#ridge-problem)
24. [Simulated Annealing](#simulated-annealing-search)
25. [Local Beam Search](#local-beam-search)
26. [Genetic Algorithms](#genetic-algorithms)
27. [Comparison](#search-algorithm-comparison)
28. [Formulas](#important-formulas)
29. [Exam Questions](#important-exam-questions)
30. [Quick Revision](#quick-revision)

---

# Unit Overview

Artificial Intelligence can solve many problems by searching through a state space.

```text
                    SEARCH STRATEGIES
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
     State Space      Uninformed        Informed
       Search           Search           Search
                          |                |
                    +-----+-----+      +---+---+
                    |     |     |      |       |
                   BFS   UCS   DFS   Greedy    A*
                    |     |     |      |
                   DLS  IDDFS  ...  Heuristics
                    |
             Bidirectional

                    LOCAL SEARCH
                         |
              +----------+----------+
              |          |          |
         Hill Climbing  SA      Local Beam
                         |
                  Genetic Algorithm
```

---

# State Space Search

State Space Search represents a problem using possible states and transitions between those states.

The basic formulation is:

```text
[S, s, O, G]
```

Where:

- `S` = set of states / next-state function
- `s` = initial state
- `O` = transition operators
- `G` = goal states

The objective is to find a sequence of transitions from the initial state to a goal state.

## Basic Search Process

```text
Initial State
      |
      v
Generate Successors
      |
      v
Select Node
      |
      v
Goal Test
   /       \
 Yes        No
  |          |
Goal       Expand
             |
             v
        Generate More
          States
```

---

# Tree Search and Graph Search

## Tree Search

Tree search can generate the same state multiple times through different paths.

Problems can include:

- Repeated states
- Redundant paths
- Infinite loops

## Graph Search

Graph search maintains an explored set and avoids states already explored or already present in the frontier.

```text
OPEN / FRONTIER
      |
      v
 Select Node
      |
      v
 Goal Test
   /       \
 Yes        No
  |          |
Goal       Expand
             |
             v
       Check OPEN /
        EXPLORED
             |
             v
        Add New States
```

---

# Uninformed Search

Uninformed search is also called **blind search**.

It does not use additional information about which state is more promising.

The main uninformed strategies are:

1. Breadth-First Search
2. Uniform-Cost Search
3. Depth-First Search
4. Depth-Limited Search
5. Iterative Deepening DFS
6. Bidirectional Search

A search strategy mainly determines the order in which nodes are expanded.

---

# 1. Breadth-First Search (BFS)

BFS expands the **shallowest unexpanded node** first.

It uses a:

```text
FIFO Queue
```

FIFO = First In, First Out.

## Example

```text
             A
           /   \
          B     C
         / \   / \
        D   E F   G
```

BFS visits:

```text
A → B → C → D → E → F → G
```

## Steps

1. Start with the initial node.
2. Put it into the frontier.
3. Remove the shallowest node.
4. Test the goal.
5. Expand if it is not the goal.
6. Add successors.
7. Repeat.

## Properties

| Property | BFS |
|---|---|
| Data Structure | FIFO Queue |
| Strategy | Shallowest first |
| Complete | Yes, if `b` is finite |
| Optimal | Yes, if step cost = 1 |
| Time | `O(b^d)` |
| Space | `O(b^d)` |

Where:

- `b` = branching factor
- `d` = depth of shallowest solution

**Main disadvantage:** high memory usage.

---

# 2. Uniform-Cost Search (UCS)

UCS expands the node with the **lowest path cost**.

It uses a priority queue ordered by:

```text
g(n)
```

where:

```text
g(n) = cost from the initial state to n
```

Example:

```text
A → B = 5
A → C = 2
A → D = 8
```

UCS selects `C` because:

```text
g(C) = 2
```

## BFS vs UCS

```text
BFS → lowest depth
UCS → lowest path cost
```

If all step costs are equal, UCS is equivalent to BFS.

## Properties

| Property | UCS |
|---|---|
| Data Structure | Priority Queue |
| Evaluation | `g(n)` |
| Complete | Yes, if step cost is positive |
| Optimal | Yes |

The goal test is applied when a node is selected for expansion.

---

# 3. Depth-First Search (DFS)

DFS expands the **deepest unexpanded node** first.

It uses:

```text
LIFO Queue / Stack
```

LIFO = Last In, First Out.

Example:

```text
             A
           /   \
          B     C
         / \
        D   E
```

One possible order:

```text
A → B → D → E → C
```

## Properties

| Property | DFS |
|---|---|
| Data Structure | Stack / LIFO |
| Strategy | Deepest first |
| Complete | No in infinite-depth spaces |
| Optimal | No |
| Time | `O(b^m)` |
| Space | `O(bm)` |

Where:

- `b` = branching factor
- `m` = maximum depth

DFS uses much less memory than BFS but can follow an infinite non-goal path.

---

# 4. Depth-Limited Search (DLS)

DLS is:

> DFS with a predetermined depth limit.

Let:

```text
l = depth limit
```

Nodes at depth `l` are treated as if they have no successors.

Example:

```text
Depth 0
   |
Depth 1
   |
Depth 2  ← Stop
```

## Properties

```text
Time  = O(b^l)
Space = O(bl)
```

DLS solves the infinite-path problem of DFS.

However, if:

```text
l < d
```

the goal may be beyond the depth limit.

DLS is a special case of DFS with `l = ∞`.

---

# 5. Iterative Deepening Depth-First Search (IDDFS)

IDDFS repeatedly increases the depth limit:

```text
0 → 1 → 2 → 3 → ...
```

until the goal is found.

It combines benefits of:

```text
DFS + BFS
```

Like DFS:

- Memory requirement is modest.

Like BFS:

- Complete when branching factor is finite.
- Optimal when path cost is a non-decreasing function of depth.

IDDFS is generally preferred when the search space is large and the solution depth is unknown.

---

# 6. Bidirectional Search

Bidirectional search performs one search from the initial state and another from the goal.

```text
Initial                         Goal
   |                              |
   v                              v
Forward Search              Backward Search
   |                              |
   +-------------> <-------------+
                  |
                 Meet
```

The motivation is:

```text
b^(d/2) + b^(d/2) << b^d
```

The searches succeed when their frontiers intersect.

---

# Informed Search

Informed search uses additional problem-specific information.

The main tool is the:

```text
Heuristic Function
```

Important topics:

- Best-First Search
- Greedy Best-First Search
- A* Search
- Heuristics
- Admissibility
- 8-Puzzle heuristics
- Dominance
- Relaxed problems

---

# Best-First Search

Best-First Search selects a node using an evaluation function:

```text
f(n)
```

The node with the lowest evaluation is expanded first.

The choice of `f(n)` determines the particular search strategy.

---

# Heuristic Functions

A heuristic function is:

```text
h(n)
```

It estimates the cost from node `n` to the goal.

For a goal state:

```text
h(goal) = 0
```

A heuristic is problem-specific and provides additional knowledge to guide search.

---

# State vs Node

A **state** represents the physical configuration of a problem.

A **node** is a search data structure that can contain:

- State
- Parent
- Children
- Depth
- Path cost `g(n)`

Therefore:

```text
State → actual configuration

Node → state + search information
```

---

# Greedy Best-First Search

Greedy Best-First Search chooses the node that appears closest to the goal.

Formula:

```text
f(n) = h(n)
```

Example:

```text
B → h(B) = 8
C → h(C) = 3
D → h(D) = 6
```

Greedy chooses `C`.

## Properties

| Property | Greedy |
|---|---|
| Formula | `f(n)=h(n)` |
| Complete | No |
| Optimal | No |
| Time | `O(b^m)` |
| Space | `O(b^m)` |

A good heuristic can dramatically improve practical performance.

---

# A* Search

A* combines actual cost and estimated remaining cost.

Formula:

```text
f(n) = g(n) + h(n)
```

Where:

```text
g(n) = actual cost from start to n

h(n) = estimated cost from n to goal

f(n) = estimated total cost through n
```

Example:

```text
g(n) = 5
h(n) = 7

f(n) = 5 + 7
     = 12
```

A* selects the node with the lowest `f(n)`.

---

# Greedy vs A*

| Feature | Greedy Best-First | A* |
|---|---|---|
| Formula | `h(n)` | `g(n)+h(n)` |
| Cost so far | No | Yes |
| Heuristic | Yes | Yes |
| Optimal | No | Yes, with appropriate conditions |
| Main idea | Move toward goal | Actual cost + estimated cost |

---

# Admissible Heuristics

A heuristic is admissible if:

```text
h(n) ≤ h*(n)
```

Where:

- `h(n)` = estimated cost
- `h*(n)` = true cost to goal

In simple words:

> An admissible heuristic never overestimates the true cost.

It is therefore optimistic.

Example if:

```text
h*(n) = 10
```

then:

```text
h(n)=7   ✓
h(n)=9   ✓
h(n)=10  ✓
h(n)=12  ✗
```

The course material states that A* tree search is optimal when the heuristic is admissible.

---

# 8-Puzzle Heuristics

Two important heuristics are:

## 1. Misplaced Tiles

```text
h1(n) = number of misplaced tiles
```

## 2. Manhattan Distance

```text
h2(n) = total Manhattan distance
```

Manhattan distance is the total number of horizontal and vertical squares from each tile's current position to its desired position.

Course example:

```text
h1(S) = 8

h2(S) = 3+1+2+2+2+3+3+2
      = 18
```

---

# Dominance of Heuristics

If two heuristics are admissible and:

```text
h2(n) ≥ h1(n)
```

for every node `n`, then:

```text
h2 dominates h1
```

The dominating heuristic is more informative and is guaranteed to expand fewer nodes in the relevant comparison.

For the 8-puzzle:

```text
h1 = Misplaced Tiles
h2 = Manhattan Distance
```

---

# Relaxed Problems

A relaxed problem is a problem with fewer restrictions on actions.

The important principle is:

> The cost of an optimal solution to a relaxed problem is an admissible heuristic for the original problem.

For the 8-puzzle:

### Relaxation 1

If a tile can move anywhere:

```text
h1(n) = misplaced tiles
```

### Relaxation 2

If a tile can move to any adjacent square:

```text
h2(n) = Manhattan distance
```

---

# Local Search

Local Search is useful for optimization problems where:

> The path to the goal is irrelevant; the goal state itself is the solution.

Local search:

- Keeps a single current state or a small set of states.
- Iteratively tries to improve the state(s).
- Is very memory efficient.
- Allows control over memory usage.

Examples:

- N-Queens
- VLSI layout
- Airline flight schedules

---

# N-Queens

Goal:

> Put `n` queens on an `n × n` board with no two queens on the same row, column, or diagonal.

A neighbor is created by:

> Moving one queen to another row in its column.

Search proceeds from one neighboring configuration to another.

---

# Local Search Design Considerations

When designing a local search problem, determine:

1. How is the problem represented?
2. What is a complete state?
3. What is the objective function?
4. How is the cost/value of a state measured?
5. What is a neighbor?
6. What is a step from one state to another?
7. How can a neighbor/step be computed?
8. Are there constraints that can be exploited?

---

# Hill-Climbing Search

Hill Climbing keeps one current state and moves toward a better neighboring state.

```text
Current State
      |
      v
Generate Neighbors
      |
      v
Evaluate Neighbors
      |
      v
Choose Better Neighbor
      |
      v
New Current State
      |
      +----> Repeat
```

The course analogy is:

> Trying to find the top of Mount Everest in a thick fog while suffering from amnesia.

---

# 8-Queens Hill-Climbing Example

The heuristic is:

```text
h = number of pairs of queens attacking each other
```

Goal:

```text
h = 0
```

Suppose:

```text
Current h = 17
```

and neighbors have:

```text
15 14 13 12 16 8
```

Choose:

```text
h = 8
```

because lower `h` is better.

So:

```text
17 → 8
```

If current:

```text
h = 12
```

and a neighbor has:

```text
h = 16
```

do not move to it because:

```text
16 > 12
```

If no neighbor has a lower `h`, the search is stuck at a local minimum.

If several neighbors have the same best value, one can be selected randomly as shown in the course example.

---

# Local Minimum

A local minimum occurs when the current state is better than all immediate neighbors, but it is not the global solution.

Example:

```text
          h=3
           |
          h=2
           |
          h=1
        / |       h=3 h=4 h=2
```

The algorithm cannot find an immediately better move, even though another part of the search space may contain:

```text
h = 0
```

---

# Local Search Difficulties

The course material highlights difficulties that apply to local search algorithms and become worse as the search space becomes higher-dimensional.

Important difficulties:

- Local minima / maxima depending on the formulation
- Ridge problem
- Dependence on initial state

---

# Ridge Problem

The ridge problem occurs when:

> Every neighbor appears to be downhill, but the search space has an uphill direction that is not represented among the available neighbors.

Conceptually:

```text
                    Top
                   /                     /     -----------------/               Current
```

Every allowed step may look worse, while the ridge itself leads upward.

The course uses a folded-paper analogy: every possible search-space step leads downhill, but the ridge leads uphill.

---

# Simulated Annealing Search

Simulated Annealing can sometimes accept a worse state.

This helps the search escape local minima.

Conceptually:

```text
High Temperature
       |
       v
More exploration
       |
       v
Temperature decreases
       |
       v
More selective behavior
```

Comparison:

```text
Hill Climbing
→ prefers better states

Simulated Annealing
→ can sometimes accept worse states
  to escape local traps
```

---

# Local Beam Search

Local Beam Search maintains multiple states.

If:

```text
k = 3
```

it may keep:

```text
State A
State B
State C
```

Successors are generated from these states, and the best `k` states are retained.

```text
      A       B       C
      |       |       |
      +-------+-------+
              |
              v
      Generate Successors
              |
              v
        Select Best k
```

Comparison:

```text
Hill Climbing → 1 current state
Local Beam    → k current states
```

---

# Genetic Algorithms

Genetic Algorithms use a population of candidate states.

A state is represented as:

```text
A string over a finite alphabet
```

A successor can be generated by combining two parent states.

Main components:

1. Population
2. Fitness Function
3. Selection
4. Crossover
5. Mutation

---

# Genetic Algorithm Process

```text
Random Population
       |
       v
Fitness Evaluation
       |
       v
Selection
       |
       v
Crossover
       |
       v
Mutation
       |
       v
New Generation
       |
       +----> Repeat
```

## Population

Start with:

```text
k randomly generated states
```

## Fitness

Higher fitness means a better state.

## Selection

Probability from the course material:

```text
P(individual)
=
individual fitness
/
total population fitness
```

## Crossover

Two fit parents are combined to produce offspring.

## Mutation

Offspring are randomly modified with a low probability.

---

# Search Algorithm Comparison

| Algorithm | Selection Criterion | Data Structure | Complete | Optimal | Main Strength |
|---|---|---|---|---|---|
| BFS | Shallowest | FIFO Queue | Yes, finite `b` | Yes, unit cost | Shallow solutions |
| UCS | Lowest `g(n)` | Priority Queue | Yes, positive step cost | Yes | Lowest cost |
| DFS | Deepest | Stack | No in infinite depth | No | Low memory |
| DLS | Deepest up to limit | Stack | Depends on limit | No | Controls depth |
| IDDFS | Increasing depth | DFS | Yes, finite `b` | Under conditions | Unknown depth |
| Bidirectional | Both directions | Two frontiers | Depends | Depends | Reduced depth |
| Greedy | Lowest `h(n)` | Priority Queue | No | No | Goal-directed |
| A* | Lowest `g(n)+h(n)` | Priority Queue | Under conditions | Yes with suitable heuristic | Cost + heuristic |
| Hill Climbing | Better neighbor | Current state | No | No | Very low memory |
| Simulated Annealing | Better / occasional worse | Current state | Not guaranteed | Not guaranteed | Escapes local traps |
| Local Beam | Best `k` states | Set of states | No | No | Multiple candidates |
| Genetic Algorithm | Fitness | Population | Not guaranteed | Not guaranteed | Population optimization |

---

# Important Formulas

## State Space

```text
[S, s, O, G]
```

## BFS

```text
Time  = O(b^d)
Space = O(b^d)
```

## DFS

```text
Time  = O(b^m)
Space = O(bm)
```

## DLS

```text
Time  = O(b^l)
Space = O(bl)
```

## Greedy

```text
f(n) = h(n)
```

## A*

```text
f(n) = g(n) + h(n)
```

## Admissibility

```text
h(n) ≤ h*(n)
```

## Bidirectional

```text
b^(d/2) + b^(d/2) << b^d
```

## Genetic Algorithm Selection

```text
P(individual)
=
individual fitness
/
total population fitness
```

---

# Important Symbols

| Symbol | Meaning |
|---|---|
| `b` | Branching factor |
| `d` | Depth of shallowest solution |
| `m` | Maximum depth |
| `l` | Depth limit |
| `g(n)` | Cost from initial state to node `n` |
| `h(n)` | Estimated cost from `n` to goal |
| `h*(n)` | True cost from `n` to goal |
| `f(n)` | Evaluation function |
| `C*` | Cost of optimal solution |
| `ε` | Minimum action/step cost |
| `k` | Number of states retained in Local Beam / population parameter where applicable |

---

# Important Exam Questions

## Short Answer

1. What is State Space Search?
2. Define initial state.
3. Define goal state.
4. What are operators?
5. What is uninformed search?
6. What is informed search?
7. Define heuristic function.
8. What is `g(n)`?
9. What is `h(n)`?
10. What is `f(n)`?
11. Define admissible heuristic.
12. What is local search?
13. What is a local minimum?
14. What is the ridge problem?
15. What is a fitness function?
16. What is crossover?
17. What is mutation?
18. What is a relaxed problem?

## Long Answer

1. Explain State Space Search with `[S,s,O,G]`.
2. Explain Tree Search and Graph Search.
3. Explain BFS with example, algorithm and properties.
4. Explain UCS with example and properties.
5. Explain DFS with example and properties.
6. Explain DLS.
7. Explain IDDFS.
8. Explain Bidirectional Search.
9. Explain Best-First Search.
10. Explain Greedy Best-First Search.
11. Explain A* Search.
12. Explain admissible heuristics.
13. Explain the 8-Puzzle heuristics.
14. Explain dominance of heuristics.
15. Explain relaxed problems.
16. Explain Local Search.
17. Explain Hill Climbing with the 8-Queens example.
18. Explain local minima and hill-climbing difficulties.
19. Explain the Ridge Problem.
20. Explain Simulated Annealing.
21. Explain Local Beam Search.
22. Explain Genetic Algorithms.
23. Compare all major search algorithms.

---

# Quick Revision

## Uninformed Search

```text
BFS  → Shallowest
UCS  → Cheapest
DFS  → Deepest
DLS  → DFS + Depth Limit
IDDFS → 0,1,2,3,...
Bidirectional → Both directions
```

## Informed Search

```text
Greedy → h(n)

A* → g(n) + h(n)
```

## Heuristic

```text
h(n) = estimated cost from n to goal

h(goal) = 0
```

Admissible:

```text
h(n) ≤ h*(n)
```

## Local Search

```text
Hill Climbing
Simulated Annealing
Local Beam
Genetic Algorithm
```

Memory trick:

```text
H → Hill Climbing
S → Simulated Annealing
L → Local Beam
G → Genetic Algorithm
```

## Genetic Algorithm

```text
Population
     ↓
Fitness
     ↓
Selection
     ↓
Crossover
     ↓
Mutation
     ↓
New Generation
```

---

# Easy Conceptual Differences

## BFS vs DFS

```text
BFS → Level by level
DFS → Deep branch first
```

## BFS vs UCS

```text
BFS → Lowest depth
UCS → Lowest path cost
```

## Greedy vs A*

```text
Greedy → h(n)
A*     → g(n) + h(n)
```

## Hill Climbing vs Simulated Annealing

```text
Hill Climbing
→ moves toward better state

Simulated Annealing
→ can sometimes accept worse state
  to escape local minimum
```

## Hill Climbing vs Local Beam

```text
Hill Climbing → 1 state
Local Beam    → k states
```

---

# Choosing an Algorithm

### Need the shallowest solution?

```text
BFS
```

### Need the least-cost solution?

```text
UCS
```

### Need low memory?

```text
DFS / IDDFS
```

### Solution depth is unknown?

```text
IDDFS
```

### Have heuristic information?

```text
Greedy / A*
```

### Need actual cost + estimated remaining cost?

```text
A*
```

### Optimization problem where final configuration matters?

```text
Local Search
```

### Population-based optimization?

```text
Genetic Algorithm
```

---

# Applications

Search strategies are fundamental in:

- GPS Navigation
- Robot Navigation
- Route Planning
- Puzzle Solving
- Game AI
- Scheduling
- Optimization
- VLSI Layout
- Airline Flight Scheduling
- Constraint Satisfaction Problems

---

# Course Assignment

The course material includes a **Missionaries and Cannibals** assignment.

Implement and solve it using one of:

- Breadth-First Search
- Uniform-Cost Search
- Depth-First Search
- Depth-Limited Search
- Iterative Deepening Search

Important requirement:

```text
Avoid repeated states
```

Use graph-based search and keep track of how many states are searched.

Possible languages:

- Java
- C++
- Python
- Prolog

---

# Learning Outcomes

After completing this unit, you should be able to:

- Understand State Space Search.
- Formulate problems using states, operators and goals.
- Explain Tree Search and Graph Search.
- Explain BFS, UCS, DFS, DLS and IDDFS.
- Explain Bidirectional Search.
- Understand informed search.
- Explain heuristic functions.
- Apply Greedy Best-First Search.
- Apply A* Search.
- Determine whether a heuristic is admissible.
- Understand 8-Puzzle heuristics.
- Explain heuristic dominance.
- Understand relaxed problems.
- Understand Local Search.
- Explain Hill Climbing.
- Identify local minima.
- Explain the Ridge Problem.
- Understand Simulated Annealing.
- Explain Local Beam Search.
- Understand Genetic Algorithms.
- Explain fitness, selection, crossover and mutation.
- Analyze time and space complexity.

---

# Final Revision Map

```text
                         AI SEARCH STRATEGIES
                                  |
             +--------------------+--------------------+
             |                    |                    |
             v                    v                    v
       STATE SPACE           UNINFORMED            INFORMED
         SEARCH                SEARCH               SEARCH
             |                    |                    |
        [S,s,O,G]           +------+------+      +----+----+
                            |      |      |      |         |
                           BFS    UCS    DFS   Greedy      A*
                            |      |      |      |         |
                           DLS   IDDFS    |      h(n)    g+h
                            |
                     Bidirectional

                                  |
                                  v
                           LOCAL SEARCH
                                  |
                 +----------------+----------------+
                 |                |                |
                 v                v                v
          Hill Climbing   Simulated Annealing  Local Beam
                 |
                 v
          Local Minima / Ridge
                 |
                 v
        Genetic Algorithms
                 |
        +--------+--------+
        |        |        |
     Fitness  Crossover Mutation
```

---

# ⭐ Key Takeaways

```text
State Space Search
        ↓
States + Operators + Goals

Uninformed Search
        ↓
No heuristic information

BFS
        ↓
Shallowest first

UCS
        ↓
Lowest path cost

DFS
        ↓
Deepest first

DLS
        ↓
DFS + depth limit

IDDFS
        ↓
Increasing depth limits

Bidirectional
        ↓
Search from both ends

Greedy
        ↓
h(n)

A*
        ↓
g(n) + h(n)

Admissible
        ↓
Never overestimates

Local Search
        ↓
Improve current state

Hill Climbing
        ↓
Better neighbor

Simulated Annealing
        ↓
Sometimes accept worse state

Local Beam
        ↓
Keep k states

Genetic Algorithm
        ↓
Population → Fitness → Selection
→ Crossover → Mutation
```


---

## Repository Purpose

- Quick revision
- Concept understanding
- Algorithm comparison
- Formula revision
