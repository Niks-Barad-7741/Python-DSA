# 🔢 Sorting Algorithms — Data Structures & Algorithms

This project demonstrates the implementation of fundamental **Sorting Algorithms**
using Python as part of a **Data Structures and Algorithms (DSA)** learning course.

The notebook contains implementations and explanations of several classic sorting
techniques used in computer science and software engineering.

---

# 📚 Algorithms Covered

- Bubble Sort
- Insertion Sort
- Selection Sort
- Merge Sort
- Quick Sort
- Counting Sort
- Bucket Sort

Each algorithm includes:
- Step-by-step visual walkthrough
- Example input/output
- Python implementation
- Time complexity

---

# 🫧 1. Bubble Sort

Bubble Sort repeatedly compares adjacent elements and swaps them if they are in the wrong order.
The largest unsorted element "bubbles up" to its correct position after each pass.

### 🎬 Step-by-Step Visual

```
Array: [ 5 | 6 | 1 | 3 ]
─────────────────────────────────────────────────────────────
STEP 01 — Placing the 1st largest element at its correct position

          i=0  ┌───┬───┬───┬───┐
               │ 5 │ 6 │ 1 │ 3 │   (start)
               └───┴───┴───┴───┘

                       ╭──Swap──╮
          i=1  ┌───┬───┬───┬───┐
               │ 5 │ 6 │ 1 │ 3 │   6 > 1 → SWAP
               └───┴───┴───┴───┘

                           ╭──Swap──╮
          i=2  ┌───┬───┬───┬───┐
               │ 5 │ 1 │ 6 │ 3 │   6 > 3 → SWAP
               └───┴───┴───┴───┘

               ┌───┬───┬───┬───┐             Sorted
               │ 5 │ 1 │ 3 │ 6 │  ◄──────────────┤ 6 ✅
               └───┴───┴───┴───┘

─────────────────────────────────────────────────────────────
STEP 02 — Placing the 2nd largest element at its correct position

                   ╭──Swap──╮
          i=0  ┌───┬───┬───┬───┐
               │ 5 │ 1 │ 3 │ 6 │   5 > 1 → SWAP
               └───┴───┴───┴───┘

                       ╭──Swap──╮
          i=1  ┌───┬───┬───┬───┐
               │ 1 │ 5 │ 3 │ 6 │   5 > 3 → SWAP
               └───┴───┴───┴───┘

               ┌───┬───┬───┬───┐        Sorted Elements
               │ 1 │ 3 │ 5 │ 6 │  ◄──────────────┤ 5 ✅ 6 ✅
               └───┴───┴───┴───┘

─────────────────────────────────────────────────────────────
STEP 03 — Placing the 3rd largest element at its correct position

               ╭──No Swap──╮
          i=0  ┌───┬───┬───┬───┐
               │ 1 │ 3 │ 5 │ 6 │   1 < 3 → No Swap
               └───┴───┴───┴───┘

               ┌───┬───┬───┬───┐   ◄──── Sorted Elements ────►
               │ 1 │ 3 │ 5 │ 6 │         All sorted ✅
               └───┴───┴───┴───┘

─────────────────────────────────────────────────────────────
Result: [ 1 | 3 | 5 | 6 ]
```

### Example

Input: `[5, 6, 1, 3]`
Output: `[1, 3, 5, 6]`

### Python Implementation

```python
def bubble_sort(arr):
    n = len(arr)

    for i in range(n):
        for j in range(0, n-i-1):
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]

    return arr
```

### Complexity

| Case    | Time Complexity |
|---------|-----------------|
| Best    | O(n)            |
| Average | O(n²)           |
| Worst   | O(n²)           |

---

# ✋ 2. Insertion Sort

Insertion Sort builds a sorted list one element at a time by picking each element
and inserting it into its correct position within the already-sorted portion.

### 🎬 Step-by-Step Visual

