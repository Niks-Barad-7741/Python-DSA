# Data Structures & Algorithms (DSA)

This document covers all the core Data Structures and Algorithms topics
studied — explained in detail with theory, real world examples,
Big O analysis, and code.

---

# 📊 TOPIC 1 — Big O Notation

## What is Big O Notation?

Big O Notation is a way to **measure how efficient your code is**.
It tells you how the speed of your code changes as the input size grows.

Instead of measuring time in seconds (which depends on your computer),
Big O measures the **number of operations** your code performs.

## Why is Big O important?

Imagine you have a list of 1 employee vs 1,000,000 employees.
Some code will handle both equally fast. Other code will become
extremely slow as the list grows. Big O tells you which is which —
**before you even run the code!**

This is critical in:
- Technical interviews
- Writing scalable production code
- Choosing the right data structure

## The 6 Common Big O Values

### O(1) — Constant Time
```
The code always takes the SAME number of steps,
no matter how big the input is!

n = 1        → 1 step
n = 1000     → 1 step
n = 1000000  → 1 step
```

**Example:**
```python
def get_first(arr):
    return arr[0]    # always 1 step!

# Real example — check if list is empty
def is_empty(arr):
    return len(arr) == 0   # always 1 step regardless of size!
```

**Real world:** Looking up a word in a dictionary using its exact page number.

---

### O(n) — Linear Time
```
Steps GROW directly with input size!

n = 10    → 10 steps
n = 100   → 100 steps
n = 1000  → 1000 steps
```

**Example:**
```python
def find_name(employees, target):
    for emp in employees:    # checks every employee!
        if emp == target:
            return True
    return False

# Real example — sum all salaries
def total_salary(salaries):
    total = 0
    for s in salaries:    # visits each salary once → O(n)
        total += s
    return total
```

**Real world:** Finding a name in an unsorted list — you check one by one.

---

### O(n²) — Quadratic Time
```
Steps EXPLODE as input grows!

n = 10   → 100 steps
n = 100  → 10,000 steps
n = 1000 → 1,000,000 steps
```

**Example:**
```python
def find_duplicate(arr):
    for i in range(len(arr)):        # n times
        for j in range(len(arr)):    # n times each!
            if i != j and arr[i] == arr[j]:
                return arr[i]

# Real example — print all pairs
def print_pairs(arr):
    for i in arr:         # outer loop n
        for j in arr:     # inner loop n
            print(i, j)   # n × n = n² pairs printed!
```

**Real world:** Comparing every employee's name with every other employee's name.

---

### O(log n) — Logarithmic Time
```
Cuts the problem in HALF each step!

n = 1000    → ~10 steps
n = 1000000 → ~20 steps
```

**Example — Binary Search:**
```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1     # throw away LEFT half!
        else:
            right = mid - 1    # throw away RIGHT half!
    return -1

# Real example — find page in 1000-page book
# Open page 500 → too high → open page 250 → too low
# Open page 375 → found! Only ~10 steps for 1000 pages!
```

**Real world:** Finding a word in a dictionary by opening the middle, then deciding left or right.

---

### O(n log n) — Log-Linear Time
```
Seen in efficient sorting algorithms!

n = 1000    → ~10,000 steps
n = 1000000 → ~20,000,000 steps
Much better than O(n²)!
```

**Example:**
```python
arr.sort()     # Python's built-in sort → O(n log n)
sorted(arr)    # also O(n log n)
# Merge Sort, Quick Sort → O(n log n)
```

### O(n²) vs O(n log n) — Why it matters:
```
n = 10,000 items:
  O(n²)      = 100,000,000 steps  😱
  O(n log n) =     130,000 steps  ✅
That's 769x FASTER!
```

---

## The 2 Simplification Rules

### Rule 1 — Drop Constants
```
O(2n)  → O(n)
O(500) → O(1)
O(3n²) → O(n²)

Why? At large scale, constants don't matter!
n = 1,000,000:
  O(2n) = 2,000,000
  O(n)  = 1,000,000
Both are huge — the 2 makes no real difference!
```

### Rule 2 — Drop Smaller Terms
```
O(n² + n) → O(n²)
O(n + 100) → O(n)

Why? The bigger term dominates!
n = 1000:
  n² = 1,000,000  ← dominates!
  n  =     1,000  ← tiny in comparison!
```

## Quick Reference

| Code Pattern | Big O |
|-------------|-------|
| `arr[0]` — direct access | O(1) |
| `len(arr)` | O(1) |
| Single `for` loop | O(n) |
| Two separate loops | O(n) |
| Loop inside loop | O(n²) |
| Binary search | O(log n) |
| `arr.sort()` | O(n log n) |

---

# 🗂️ TOPIC 2 — Arrays

## What is an Array?

An Array is a **collection of items stored in continuous memory locations**.
Think of it like seats in a cinema — all numbered and side by side.

```
Index:   0     1     2     3     4
       [ 10 ] [ 20 ] [ 30 ] [ 40 ] [ 50 ]
         ↑
    Memory address 100, 101, 102, 103, 104
```

Because items are stored continuously, Python can calculate the
exact memory address of any element instantly:
```
address = start_address + index
arr[3]  = 100 + 3 = address 103 → O(1)!
```

## Why use Arrays?

- **Fast access** by index — O(1)
- **Simple structure** — easy to understand
- **Memory efficient** — no extra pointers needed
- **Cache friendly** — items next to each other in memory

## When NOT to use Arrays?

- When you frequently insert or delete at the **beginning** — O(n) because everything shifts
- When you don't know the size in advance

## Array Operations and Big O

| Operation | Big O | Explanation |
|-----------|-------|-------------|
| Access `arr[i]` | O(1) ⚡ | Direct address calculation |
| Search | O(n) | Must check every element |
| Insert at end | O(1) ⚡ | Just add at back |
| Insert at start | O(n) 🐢 | Shifts ALL elements right |
| Delete at end | O(1) ⚡ | Just remove last |
| Delete at start | O(n) 🐢 | Shifts ALL elements left |

## Implementation

```python
arr = [10, 20, 30, 40, 50]

arr[2]           # O(1) — access index 2 → 30
arr.append(60)   # O(1) — add at end
arr.insert(0, 5) # O(n) — insert at start, shifts everyone
arr.pop()        # O(1) — remove from end
arr.pop(0)       # O(n) — remove from start, shifts everyone
30 in arr        # O(n) — search checks every element

# Real example — store student scores
scores = [95, 87, 91, 78, 88]
print(scores[0])          # 95 — instant O(1)!
scores.append(92)         # add new score at end O(1)
scores.insert(0, 100)     # add at start — shifts all O(n)
print(max(scores))        # 100 — O(n) to find max
```

## Real World Uses

- Storing a list of students
- Storing pixel values in an image
- Storing daily temperature readings

---

# 🔗 TOPIC 3 — Linked Lists

## What is a Linked List?

A Linked List is a collection of items where each item is stored
**anywhere in memory**, connected to the next item using a **pointer**.

Unlike arrays, items are NOT stored next to each other.
Each item (called a **Node**) contains:
1. The **value** (the actual data)
2. A **pointer** to the next node

```
HEAD
 ↓
[10 | •]──→ [20 | •]──→ [30 | •]──→ [40 | None]
address       address      address      address
  100           500          230          890
```

The items are scattered in memory but connected by pointers.

## Why use Linked Lists?

- **Fast insert/delete at start** — O(1) because only the HEAD pointer updates
- **Dynamic size** — grows and shrinks easily, no shifting needed
- **Efficient memory** — only uses as much memory as needed

## Why NOT use Linked Lists?

- **Slow access by index** — O(n) because you must follow pointers one by one
- **Extra memory** for storing pointers
- **Not cache friendly** — items scattered in memory

## Key Terminology

| Term | Meaning |
|------|---------|
| Node | Single element (value + pointer) |
| HEAD | Pointer to first node |
| TAIL | Pointer to last node |
| Pointer | Memory address of next node |
| Traversal | Walking through nodes one by one |

## Linked List Operations and Big O

| Operation | Big O | Explanation |
|-----------|-------|-------------|
| Access by index | O(n) 🐢 | Follow pointers one by one |
| Search | O(n) | Check every node |
| Insert at start | O(1) ⚡ | Just update HEAD pointer |
| Insert at end | O(n) 🐢 | Must traverse to last node |
| Delete at start | O(1) ⚡ | Just move HEAD forward |
| Delete at end | O(n) 🐢 | Must find second-to-last node |

## Implementation from Scratch

```python
class Node:
    def __init__(self, value):
        self.value = value    # the data
        self.next  = None     # pointer to next node

class LinkedList:
    def __init__(self):
        self.head = None
        self.size = 0

    def insert_at_start(self, value):    # O(1)
        new_node      = Node(value)
        new_node.next = self.head
        self.head     = new_node
        self.size    += 1

    def insert_at_end(self, value):      # O(n)
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node
        self.size += 1

    def delete_from_start(self):         # O(1)
        if self.head is None:
            return "Empty!"
        removed   = self.head.value
        self.head = self.head.next
        self.size -= 1
        return removed

    def search(self, value):             # O(n)
        current  = self.head
        position = 0
        while current:
            if current.value == value:
                return f"Found at position {position}!"
            current   = current.next
            position += 1
        return "Not found!"

    def display(self):
        elements = []
        current  = self.head
        while current:
            elements.append(str(current.value))
            current = current.next
        print(" → ".join(elements) + " → None")


# Real example — music playlist
playlist = LinkedList()
playlist.insert_at_end("Shape of You")
playlist.insert_at_end("Blinding Lights")
playlist.insert_at_end("Levitating")
playlist.insert_at_start("Stay")       # O(1) — add to front instantly!
playlist.display()
# Stay → Shape of You → Blinding Lights → Levitating → None
```

