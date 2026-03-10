# Data Structures & Algorithms (DSA)

This document covers all the core Data Structures and Algorithms topics
studied today — explained in detail with theory, real world examples,
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
```

**Real world:** Comparing every employee's name with every other employee's name.

---

### O(log n) — Logarithmic Time
```
Cuts the problem in HALF each step!

n = 1000   → ~10 steps
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
```

**Real world:** Finding a word in a dictionary by opening the middle, then deciding left or right.

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

arr[2]          # O(1) — access index 2 → 30
arr.append(60)  # O(1) — add at end
arr.insert(0,5) # O(n) — insert at start, shifts everyone
arr.pop()       # O(1) — remove from end
arr.pop(0)      # O(n) — remove from start, shifts everyone
30 in arr       # O(n) — search checks every element
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
        self.next = None      # pointer to next node

class LinkedList:
    def __init__(self):
        self.head = None
        self.size = 0

    def insert_at_start(self, value):    # O(1)
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node
        self.size += 1

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
        removed = self.head.value
        self.head = self.head.next
        self.size -= 1
        return removed

    def search(self, value):             # O(n)
        current = self.head
        position = 0
        while current:
            if current.value == value:
                return f"Found at position {position}!"
            current = current.next
            position += 1
        return "Not found!"

    def display(self):
        elements = []
        current = self.head
        while current:
            elements.append(str(current.value))
            current = current.next
        print(" → ".join(elements) + " → None")
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
# Every action is pushed onto a stack
# Ctrl+Z pops the last action
undo_stack.push("typed Hello")
undo_stack.push("typed World")
undo_stack.pop()    # undoes "typed World" first!
```

### 2. Bracket Matching (Interview Question!)
```python
# Check if brackets are balanced
# ({[]}) → balanced ✅
# ([)]   → not balanced ❌
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
```

### 3. Browser Back Button
```python
# Each visited page pushed to history stack
# Back button pops the last page
history.push("google.com")
history.push("github.com")
history.pop()    # goes back to google.com!
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
# Documents sent in order, printed in order!
printer.enqueue("Resume.pdf")
printer.enqueue("Report.docx")
printer.dequeue()    # Resume printed first!
```

### 2. Customer Support
```python
# First customer to raise ticket = first to be resolved!
support.enqueue("Nikhil - issue with login")
support.enqueue("Priya  - payment failed")
support.dequeue()    # Nikhil helped first!
```

### 3. CPU Task Scheduling
```python
# OS queues tasks, processes them in order!
cpu_queue.enqueue("Task A")
cpu_queue.enqueue("Task B")
cpu_queue.dequeue()    # Task A runs first!
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
# Converts any key into a number (index)
def _hash(self, key):
    return sum(ord(c) for c in str(key)) % self.size
# "Nikhil" → 78+105+107+104+105+108 = 607 → 607%10 = 7
```

### Step 2 — Storing value
```
array[7] = 95    # Nikhil's marks stored at index 7
```

### Step 3 — Retrieving value
```
hash("Nikhil") → 7 → array[7] → 95    # O(1)!
```

## What is a Collision?

A **collision** happens when two different keys produce the same index.

```
hash("Nikhil") → 7
hash("Priya")  → 7    ← COLLISION! Both want index 7!
```

### Solution — Chaining
Store multiple values at same index using a list:
```
Index 7: [ [Nikhil, 95], [Priya, 87] ]
```

## Hash Table Big O

| Operation | Average | Worst Case |
|-----------|---------|------------|
| Insert | O(1) ⚡ | O(n) |
| Search | O(1) ⚡ | O(n) |
| Delete | O(1) ⚡ | O(n) |
| Access | O(1) ⚡ | O(n) |

> Worst case O(n) only if ALL keys collide — extremely rare with a good hash function!

## Python dict — Built-in Hash Table

```python
# Python's dict IS a hash table!

d = {}

# Insert / Update — O(1)
d["Nikhil"] = 95
d["Priya"]  = 87

# Access — O(1)
print(d["Nikhil"])           # 95

# Safe access with default — O(1)
print(d.get("Karan", 0))     # 0 (not found!)

# Delete — O(1)
del d["Priya"]

# Check existence — O(1)
print("Nikhil" in d)         # True

# All keys, values, pairs
print(d.keys())
print(d.values())
print(d.items())

# Update multiple at once
d.update({"bonus": 15000, "rank": 1})

# Remove and return
val = d.pop("rank")

# Clear all
d.clear()
```

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
text = "nikhil is learning python nikhil is great"
freq = {}
for word in text.split():
    freq[word] = freq.get(word, 0) + 1
# {'nikhil': 2, 'is': 2, 'learning': 1, ...}
```

### 2. Caching (Memoization)
```python
cache = {}
def get_data(key):
    if key in cache:
        return cache[key]    # O(1) instant!
    result = fetch_from_db(key)  # slow!
    cache[key] = result
    return result
```

### 3. Employee Lookup System
```python
employees = {
    "EMP001": {"name": "Nikhil", "dept": "Finance"},
    "EMP002": {"name": "Priya",  "dept": "HR"},
}
# O(1) lookup by ID — no searching!
emp = employees.get("EMP001")
```

### 4. First Non-Repeating Character (Interview Question!)
```python
def first_unique(s):
    freq = {}
    for char in s:
        freq[char] = freq.get(char, 0) + 1
    for char in s:
        if freq[char] == 1:
            return char
    return None
# "nikhil" → 'n'
# "aabbcd" → 'c'
```

---

# 🏆 Complete DSA Summary

## All Data Structures at a Glance

| Structure | Access | Search | Insert Start | Insert End | Use When |
|-----------|--------|--------|-------------|-----------|----------|
| Array | O(1) ⚡ | O(n) | O(n) 🐢 | O(1) ⚡ | Fast access by index |
| Linked List | O(n) 🐢 | O(n) | O(1) ⚡ | O(n) 🐢 | Fast insert at start |
| Stack | O(n) | O(n) | O(1) ⚡ | O(1) ⚡ | LIFO — undo, history |
| Queue | O(n) | O(n) | O(1) ⚡ | O(1) ⚡ | FIFO — scheduling |
| Hash Table | O(1) ⚡ | O(1) ⚡ | O(1) ⚡ | O(1) ⚡ | Key-value lookup |

## Which to Use When?

```
Need fast access by index?          → Array
Need fast insert/delete at start?   → Linked List
Need LIFO (last in first out)?      → Stack
Need FIFO (first in first out)?     → Queue
Need fast key-value lookup?         → Hash Table
```

## Big O Quick Reference

```
O(1)      → Constant    — instant, no loops
O(log n)  → Log         — binary search, cuts in half
O(n)      → Linear      — single loop
O(n log n)→ Log-Linear  → good sorting (Python sort)
O(n²)     → Quadratic   — nested loops
O(2ⁿ)     → Exponential → avoid! very slow
```

---

# Technologies Used

- **Python 3.11**
- **collections.deque** — efficient Queue implementation
- **Built-in dict** — Hash Table implementation