```
Array: [ 8 | 3 | 5 | 2 ]
─────────────────────────────────────────────────────────────
STEP 01 — Insert element 3 into sorted portion

  Sorted  │ Unsorted
  ────────┼─────────────────────
  ┌───┐   │  ┌───┬───┬───┐
  │ 8 │   │  │ 3 │ 5 │ 2 │       key = 3
  └───┘   │  └───┴───┴───┘

  key(3) < 8 → shift 8 right, insert 3 at start

               ┌───┬───┬───┬───┐
               │ 3 │ 8 │ 5 │ 2 │
               └───┴───┴───┴───┘
               └───┘
               Sorted ✅

─────────────────────────────────────────────────────────────
STEP 02 — Insert element 5 into sorted portion

  Sorted      │ Unsorted
  ────────────┼─────────────────
  ┌───┬───┐   │  ┌───┬───┐
  │ 3 │ 8 │   │  │ 5 │ 2 │       key = 5
  └───┴───┘   │  └───┴───┘

  key(5) < 8 → shift 8 right
  key(5) > 3 → stop, insert 5 here

               ┌───┬───┬───┬───┐
               │ 3 │ 5 │ 8 │ 2 │
               └───┴───┴───┴───┘
               └─────────┘
               Sorted ✅

─────────────────────────────────────────────────────────────
STEP 03 — Insert element 2 into sorted portion

  Sorted          │ Unsorted
  ────────────────┼───────────
  ┌───┬───┬───┐   │  ┌───┐
  │ 3 │ 5 │ 8 │   │  │ 2 │       key = 2
  └───┴───┴───┘   │  └───┘

  key(2) < 8 → shift 8 right
  key(2) < 5 → shift 5 right
  key(2) < 3 → shift 3 right
  Start of array  → insert 2 at position 0

               ┌───┬───┬───┬───┐   ◄──── Sorted Elements ────►
               │ 2 │ 3 │ 5 │ 8 │         All sorted ✅
               └───┴───┴───┴───┘

─────────────────────────────────────────────────────────────
Result: [ 2 | 3 | 5 | 8 ]
```

### Example

Input: `[8, 3, 5, 2]`
Output: `[2, 3, 5, 8]`

### Python Implementation

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1

        while j >= 0 and key < arr[j]:
            arr[j + 1] = arr[j]
            j -= 1

        arr[j + 1] = key

    return arr
```

### Complexity

| Case    | Time Complexity |
|---------|-----------------|
| Best    | O(n)            |
| Average | O(n²)           |
| Worst   | O(n²)           |

---

# 🔎 3. Selection Sort

Selection Sort repeatedly finds the minimum element from the unsorted portion
and places it at the beginning of the unsorted portion.

### 🎬 Step-by-Step Visual

```
Array: [ 29 | 10 | 14 | 37 ]
─────────────────────────────────────────────────────────────
STEP 01 — Place the 1st smallest element at position 0

  ┌────┬────┬────┬────┐
  │ 29 │ 10 │ 14 │ 37 │
  └────┴────┴────┴────┘
    ↑    ↑    ↑    ↑
   i=0  scan all  →  min = 10  (at index 1)

  Swap  29 ↔ 10

               ┌────┬────┬────┬────┐            Sorted
               │ 10 │ 29 │ 14 │ 37 │  ◄──────────┤ 10 ✅
               └────┴────┴────┴────┘

─────────────────────────────────────────────────────────────
STEP 02 — Place the 2nd smallest element at position 1

  ┌────┬────┬────┬────┐
  │ 10 │ 29 │ 14 │ 37 │
  └────┴────┴────┴────┘
         ↑    ↑    ↑
        i=1  scan rest  →  min = 14  (at index 2)

  Swap  29 ↔ 14

               ┌────┬────┬────┬────┐       Sorted Elements
               │ 10 │ 14 │ 29 │ 37 │  ◄──────────────┤ 10 ✅ 14 ✅
               └────┴────┴────┴────┘

─────────────────────────────────────────────────────────────
STEP 03 — Place the 3rd smallest element at position 2

  ┌────┬────┬────┬────┐
  │ 10 │ 14 │ 29 │ 37 │
  └────┴────┴────┴────┘
               ↑    ↑
              i=2  scan rest  →  min = 29  (already in place)

  No Swap needed

               ┌────┬────┬────┬────┐   ◄──── Sorted Elements ────►
               │ 10 │ 14 │ 29 │ 37 │         All sorted ✅
               └────┴────┴────┴────┘

─────────────────────────────────────────────────────────────
Result: [ 10 | 14 | 29 | 37 ]
```

### Example

Input: `[29, 10, 14, 37]`
Output: `[10, 14, 29, 37]`

### Python Implementation

```python
def selection_sort(arr):
    n = len(arr)

    for i in range(n):
        min_index = i

        for j in range(i+1, n):
            if arr[j] < arr[min_index]:
                min_index = j

        arr[i], arr[min_index] = arr[min_index], arr[i]

    return arr