## Real World Uses

- **Music playlist** — each song points to next song
- **Browser history** — each page points to previous page
- **Undo functionality** — each action points to previous action

---

## ⚔️ Array vs Linked List — Final Comparison

| Feature | Array | Linked List |
|---------|-------|-------------|
| Memory | Continuous | Scattered |
| Access by index | O(1) ⚡ | O(n) 🐢 |
| Search | O(n) | O(n) |
| Insert at start | O(n) 🐢 | O(1) ⚡ |
| Insert at end | O(1) ⚡ | O(n) 🐢 |
| Delete at start | O(n) 🐢 | O(1) ⚡ |
| Extra memory | No | Yes (pointers) |

```
Use ARRAY       → when you need fast ACCESS by index!
Use LINKED LIST → when you need fast INSERT/DELETE at start!
```

---

# 📚 TOPIC 4 — Stacks

## What is a Stack?

A Stack is a data structure that follows the **LIFO** principle:
**Last In, First Out**.

Think of a stack of plates:
- You can only add a plate on **TOP**
- You can only remove a plate from **TOP**
- The LAST plate placed = FIRST plate removed!

```
Push →  [  30  ]  ← Pop    (TOP)
        [  20  ]
        [  10  ]           (BOTTOM)
```

## Why use a Stack?

- Perfect when you need to **reverse** something
- Perfect when you need to **track history** and go back
- Perfect for **matching pairs** like brackets
- All operations are O(1) — extremely fast!

## Key Operations

| Operation | Big O | Description |
|-----------|-------|-------------|
| push() | O(1) ⚡ | Add item to top |
| pop() | O(1) ⚡ | Remove item from top |
| peek() | O(1) ⚡ | See top item without removing |
| is_empty() | O(1) ⚡ | Check if stack is empty |
| size() | O(1) ⚡ | Get number of items |
| search() | O(n) | Find an item |
| clear() | O(1) | Remove all items |
| contains() | O(n) | Check if item exists |

## Implementation

```python
class Stack:
    def __init__(self):
        self.stack = []
        self._size = 0

    def push(self, value):           # O(1) — add to top
        self.stack.append(value)
        self._size += 1

    def pop(self):                   # O(1) — remove from top
        if self.is_empty():
            return "Stack Underflow! Stack is empty!"
        self._size -= 1
        return self.stack.pop()

    def peek(self):                  # O(1) — see top
        if self.is_empty():
            return "Stack is empty!"
        return self.stack[-1]

    def is_empty(self):              # O(1)
        return self._size == 0

    def size(self):                  # O(1)
        return self._size

    def search(self, value):         # O(n)
        for i in range(len(self.stack) - 1, -1, -1):
            if self.stack[i] == value:
                return f"Found at position {len(self.stack)-1-i} from top!"
        return "Not found!"

    def clear(self):                 # O(1)
        self.stack = []
        self._size = 0

    def contains(self, value):       # O(n)
        return value in self.stack

    def to_list(self):               # O(n) — top to bottom
        return self.stack[::-1]
```

## Real World Uses

### 1. Undo (Ctrl+Z)
```python
undo_stack = Stack()
undo_stack.push("typed H")
undo_stack.push("typed He")
undo_stack.push("typed Hel")
undo_stack.push("typed Hello")

print(undo_stack.peek())   # "typed Hello" ← current state
undo_stack.pop()           # undo → back to "typed Hel"
print(undo_stack.peek())   # "typed Hel" ✅
```

### 2. Bracket Matching (Interview Question!)
```python
def is_balanced(expression):
    stack = Stack()
    pairs = {')': '(', '}': '{', ']': '['}
    for char in expression:
        if char in "({[":
            stack.push(char)
        elif char in ")}]":
            if stack.is_empty() or stack.pop() != pairs[char]:
                return False
    return stack.is_empty()

print(is_balanced("({[]})"))  # True  ✅
print(is_balanced("([)]"))    # False ❌
print(is_balanced("{[]}"))    # True  ✅
```

### 3. Browser Back + Forward Button
```python
history = Stack()
forward = Stack()

history.push("google.com")
history.push("github.com")
history.push("claude.ai")

# Back button
forward.push(history.pop())    # save claude.ai to forward
print(history.peek())          # github.com ✅

# Forward button
history.push(forward.pop())    # restore claude.ai
print(history.peek())          # claude.ai ✅
```

## Important Terms

```
Stack Overflow  → pushing too many items, memory full!
Stack Underflow → popping from an empty stack!
```

---

# 🔄 TOPIC 5 — Queues

## What is a Queue?

A Queue is a data structure that follows the **FIFO** principle:
**First In, First Out**.

Think of a line at a ticket counter:
- New people join at the **BACK**
- People are served from the **FRONT**
- The FIRST person in line = FIRST person served!

```
Enqueue → [ Nikhil | Priya | Sara ] → Dequeue
           BACK                FRONT
```

## Why use a Queue?

- Perfect for **waiting lists** and task scheduling
- Perfect when **order matters** — first come, first served
- Perfect for **processing tasks** in the order they arrive
- All main operations are O(1) — extremely fast!

## Key Operations

| Operation | Big O | Description |
|-----------|-------|-------------|
| enqueue() | O(1) ⚡ | Add item to back |
| dequeue() | O(1) ⚡ | Remove item from front |
| peek() | O(1) ⚡ | See front item without removing |
| peek_rear() | O(1) ⚡ | See back item without removing |
| is_empty() | O(1) ⚡ | Check if queue is empty |
| size() | O(1) ⚡ | Get number of items |
| search() | O(n) | Find an item |
| clear() | O(1) | Remove all items |
| contains() | O(n) | Check if item exists |

## Implementation

```python
from collections import deque    # faster than list!

class Queue:
    def __init__(self):
        self.queue = deque()
        self._size = 0

    def enqueue(self, value):        # O(1) — add to back
        self.queue.append(value)
        self._size += 1

    def dequeue(self):               # O(1) — remove from front
        if self.is_empty():
            return "Queue Underflow! Queue is empty!"
        self._size -= 1
        return self.queue.popleft()

    def peek(self):                  # O(1) — see front
        if self.is_empty():
            return "Queue is empty!"
        return self.queue[0]

    def peek_rear(self):             # O(1) — see back
        if self.is_empty():
            return "Queue is empty!"
        return self.queue[-1]

    def is_empty(self):              # O(1)
        return self._size == 0

    def size(self):                  # O(1)
        return self._size

    def search(self, value):         # O(n)
        for i, item in enumerate(self.queue):
            if item == value:
                return f"Found at position {i} from front!"
        return "Not found!"

    def clear(self):                 # O(1)
        self.queue.clear()
        self._size = 0

    def contains(self, value):       # O(n)
        return value in self.queue

    def to_list(self):               # O(n)
        return list(self.queue)
```

> **Why deque instead of list?**
> `list.pop(0)` is O(n) because it shifts everything left.
> `deque.popleft()` is O(1) — designed for this exact purpose!

## Real World Uses

### 1. Printer Queue
```python
printer = Queue()
printer.enqueue("Resume.pdf")
printer.enqueue("Report.docx")
printer.enqueue("Invoice.xlsx")

print(f"Next to print: {printer.peek()}")   # Resume.pdf
printer.dequeue()    # Resume printed first!
printer.dequeue()    # Report printed second!
print(f"Remaining: {printer.size()}")        # 1
```

### 2. Customer Support Ticket System
```python
support = Queue()
support.enqueue("Nikhil - login issue")
support.enqueue("Priya  - payment failed")
support.enqueue("Sara   - account locked")

while not support.is_empty():
    ticket = support.dequeue()
    print(f"Resolving: {ticket}")
# Nikhil resolved first (raised ticket first!) ✅
```

### 3. CPU Task Scheduling
```python
cpu = Queue()
cpu.enqueue("Task A — compile code")
cpu.enqueue("Task B — run tests")
cpu.enqueue("Task C — deploy")
cpu.dequeue()    # Task A runs first! ✅
```

---

## ⚔️ Stack vs Queue — Final Comparison

| Feature | Stack | Queue |
|---------|-------|-------|
| Principle | LIFO | FIFO |
| Full name | Last In First Out | First In First Out |
| Add item | push() — to TOP | enqueue() — to BACK |
| Remove item | pop() — from TOP | dequeue() — from FRONT |
| See next item | peek() — TOP | peek() — FRONT |
| Real world | Undo, Back button | Printer, CPU tasks |
| Analogy | Stack of plates | Queue at counter |

---

# #️⃣ TOPIC 6 — Hash Tables

## What is a Hash Table?

A Hash Table is a data structure that stores data as **KEY → VALUE pairs**.
It uses a **hash function** to convert a key into an array index,
allowing near-instant access to any value.

```
Key      Hash Function    Index    Value
"Nikhil" ────────────→     3   →   95
"Priya"  ────────────→     7   →   87
"Sara"   ────────────→     1   →   91
```

## Why use a Hash Table?

