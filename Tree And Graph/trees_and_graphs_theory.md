
# 🌳 Trees and Graphs — Basic Concepts

This document contains the **fundamental theory of Trees and Graphs** used in
**Data Structures and Algorithms (DSA)**.

It covers:

- Tree basics
- Binary Trees
- Binary Search Trees (BST)
- Tree terminology
- Tree traversals
- Graph basics
- Graph types
- Graph representation
- Graph traversal algorithms

---

# 1️⃣ What is a Tree?

A **Tree** is a hierarchical (non‑linear) data structure made of **nodes connected by edges**.

Unlike arrays or linked lists, trees **branch like a real tree**.

Example:

```
          [10]          ← Root
         /    \
       [5]    [15]
       / \    /  \
     [3] [7] [12] [20]
```

---

# Tree Terminology

| Term | Meaning | Example |
|-----|-----|-----|
Root | Topmost node | 10 |
Parent | Node with children | 5, 15 |
Child | Node below parent | 3,7,12,20 |
Leaf | Node with no children | 3,7,12,20 |
Edge | Connection between nodes | lines |
Height | Longest path root → leaf | 2 |
Depth | Distance from root | 10=0 |
Subtree | Node + its children | [5,3,7] |

---

# Tree Properties

1. A tree with **n nodes has n−1 edges**
2. There is **exactly one path** between nodes
3. Trees **do not contain cycles**
4. Trees are **connected graphs**

---

# 2️⃣ Binary Tree

A **Binary Tree** is a tree where each node has **at most two children**.

Children are called:

- Left Child
- Right Child

Example:

```
          [10]
         /    \
       [5]    [15]
       / \      \
     [3] [7]   [20]
```

Rules:

• Maximum **2 children per node**  
• Children are **LEFT and RIGHT**  
• No ordering rule required

---

# Types of Binary Trees

## Full Binary Tree

Each node has **0 or 2 children**.

```
      A
     / \
    B   C
   / \
  D   E
```

---

## Complete Binary Tree

All levels filled except possibly the last level.

Nodes are filled **left to right**.

---

## Perfect Binary Tree

All nodes have **two children** and all leaves are at the **same level**.

```
        A
      /   \
     B     C
    / \   / \
   D   E  F   G
```

---

# 3️⃣ Binary Search Tree (BST)

A **Binary Search Tree** is a Binary Tree with ordering rules.

Rules:

1. Left subtree values are **smaller than the node**
2. Right subtree values are **greater than the node**

Example:

```
          [10]
         /    \
       [5]    [15]
       / \    /  \
     [3] [7] [12] [20]
```

Example check:

```
Node 10
Left 5  → smaller
Right 15 → larger
```

---

# Why BST is Useful

Searching becomes faster because each comparison removes **half the tree**.

Average complexity:

| Operation | Complexity |
|----------|-----------|
Search | O(log n) |
Insert | O(log n) |
Delete | O(log n) |

Worst case (unbalanced tree):

```
[1]
  \
  [2]
    \
    [3]
```

This behaves like a linked list.

Worst case complexity:

```
O(n)
```

---

# Tree Traversals

Traversal = visiting every node in a tree.

Example tree:

```
      [10]
     /    \
   [5]    [15]
   / \
 [3] [7]
```

---

## 1️⃣ Inorder Traversal

Order:

```
Left → Root → Right
```

Result:

```
3 → 5 → 7 → 10 → 15
```

In a BST this produces **sorted order**.

---

## 2️⃣ Preorder Traversal

Order:

```
Root → Left → Right
```

Result:

```
10 → 5 → 3 → 7 → 15
```

Use case:

• Copying a tree

---

## 3️⃣ Postorder Traversal

Order:

```
Left → Right → Root
```

Result:

```
3 → 7 → 5 → 15 → 10
```

Use case:

• Deleting a tree

---

# 🌐 Graphs

A **Graph** is a non‑linear data structure consisting of:

- Vertices (nodes)
- Edges (connections)

Graphs represent **networks and relationships**.

Example:

```
A ----- B
|       |
|       |
C ----- D
```

Vertices:

```
A, B, C, D
```

Edges:

Connections between vertices.

---

# Graph Terminology

| Term | Meaning |
|-----|------|
Vertex | Node in a graph |
Edge | Connection between vertices |
Degree | Number of edges connected |
Path | Sequence of vertices |
Cycle | Path that starts and ends at same vertex |
Connected Graph | All nodes reachable |
Disconnected Graph | Some nodes unreachable |

---

# Types of Graphs

## Undirected Graph

Edges have **no direction**.

```
A --- B
```

Meaning:

```
A connected to B
B connected to A
```

---

## Directed Graph (Digraph)

Edges have **direction**.

```
A → B
```

Meaning:

```
A points to B
```

---

## Weighted Graph

Edges have **weights or costs**.

Example:

```
A ---5--- B
```

Used in:

- maps
- routing
- shortest path problems

---

# Graph Representation

## Adjacency Matrix

Example:

```
   A B C D
A [0 1 1 0]
B [1 0 0 1]
C [1 0 0 1]
D [0 1 1 0]
```

---

## Adjacency List

Example:

```
A → B, C
B → A, D
C → A, D
D → B, C
```

This representation uses **less memory**.

---

# Graph Traversal

Traversal means **visiting all vertices in a graph**.

Two main algorithms:

---

## Breadth First Search (BFS)

Uses **Queue**.

Visits nodes **level by level**.

Example order:

```
A → B → C → D
```

---

## Depth First Search (DFS)

Uses **Stack or Recursion**.

Explores **deep path first**.

Example order:

```
A → B → D → C
```

---

# Applications

## Tree Applications

- File systems
- HTML DOM
- Database indexing
- AI decision trees

---

## Graph Applications

- Google Maps
- Social networks
- Network routing
- Recommendation systems

---

# Summary

| Structure | Purpose |
|---------|---------|
Tree | Hierarchical relationships |
Binary Tree | Max 2 children |
Binary Search Tree | Ordered search |
Graph | Network relationships |