```

### Complexity

| Case    | Time Complexity |
|---------|-----------------|
| Best    | O(n²)           |
| Average | O(n²)           |
| Worst   | O(n²)           |

---

# ⚡ 4. Merge Sort

Merge Sort is a divide-and-conquer algorithm that splits the array in half recursively,
sorts each half, then merges them back together in order.

### 🎬 Step-by-Step Visual

```
Array: [ 38 | 27 | 43 | 3 ]
─────────────────────────────────────────────────────────────
STEP 01 — DIVIDE: Split array into halves recursively

               ┌────┬────┬────┬───┐
               │ 38 │ 27 │ 43 │ 3 │
               └────┴────┴────┴───┘
                      /          \
            ┌────┬────┐          ┌────┬───┐
            │ 38 │ 27 │          │ 43 │ 3 │
            └────┴────┘          └────┴───┘
             /        \           /       \
         ┌────┐     ┌────┐    ┌────┐    ┌───┐
         │ 38 │     │ 27 │    │ 43 │    │ 3 │
         └────┘     └────┘    └────┘    └───┘
         (single elements — base case ✅)

─────────────────────────────────────────────────────────────
STEP 02 — MERGE: Combine sorted pairs

  Merge [ 38 ] + [ 27 ]:
    Compare 38 vs 27 → pick 27, then 38
                ┌────┬────┐
                │ 27 │ 38 │  ✅
                └────┴────┘

  Merge [ 43 ] + [ 3 ]:
    Compare 43 vs 3  → pick  3, then 43
                ┌───┬────┐
                │ 3 │ 43 │  ✅
                └───┴────┘

─────────────────────────────────────────────────────────────
STEP 03 — MERGE: Final merge of both sorted halves

  Left:  [ 27 | 38 ]        Right: [ 3 | 43 ]

  i=0   Compare 27 vs  3  →  pick  3   →  [  3          ]
  i=1   Compare 27 vs 43  →  pick 27   →  [  3, 27      ]
  i=2   Compare 38 vs 43  →  pick 38   →  [  3, 27, 38  ]
  i=3   Remaining 43      →  pick 43   →  [  3, 27, 38, 43 ]

               ┌───┬────┬────┬────┐   ◄──── Sorted Elements ────►
               │ 3 │ 27 │ 38 │ 43 │         All sorted ✅
               └───┴────┴────┴────┘

─────────────────────────────────────────────────────────────
Result: [ 3 | 27 | 38 | 43 ]
```

### Example

Input: `[38, 27, 43, 3]`
Output: `[3, 27, 38, 43]`

### Python Implementation

```python
def merge_sort(arr):
    if len(arr) > 1:

        mid = len(arr) // 2
        left = arr[:mid]
        right = arr[mid:]

        merge_sort(left)
        merge_sort(right)

        i = j = k = 0

        while i < len(left) and j < len(right):
            if left[i] < right[j]:
                arr[k] = left[i]
                i += 1
            else:
                arr[k] = right[j]
                j += 1
            k += 1

        while i < len(left):
            arr[k] = left[i]
            i += 1
            k += 1

        while j < len(right):
            arr[k] = right[j]
            j += 1
            k += 1

    return arr
```

### Complexity

| Case    | Time Complexity |
|---------|-----------------|
| Best    | O(n log n)      |
| Average | O(n log n)      |
| Worst   | O(n log n)      |

---

# 🚀 5. Quick Sort

Quick Sort picks a pivot element, partitions all other elements into
"less than pivot" and "greater than pivot" groups, then recursively sorts each group.

### 🎬 Step-by-Step Visual

```
Array: [ 10 | 7 | 8 | 9 | 1 ]
─────────────────────────────────────────────────────────────
STEP 01 — Choose pivot & partition  (pivot = middle element = 8)

  ┌────┬───┬───┬───┬───┐
  │ 10 │ 7 │ 8 │ 9 │ 1 │
  └────┴───┴───┴───┴───┘
               ▲
            pivot = 8

  Classify every element:
    10 > 8  →  RIGHT
     7 < 8  →  LEFT
     8 = 8  →  MIDDLE
     9 > 8  →  RIGHT
     1 < 8  →  LEFT

  ┌──────────┐   ┌──────────┐   ┌───────────┐
  │  LEFT    │   │  MIDDLE  │   │   RIGHT   │
  │  [ 7,1 ] │ + │  [ 8 ]   │ + │  [10, 9]  │
  └──────────┘   └──────────┘   └───────────┘