- **O(1) average** for insert, search, delete — incredibly fast!
- **Key-value storage** — natural way to represent real world data
- **No searching needed** — jump directly to the value!
- Used everywhere in real world systems

## How does it work internally?

### Step 1 — Hash Function
```python
def _hash(self, key):
    return sum(ord(c) for c in str(key)) % self.size
# "Nikhil" → 78+105+107+104+105+108 = 607 → 607%10 = 7
```

### Step 2 — Collision (Chaining)
```
hash("Nikhil") → 7
hash("Priya")  → 7    ← COLLISION!

Solution — store both at index 7 using a list:
Index 7: [ [Nikhil, 95], [Priya, 87] ]
```

## Hash Table Big O

| Operation | Average | Worst Case |
|-----------|---------|------------|
| Insert | O(1) ⚡ | O(n) |
| Search | O(1) ⚡ | O(n) |
| Delete | O(1) ⚡ | O(n) |
| Access | O(1) ⚡ | O(n) |

## All dict Methods

| Method | Big O | Description |
|--------|-------|-------------|
| `d[key] = val` | O(1) | Insert or Update |
| `d[key]` | O(1) | Access (KeyError if missing) |
| `d.get(key, default)` | O(1) | Safe access with default |
| `del d[key]` | O(1) | Delete key |
| `d.pop(key)` | O(1) | Delete and return value |
| `key in d` | O(1) | Check if key exists |
| `d.keys()` | O(1) | Get all keys |
| `d.values()` | O(1) | Get all values |
| `d.items()` | O(1) | Get all key-value pairs |
| `d.update({...})` | O(k) | Merge another dict |
| `d.clear()` | O(1) | Remove all items |
| `len(d)` | O(1) | Number of keys |

## Real World Uses

### 1. Word Frequency Counter
```python
text = "nikhil is learning python nikhil is great at python"
freq = {}
for word in text.split():
    freq[word] = freq.get(word, 0) + 1
# {'nikhil': 2, 'is': 2, 'python': 2, 'learning': 1, ...}

most_common = max(freq, key=freq.get)
print(f"Most common: '{most_common}'")   # nikhil 😄
```

### 2. Caching
```python
cache = {}
def get_user(user_id):
    if user_id in cache:
        return cache[user_id]          # O(1) instant!
    data = fetch_from_database(user_id)
    cache[user_id] = data
    return data

get_user("U001")   # MISS → fetches from DB
get_user("U001")   # HIT  → instant from cache! ✅
```

### 3. First Non-Repeating Character (Interview Question!)
```python
def first_unique(s):
    freq = {}
    for char in s:
        freq[char] = freq.get(char, 0) + 1
    for char in s:
        if freq[char] == 1:
            return char
    return None

print(first_unique("nikhil"))   # 'n' ✅
print(first_unique("aabbcd"))   # 'c' ✅
print(first_unique("aabb"))     # None ✅
```

---

# 🌳 TOPIC 7 — Binary Trees & BST

## What is a Tree?

A Tree is a **hierarchical data structure**. Unlike arrays and linked lists
which are linear, trees branch out like a real tree!

```
          [10]          ← Root (topmost node, no parent)
         /    \
       [5]    [15]      ← Internal nodes (have children)
       / \    /  \
     [3] [7][12] [20]   ← Leaf nodes (no children)
```

## Key Terminology

| Term | Meaning | Example (above) |
|------|---------|----------------|
| Root | Topmost node, no parent | 10 |
| Parent | Node with children | 5, 15 |
| Child | Node below a parent | 3, 7, 12, 20 |
| Leaf | Node with NO children | 3, 7, 12, 20 |
| Height | Longest path root → leaf | 2 |
| Depth | Distance from root | 10=0, 5=1, 3=2 |
| Subtree | Any node + its children | [5, 3, 7] |

## What is a Binary Search Tree (BST)?

A BST is a Binary Tree with **ordering rules**:
- Left child is **SMALLER** than parent
- Right child is **LARGER** than parent

```
          [10]
         /    \
       [5]    [15]       ✅ 5 < 10, 15 > 10
       / \    /  \
     [3] [7][12] [20]    ✅ 3 < 5 < 7, 12 < 15 < 20
```

This ordering means **search becomes O(log n)** — each comparison
eliminates half the remaining tree!

## Tree Traversals

```
3 ways to visit every node!

Tree:       [10]
           /    \
         [5]    [15]
         / \
       [3] [7]

1. INORDER   (Left → Root → Right) → 3, 5, 7, 10, 15
   ✅ gives SORTED output in a BST!

2. PREORDER  (Root → Left → Right) → 10, 5, 3, 7, 15
   ✅ used to COPY a tree!

3. POSTORDER (Left → Right → Root) → 3, 7, 5, 15, 10
   ✅ used to DELETE a tree safely!
```

## BST Big O

| Operation | Average | Worst Case |
|-----------|---------|------------|
| Search | O(log n) ⚡ | O(n) |
| Insert | O(log n) ⚡ | O(n) |
| Delete | O(log n) ⚡ | O(n) |

> Worst case O(n) when inserting sorted data — tree becomes a linked list!
> Solution: Use AVL Tree (self-balancing)!

## Implementation

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.left  = None
        self.right = None

class BinarySearchTree:
    def __init__(self):
        self.root = None

    def insert(self, value):
        if self.root is None: self.root = Node(value)
        else: self._insert(self.root, value)

    def _insert(self, node, value):
        if value < node.value:
            if node.left is None: node.left = Node(value)
            else: self._insert(node.left, value)
        else:
            if node.right is None: node.right = Node(value)
            else: self._insert(node.right, value)

    def search(self, value):
        return self._search(self.root, value)

    def _search(self, node, value):
        if node is None:         return False
        if node.value == value:  return True
        elif value < node.value: return self._search(node.left, value)
        else:                    return self._search(node.right, value)

    def inorder(self):
        result = []
        self._inorder(self.root, result)
        return result

    def _inorder(self, node, result):
        if node:
            self._inorder(node.left, result)
            result.append(node.value)
            self._inorder(node.right, result)


# Real example — employee ID lookup
bst = BinarySearchTree()
for emp_id in [1050, 1025, 1075, 1010, 1040, 1060, 1090]:
    bst.insert(emp_id)

print(bst.inorder())         # [1010, 1025, 1040, 1050, 1060, 1075, 1090] ✅
print(bst.search(1040))      # True — found in O(log n)!
print(bst.search(9999))      # False
```

## Real World Uses

- **File systems** — directory tree structure
- **Databases** — B-trees for fast indexing
- **Expression parsing** — math expression trees

---

# ⚖️ TOPIC 8 — AVL Trees (Self-Balancing)

## What is an AVL Tree?

AVL = Self-Balancing BST. It **automatically rotates** nodes to stay balanced
so search is ALWAYS O(log n), never O(n)!

```
Normal BST (insert 1,2,3,4,5):    AVL Tree (same input):
[1]                                      [3]
  \                                     /   \
  [2]                                 [2]   [4]
    \                                 /       \
    [3]                             [1]       [5]
      \
      [4]      Height = 4!        Height = 2! ← always O(log n)!
        \
        [5]
```

## Balance Factor

```
Balance Factor = Height(left subtree) - Height(right subtree)

Allowed: -1, 0, +1

If balance = +2 or -2 → ROTATE to fix!

Example:
    [10]   ← balance = 2 - 0 = 2  ❌ TOO UNBALANCED!
    /
  [5]
  /
[3]

After Right Rotation:
  [5]
  / \
[3] [10]   ← balance = 1 - 1 = 0 ✅ FIXED!
```

## 4 Rotation Types

| Case | When | Fix |
|------|------|-----|
| Left-Left (LL) | Left subtree is left-heavy | Right Rotation |
| Right-Right (RR) | Right subtree is right-heavy | Left Rotation |
| Left-Right (LR) | Left subtree is right-heavy | Left then Right |
| Right-Left (RL) | Right subtree is left-heavy | Right then Left |

## AVL vs BST

```
BST  → O(log n) average, O(n) worst (can become unbalanced!)
AVL  → O(log n) ALWAYS guaranteed! ✅

With 1,000,000 items:
  BST worst case → 1,000,000 steps 😱
  AVL always     →        20 steps ⚡
```

## Real World Uses

- **Databases** needing guaranteed O(log n) lookup
- **Memory allocators** — fast search for free memory blocks
- **Router tables** — fast IP address lookup

---

# 🏔️ TOPIC 9 — Heaps

## What is a Heap?

A Heap is a **Complete Binary Tree** with one ordering rule!

```
MAX HEAP → Parent always LARGER than children
        [50]            ← always the MAXIMUM at top!
       /    \
     [30]  [40]
     / \   /
   [10][20][35]

MIN HEAP → Parent always SMALLER than children
        [10]            ← always the MINIMUM at top!
       /    \
     [20]  [30]
     / \   /
   [50][40][35]
```

## Stored as Array (no pointers needed!)

```
Tree:          Array:
    [50]       [50, 30, 40, 10, 20, 35]
   /    \       0   1   2   3   4   5
 [30]  [40]
 / \   /
[10][20][35]

Smart index formulas:
  Parent of i    = (i-1) // 2
  Left child     = 2*i + 1
  Right child    = 2*i + 2

Example: node at index 1 (value=30)
  Parent      = (1-1)//2 = 0  → 50 ✅
  Left child  = 2×1+1    = 3  → 10 ✅
  Right child = 2×1+2    = 4  → 20 ✅
