# 📘 Algorithms & String Manipulation — Complete Visual Reference

> Theory + Visual Step-by-Step + Code for every topic.

---

## 📑 Table of Contents

1. [Searching Algorithms](#1-searching-algorithms)
   - [Linear Search](#11-linear-search)
   - [Binary Search](#12-binary-search)
   - [Ternary Search](#13-ternary-search)
   - [Jump Search](#14-jump-search)
   - [Exponential Search](#15-exponential-search)
2. [String Manipulation Algorithms](#2-string-manipulation-algorithms)
   - [Reversing a String](#21-reversing-a-string)
   - [Reversing Words](#22-reversing-words)
   - [Rotations](#23-rotations)
   - [Removing Duplicates](#24-removing-duplicates)
   - [Most Repeated Character](#25-most-repeated-character)
   - [Anagrams](#26-anagrams)
   - [Palindrome](#27-palindrome)
3. [Recursion](#3-recursion)
4. [Complexity Summary](#4-complexity-summary)

---

## 1. Searching Algorithms

Searching algorithms locate a target element inside a data structure. The right choice depends on whether data is sorted and how large it is.

---

### 1.1 Linear Search

#### 📖 Theory

Scans **every element** one by one from left to right until the target is found or the array ends. Works on both sorted and unsorted data.

#### 🔍 Visual — Searching for `6` in `[3, 1, 7, 6, 9]`

```
Index:  0    1    2    3    4
      ┌────┬────┬────┬────┬────┐
arr = │  3 │  1 │  7 │  6 │  9 │
      └────┴────┴────┴────┴────┘

Step 1:  arr[0] = 3  ──►  3 == 6 ? ❌  move right
         ┌────┐
         │  3 │ ← checking
         └────┘

Step 2:  arr[1] = 1  ──►  1 == 6 ? ❌  move right
              ┌────┐
              │  1 │ ← checking
              └────┘

Step 3:  arr[2] = 7  ──►  7 == 6 ? ❌  move right
                   ┌────┐
                   │  7 │ ← checking
                   └────┘

Step 4:  arr[3] = 6  ──►  6 == 6 ? ✅  FOUND at index 3
                        ┌────┐
                        │  6 │ ← FOUND ✅
                        └────┘
```

#### ⚙️ Algorithm Flow

```
START
  │
  ▼
i = 0
  │
  ▼
┌─────────────────────┐
│  i < len(arr) ?     │──── NO ──► return -1  (Not Found)
└─────────────────────┘
  │ YES
  ▼
┌─────────────────────┐
│  arr[i] == target ? │──── YES ──► return i  (Found ✅)
└─────────────────────┘
  │ NO
  ▼
  i = i + 1
  │
  └──────────────────► (loop back)
```

| Property        | Value  |
|-----------------|--------|
| Time (Best)     | O(1)   |
| Time (Worst)    | O(n)   |
| Space           | O(1)   |
| Requires Sorted | ❌ No  |

#### 💻 Code (Python)

```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i        # Found at index i
    return -1               # Not found

arr = [3, 1, 7, 6, 9]
print(linear_search(arr, 6))   # Output: 3
print(linear_search(arr, 99))  # Output: -1
```

---

### 1.2 Binary Search

#### 📖 Theory

Works **only on sorted arrays**. Repeatedly cuts the search space in half by comparing the middle element to the target.

#### 🧮 How to Find `mid`

The midpoint index is calculated as:

```
mid = (low + high) // 2
```

**Why this works:**
- `low` is the start of the current search window, `high` is the end.
- Their average gives the exact center index.
- Integer division `//` floors the result so it's always a valid index.

```
Example:  low=0, high=9
  mid = (0 + 9) // 2 = 4   ← index 4 is the center

Example:  low=5, high=9
  mid = (5 + 9) // 2 = 7   ← index 7 is the center of [5..9]
```

> ⚠️ **Integer Overflow Warning (important in C++/Java):**
> If `low` and `high` are very large integers, `low + high` can overflow.
> The **safe formula** is:
> ```
> mid = low + (high - low) // 2
> ```
> This is mathematically identical but avoids overflow. Python handles big integers
> natively so both work, but prefer the safe form as a habit.

**After comparing `arr[mid]` to target:**
- `arr[mid] == target` → found, return `mid`
- `arr[mid] < target`  → target is in the RIGHT half → `low = mid + 1`
- `arr[mid] > target`  → target is in the LEFT half  → `high = mid - 1`

We add/subtract 1 because `arr[mid]` itself was already checked and ruled out.

#### 🔍 Visual — Searching for `7` in `[-5, -2, 0, 1, 2, 4, 5, 6, 7, 10]`

```
Index:   0    1    2    3    4    5    6    7    8    9
       ┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
 arr = │ -5 │ -2 │  0 │  1 │  2 │  4 │  5 │  6 │  7 │ 10 │
       └────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
        LOW                   MID                      HIGH

──────────────────────────────────────────────────────────
STEP 1:  low=0, high=9  →  mid = (0+9)//2 = 4
         arr[4] = 2  ──►  2 < 7  →  go RIGHT  (low = mid+1 = 5)
       ┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
       │ -5 │ -2 │  0 │  1 │[2] │  4 │  5 │  6 │  7 │ 10 │
       └────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
                              ^^^MID  (too small, go right ➡️)

──────────────────────────────────────────────────────────
STEP 2:  low=5, high=9  →  mid = (5+9)//2 = 7
         arr[7] = 6  ──►  6 < 7  →  go RIGHT  (low = mid+1 = 8)
       ┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
       │ -5 │ -2 │  0 │  1 │  2 │  4 │  5 │[6] │  7 │ 10 │
       └────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
                                              ^^^MID (too small, go right ➡️)

──────────────────────────────────────────────────────────
STEP 3:  low=8, high=9  →  mid = (8+9)//2 = 8
         arr[8] = 7  ──►  7 == 7  →  ✅ FOUND at index 8
       ┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
       │ -5 │ -2 │  0 │  1 │  2 │  4 │  5 │  6 │[7] │ 10 │
       └────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
                                         LOW  ^^^MID  HIGH
                                                ✅ FOUND!
```

#### ⚙️ Algorithm Flow

```
START: low = 0, high = n-1
  │
  ▼
┌──────────────────┐
│  low <= high ?   │──── NO ──► return -1  (Not Found)
└──────────────────┘
  │ YES
  ▼
mid = low + (high - low) // 2     ← safe mid formula
  │
  ▼
┌──────────────────────┐
│  arr[mid] == target? │──── YES ──► return mid  ✅
└──────────────────────┘
  │ NO
  ├── arr[mid] < target ──► low  = mid + 1  (search RIGHT ➡️)
  └── arr[mid] > target ──► high = mid - 1  (search LEFT  ⬅️)
  │
  └──────────────────► (loop back)
```

| Property        | Value    |
|-----------------|----------|
| Time (Best)     | O(1)     |
| Time (Worst)    | O(log n) |
| Space           | O(1)     |
| Requires Sorted | ✅ Yes   |

> **Why O(log n)?** Each step halves the search space. Starting with n elements:
> after 1 step → n/2, after 2 steps → n/4, ... after k steps → n/2ᵏ = 1
> Solving: k = log₂(n). So at most log₂(n) comparisons are needed.

#### 💻 Code (Python)

```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = low + (high - low) // 2   # safe mid formula
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1       # Go right
        else:
            high = mid - 1      # Go left
    return -1

arr = [-5, -2, 0, 1, 2, 4, 5, 6, 7, 10]
print(binary_search(arr, 7))   # Output: 8
print(binary_search(arr, 3))   # Output: -1
```

---

### 1.3 Ternary Search

#### 📖 Theory

Divides the sorted array into **three equal parts** using two midpoints (mid1, mid2). Eliminates one third of the array each step.

#### 🧮 How to Find `mid1` and `mid2`

The array from `low` to `high` has a total range of `(high - low)`. To split it into 3 equal thirds:

```
mid1 = low + (high - low) // 3
mid2 = high - (high - low) // 3
```

**Why this formula:**
- `(high - low) // 3` is the size of one-third of the current window.
- `mid1` = start + one-third → marks the boundary between the **1st and 2nd** third.
- `mid2` = end − one-third   → marks the boundary between the **2nd and 3rd** third.
- The **middle third** lives in the range `(mid1, mid2)` exclusive.

```
Example:  low=0, high=7  →  range = 7

  one-third = 7 // 3 = 2

  mid1 = 0 + 2 = 2      ← 1/3 from the left
  mid2 = 7 - 2 = 5      ← 1/3 from the right

  ┌────┬────┬────┬────┬────┬────┬────┬────┐
  │  0 │  1 │MID1│  3 │  4 │MID2│  6 │  7 │
  └────┴────┴────┴────┴────┴────┴────┴────┘
  [── 1st third ──] [── 2nd third ──] [─ 3rd ─]
```

**Decision logic after computing mid1 and mid2:**
- `target == arr[mid1]` → found ✅
- `target == arr[mid2]` → found ✅
- `target < arr[mid1]`  → target in LEFT third  → `high = mid1 - 1`
- `target > arr[mid2]`  → target in RIGHT third → `low = mid2 + 1`
- else                  → target in MIDDLE third → `low = mid1+1, high = mid2-1`

#### 🔍 Visual — Searching for `8` in `[1, 3, 5, 6, 8, 10, 12, 15]`

```
Index:   0    1    2    3    4    5    6    7
       ┌────┬────┬────┬────┬────┬────┬────┬────┐
 arr = │  1 │  3 │  5 │  6 │  8 │ 10 │ 12 │ 15 │
       └────┴────┴────┴────┴────┴────┴────┴────┘
        LOW          MID1      MID2          HIGH

──────────────────────────────────────────────────
STEP 1:  low=0, high=7
         mid1 = 0 + (7-0)//3 = 2   →  arr[2] = 5
         mid2 = 7 - (7-0)//3 = 5   →  arr[5] = 10

       ┌────┬────┬────┬────┬────┬────┬────┬────┐
       │  1 │  3 │[5] │  6 │  8 │[10]│ 12 │ 15 │
       └────┴────┴────┴────┴────┴────┴────┴────┘
                 ^^^               ^^^
                mid1              mid2

  target(8) > mid1(5)  and  target(8) < mid2(10)
  → Search MIDDLE third: low = mid1+1 = 3, high = mid2-1 = 4

──────────────────────────────────────────────────
STEP 2:  low=3, high=4
         mid1 = 3 + (4-3)//3 = 3   →  arr[3] = 6
         mid2 = 4 - (4-3)//3 = 4   →  arr[4] = 8

       ┌────┬────┬────┬────┬────┬────┬────┬────┐
       │  1 │  3 │  5 │[6] │[8] │ 10 │ 12 │ 15 │
       └────┴────┴────┴────┴────┴────┴────┴────┘
                          ^^^  ^^^
                         mid1  mid2

  arr[mid2] = 8 == target  →  ✅ FOUND at index 4
```

#### ⚙️ Algorithm Flow

```
START: low=0, high=n-1
  │
  ▼
┌──────────────────┐
│  low <= high ?   │──── NO ──► return -1
└──────────────────┘
  │ YES
  ▼
mid1 = low + (high-low)//3
mid2 = high - (high-low)//3
  │
  ├── arr[mid1] == target  ──► return mid1  ✅
  ├── arr[mid2] == target  ──► return mid2  ✅
  │
  ├── target < arr[mid1]   ──► high = mid1-1       (LEFT third  ⬅️)
  ├── target > arr[mid2]   ──► low  = mid2+1       (RIGHT third ➡️)
  └── else                 ──► low=mid1+1, high=mid2-1  (MIDDLE ↔️)
  │
  └──────────────────► (loop back)
```

| Property        | Value     |
|-----------------|-----------|
| Time (Best)     | O(1)      |
| Time (Worst)    | O(log₃ n) |
| Space           | O(1)      |
| Requires Sorted | ✅ Yes    |

> **Why O(log₃ n) but NOT faster than Binary Search?**
> Each step eliminates 1/3 of the array but requires **2 comparisons** (checking both mid1 and mid2).
> Binary Search eliminates 1/2 of the array with only **1 comparison**.
> The total comparisons work out higher for Ternary Search in practice — Binary Search is preferred.

#### 💻 Code (Python)

```python
def ternary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid1 = low + (high - low) // 3
        mid2 = high - (high - low) // 3
        if arr[mid1] == target: return mid1
        if arr[mid2] == target: return mid2
        if target < arr[mid1]:
            high = mid1 - 1
        elif target > arr[mid2]:
            low = mid2 + 1
        else:
            low, high = mid1+1, mid2-1
    return -1

arr = [1, 3, 5, 6, 8, 10, 12, 15]
print(ternary_search(arr, 8))   # Output: 4
```

---

### 1.4 Jump Search

#### 📖 Theory

**Jumps** forward by √n steps at a time through the sorted array, then does a **linear scan** once the target range is found.

#### 🧮 Why Block Size = √n ?

The block (jump) size is:

```
step = int(√n)
```

**Why √n is the optimal block size — derivation:**

Suppose we use a block size of `b`:
- **Phase 1 jumps** = `n / b` in the worst case (to scan the whole array)
- **Phase 2 linear steps** = `b - 1` in the worst case (scanning one full block)
- **Total comparisons** = `n/b + b`

To find the `b` that minimizes this, take the derivative and set to zero:

```
d/db (n/b + b) = -n/b² + 1 = 0
→  b² = n
→  b  = √n   ✅
```

So `√n` gives minimum total work of `√n + √n = 2√n` → **O(√n)**.

```
Example:  n = 100
  optimal b = √100 = 10

  Worst case jumps:  100/10 = 10
  Worst case linear: 10 - 1 = 9
  Total: ~19 comparisons  (vs 100 for linear, ~7 for binary)
```

#### 🔍 Visual — Searching for `55` in `[10, 20, 30, 40, 50, 55, 60, 70, 80, 90]`

```
n=10,  block size = √10 ≈ 3

Index:   0    1    2    3    4    5    6    7    8    9
       ┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
 arr = │ 10 │ 20 │ 30 │ 40 │ 50 │ 55 │ 60 │ 70 │ 80 │ 90 │
       └────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘

PHASE 1 — JUMPING FORWARD (by block size = 3)
─────────────────────────────────────────────
Jump 1:  check arr[2] = 30   →  30 < 55  ✈️ jump again
         [10][20][30]
               ↑
              prev=0, step=3

Jump 2:  check arr[5] = 55   →  55 >= 55  🛬 STOP! found range
                    [40][50][55]
                          ↑
                         prev=3, step=6

PHASE 2 — LINEAR SCAN (from prev=3 forward)
────────────────────────────────────────────
  index 3: arr[3] = 40  →  40 < 55  move forward →
  index 4: arr[4] = 50  →  50 < 55  move forward →
  index 5: arr[5] = 55  →  55 == 55  ✅ FOUND at index 5

       ┌────┬────┬────┬────┬────┬────┬────┬────┬────┬────┐
       │ 10 │ 20 │ 30 │ 40 │ 50 │[55]│ 60 │ 70 │ 80 │ 90 │
       └────┴────┴────┴────┴────┴────┴────┴────┴────┴────┘
                                    ✅
```

#### ⚙️ Algorithm Flow

```
START: step = √n,  prev = 0
  │
  ▼
┌─────────────────────────────────┐
│  arr[min(step,n)-1] < target ?  │──── NO ──► go to linear scan
└─────────────────────────────────┘
  │ YES
  ▼
prev = step                         ← save last jump
step += √n                          ← jump forward ✈️
  │
  ├── prev >= n  ──► return -1
  └──────────────────► (loop back)

LINEAR SCAN from prev to min(step, n):
  ├── arr[prev] < target   ──►  prev++
  ├── arr[prev] == target  ──►  return prev  ✅
  └── prev reached end     ──►  return -1
```

| Property        | Value  |
|-----------------|--------|
| Time (Best)     | O(1)   |
| Time (Worst)    | O(√n)  |
| Space           | O(1)   |
| Requires Sorted | ✅ Yes |

#### 💻 Code (Python)

```python
import math

def jump_search(arr, target):
    n = len(arr)
    step = int(math.sqrt(n))   # optimal block size = √n
    prev = 0

    # Phase 1: Jump forward
    while arr[min(step, n) - 1] < target:
        prev = step
        step += int(math.sqrt(n))
        if prev >= n:
            return -1

    # Phase 2: Linear scan
    while arr[prev] < target:
        prev += 1
        if prev == min(step, n):
            return -1

    return prev if arr[prev] == target else -1

arr = [10, 20, 30, 40, 50, 55, 60, 70, 80, 90]
print(jump_search(arr, 55))  # Output: 5
```

---

### 1.5 Exponential Search

#### 📖 Theory

**Doubles** the index (1 → 2 → 4 → 8 → 16...) to quickly narrow the range where the target lives, then runs **Binary Search** inside that range. Best for large or unbounded arrays.

#### 🧮 Why Doubling? And Why `i // 2` as the Lower Bound?

**Phase 1 — Why powers of 2 (doubling)?**

The index follows: `i = 1, 2, 4, 8, 16, ...` (i.e., 2⁰, 2¹, 2², 2³, ...)

```
Each step:  i = i * 2
```

- Doubling covers exponentially more ground with each step.
- To reach index `k`, it takes only `log₂(k)` doublings.
- This locates the correct range in **O(log n)** steps, even before Binary Search begins.
- Any multiplier > 1 would work, but 2 is standard — it's simple, cache-friendly, and gives exact powers of 2.

**Phase 2 — Why `i // 2` as the lower bound for Binary Search?**

When the loop stops at index `i` (meaning `arr[i] > target`):
- `arr[i]    > target` → target is NOT at or beyond index `i`
- `arr[i//2] ≤ target` → the previous step where we didn't stop

So the target **must lie in the window `[i//2, i]`**.

```
Doubling trace:  i = 1 → 2 → 4 → 8 → stops at 16

  arr[8]  ≤ target   (last step that passed)
  arr[16] > target   (first overshoot)

  → target lives in  [8, 16]  =  [i//2, min(i, n-1)]   ✅
```

Binary Search is applied only to this narrow window, not the full array.

#### 🔍 Visual — Searching for `70` in `[5, 10, 20, 35, 50, 60, 70, 80, 90]`

```
Index:   0    1    2    3    4    5    6    7    8
       ┌────┬────┬────┬────┬────┬────┬────┬────┬────┐
 arr = │  5 │ 10 │ 20 │ 35 │ 50 │ 60 │ 70 │ 80 │ 90 │
       └────┴────┴────┴────┴────┴────┴────┴────┴────┘

PHASE 1 — EXPONENTIAL RANGE FINDING
────────────────────────────────────
  i=1:  arr[1] = 10  ≤ 70  →  i = 1×2 = 2  📈
  i=2:  arr[2] = 20  ≤ 70  →  i = 2×2 = 4  📈
  i=4:  arr[4] = 50  ≤ 70  →  i = 4×2 = 8  📈
  i=8:  arr[8] = 90  > 70  →  STOP! 🛑

  Window found: [ i//2 = 4 ]  to  [ min(i,8) = 8 ]
       ┌────┬────┬────┬────┬────┐
       │ 50 │ 60 │ 70 │ 80 │ 90 │  ← Binary Search here
       └────┴────┴────┴────┴────┘
  idx:  4    5    6    7    8

PHASE 2 — BINARY SEARCH in window [4..8]
──────────────────────────────────────────
  low=4, high=8  →  mid = 4 + (8-4)//2 = 6  →  arr[6]=70 == 70  ✅

       ┌────┬────┬────┬────┬────┬────┬────┬────┬────┐
       │  5 │ 10 │ 20 │ 35 │ 50 │ 60 │[70]│ 80 │ 90 │
       └────┴────┴────┴────┴────┴────┴────┴────┴────┘
                                         ✅ index 6
```

#### ⚙️ Algorithm Flow

```
START
  │
  ├── arr[0] == target  ──►  return 0  ✅
  │
  ▼
i = 1
  │
  ▼
┌─────────────────────────────────┐
│  i < n  AND  arr[i] <= target ? │──── NO ──► window found
└─────────────────────────────────┘
  │ YES
  ▼
i = i * 2   (double the range 📈)
  │
  └──────────────────► (loop back)

BINARY SEARCH on arr[ i//2 ... min(i, n-1) ]
  └── return result  ✅
```

| Property        | Value                    |
|-----------------|--------------------------|
| Time (Best)     | O(1)                     |
| Time (Worst)    | O(log n)                 |
| Space           | O(1)                     |
| Requires Sorted | ✅ Yes                   |
| Best Use        | Large / unbounded arrays |

#### 💻 Code (Python)

```python
def binary_search(arr, low, high, target):
    while low <= high:
        mid = low + (high - low) // 2   # safe mid formula
        if arr[mid] == target: return mid
        elif arr[mid] < target: low = mid + 1
        else: high = mid - 1
    return -1

def exponential_search(arr, target):
    n = len(arr)
    if arr[0] == target: return 0
    i = 1
    while i < n and arr[i] <= target:
        i *= 2                          # Double the range
    # i//2 guaranteed <= target; min(i, n-1) caps the upper bound
    return binary_search(arr, i // 2, min(i, n - 1), target)

arr = [5, 10, 20, 35, 50, 60, 70, 80, 90]
print(exponential_search(arr, 70))  # Output: 6
```

---

## 2. String Manipulation Algorithms

---

### 2.1 Reversing a String

#### 📖 Theory

Returns characters in **reverse order** by swapping from both ends and moving inward.

#### 🧮 How to Set Up the Two Pointers

```
left  = 0              ← starts at the first character (index 0)
right = len(s) - 1     ← starts at the last character
```

After each swap: `left += 1` and `right -= 1`.
Stop when `left >= right` (pointers meet or cross at the center).

**Total swaps = n // 2** — only half the positions need to be swapped since each swap fixes two characters at once.

```
"HELLO"  (length = 5)
  left starts at 0 (H),  right starts at 4 (O)
  Swaps needed: 5//2 = 2  (indices 0↔4, then 1↔3; center index 2 stays)
```

#### 🔍 Visual — Reversing `"HELLO"`

```
Original:
  ┌───┬───┬───┬───┬───┐
  │ H │ E │ L │ L │ O │
  └───┴───┴───┴───┴───┘
    0   1   2   3   4
    ↑                ↑
   left            right

Step 1: swap s[0] H  ↔  s[4] O
  ┌───┬───┬───┬───┬───┐
  │ O │ E │ L │ L │ H │
  └───┴───┴───┴───┴───┘
        ↑       ↑
       left   right

Step 2: swap s[1] E  ↔  s[3] L
  ┌───┬───┬───┬───┬───┐
  │ O │ L │ L │ E │ H │
  └───┴───┴───┴───┴───┘
            ↑
        left=right=2  →  STOP (n//2 = 2 swaps done)

Result:  "OLLEH"  ✅
```

#### ⚙️ Algorithm Flow

```
left = 0,  right = len(s) - 1
  │
  ▼
┌─────────────────┐
│  left < right ? │──── NO ──► return result  ✅
└─────────────────┘
  │ YES
  ▼
swap(s[left], s[right])
left++,  right--
  │
  └──► (loop back)
```

| Time | Space |
|------|-------|
| O(n) | O(1)  |

#### 💻 Code (Python)

```python
def reverse_string(s):
    s = list(s)
    left, right = 0, len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
    return ''.join(s)

print(reverse_string("HELLO"))  # Output: OLLEH
```

---

### 2.2 Reversing Words

#### 📖 Theory

Reverses the **order of words** in a sentence (not the letters within each word).

#### 🔍 Visual — Reversing words in `"Hello World from Python"`

```
Input:  "Hello World from Python"
             │
             ▼  SPLIT by spaces
             │
  ┌─────────┬─────────┬────────┬────────┐
  │ "Hello" │ "World" │ "from" │"Python"│
  └─────────┴─────────┴────────┴────────┘
      [0]       [1]       [2]      [3]
             │
             ▼  REVERSE the list
             │
  ┌────────┬────────┬─────────┬─────────┐
  │"Python"│ "from" │ "World" │ "Hello" │
  └────────┴────────┴─────────┴─────────┘
      [0]      [1]       [2]       [3]
             │
             ▼  JOIN with spaces
             │
        "Python from World Hello"  ✅
```

#### ⚙️ Algorithm Flow

```
sentence
   │
   ├──[Split]──► ["Hello", "World", "from", "Python"]
   │
   ├──[Reverse]─► ["Python", "from", "World", "Hello"]
   │
   └──[Join " "]─► "Python from World Hello"  ✅
```

| Time | Space |
|------|-------|
| O(n) | O(n)  |

#### 💻 Code (Python)

```python
def reverse_words(sentence):
    words = sentence.split()
    words.reverse()
    return ' '.join(words)

print(reverse_words("Hello World from Python"))
# Output: Python from World Hello
```

---

### 2.3 Rotations

#### 📖 Theory

A rotation **shifts** all characters by `k` positions left or right, wrapping around. We can also check if one string is a rotation of another.

#### 🧮 How the Rotation Formulas Work

**Left Rotation by k:**
```
result = s[k:] + s[:k]
```
- `s[k:]` — everything from index k to the end (stays in place)
- `s[:k]`  — the first k characters (wrap around to the end)

**Right Rotation by k:**
```
result = s[-k:] + s[:-k]
```
- `s[-k:]`  — the last k characters (wrap around to the front)
- `s[:-k]`  — everything except the last k characters

**Why `k = k % len(s)` first?**
Rotating a string of length n by exactly n positions gives back the original.
So rotating by k is always equivalent to rotating by `k % n`.
This prevents incorrect slicing when k is larger than the string length.

```
"ABCDEF"  (length = 6)

Left rotate by k=2:
  k = 2 % 6 = 2
  s[2:] + s[:2]  =  "CDEF" + "AB"  =  "CDEFAB"  ✅

Right rotate by k=2:
  k = 2 % 6 = 2
  s[-2:] + s[:-2]  =  "EF" + "ABCD"  =  "EFABCD"  ✅

Left rotate by k=8 (k > length):
  k = 8 % 6 = 2  →  same result as k=2  ✅
```

**Is Rotation check — why `s2 in (s1 + s1)`?**

Concatenating s1 with itself creates a string that contains **every possible rotation** of s1 as a substring:

```
s1 = "ABCDEF"
s1+s1 = "ABCDEFABCDEF"
         ^^^^^^         rotation by 0  (original)
          ^^^^^^        rotation by 1
           ^^^^^^       rotation by 2  ← "CDEFAB" is here
            ^^^^^^      rotation by 3  ...and so on
```

If s2 appears anywhere in `s1+s1`, it must be one of those rotations.

#### 🔍 Visual — Left Rotate `"ABCDEF"` by 2

```
Original:
  ┌───┬───┬───┬───┬───┬───┐
  │ A │ B │ C │ D │ E │ F │
  └───┴───┴───┴───┴───┴───┘
    0   1   2   3   4   5

Left rotate by k=2  →  first 2 chars move to the END:
  ┌───┬───┐   ┌───┬───┬───┬───┐
  │ A │ B │ + │ C │ D │ E │ F │   ← split at k=2
  └───┴───┘   └───┴───┴───┴───┘
   s[:2]           s[2:]

Rearrange as  s[k:] + s[:k] :
  ┌───┬───┬───┬───┐   ┌───┬───┐
  │ C │ D │ E │ F │ + │ A │ B │  =  "CDEFAB"  ✅
  └───┴───┴───┴───┘   └───┴───┘
```

#### 🔍 Visual — Is Rotation Check

```
s1 = "ABCDEF"
s2 = "CDEFAB"    ← is this a rotation of s1?

Concatenate s1+s1  →  "ABCDEFABCDEF"
                             ┌──────┐
Is s2 a substring?  →    "AB│CDEFAB│CDEF"   ✅ YES
                             └──────┘
→ s2 IS a rotation of s1
```

#### ⚙️ Algorithm Flow

```
LEFT ROTATE by k:
  k = k % len(s)
  return s[k:] + s[:k]

RIGHT ROTATE by k:
  k = k % len(s)
  return s[-k:] + s[:-k]

IS ROTATION (s1, s2):
  len(s1) == len(s2)  AND  s2 in (s1 + s1)  →  True / False
```

| Time | Space |
|------|-------|
| O(n) | O(n)  |

#### 💻 Code (Python)

```python
def left_rotate(s, k):
    k %= len(s)
    return s[k:] + s[:k]

def right_rotate(s, k):
    k %= len(s)
    return s[-k:] + s[:-k]

def is_rotation(s1, s2):
    return len(s1) == len(s2) and s2 in (s1 + s1)

print(left_rotate("ABCDEF", 2))         # Output: CDEFAB
print(right_rotate("ABCDEF", 2))        # Output: EFABCD
print(is_rotation("ABCDEF", "CDEFAB"))  # Output: True
```

---

### 2.4 Removing Duplicates

#### 📖 Theory

Removes repeated characters, keeping only the **first occurrence** of each character in order.

#### 🔍 Visual — Remove duplicates from `"programming"`

```
Input: "programming"

  Char │ In seen set? │ Action   │ Result so far
  ─────┼──────────────┼──────────┼───────────────
   p   │     ❌       │  ADD  ✅  │  "p"
   r   │     ❌       │  ADD  ✅  │  "pr"
   o   │     ❌       │  ADD  ✅  │  "pro"
   g   │     ❌       │  ADD  ✅  │  "prog"
   r   │     ✅       │  SKIP ❌  │  "prog"
   a   │     ❌       │  ADD  ✅  │  "proga"
   m   │     ❌       │  ADD  ✅  │  "progam"
   m   │     ✅       │  SKIP ❌  │  "progam"
   i   │     ❌       │  ADD  ✅  │  "progami"
   n   │     ❌       │  ADD  ✅  │  "progamin"
   g   │     ✅       │  SKIP ❌  │  "progamin"

Output: "progamin"  ✅
```

#### ⚙️ Algorithm Flow

```
seen = { }  (empty set)
result = [ ]
  │
  ▼
For each char in string:
  │
  ├── char NOT in seen  ──►  seen.add(char) + result.append(char)
  └── char IN seen      ──►  skip
  │
  ▼
return ''.join(result)  ✅
```

| Time | Space |
|------|-------|
| O(n) | O(n)  |

#### 💻 Code (Python)

```python
def remove_duplicates(s):
    seen = set()
    result = []
    for char in s:
        if char not in seen:
            seen.add(char)
            result.append(char)
    return ''.join(result)

print(remove_duplicates("programming"))  # Output: progamin
print(remove_duplicates("aabbccdd"))     # Output: abcd
```

---

### 2.5 Most Repeated Character

#### 📖 Theory

Finds the character with the **highest frequency** by building a count map, then finding the maximum.

#### 🔍 Visual — Most repeated char in `"aabbbbcc"`

```
Input: "aabbbbcc"

Build frequency map:
  ┌───┬───┬───┬───┬───┬───┬───┬───┐
  │ a │ a │ b │ b │ b │ b │ c │ c │
  └───┴───┴───┴───┴───┴───┴───┴───┘

  freq = { 'a': 2,  'b': 4,  'c': 2 }

  Bar view:
   b │████████  (4)  ← MAX
   a │████      (2)
   c │████      (2)
     └─────────────

  → Most repeated = 'b'  ✅
```

#### ⚙️ Algorithm Flow

```
freq = { }
  │
  ▼
For each char in string:
  freq[char] += 1          ← count occurrences
  │
  ▼
return max(freq, key=freq.get)   ← char with highest count  ✅
```

| Time | Space |
|------|-------|
| O(n) | O(k)  |
*(k = unique characters)*

#### 💻 Code (Python)

```python
def most_repeated_char(s):
    freq = {}
    for char in s:
        freq[char] = freq.get(char, 0) + 1
    return max(freq, key=freq.get)

print(most_repeated_char("aabbbbcc"))     # Output: b
print(most_repeated_char("programming"))  # Output: g
```

---

### 2.6 Anagrams

#### 📖 Theory

Two strings are **anagrams** if they use exactly the same characters with the same frequencies (order doesn't matter).

#### 🔍 Visual — Are `"listen"` and `"silent"` anagrams?

```
Method 1 — Sort & Compare:
  ┌───┬───┬───┬───┬───┬───┐      ┌───┬───┬───┬───┬───┬───┐
  │ l │ i │ s │ t │ e │ n │      │ s │ i │ l │ e │ n │ t │
  └───┴───┴───┴───┴───┴───┘      └───┴───┴───┴───┴───┴───┘
        "listen"                        "silent"
              │  sort                       │  sort
              ▼                             ▼
  ┌───┬───┬───┬───┬───┬───┐      ┌───┬───┬───┬───┬───┬───┐
  │ e │ i │ l │ n │ s │ t │  ==  │ e │ i │ l │ n │ s │ t │
  └───┴───┴───┴───┴───┴───┘      └───┴───┴───┴───┴───┴───┘
        "eilnst"               ==       "eilnst"   ✅ ANAGRAM!

──────────────────────────────────────────────────────────
Method 2 — Frequency Map:

  "listen"  →  { l:1, i:1, s:1, t:1, e:1, n:1 }
  "silent"  →  { s:1, i:1, l:1, e:1, n:1, t:1 }
                         ↕
            Both maps identical  ✅  ANAGRAM!
```

#### ⚙️ Algorithm Flow

```
METHOD 1 (Sort):
  sorted(s1) == sorted(s2)  ──► True / False

METHOD 2 (Frequency):
  freq = {}
  For each char in s1:  freq[char] += 1   (count up)
  For each char in s2:  freq[char] -= 1   (count down)
    └── if freq[char] < 0  ──► NOT anagram ❌
  All zero  ──► ANAGRAM  ✅
```

| Method | Time       | Space |
|--------|------------|-------|
| Sort   | O(n log n) | O(n)  |
| Freq   | O(n)       | O(n)  |

#### 💻 Code (Python)

```python
def are_anagrams(s1, s2):
    if len(s1) != len(s2): return False
    freq = {}
    for c in s1: freq[c] = freq.get(c, 0) + 1
    for c in s2:
        freq[c] = freq.get(c, 0) - 1
        if freq[c] < 0: return False
    return True

print(are_anagrams("listen", "silent"))     # Output: True
print(are_anagrams("triangle", "integral")) # Output: True
print(are_anagrams("hello", "world"))       # Output: False
```

---

### 2.7 Palindrome

#### 📖 Theory

A string is a **palindrome** if it reads identically forwards and backwards.

#### 🧮 How the Two-Pointer Positions Work

```
left  = 0              ← start of string
right = len(s) - 1     ← end of string
```

Both pointers move **inward** by 1 after each successful match.
Stop condition: `left >= right` (all pairs have been verified).

If at any point `s[left] != s[right]` → immediately return False.

**Total comparisons = n // 2** — only half the string is checked since we compare symmetric pairs simultaneously.

```
"racecar"  (length = 7)
  left=0(r), right=6(r)  → match, move inward
  left=1(a), right=5(a)  → match, move inward
  left=2(c), right=4(c)  → match, move inward
  left=3 >= right=3      → STOP, palindrome ✅

  Total comparisons: 7//2 = 3
```

#### 🔍 Visual — Is `"racecar"` a palindrome?

```
  ┌───┬───┬───┬───┬───┬───┬───┐
  │ r │ a │ c │ e │ c │ a │ r │
  └───┴───┴───┴───┴───┴───┴───┘
    0   1   2   3   4   5   6
    ↑                       ↑
   left                   right

Step 1:  s[0]='r'  ==  s[6]='r'  ✅  left++, right--
  ┌───┬───┬───┬───┬───┬───┬───┐
  │ r │ a │ c │ e │ c │ a │ r │
  └───┴───┴───┴───┴───┴───┴───┘
        ↑               ↑
       left           right

Step 2:  s[1]='a'  ==  s[5]='a'  ✅  left++, right--

Step 3:  s[2]='c'  ==  s[4]='c'  ✅  left++, right--

Step 4:  left(3) >= right(3)  →  STOP  →  return True  ✅

──────────────────────────────────────────
Counter example: "hello"
  ┌───┬───┬───┬───┬───┐
  │ h │ e │ l │ l │ o │
  └───┴───┴───┴───┴───┘
    ↑               ↑
   left           right
  s[0]='h'  ≠  s[4]='o'  ❌  →  return False immediately
```

#### ⚙️ Algorithm Flow

```
left = 0,  right = len(s) - 1
  │
  ▼
┌─────────────────┐
│  left < right ? │──── NO ──► return True  ✅ (all matched)
└─────────────────┘
  │ YES
  ▼
┌───────────────────────────┐
│  s[left] == s[right] ?    │──── NO ──► return False  ❌
└───────────────────────────┘
  │ YES
  ▼
left++,  right--
  │
  └──► (loop back)
```

| Time | Space |
|------|-------|
| O(n) | O(1)  |

#### 💻 Code (Python)

```python
def is_palindrome(s):
    s = s.lower().replace(" ", "")
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True

print(is_palindrome("racecar"))                      # Output: True
print(is_palindrome("A man a plan a canal Panama"))  # Output: True
print(is_palindrome("hello"))                        # Output: False
```

---

## 3. Recursion

#### 📖 Theory

Recursion is when a function **calls itself** with a smaller input until a **base case** stops it.

#### 🧮 How Recursion Works — The Call Stack

Every recursive call is pushed onto the **call stack** (a region of memory). Each stack frame stores the function's local variables and the return address. When the base case is reached, frames are **popped** in reverse order (LIFO — Last In, First Out).

```
Call stack grows DOWN as recursive calls are made:
  ┌─────────────────────┐  ← pushed last (base case, resolved first)
  │  factorial(0) = 1   │
  ├─────────────────────┤
  │  factorial(1) = 1×? │
  ├─────────────────────┤
  │  factorial(2) = 2×? │
  ├─────────────────────┤
  │  factorial(3) = 3×? │
  ├─────────────────────┤
  │  factorial(4) = 4×? │  ← pushed first (original call)
  └─────────────────────┘

Resolves back UP once base case returns:
  factorial(0) = 1
  factorial(1) = 1 × 1 = 1
  factorial(2) = 2 × 1 = 2
  factorial(3) = 3 × 2 = 6
  factorial(4) = 4 × 6 = 24  ✅
```

**Stack depth = number of recursive calls.**
For linear recursion (like factorial): depth = n → **O(n) space**.

#### 🔍 Visual — `factorial(4)` Call Stack

```
GOING DOWN (building calls):
  factorial(4)
  └──► 4 × factorial(3)
            └──► 3 × factorial(2)
                      └──► 2 × factorial(1)
                                └──► 1 × factorial(0)
                                          └──► return 1  🛑 BASE CASE

COMING BACK UP (resolving):
  factorial(0) ──────────────────── returns  1
  factorial(1) = 1 × 1  ─────────── returns  1
  factorial(2) = 2 × 1  ─────────── returns  2
  factorial(3) = 3 × 2  ─────────── returns  6
  factorial(4) = 4 × 6  ─────────── returns 24  ✅
```

#### 🔍 Visual — Fibonacci Tree `fib(4)`

```
                       fib(4)
                      /      \
                fib(3)        fib(2)
               /     \        /    \
           fib(2)   fib(1)  fib(1) fib(0)
           /    \     │        │      │
        fib(1) fib(0) 1        1      0
           │     │
           1     0

  fib(4) = 3  ✅
  (0+1=1, 1+1=2, 1+2=3)
```

> ⚠️ **Fibonacci Time Complexity Warning — O(2ⁿ):**
>
> Unlike factorial (which makes 1 call per step), Fibonacci makes **2 calls per step**, forming a binary tree of calls:
>
> ```
> Level 0:  fib(n)              →  1 call
> Level 1:  fib(n-1), fib(n-2)  →  2 calls
> Level 2:                       →  4 calls
> ...
> Level n:                       →  2ⁿ calls
>
> Total ≈ 2⁰ + 2¹ + 2² + ... + 2ⁿ = O(2ⁿ)
> ```
>
> fib(50) would require ~1 quadrillion calls without optimization!
>
> **Fix: Memoization** caches already-computed results, reducing to O(n):
> ```python
> from functools import lru_cache
>
> @lru_cache(maxsize=None)
> def fibonacci(n):
>     if n <= 1: return n
>     return fibonacci(n-1) + fibonacci(n-2)
> ```

#### 🔍 Visual — Recursive Binary Search

```
arr=[-5,-2,0,1,2,4,5,6,7,10]  target=7

  Call 1: low=0,  high=9  →  mid=4, arr[4]=2  < 7  →  go RIGHT ➡️
    │
    └──► Call 2: low=5,  high=9  →  mid=7, arr[7]=6  < 7  →  go RIGHT ➡️
           │
           └──► Call 3: low=8,  high=9  →  mid=8, arr[8]=7 == 7
                         return 8  ✅
           └─────── return 8
    └─────── return 8
```

#### ⚙️ Structure of Every Recursive Function

```
def recursive_function(input):

  ╔══════════════════════════════════════╗
  ║  BASE CASE  (stopping condition)     ║  ← REQUIRED — prevents infinite loop
  ║  if input == smallest_possible:      ║
  ║      return simple_value             ║
  ╚══════════════════════════════════════╝

  ╔══════════════════════════════════════╗
  ║  RECURSIVE CASE                      ║
  ║  return recursive_function(          ║
  ║      smaller_version_of_input        ║  ← MUST shrink every call
  ║  )                                   ║
  ╚══════════════════════════════════════╝
```

| Property       | Description                                      |
|----------------|--------------------------------------------------|
| Base Case      | Stops recursion — REQUIRED                       |
| Recursive Case | Calls itself with smaller input                  |
| Call Stack     | Each call uses stack memory → O(n) space         |
| Stack Overflow | Happens if base case is missing/wrong            |
| Factorial Time | O(n) — one call per step                         |
| Fibonacci Time | O(2ⁿ) without memoization — use @lru_cache!      |

#### 💻 Example 1 — Factorial

```python
def factorial(n):
    if n == 0: return 1               # Base case
    return n * factorial(n - 1)       # Recursive case

print(factorial(5))  # Output: 120
```

#### 💻 Example 2 — Fibonacci

```python
def fibonacci(n):
    if n == 0: return 0               # Base case
    if n == 1: return 1               # Base case
    return fibonacci(n-1) + fibonacci(n-2)  # Recursive case — O(2ⁿ) without memo!

for i in range(8):
    print(fibonacci(i), end=" ")      # Output: 0 1 1 2 3 5 8 13
```

#### 💻 Example 3 — Recursive Binary Search

```python
def binary_search_recursive(arr, target, low, high):
    if low > high: return -1                       # Base case: not found
    mid = low + (high - low) // 2                 # safe mid formula
    if arr[mid] == target: return mid              # Base case: found
    elif arr[mid] < target:
        return binary_search_recursive(arr, target, mid+1, high)
    else:
        return binary_search_recursive(arr, target, low, mid-1)

arr = [-5, -2, 0, 1, 2, 4, 5, 6, 7, 10]
print(binary_search_recursive(arr, 7, 0, len(arr)-1))  # Output: 8
```

#### 💻 Example 4 — Recursive String Reversal

```python
def reverse_recursive(s):
    if len(s) <= 1: return s                    # Base case
    return s[-1] + reverse_recursive(s[:-1])   # Recursive case

print(reverse_recursive("Hello"))  # Output: olleH
```

#### 💻 Example 5 — Recursive Palindrome Check

```python
def is_palindrome_recursive(s, left, right):
    if left >= right: return True               # Base case: done
    if s[left] != s[right]: return False        # Base case: mismatch
    return is_palindrome_recursive(s, left+1, right-1)

s = "racecar"
print(is_palindrome_recursive(s, 0, len(s)-1))  # Output: True
```

---

## 4. Complexity Summary

| Algorithm          | Best     | Worst    | Space | Sorted? |
|--------------------|----------|----------|-------|---------|
| Linear Search      | O(1)     | O(n)     | O(1)  | ❌      |
| Binary Search      | O(1)     | O(log n) | O(1)  | ✅      |
| Ternary Search     | O(1)     | O(log₃n) | O(1)  | ✅      |
| Jump Search        | O(1)     | O(√n)    | O(1)  | ✅      |
| Exponential Search | O(1)     | O(log n) | O(1)  | ✅      |
| Reverse String     | O(n)     | O(n)     | O(1)  | —       |
| Reverse Words      | O(n)     | O(n)     | O(n)  | —       |
| Remove Duplicates  | O(n)     | O(n)     | O(n)  | —       |
| Most Repeated Char | O(n)     | O(n)     | O(k)  | —       |
| Anagram Check      | O(n)     | O(n)     | O(n)  | —       |
| Palindrome Check   | O(1)     | O(n)     | O(1)  | —       |
| Recursion (fact.)  | O(n)     | O(n)     | O(n)  | —       |
| Recursion (fib.)   | O(2ⁿ)    | O(2ⁿ)    | O(n)  | —       |

---

## 🧠 Quick Tips

- Use **Binary Search** when array is sorted and static.
- Use **Linear Search** for unsorted or small arrays.
- Use **Exponential Search** for very large or unbounded sorted arrays.
- Use **Jump Search** as a middle ground between linear and binary.
- Always define a **Base Case** in recursion — missing it causes stack overflow.
- For string problems, **frequency maps** and **two pointers** solve most challenges.
- Always use `mid = low + (high - low) // 2` over `(low + high) // 2` to avoid integer overflow in other languages.
- Naive Fibonacci recursion is **O(2ⁿ)** — always use memoization (`@lru_cache`) for large inputs.
- Rotation by k is the same as rotation by `k % n` — always normalize k first.
- Jump Search's optimal block size `√n` comes from minimizing `n/b + b` → derivative gives `b = √n`.