─────────────────────────────────────────────────────────────
STEP 02 — Recurse on LEFT:  [ 7 | 1 ]   (pivot = 7)

  ┌───┬───┐
  │ 7 │ 1 │    pivot = 7
  └───┴───┘

  1 < 7 → LEFT     7 = 7 → MIDDLE     (no RIGHT)

  [ 1 ] + [ 7 ] = [ 1 | 7 ]  ✅

─────────────────────────────────────────────────────────────
STEP 03 — Recurse on RIGHT:  [ 10 | 9 ]   (pivot = 10)

  ┌────┬───┐
  │ 10 │ 9 │    pivot = 10
  └────┴───┘

  9 < 10 → LEFT     10 = 10 → MIDDLE     (no RIGHT)

  [ 9 ] + [ 10 ] = [ 9 | 10 ]  ✅

─────────────────────────────────────────────────────────────
STEP 04 — Combine all parts

  [ 1, 7 ]  +  [ 8 ]  +  [ 9, 10 ]

               ┌───┬───┬───┬───┬────┐   ◄──── Sorted Elements ────►
               │ 1 │ 7 │ 8 │ 9 │ 10 │         All sorted ✅
               └───┴───┴───┴───┴────┘

─────────────────────────────────────────────────────────────
Result: [ 1 | 7 | 8 | 9 | 10 ]
```

### Example

Input: `[10, 7, 8, 9, 1]`
Output: `[1, 7, 8, 9, 10]`

### Python Implementation

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr)//2]

    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)
```

### Complexity

| Case    | Time Complexity |
|---------|-----------------|
| Best    | O(n log n)      |
| Average | O(n log n)      |
| Worst   | O(n²)           |

---

# 🧮 6. Counting Sort

Counting Sort works by counting the occurrences of each unique element,
then using those counts to place elements directly into their correct sorted positions.

### 🎬 Step-by-Step Visual

```
Array: [ 4 | 2 | 2 | 8 | 3 ]
─────────────────────────────────────────────────────────────
STEP 01 — Count occurrences of each value

  Scan each element and tally into count array:

    see 4  →  count[4]++
    see 2  →  count[2]++
    see 2  →  count[2]++
    see 8  →  count[8]++
    see 3  →  count[3]++

  Count Array  (index = value, cell = how many times it appears):

  index  │  0  │  1  │  2  │  3  │  4  │  5  │  6  │  7  │  8  │
  ───────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
  count  │  0  │  0  │  2  │  1  │  1  │  0  │  0  │  0  │  1  │
                             ▲     ▲     ▲                   ▲
                            (2)   (3)   (4)                 (8)
                           ×  2  ×  1  ×  1               ×  1

─────────────────────────────────────────────────────────────
STEP 02 — Rebuild sorted array from count array

  index 0  →  count 0  →  skip
  index 1  →  count 0  →  skip
  index 2  →  count 2  →  output [ 2, 2 ]
  index 3  →  count 1  →  output [ 3 ]
  index 4  →  count 1  →  output [ 4 ]
  index 5  →  count 0  →  skip
  index 6  →  count 0  →  skip
  index 7  →  count 0  →  skip
  index 8  →  count 1  →  output [ 8 ]

─────────────────────────────────────────────────────────────
STEP 03 — Final sorted array

               ┌───┬───┬───┬───┬───┐   ◄──── Sorted Elements ────►
               │ 2 │ 2 │ 3 │ 4 │ 8 │         All sorted ✅
               └───┴───┴───┴───┴───┘

─────────────────────────────────────────────────────────────
Result: [ 2 | 2 | 3 | 4 | 8 ]
```

### Example

Input: `[4, 2, 2, 8, 3]`
Output: `[2, 2, 3, 4, 8]`

### Python Implementation

```python
def counting_sort(arr):
    max_val = max(arr)
    count = [0] * (max_val + 1)

    for num in arr:
        count[num] += 1

    sorted_arr = []

    for i in range(len(count)):
        sorted_arr.extend([i] * count[i])

    return sorted_arr
```