```

## Heap Big O

| Operation | Big O |
|-----------|-------|
| Insert | O(log n) ⚡ |
| Get max/min | O(1) ⚡ |
| Remove max/min | O(log n) ⚡ |
| Build heap | O(n) |
| Search | O(n) |

## Real World Uses

### 1. Priority Queue — Hospital Emergency Room
```python
import heapq

er = []
# (priority, patient) — 1=critical, 3=normal
heapq.heappush(er, (3, "Nikhil  - Headache"))
heapq.heappush(er, (1, "Priya   - Heart Attack"))
heapq.heappush(er, (2, "Sara    - Broken Arm"))
heapq.heappush(er, (1, "Raj     - Stroke"))

while er:
    priority, patient = heapq.heappop(er)
    label = "🔴 CRITICAL" if priority==1 else "🟡 SERIOUS" if priority==2 else "🟢 NORMAL"
    print(f"{label} → {patient}")

# 🔴 CRITICAL → Priya   - Heart Attack   ✅
# 🔴 CRITICAL → Raj     - Stroke
# 🟡 SERIOUS  → Sara    - Broken Arm
# 🟢 NORMAL   → Nikhil  - Headache  (just a headache 😄)
```

### 2. Finding K Largest Elements
```python
import heapq

scores = [95, 87, 91, 78, 99, 88, 76, 94]
top3   = heapq.nlargest(3, scores)
print(f"Top 3 scores: {top3}")   # [99, 95, 94] ✅
```

### 3. Max Heap (negate trick!)
```python
import heapq

max_heap = []
for v in [30, 10, 50, 20, 40]:
    heapq.heappush(max_heap, -v)         # negate to fake max heap!

print(-heapq.heappop(max_heap))          # 50 ✅ (largest first!)
```

---

# 🔤 TOPIC 10 — Tries (Prefix Trees)

## What is a Trie?

A Trie stores **strings** where each **node is a single character**.
Words that share a prefix share the same path in the tree!

```
Storing: "cat", "car", "card", "care", "bat"

        root
       /    \
      c      b
      |      |
      a      a
     / \     |
    t*  r    t*         (* = marks end of word)
       / \
      d*  e*

"ca" prefix shared by cat, car, card, care — stored ONCE! ✅
```

## Why use a Trie?

- **Autocomplete** — Google/Bing search suggestions!
- **Spell checker** — check if word exists instantly
- **Prefix search** — find all words starting with "ca" in O(m)
- Much faster than linear search through list of strings!

## Trie Big O (m = length of word)

| Operation | Big O |
|-----------|-------|
| Insert | O(m) ⚡ |
| Search exact word | O(m) ⚡ |
| Prefix search | O(m) ⚡ |
| Autocomplete | O(m + results) |
| Delete | O(m) |

## Implementation

```python
class TrieNode:
    def __init__(self):
        self.children = {}      # char → TrieNode
        self.is_end   = False   # True = complete word ends here!

class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word):           # O(m)
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True

    def search(self, word):           # O(m) — exact match only!
        node = self.root
        for char in word:
            if char not in node.children: return False
            node = node.children[char]
        return node.is_end            # must be end of word!

    def starts_with(self, prefix):    # O(m) — prefix check!
        node = self.root
        for char in prefix:
            if char not in node.children: return False
            node = node.children[char]
        return True

    def autocomplete(self, prefix):   # O(m + results)
        node = self.root
        for char in prefix:
            if char not in node.children: return []
            node = node.children[char]
        results = []
        self._dfs(node, prefix, results)
        return results

    def _dfs(self, node, current, results):
        if node.is_end: results.append(current)
        for char, child in node.children.items():
            self._dfs(child, current + char, results)


# Real example — Google autocomplete
trie = Trie()
for term in ["python", "python tutorial", "data science",
             "data structures", "machine learning"]:
    trie.insert(term)

print(trie.autocomplete("py"))     # ['python', 'python tutorial'] ✅
print(trie.autocomplete("data"))   # ['data science', 'data structures'] ✅
print(trie.search("python"))       # True ✅
print(trie.search("pyth"))         # False ← prefix, not full word! ✅
print(trie.starts_with("pyth"))    # True  ← prefix exists! ✅
```

## Real World Uses

- **Google/Bing** — search autocomplete suggestions
- **IDE code completion** — suggests variable/function names
- **Spell checkers** — fast dictionary word lookup
- **IP routing tables** — network prefix matching

---

# 🕸️ TOPIC 11 — Graphs

## What is a Graph?

A Graph is a collection of **nodes (vertices)** connected by **edges**.
Unlike trees, there is no root, no parent-child rule, and nodes can
connect to ANY other node — even forming loops!

```
Nikhil ──── Priya
  |         /   \
Sara ── Raj    Divya

Nodes (Vertices) = Nikhil, Priya, Sara, Raj, Divya
Edges            = the connections between them
```

## Types of Graphs

```
1. UNDIRECTED — edges go BOTH ways
   Nikhil ←→ Priya   (Facebook friends — mutual!)

2. DIRECTED — edges go ONE way
   Nikhil → Priya    (Instagram — Nikhil follows Priya)
   Priya  ↛ Nikhil   (Priya doesn't follow back! 😂)

3. WEIGHTED — edges have COST or DISTANCE
   Ahmedabad ──530km── Mumbai
   Ahmedabad ──950km── Delhi

4. CYCLIC — has a loop (comes back to start)
   A → B → C → A

5. ACYCLIC — no loops
   A → B → C  (never loops back)
```

## How to Store a Graph

```
ADJACENCY LIST (most common):
  Each node stores a list of its neighbors!

  Nikhil → [Priya, Sara]
  Priya  → [Nikhil, Raj, Divya]
  Sara   → [Nikhil, Raj]

  ✅ Memory efficient for sparse graphs
  ✅ Fast to add new edges

ADJACENCY MATRIX:
  2D grid — 1=connected, 0=not connected

         Nikhil  Priya  Sara
  Nikhil    0      1     1
  Priya     1      0     0
  Sara      1      0     0

  ✅ O(1) edge lookup
  ❌ O(n²) memory — wasteful for large graphs
```

## Graph Traversals

```
BFS (Breadth First Search):
  Visit level by level! Uses a QUEUE.
  Like dropping a stone in water — ripples outward!
  1 → [2, 3] → [4, 5]

DFS (Depth First Search):
  Go as DEEP as possible first! Uses STACK or Recursion.
  Like exploring a maze — go far, then backtrack!
  1 → 2 → 4 → backtrack → 5 → backtrack → 3
```

## Graph Big O (V = vertices, E = edges)

| Operation | Adjacency List |
|-----------|---------------|
| Add vertex | O(1) |
| Add edge | O(1) |
| BFS / DFS | O(V + E) |
| Check edge exists | O(V) |

## Implementation

```python
from collections import deque

class Graph:
    def __init__(self, directed=False):
        self.adjacency_list = {}
        self.directed       = directed

    def add_edge(self, v1, v2):
        if v1 not in self.adjacency_list: self.adjacency_list[v1] = []
        if v2 not in self.adjacency_list: self.adjacency_list[v2] = []
        self.adjacency_list[v1].append(v2)
        if not self.directed:
            self.adjacency_list[v2].append(v1)   # both ways!

    def bfs(self, start):               # Level by level — uses Queue!
        visited = set([start])
        queue   = deque([start])
        result  = []
        while queue:
            v = queue.popleft()
            result.append(v)
            for n in self.adjacency_list[v]:
                if n not in visited:
                    visited.add(n)
                    queue.append(n)
        return result

    def dfs(self, start):               # Deep first — uses Recursion!
        visited = set()
        result  = []
        def _dfs(v):
            visited.add(v)
            result.append(v)
            for n in self.adjacency_list[v]:
                if n not in visited: _dfs(n)
        _dfs(start)
        return result

    def has_path(self, start, end):
        visited = set()
        def _dfs(v):
            if v == end: return True
            visited.add(v)
            for n in self.adjacency_list[v]:
                if n not in visited and _dfs(n): return True
            return False
        return _dfs(start)


# Real example — social network
g = Graph()
g.add_edge("Nikhil", "Priya")
g.add_edge("Nikhil", "Sara")
g.add_edge("Priya",  "Raj")
g.add_edge("Priya",  "Divya")
g.add_edge("Sara",   "Raj")

print(g.bfs("Nikhil"))                       # ['Nikhil','Priya','Sara','Raj','Divya']
print(g.dfs("Nikhil"))                       # ['Nikhil','Priya','Raj','Sara','Divya']
print(g.has_path("Nikhil", "Divya"))         # True ✅
print(g.has_path("Nikhil", "Karan"))         # False ✅ (Karan not in graph!)

# Real example — directed graph (Instagram)
ig = Graph(directed=True)
ig.add_edge("Nikhil", "Priya")    # Nikhil follows Priya
ig.add_edge("Priya",  "Nikhil")   # Priya follows back
ig.add_edge("Sara",   "Nikhil")   # Sara follows Nikhil
print(ig.adjacency_list["Nikhil"])   # ['Priya'] — Nikhil follows only Priya
```

## Real World Uses

- **Social networks** — friends, followers (Facebook, Instagram)
- **Google Maps** — shortest path between locations
- **Recommendation systems** — "people you may know"
- **Web crawlers** — crawl links between web pages

---

# 🔃 TOPIC 12 — Sorting Algorithms

## Why Sort?

```
Unsorted: [64, 25, 12, 45, 78, 11]
Sorted:   [11, 12, 25, 45, 64, 78]

Benefits:
→ Binary search only works on SORTED data!
→ Finding min/max becomes instant!
→ Clean reports and dashboards!
→ Databases rely on sorting constantly!
```

## All 7 Algorithms at a Glance

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | ❌ |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | ❌ |
| Counting Sort | O(n+k) | O(n+k) | O(n+k) | O(k) | ✅ |
| Bucket Sort | O(n+k) | O(n+k) | O(n²) | O(n) | ✅ |

> **Stable** = equal elements keep their original relative order

---

## 1️⃣ Bubble Sort

**Idea:** Compare adjacent pairs, swap if wrong order.
The LARGEST element "bubbles" to the end each pass!

```
[64, 25, 12, 45, 11]

Pass 1:
64>25 → swap → [25, 64, 12, 45, 11]
64>12 → swap → [25, 12, 64, 45, 11]
64>45 → swap → [25, 12, 45, 64, 11]
64>11 → swap → [25, 12, 45, 11, 64] ← 64 in place! ✅

Pass 2:
25>12 → swap → [12, 25, 45, 11, 64]
25<45 → ok
45>11 → swap → [12, 25, 11, 45, 64] ← 45 in place! ✅
...
```

```python
def bubble_sort(arr):
    arr = arr.copy()
    n   = len(arr)
    for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):     # last i already in place!
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swapped = True
        if not swapped: break              # already sorted → stop early!
    return arr

