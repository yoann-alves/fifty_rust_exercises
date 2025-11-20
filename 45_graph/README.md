# Exercise 45: Graph

## 🎯 Objectives

Implement a graph data structure with algorithms:

- Adjacency list representation
- Breadth-First Search (BFS)
- Depth-First Search (DFS)
- Cycle detection
- Shortest path with Dijkstra's algorithm

## 📚 Concepts

- Graph representation (adjacency list)
- Graph traversal algorithms
- Queues and stacks for traversal
- Cycle detection in directed/undirected graphs
- Priority queue for Dijkstra
- Path reconstruction

## 📖 Background

**Graphs** are collections of vertices (nodes) connected by edges. They model relationships between entities.

**Graph types:**

```
Directed:    A → B (one-way connection)
Undirected:  A — B (two-way connection)
Weighted:    A —5→ B (edges have values/costs)
Unweighted:  A → B (all edges equal)
```

**Real-world examples:**

```
Social network:    People (vertices), Friendships (edges)
Map/GPS:           Cities (vertices), Roads (edges with distances)
Dependencies:      Tasks (vertices), Prerequisites (directed edges)
Internet:          Routers (vertices), Connections (edges)
```

**Traversal algorithms:**

- **BFS (Breadth-First)**: Explore level by level, like ripples in water
- **DFS (Depth-First)**: Explore one path fully before backtracking

**Cycle detection:**

```
Acyclic:  A → B → C (no loops)
Cyclic:   A → B → C → A (returns to start)
```

**Shortest path (Dijkstra):**
Finding the minimum-cost path between two vertices in a weighted graph.

**Adjacency list structure:**

```
Graph with edges: 1→2, 1→3, 2→4
Represented as:
1: [2, 3]
2: [4]
3: []
4: []
```

## ⚙️ Requirements

**First Pass:**

- ✅ Graph struct with adjacency list
- ✅ Add vertices and edges
- ✅ BFS traversal
- ✅ DFS traversal
- ✅ Works with basic vertex types
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Doc comments explaining algorithms
- ✅ **Graph operations**:
  - Add/remove vertices
  - Add/remove edges (directed/undirected)
  - Check edge existence
  - Get neighbors of a vertex
  - Count vertices and edges
- ✅ **Traversals**:
  - BFS returning visited order
  - DFS (recursive and/or iterative)
  - Path tracking during traversal
  - Check connectivity between nodes
- ✅ **Cycle detection**:
  - Detect cycles in directed graphs
  - Detect cycles in undirected graphs
  - Optionally return the cycle path
- ✅ **Shortest path**:
  - Dijkstra's algorithm implementation
  - Return both distance and path
  - Handle disconnected vertices
  - Support weighted edges
- ✅ **Advanced features**:
  - Topological sort (for DAGs)
  - Count connected components
  - Check if graph is bipartite
  - Graph statistics
- ✅ **Generic implementation**:
  - Support any hashable vertex type
  - Not limited to integers
- ✅ **Display**: Print adjacency list in readable format

## 🚫 Constraints

- Standard library only
- Can use `std::collections` (HashMap, HashSet, VecDeque, BinaryHeap)
- Must implement algorithms yourself (no external graph libraries)

## 💡 Approaches

**Data structure choices:**

- Adjacency list: HashMap of vertex → list of neighbors
- For weighted graphs: store (neighbor, weight) pairs
- For unweighted: just store neighbor vertices
- Track if graph is directed or undirected

**BFS strategy:**

- Use a queue (FIFO)
- Track visited vertices to avoid cycles
- Process neighbors level by level

**DFS strategy:**

- Use a stack (LIFO) or recursion
- Track visited vertices
- Explore one branch fully before backtracking

**Cycle detection approaches:**

- Directed: Track recursion stack during DFS
- Undirected: Check if you revisit a vertex that isn't the parent

**Dijkstra approach:**

- Use a priority queue (min-heap)
- Track distances from start vertex
- Update distances when finding shorter paths
- Reconstruct path by tracking previous vertices

**Generic vertices:**

- Use trait bounds: `T: Eq + Hash + Clone`
- HashMap keys must be hashable and comparable

## ✅ Validation

Basic graph operations:

```
Create undirected graph
Add vertices: 1, 2, 3, 4
Add edges: 1-2, 1-3, 2-4, 3-4

Visual representation:
  1 --- 2
  |     |
  3 --- 4

Vertices: 4
Edges: 4
```

BFS from vertex 1:

```
Possible orders: [1, 2, 3, 4] or [1, 3, 2, 4]
(order depends on neighbor insertion order)
First vertex visited: 1
All 4 vertices visited
```

DFS from vertex 1:

```
Possible orders: [1, 2, 4, 3] or [1, 3, 4, 2]
(depends on traversal choices)
First vertex visited: 1
All 4 vertices visited
```

Cycle detection (directed):

```
Graph: 1→2, 2→3, 3→1
Has cycle: Yes (1→2→3→1)

Graph: 1→2, 2→3, 1→3
Has cycle: No (DAG)
```

Cycle detection (undirected):

```
Graph: 1-2, 2-3, 3-1
Has cycle: Yes (triangle)

Graph: 1-2, 2-3
Has cycle: No (tree)
```

Dijkstra shortest path:

```
Graph (directed, weighted):
A --4--> B
|        |
2        1
|        |
v        v
C --8--> D --2--> E
|
10
v
E

Path A to E: A → C → B → D → E
Distance: 2 + 1 + 5 + 2 = 10
(not A → C → E which is 12)
```

Connected components:

```
Graph with two separate parts:
1-2-3 (component 1)
4-5 (component 2)

Component count: 2
```

## 🔍 Challenge

Implement A\* search algorithm for pathfinding with heuristics, or add support for finding minimum spanning trees (Kruskal's or Prim's algorithm), or detect strongly connected components in directed graphs.

---

**Previous:** [44_binary_tree](../44_binary_tree/README.md) | **Next:** [46_concurrent_downloader](../46_concurrent_downloader/README.md)