### Complexity

| Case    | Time Complexity |
|---------|-----------------|
| Best    | O(n + k)        |
| Average | O(n + k)        |
| Worst   | O(n + k)        |

> `k` = range of input values

---

# 🪣 7. Bucket Sort

Bucket Sort distributes elements into a number of buckets, sorts each bucket
individually (using any sorting algorithm), then concatenates all buckets in order.

### 🎬 Step-by-Step Visual

```
Array: [ 0.42 | 0.32 | 0.23 | 0.52 | 0.25 ]
(5 elements → 5 buckets,   bucket index = int(value × 5))
─────────────────────────────────────────────────────────────
STEP 01 — Distribute elements into buckets

  0.42  →  int(0.42 × 5) = int(2.10) = 2  →  bucket[2]
  0.32  →  int(0.32 × 5) = int(1.60) = 1  →  bucket[1]
  0.23  →  int(0.23 × 5) = int(1.15) = 1  →  bucket[1]
  0.52  →  int(0.52 × 5) = int(2.60) = 2  →  bucket[2]
  0.25  →  int(0.25 × 5) = int(1.25) = 1  →  bucket[1]

  bucket[0]:  [                         ]  empty
  bucket[1]:  [  0.32  |  0.23  |  0.25 ]
  bucket[2]:  [  0.42  |  0.52          ]
  bucket[3]:  [                         ]  empty
  bucket[4]:  [                         ]  empty

─────────────────────────────────────────────────────────────
STEP 02 — Sort each individual bucket

  bucket[0]:  [                         ]  empty, skip
  bucket[1]:  [  0.23  |  0.25  |  0.32 ]  sorted ✅
  bucket[2]:  [  0.42  |  0.52          ]  sorted ✅
  bucket[3]:  [                         ]  empty, skip
  bucket[4]:  [                         ]  empty, skip

─────────────────────────────────────────────────────────────
STEP 03 — Concatenate all buckets in order

  bucket[0]  →  []
  bucket[1]  →  [ 0.23, 0.25, 0.32 ]
  bucket[2]  →  [ 0.42, 0.52 ]
  bucket[3]  →  []
  bucket[4]  →  []

  []  +  [0.23, 0.25, 0.32]  +  [0.42, 0.52]  +  []  +  []

               ┌──────┬──────┬──────┬──────┬──────┐
               │ 0.23 │ 0.25 │ 0.32 │ 0.42 │ 0.52 │   ◄── Sorted ✅
               └──────┴──────┴──────┴──────┴──────┘

─────────────────────────────────────────────────────────────
Result: [ 0.23 | 0.25 | 0.32 | 0.42 | 0.52 ]
```

### Example

Input: `[0.42, 0.32, 0.23, 0.52, 0.25]`
Output: `[0.23, 0.25, 0.32, 0.42, 0.52]`

### Python Implementation

```python
def bucket_sort(arr):
    bucket = [[] for _ in range(len(arr))]

    for num in arr:
        index = int(num * len(arr))
        bucket[index].append(num)

    for b in bucket:
        b.sort()

    result = []
    for b in bucket:
        result.extend(b)

    return result
```

### Complexity

| Case    | Time Complexity |
|---------|-----------------|
| Best    | O(n + k)        |
| Average | O(n + k)        |
| Worst   | O(n²)           |

> `k` = number of buckets

---

# 🧠 Algorithm Comparison

| Algorithm      | Best       | Average    | Worst      |
|----------------|------------|------------|------------|
| Bubble Sort    | O(n)       | O(n²)      | O(n²)      |
| Insertion Sort | O(n)       | O(n²)      | O(n²)      |
| Selection Sort | O(n²)      | O(n²)      | O(n²)      |
| Merge Sort     | O(n log n) | O(n log n) | O(n log n) |
| Quick Sort     | O(n log n) | O(n log n) | O(n²)      |
| Counting Sort  | O(n+k)     | O(n+k)     | O(n+k)     |
| Bucket Sort    | O(n+k)     | O(n+k)     | O(n²)      |

---

# 🎯 Learning Goals

This project helps understand:

- Sorting algorithm design
- Time complexity analysis
- Algorithm efficiency comparisons
- Python implementation of classic algorithms

---

# 📌 Summary

Sorting algorithms are fundamental in computer science and are widely used in
databases, searching, and data processing systems.