print(bubble_sort([64, 25, 12, 45, 11]))  # [11, 12, 25, 45, 64] ✅
```

---

## 2️⃣ Selection Sort

**Idea:** Find the MINIMUM, place it at the start. Repeat for remaining array!

```
[64, 25, 12, 45, 11]

Pass 1: min=11 at index 4 → swap with 64 → [11, 25, 12, 45, 64] ✅
Pass 2: min=12 at index 2 → swap with 25 → [11, 12, 25, 45, 64] ✅
Pass 3: min=25 already in place → no swap ✅
Done!
```

```python
def selection_sort(arr):
    arr = arr.copy()
    n   = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i+1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

print(selection_sort([64, 25, 12, 45, 11]))  # [11, 12, 25, 45, 64] ✅
```

---

## 3️⃣ Insertion Sort

**Idea:** Like sorting playing cards in your hand!
Pick each card and insert it into the correct position!

```
[64, 25, 12, 45, 11]

[64]             ← first card, already "sorted"
[25, 64]         ← 25 < 64, insert before
[12, 25, 64]     ← 12 smallest so far, insert at start
[12, 25, 45, 64] ← 45 between 25 and 64
[11, 12, 25, 45, 64] ← 11 smallest, insert at start ✅
```

```python
def insertion_sort(arr):
    arr = arr.copy()
    for i in range(1, len(arr)):
        key = arr[i]       # card to insert!
        j   = i - 1
        while j >= 0 and arr[j] > key:
            arr[j+1] = arr[j]    # shift right!
            j -= 1
        arr[j+1] = key           # place card here!
    return arr

print(insertion_sort([64, 25, 12, 45, 11]))  # [11, 12, 25, 45, 64] ✅
```

---

## 4️⃣ Merge Sort

**Idea:** Divide & Conquer! Split in half → sort each half → merge!

```
DIVIDE:
[64, 25, 12, 45, 11]
[64, 25]    [12, 45, 11]
[64][25]    [12][45][11]

MERGE:
[25, 64]    [12][11, 45]
[25, 64]    [11, 12, 45]
[11, 12, 25, 45, 64] ✅

Why O(n log n)?
→ Splits log n times (like binary search!)
→ Each merge step takes O(n)
→ Total = O(n × log n) = O(n log n)!
```

```python
def merge_sort(arr):
    if len(arr) <= 1: return arr
    mid   = len(arr) // 2
    left  = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j  = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]: result.append(left[i]);  i += 1
        else:                   result.append(right[j]); j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

print(merge_sort([64, 25, 12, 45, 11]))  # [11, 12, 25, 45, 64] ✅
```

---

## 5️⃣ Quick Sort

**Idea:** Pick a PIVOT → smaller elements left, larger right → recurse!

```
[64, 25, 12, 45, 11]   pivot = 45 (middle element)

Left  (< 45): [25, 12, 11]
Pivot:        [45]
Right (> 45): [64]

Now sort [25, 12, 11] with pivot=12:
  Left=[11], Mid=[12], Right=[25]

Final: [11,12,25] + [45] + [64] = [11, 12, 25, 45, 64] ✅
```

```python
def quick_sort(arr):
    if len(arr) <= 1: return arr
    pivot = arr[len(arr) // 2]
    left  = [x for x in arr if x < pivot]
    mid   = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left) + mid + quick_sort(right)

print(quick_sort([64, 25, 12, 45, 11]))  # [11, 12, 25, 45, 64] ✅
```

---

## 6️⃣ Counting Sort

**Idea:** Count how many times each number appears, then rebuild sorted array!
Only works for **integers in a known range!**

```
[4, 2, 2, 8, 3, 3, 1]

Step 1 — Count occurrences:
index: 0  1  2  3  4  5  6  7  8
count: 0  1  2  2  1  0  0  0  1

Step 2 — Rebuild:
1 appears 1 time  → [1]
2 appears 2 times → [1, 2, 2]
3 appears 2 times → [1, 2, 2, 3, 3]
4 appears 1 time  → [1, 2, 2, 3, 3, 4]
8 appears 1 time  → [1, 2, 2, 3, 3, 4, 8] ✅

O(n+k) where k = max value!
Faster than O(n log n) when k is small!
```

```python
def counting_sort(arr):
    max_val = max(arr)
    count   = [0] * (max_val + 1)
    for num in arr:
        count[num] += 1
    result = []
    for i, c in enumerate(count):
        result.extend([i] * c)
    return result

print(counting_sort([4, 2, 2, 8, 3, 3, 1]))  # [1, 2, 2, 3, 3, 4, 8] ✅
```

---

## 7️⃣ Bucket Sort

**Idea:** Distribute elements into buckets → sort each bucket → combine!
Best for **uniformly distributed float** data!

```
[0.42, 0.32, 0.73, 0.11, 0.85, 0.56]

Bucket 0 [0.0–0.2]: [0.11]
Bucket 1 [0.2–0.4]: [0.32, 0.42] → sort → [0.32, 0.42]
Bucket 2 [0.4–0.6]: [0.56]
Bucket 3 [0.6–0.8]: [0.73]
Bucket 4 [0.8–1.0]: [0.85]

Combine all: [0.11, 0.32, 0.42, 0.56, 0.73, 0.85] ✅
```

```python
def bucket_sort(arr):
    n            = len(arr)
    max_val      = max(arr)
    min_val      = min(arr)
    bucket_range = (max_val - min_val) / n + 1
    buckets      = [[] for _ in range(n)]
    for num in arr:
        idx = int((num - min_val) / bucket_range)
        if idx >= n: idx = n - 1
        buckets[idx].append(num)
    result = []
    for bucket in buckets:
        bucket.sort()
        result.extend(bucket)
    return result

print(bucket_sort([0.42, 0.32, 0.73, 0.11, 0.85, 0.56]))
# [0.11, 0.32, 0.42, 0.56, 0.73, 0.85] ✅
```

---

## When to Use Which Sorting Algorithm?

```
Small array (n < 10)?          → Insertion Sort  (simple, O(n) best case)
General purpose?               → Merge Sort      (guaranteed O(n log n))
Memory constrained?            → Quick Sort      (O(log n) space)
Data almost sorted?            → Insertion Sort  (O(n) best case!)
Integers with small range?     → Counting Sort   (O(n+k) super fast!)
Uniformly distributed floats?  → Bucket Sort     (O(n+k) average)
Python built-in?               → sorted()/.sort() (TimSort hybrid!)
```

---

# 🔍 TOPIC 13 — Searching Algorithms

## Why Searching?

```
You have 1,000,000 employees.
You need to find "Nikhil".

Bad search   → check every employee one by one → O(n) 🐢
Smart search → use patterns to find faster     → O(log n) ⚡

Choosing the right algorithm saves MILLIONS of operations!
```

## All 5 Algorithms at a Glance

| Algorithm | Best | Average | Worst | Space | Sorted? |
|-----------|------|---------|-------|-------|---------|
| Linear Search | O(1) | O(n) | O(n) | O(1) | ❌ No |
| Binary Search | O(1) | O(log n) | O(log n) | O(1) | ✅ Yes |
| Ternary Search | O(1) | O(log₃ n) | O(log₃ n) | O(1) | ✅ Yes |
| Jump Search | O(1) | O(√n) | O(√n) | O(1) | ✅ Yes |
| Exponential Search | O(1) | O(log n) | O(log n) | O(1) | ✅ Yes |

---

## 1️⃣ Linear Search

**Idea:** Check EVERY element one by one until you find the target!

```
Array:  [64, 25, 12, 45, 11]
Target: 45

Step 1: 64 == 45? ❌
Step 2: 25 == 45? ❌
Step 3: 12 == 45? ❌
Step 4: 45 == 45? ✅ FOUND at index 3!

Use when: Unsorted array OR small array
```

**Big O:** Best=O(1) | Average=O(n) | Worst=O(n) | Space=O(1)

```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i       # found! return index
    return -1              # not found!

