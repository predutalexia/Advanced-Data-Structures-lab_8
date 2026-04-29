# Advanced-Data-Structures-lab_8
# Disjoint Sets (Union-Find) 

## How to compile & run

```bash
g++ -std=c++17 -o disjoint_sets.exe disjoint_sets.cpp
./disjoint_sets.exe
```

## Core DSU structure

The `DSU` struct is reused across all problems and supports:

- **find(x)** — returns the root of x's component using path compression
- **unite(u, v)** — merges two components using union by rank, returns `false` if already connected
- **connected(u, v)** — checks if u and v are in the same component
- **compSize(x)** — returns the size of x's component

Time complexity: nearly O(1) per operation (O(α(n)) amortized).

## Problems

### Problem 1 — Count connected components
Given `n` nodes and a list of edges, count how many connected components exist.

**Approach:** Start with `n` components. Each successful `unite()` reduces the count by 1.

**Example:**
- Input: n=5, edges={(0,1),(1,2),(3,4)}
- Output: `2`

---

### Problem 2 — Cycle detection
Detect whether an undirected graph contains a cycle.

**Approach:** For each edge (u, v), if `find(u) == find(v)` they are already connected — adding this edge creates a cycle.

**Example:**
- Input: edges={(0,1),(1,2),(2,0),(2,3)} → `yes`
- Input: edges={(0,1),(1,2),(2,3)} → `no`

---

### Problem 3 — Number of provinces
Given an `n x n` adjacency matrix `isConnected`, return the number of provinces (groups of directly or indirectly connected cities).

**Approach:** Same as Problem 1 but reads input from a matrix instead of an edge list.

**Example:**
```
isConnected = [[1,1,0],
               [1,1,0],
               [0,0,1]]
```
Output: `2`

---

### Problem 4 — Social network friend groups
Given `n` users and a list of friendship events, return the total number of friend groups and their members.

**Approach:** Process all friendships with `unite()`, then group nodes by their root.

**Example:**
- Input: n=7, friendships={(0,1),(1,2),(3,4),(5,6)}
- Output:
```
3 Groups
Group 1: {0,1,2} size 3
Group 2: {3,4} size 2
Group 3: {5,6} size 2
```