arr = [64, 25, 12, 45, 11]
print(linear_search(arr, 45))   # 3 ✅
print(linear_search(arr, 99))   # -1 ✅
```

---

## 2️⃣ Binary Search

**Idea:** SORTED arrays only! Cut the array in HALF each step!

```
Sorted: [11, 12, 25, 45, 64, 78, 99]
Target: 78

Step 1: left=0, right=6, mid=3 → arr[3]=45 < 78 → go RIGHT!
Step 2: left=4, right=6, mid=5 → arr[5]=78 == 78 ✅ FOUND!

Only 2 steps for 7 elements!
For 1,000,000 elements → only ~20 steps! ⚡

Rule:
  arr[mid] == target → FOUND!
  arr[mid]  < target → go RIGHT (left  = mid+1)
  arr[mid]  > target → go LEFT  (right = mid-1)
```

**Big O:** Best=O(1) | Average=O(log n) | Worst=O(log n) | Space=O(1)

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = left + (right - left) // 2    # avoids overflow!
        if arr[mid] == target:   return mid
        elif arr[mid] < target:  left  = mid + 1   # go RIGHT!
        else:                    right = mid - 1   # go LEFT!
    return -1

arr = [11, 12, 25, 45, 64, 78, 99]    # MUST be sorted!
print(binary_search(arr, 78))   # 5 ✅
print(binary_search(arr, 50))   # -1 ✅
```

---

## 3️⃣ Ternary Search

**Idea:** Like Binary but divides into THREE parts using TWO midpoints!

```
Sorted: [11, 12, 25, 45, 64, 78, 99]
Target: 78

Step 1:
  mid1 = left + (right-left)//3 = 2 → arr[2]=25
  mid2 = right - (right-left)//3 = 4 → arr[4]=64

  78 > arr[mid2]=64 → go RIGHT third!

Step 2: left=5, mid1=5 → arr[5]=78 ✅ FOUND!

3 Regions:
  target < arr[mid1] → LEFT third   (right = mid1-1)
  target > arr[mid2] → RIGHT third  (left  = mid2+1)
  else               → MIDDLE third
```

**Big O:** Best=O(1) | Average=O(log₃ n) | Worst=O(log₃ n) | Space=O(1)

```python
def ternary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        third = (right - left) // 3
        mid1  = left  + third      # 1/3 point
        mid2  = right - third      # 2/3 point
        if arr[mid1] == target: return mid1
        if arr[mid2] == target: return mid2
        if target < arr[mid1]:    right = mid1 - 1   # left third!
        elif target > arr[mid2]:  left  = mid2 + 1   # right third!
        else:  left = mid1 + 1;   right = mid2 - 1   # middle third!
    return -1

arr = [11, 12, 25, 45, 64, 78, 99]
print(ternary_search(arr, 78))   # 5 ✅
print(ternary_search(arr, 50))   # -1 ✅
```

---

## 4️⃣ Jump Search

**Idea:** Jump in fixed steps of √n, then linear search backwards!

```
Sorted: [11, 12, 25, 45, 64, 78, 99, 112, 130]
Target: 78   |   Step = √9 = 3

JUMP phase:
  index 0→2  → arr[2]=25  < 78 → jump!
  index 3→5  → arr[5]=78 ≥ 78 → STOP! Overshot!

LINEAR phase (search back from index 3):
  arr[3]=45 < 78 → forward
  arr[4]=64 < 78 → forward
  arr[5]=78 == 78 ✅ FOUND!

Why √n step? Jump n/√n = √n times + √n linear = O(√n) total!
```

**Big O:** Best=O(1) | Average=O(√n) | Worst=O(√n) | Space=O(1)

```python
import math

def jump_search(arr, target):
    n    = len(arr)
    step = int(math.sqrt(n))    # optimal step = √n
    prev = 0
    while arr[min(step, n) - 1] < target:
        prev = step
        step += int(math.sqrt(n))
        if prev >= n: return -1
    while arr[prev] < target:
        prev += 1
        if prev == min(step, n): return -1
    if arr[prev] == target: return prev
    return -1

arr = [11, 12, 25, 45, 64, 78, 99, 112, 130]
print(jump_search(arr, 78))    # 5 ✅
print(jump_search(arr, 50))    # -1 ✅
```

---

## 5️⃣ Exponential Search

**Idea:** DOUBLE the index until overshoot, then Binary Search in that range!

```
Sorted: [11, 12, 25, 45, 64, 78, 99, 112, 130]
Target: 78

DOUBLING phase:
  index 1 → arr[1]=12  ≤ 78 → double to 2!
  index 2 → arr[2]=25  ≤ 78 → double to 4!
  index 4 → arr[4]=64  ≤ 78 → double to 8!
  index 8 → arr[8]=130 > 78 → STOP! Overshot!

Binary Search in arr[4..8] → finds 78 at index 5! ✅

Why useful?
→ Unbounded arrays (unknown size!)
→ Target near the start → finds range quickly!
```

**Big O:** Best=O(1) | Average=O(log n) | Worst=O(log n) | Space=O(1)

```python
def binary_search_range(arr, target, left, right):
    while left <= right:
        mid = left + (right - left) // 2
        if arr[mid] == target:   return mid
        elif arr[mid] < target:  left  = mid + 1
        else:                    right = mid - 1
    return -1

def exponential_search(arr, target):
    n = len(arr)
    if arr[0] == target: return 0
    i = 1
    while i < n and arr[i] <= target:
        i *= 2                              # double!
    left  = i // 2
    right = min(i, n - 1)
    return binary_search_range(arr, target, left, right)  # search range only!

arr = [11, 12, 25, 45, 64, 78, 99, 112, 130]
print(exponential_search(arr, 78))    # 5 ✅
print(exponential_search(arr, 11))    # 0 ✅
print(exponential_search(arr, 50))    # -1 ✅
```

---

## When to Use Which Searching Algorithm?

```
Unsorted array?              → Linear Search   (only option!)
Sorted array, general?       → Binary Search   (O(log n) always!)
Sorted, unimodal function?   → Ternary Search  (peak/min finding!)
Sorted, simple to code?      → Jump Search     (O(√n), easy!)
Unbounded / infinite array?  → Exponential     (unknown size!)
Target near the start?       → Exponential     (doubles fast!)
```

### Performance on n = 1,000,000 elements:
```
Linear Search      → up to 1,000,000 steps 😱
Jump Search        →          1,000 steps  (√1M)
Binary Search      →             20 steps  ⚡
Exponential Search →             20 steps  ⚡
```

---

# 🔤 TOPIC 14 — String Manipulation Algorithms

## Why String Manipulation?

```
Strings are everywhere in real software:
→ User input validation
→ Search engines
→ Password checkers
→ Chat apps, compilers, IDEs

These 7 problems are the most asked in coding interviews!
```

## All 7 Problems at a Glance

| Problem | Technique | Time | Space |
|---------|-----------|------|-------|
| Reverse a String | Two Pointer | O(n) | O(n) |
| Reverse Words | Split + Two Pointer | O(n) | O(n) |
| Rotations | Slicing | O(n) | O(n) |
| Remove Duplicates | Set + List | O(n) | O(k) |
| Most Repeated Char | Hash Map | O(n) | O(k) |
| Anagram | Sort / Frequency Map | O(n log n) / O(n) | O(n) |
| Palindrome | Two Pointer | O(n) | O(1) |

---

## 1️⃣ Reversing a String

**Idea:** Two pointers — one at start, one at end — swap and move inward!

```
s = ['H', 'e', 'l', 'l', 'o']
     ↑                    ↑
   left=0              right=4

Step 1: swap H ↔ o → ['o', 'e', 'l', 'l', 'H']
Step 2: swap e ↔ l → ['o', 'l', 'l', 'e', 'H']
Step 3: left=2, right=2 → STOP!
Result: 'olleH' ✅
```

```python
# Method 1 — Two Pointer (manual)
def string_reversal(s):
    s     = list(s)
    left  = 0
    right = len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left  += 1
        right -= 1
    return ''.join(s)

# Method 2 — Slicing (one-liner!)
def string_reversal_slice(s):
    return s[::-1]

print(string_reversal("Hello, World!"))   # '!dlroW ,olleH' ✅
print(string_reversal_slice("nikhil"))    # 'lihkin' ✅
```

---

## 2️⃣ Reversing Words

**Idea:** Split sentence into words, then reverse the ORDER of words (not letters)!

```
s = "Hello World from Python"

Split:  ['Hello', 'World', 'from', 'Python']
Swap:   ['Python', 'from', 'World', 'Hello']
Join:   'Python from World Hello' ✅

NOTE: Letters INSIDE each word stay the same!
      Only the ORDER of words is reversed!
```

```python
# Method 1 — Two Pointer (manual)
def reverse_words(s):
    words = s.split()
    left, right = 0, len(words) - 1
    while left < right:
        words[left], words[right] = words[right], words[left]
        left += 1; right -= 1
    return ' '.join(words)

# Method 2 — Built-in
def reverse_words_builtin(s):
    return ' '.join(s.split()[::-1])

print(reverse_words("Hello World from Python"))   # 'Python from World Hello' ✅
```

---

## 3️⃣ String Rotations

**Idea:** Shift all characters left or right by n positions!

```
s = "ABCDEF"   n = 2

LEFT  ROTATE: s[2:] + s[:2]  → 'CDEF' + 'AB'  → 'CDEFAB' ✅
RIGHT ROTATE: s[-2:] + s[:-2] → 'EF' + 'ABCD'  → 'EFABCD' ✅

IS ROTATION trick:
  s1+s1 = 'ABCDEFABCDEF'
  Is 'CDEFAB' in 'ABCDEFABCDEF'? → YES! ✅
  Any rotation of s1 always appears inside s1+s1!

Why n % len(s)?
  Rotating 8 on length-6 string = rotating by 2!
  8 % 6 = 2 → prevents unnecessary full rotations!
```

```python
def left_rotate(s, n):
    n = n % len(s)
    return s[n:] + s[:n]

def right_rotate(s, n):
    n = n % len(s)
    return s[-n:] + s[:-n]

def is_rotation(s1, s2):
    return len(s1) == len(s2) and s2 in (s1 + s1)

print(left_rotate("ABCDEF", 2))          # 'CDEFAB' ✅
print(right_rotate("ABCDEF", 2))         # 'EFABCD' ✅
print(is_rotation("ABCDEF", "CDEFAB"))   # True ✅
print(is_rotation("ABCDEF", "ABCXYZ"))   # False ✅
```

---

## 4️⃣ Removing Duplicates

**Idea:** Use a set to track seen characters — only keep first occurrence!

```
s = 'programming'

'p' → not seen → ADD → result=[p]
'r' → not seen → ADD → result=[p,r]
'o' → not seen → ADD → result=[p,r,o]
'g' → not seen → ADD → result=[p,r,o,g]
'r' → SEEN     → SKIP ❌
'a' → not seen → ADD → result=[p,r,o,g,a]
'm' → not seen → ADD → result=[p,r,o,g,a,m]
'm' → SEEN     → SKIP ❌
'i' → not seen → ADD → result=[p,r,o,g,a,m,i]
'n' → not seen → ADD → result=[p,r,o,g,a,m,i,n]
'g' → SEEN     → SKIP ❌

Result: 'programin' ✅
```

```python
def remove_duplicates(s):
    seen   = set()
    result = []
    for char in s:
        if char not in seen:
            seen.add(char)
            result.append(char)
    return ''.join(result)

print(remove_duplicates("programming"))   # 'programin' ✅
print(remove_duplicates("aabbccdd"))      # 'abcd' ✅
print(remove_duplicates("nikhil"))        # 'nikhl' ✅
```

---

## 5️⃣ Most Repeated Character

**Idea:** Count frequency of every character using a hash map, return max!

```
s = 'programming'

Frequency map: {p:1, r:2, o:1, g:2, a:1, m:2, i:1, n:1}

max by value → 'r' (first with count 2)

Result: 'r' ✅ (appears 2 times)
```

```python
def most_frequent(s):
    frequency = {}
    for char in s:
        frequency[char] = frequency.get(char, 0) + 1
    return max(frequency, key=frequency.get)

def most_frequent_with_count(s):
    frequency = {}
    for char in s:
        frequency[char] = frequency.get(char, 0) + 1
    best = max(frequency, key=frequency.get)
    return best, frequency[best]

char, count = most_frequent_with_count("programming")
print(f"'{char}' appears {count} times")   # 'r' appears 2 times ✅

char, count = most_frequent_with_count("aabbbbcc")
print(f"'{char}' appears {count} times")   # 'b' appears 4 times ✅
```

---

## 6️⃣ Anagrams

**Definition:** Two strings with the **same characters** in **different order**!

```
'listen' and 'silent'
  sorted: e,i,l,n,s,t  =  e,i,l,n,s,t  → ANAGRAM! ✅

'hello' and 'world'
  sorted: e,h,l,l,o  ≠  d,l,o,r,w      → NOT anagram! ❌

Method 1 — Sort:        O(n log n)
Method 2 — Freq Map:    O(n) ← faster!
```

```python
# Method 1 — Sort and compare
def anagram_sort(s1, s2):
    return sorted(s1.lower()) == sorted(s2.lower())

# Method 2 — Frequency map (O(n)!)
def anagram_frequency(s1, s2):
    if len(s1) != len(s2): return False
    freq = {}
    for char in s1: freq[char] = freq.get(char, 0) + 1   # count s1!
    for char in s2:
        freq[char] = freq.get(char, 0) - 1                # subtract s2!
        if freq[char] < 0: return False                    # s2 has extra char!
    return True

print(anagram_sort("listen", "silent"))       # True ✅
print(anagram_sort("hello", "world"))         # False ✅
print(anagram_frequency("listen", "silent"))  # True ✅
print(anagram_frequency("hello", "world"))    # False ✅
```

---

## 7️⃣ Palindrome

**Definition:** Reads the same forwards AND backwards!

```
'madam' → forward: m-a-d-a-m
           backward: m-a-d-a-m → SAME! ✅

'hello' → forward: h-e-l-l-o
           backward: o-l-l-e-h → DIFFERENT! ❌

Two Pointer:
  m  a  d  a  m
  ↑              ↑
left=0        right=4

Step 1: s[0]='m' == s[4]='m' ✅ → move inward
Step 2: s[1]='a' == s[3]='a' ✅ → move inward
Step 3: left=2 >= right=2 → STOP → Palindrome! ✅
```

```python
# Method 1 — Two Pointer (O(1) space!)
def palindrome(s):
    left  = 0
    right = len(s) - 1
    while left < right:
        if s[left] != s[right]: return False
        left  += 1
        right -= 1
    return True

# Method 2 — Slicing (O(n) space)
def palindrome_slice(s):
    return s == s[::-1]

# Real world — ignore spaces and case!
def palindrome_clean(s):
    cleaned = ''.join(c.lower() for c in s if c.isalnum())
    return palindrome(cleaned)

print(palindrome("madam"))                           # True ✅
print(palindrome("hello"))                           # False ✅
print(palindrome_clean("A man a plan a canal Panama"))  # True ✅
```

---

# 🔁 TOPIC 15 — Recursion

## What is Recursion?

```
A function that calls ITSELF to solve smaller
versions of the same problem!

factorial(5)
  └─ 5 × factorial(4)
         └─ 4 × factorial(3)
                └─ 3 × factorial(2)
                       └─ 2 × factorial(1)
                              └─ 1 × factorial(0)
                                     └─ 1  ← BASE CASE!
```

## Every Recursive Function MUST have:

```
1. BASE CASE      → the STOPPING condition (prevents infinite loop!)
2. RECURSIVE CASE → calls itself with a SMALLER input!

Without base case → Stack Overflow! 💥
Without getting smaller → infinite recursion! 💥
```

## How the Call Stack Works:

```
PUSH phase (going DOWN):     POP phase (coming back UP):
┌─────────────────┐          factorial(0) → 1
│ factorial(0)    │          factorial(1) → 1×1 = 1
│ factorial(1)    │          factorial(2) → 2×1 = 2
│ factorial(2)    │          factorial(3) → 3×2 = 6 ✅
│ factorial(3)    │
└─────────────────┘
      CALL STACK
```

## Recursion vs Iteration:

| | Recursion | Iteration |
|--|-----------|----------|
| Code | Cleaner, elegant | More explicit |
| Memory | O(n) call stack | O(1) |
| Speed | Slightly slower | Slightly faster |
| Best for | Trees, Graphs, D&C | Simple loops |

---

## 1️⃣ Factorial

**Formula:** `n! = n × (n-1)!` | **Base:** `factorial(0) = 1`

```
factorial(4):
  → 4 × factorial(3)
         → 3 × factorial(2)
                → 2 × factorial(1)
                       → 1 × factorial(0)
                              → 1  ← BASE!
Coming back:
  factorial(1) = 1×1 = 1
  factorial(2) = 2×1 = 2
  factorial(3) = 3×2 = 6
  factorial(4) = 4×6 = 24 ✅
```

**Big O:** Time=O(n) | Space=O(n) — n frames on call stack!

```python
def factorial(n):
    if n < 0:  return "Negative number is not allowed!"
    if n == 0: return 1                      # BASE CASE!
    return n * factorial(n - 1)              # RECURSIVE CASE!

print(factorial(0))    # 1 ✅
print(factorial(5))    # 120 ✅
print(factorial(10))   # 3628800 ✅
print(factorial(-3))   # Negative number is not allowed! ✅
```

---

## 2️⃣ Fibonacci

**Formula:** `fib(n) = fib(n-1) + fib(n-2)` | **Base:** `fib(0)=0, fib(1)=1`

```
Sequence: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34 ...

⚠️ Naive recursion is O(2ⁿ) — fib(3) computed multiple times!

fib(5):
          fib(5)
         /      \
      fib(4)   fib(3)  ← computed twice!
      /    \
   fib(3) fib(2)       ← computed again!

✅ Fix: Memoization — cache results → O(n)!
```

**Big O:** Naive=O(2ⁿ) 😱 | Memoized=O(n) ✅ | Space=O(n)

```python
# Naive — O(2ⁿ)
def fibonacci(n):
    if n < 0:  return "Negative number is not allowed!"   # guard FIRST!
    if n == 0: return 0
    if n == 1: return 1
    return fibonacci(n - 1) + fibonacci(n - 2)

# Memoized — O(n) ← much faster!
def fibonacci_memo(n, memo={}):
    if n < 0:      return "Negative number is not allowed!"
    if n == 0:     return 0
    if n == 1:     return 1
    if n in memo:  return memo[n]      # already computed? return instantly!
    memo[n] = fibonacci_memo(n-1, memo) + fibonacci_memo(n-2, memo)
    return memo[n]

print([fibonacci(i) for i in range(10)])   # [0,1,1,2,3,5,8,13,21,34] ✅
print(fibonacci_memo(30))                   # 832040 — instant! ✅
```

---

## 3️⃣ Recursive Binary Search

**Idea:** Same as iterative, but pass the range recursively!

```
binary_search(arr, 9, L=0, R=8)
  M=4 → arr[4]=5 < 9 → go RIGHT!
  └─ binary_search(arr, 9, L=5, R=8)
       M=6 → arr[6]=7 < 9 → go RIGHT!
       └─ binary_search(arr, 9, L=7, R=8)
            M=7 → arr[7]=8 < 9 → go RIGHT!
            └─ binary_search(arr, 9, L=8, R=8)
                 M=8 → arr[8]=9 == 9 ✅ return 8!

BASE CASES:
  L > R          → return -1  (not found!)
  arr[M]==target → return M   (found!)
```

**Big O:** Time=O(log n) | Space=O(log n) — log n frames on call stack!

```python
def binary_search_recursive(arr, target, L, R):
    if L > R: return -1                                 # BASE CASE — not found!
    M = L + ((R - L) // 2)
    if arr[M] == target: return M                       # BASE CASE — found!
    if arr[M] > target:  return binary_search_recursive(arr, target, L, M-1)   # LEFT!
    return binary_search_recursive(arr, target, M+1, R)                         # RIGHT!

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(binary_search_recursive(arr, 9,  0, len(arr)-1))   # 8 ✅
print(binary_search_recursive(arr, 1,  0, len(arr)-1))   # 0 ✅
print(binary_search_recursive(arr, 10, 0, len(arr)-1))   # -1 ✅
```

---

## 4️⃣ Recursive String Reversal

**Idea:** Take LAST character + recursively reverse the rest!

```
reverse('Hello')
  = 'o' + reverse('Hell')
           = 'l' + reverse('Hel')
                    = 'l' + reverse('He')
                             = 'e' + reverse('H')
                                      = 'H' + reverse('')
                                               = ''  ← BASE CASE!

Coming back up:
  'H' → 'eH' → 'leH' → 'lleH' → 'olleH' ✅
```

**Big O:** Time=O(n) | Space=O(n) — n frames on call stack!

```python
def reverse_string(s):
    if len(s) == 0: return s                 # BASE CASE!
    return s[-1] + reverse_string(s[:-1])    # RECURSIVE CASE!

print(reverse_string("nikhil"))         # 'lihkin' ✅
print(reverse_string("Hello, World!"))  # '!dlroW ,olleH' ✅
print(reverse_string("racecar"))        # 'racecar' ✅
```

---

## 5️⃣ Recursive Palindrome

**Idea:** Compare outermost characters — if match, recurse inward!

```
is_palindrome('madam', left=0, right=4)

Step 1: s[0]='m' == s[4]='m' ✅ → recurse inward!
  └─ is_palindrome('madam', left=1, right=3)
       Step 2: s[1]='a' == s[3]='a' ✅ → recurse inward!
         └─ is_palindrome('madam', left=2, right=2)
              Step 3: left=2 >= right=2 → BASE CASE → True! ✅

BASE CASES:
  left >= right        → True  (all matched!)
  s[left] != s[right] → False (mismatch!)
```

**Big O:** Time=O(n) | Space=O(n) — n/2 frames on call stack!

```python
def is_palindrome_recursive(s, left, right):
    if left >= right:       return True                          # BASE CASE!
    if s[left] != s[right]: return False                         # BASE CASE!
    return is_palindrome_recursive(s, left + 1, right - 1)       # RECURSIVE!

# Wrapper — no need to pass left/right manually!
def palindrome_recursive(s):
    return is_palindrome_recursive(s, 0, len(s) - 1)

print(palindrome_recursive("madam"))    # True ✅
print(palindrome_recursive("hello"))    # False ✅
print(palindrome_recursive("racecar"))  # True ✅
```

---

## When to Use Recursion vs Iteration?

```
Use RECURSION when:
  → Problem naturally divides into smaller subproblems
  → Working with Trees, Graphs, Divide & Conquer
  → Code clarity matters more than raw speed
  → e.g. Tree traversal, Merge Sort, DFS

Use ITERATION when:
  → Simple loops are sufficient
  → Memory efficiency is critical (O(1) vs O(n) stack)
  → Risk of deep recursion / Stack Overflow
  → e.g. Summing a list, finding max, linear search
```

---

# 🏆 Complete DSA Summary — All 15 Topics

## All Data Structures at a Glance

| Structure | Access | Search | Insert | Use When |
|-----------|--------|--------|--------|----------|
| Array | O(1) ⚡ | O(n) | O(1) end / O(n) start | Fast index access |
| Linked List | O(n) | O(n) | O(1) start | Fast insert at front |
| Stack | O(n) | O(n) | O(1) | LIFO — undo, history |
| Queue | O(n) | O(n) | O(1) | FIFO — scheduling |
| Hash Table | O(1) ⚡ | O(1) ⚡ | O(1) ⚡ | Key-value lookup |
| BST | — | O(log n) avg | O(log n) avg | Ordered data |
| AVL Tree | — | O(log n) ✅ | O(log n) ✅ | Balanced BST always |
| Heap | — | O(n) | O(log n) | Get min/max fast |
| Trie | — | O(m) ⚡ | O(m) ⚡ | String prefix search |
| Graph | — | O(V+E) | O(1) | Networks, maps |

## All Searching Algorithms at a Glance

| Algorithm | Best | Worst | Sorted? | Best For |
|-----------|------|-------|---------|---------|
| Linear | O(1) | O(n) | No | Unsorted / small arrays |
| Binary | O(1) | O(log n) | Yes | General purpose |
| Ternary | O(1) | O(log₃ n) | Yes | Unimodal functions |
| Jump | O(1) | O(√n) | Yes | Simple sorted search |
| Exponential | O(1) | O(log n) | Yes | Unbounded arrays |

## All Sorting Algorithms at a Glance

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | ❌ |
| Insertion | O(n) | O(n²) | O(n²) | O(1) | ✅ |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | ✅ |
| Quick | O(n log n) | O(n log n) | O(n²) | O(log n) | ❌ |
| Counting | O(n+k) | O(n+k) | O(n+k) | O(k) | ✅ |
| Bucket | O(n+k) | O(n+k) | O(n²) | O(n) | ✅ |

## All String Problems at a Glance

| Problem | Technique | Time | Space |
|---------|-----------|------|-------|
| Reverse String | Two Pointer | O(n) | O(n) |
| Reverse Words | Split + Swap | O(n) | O(n) |
| Rotation | Slicing | O(n) | O(n) |
| Remove Duplicates | Set + List | O(n) | O(k) |
| Most Frequent Char | Hash Map | O(n) | O(k) |
| Anagram | Freq Map | O(n) | O(k) |
| Palindrome | Two Pointer | O(n) | O(1) |

## All Recursion Problems at a Glance

| Problem | Base Case | Time | Space |
|---------|-----------|------|-------|
| Factorial | n==0 → 1 | O(n) | O(n) |
| Fibonacci (naive) | n≤1 → n | O(2ⁿ) | O(n) |
| Fibonacci (memo) | n≤1 → n | O(n) | O(n) |
| Binary Search | L>R or found | O(log n) | O(log n) |
| String Reversal | len==0 | O(n) | O(n) |
| Palindrome | left≥right | O(n) | O(n) |

## Master Big O Reference

```
O(1)       → Constant    — instant, no loops
O(log n)   → Log         — binary search, halving each step
O(√n)      → Square root — jump search
O(n)       → Linear      — single loop
O(n log n) → Log-Linear  — efficient sorting
O(n²)      → Quadratic   — nested loops (avoid for large n!)
O(2ⁿ)      → Exponential → avoid! (naive recursion without memo)
```

## Master Decision Guide

```
CHOOSING A DATA STRUCTURE:
  Fast access by index?           → Array
  Fast insert at start?           → Linked List
  LIFO (undo, back button)?       → Stack
  FIFO (queue, scheduling)?       → Queue
  Key-value O(1) lookup?          → Hash Table
  Sorted data, range queries?     → BST / AVL Tree
  Always need min or max fast?    → Heap
  Autocomplete, prefix search?    → Trie
  Model a network or map?         → Graph

CHOOSING A SEARCH ALGORITHM:
  Unsorted array?                 → Linear Search
  Sorted, general purpose?        → Binary Search
  Sorted, unknown size?           → Exponential Search
  Peak in unimodal function?      → Ternary Search

CHOOSING A SORT ALGORITHM:
  General purpose?                → Merge Sort
  Memory constrained?             → Quick Sort
  Small or nearly sorted?         → Insertion Sort
  Integers, small range?          → Counting Sort
  Uniform float distribution?     → Bucket Sort
  Python production code?         → sorted() / .sort()

RECURSION vs ITERATION:
  Trees, Graphs, D&C problems?    → Recursion
  Simple loops, memory critical?  → Iteration
  Fibonacci, large n?             → Memoized Recursion
```

---

# Technologies Used

- **Python 3.11**
- **collections.deque** — efficient Queue implementation
- **Built-in dict** — Hash Table implementation
- **heapq module** — built-in Min Heap / Priority Queue
- **math module** — math.sqrt() for Jump Search
