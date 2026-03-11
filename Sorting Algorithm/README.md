
# 🔢 Sorting Algorithms — Data Structures & Algorithms

This project demonstrates the implementation of fundamental **Sorting Algorithms**
using Python as part of a **Data Structures and Algorithms (DSA)** learning course.

The notebook contains implementations and explanations of several classic sorting
techniques used in computer science and software engineering.

---

# 📚 Algorithms Covered

The project includes implementations for the following algorithms:

- Bubble Sort
- Insertion Sort
- Selection Sort
- Merge Sort
- Quick Sort
- Counting Sort
- Bucket Sort

Each algorithm below includes:

- Explanation
- Example
- Python implementation (syntax)

---

# 🫧 1. Bubble Sort

Bubble Sort repeatedly compares adjacent elements and swaps them if they
are in the wrong order.

### Example

Input:
[5, 2, 9, 1]

Output:
[1, 2, 5, 9]

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

| Case | Time Complexity |
|-----|-----|
| Best | O(n) |
| Average | O(n²) |
| Worst | O(n²) |

---

# ✋ 2. Insertion Sort

Insertion Sort builds the sorted list one element at a time.

### Example

Input:
[8, 3, 5, 2]

Output:
[2, 3, 5, 8]

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

| Case | Time Complexity |
|-----|-----|
| Best | O(n) |
| Average | O(n²) |
| Worst | O(n²) |

---

# 🔎 3. Selection Sort

Selection Sort repeatedly selects the smallest element and moves it to the beginning.

### Example

Input:
[29, 10, 14, 37]

Output:
[10, 14, 29, 37]

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

| Case | Time Complexity |
|-----|-----|
| Best | O(n²) |
| Average | O(n²) |
| Worst | O(n²) |

---

# ⚡ 4. Merge Sort

Merge Sort is a divide-and-conquer algorithm.

### Example

Input:
[38, 27, 43, 3]

Output:
[3, 27, 38, 43]

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

| Case | Time Complexity |
|-----|-----|
| Best | O(n log n) |
| Average | O(n log n) |
| Worst | O(n log n) |

---

# 🚀 5. Quick Sort

Quick Sort selects a pivot element and partitions the array around it.

### Example

Input:
[10, 7, 8, 9, 1]

Output:
[1, 7, 8, 9, 10]

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

| Case | Time Complexity |
|-----|-----|
| Best | O(n log n) |
| Average | O(n log n) |
| Worst | O(n²) |

---

# 🧮 6. Counting Sort

Counting Sort counts how many times each element appears.

### Example

Input:
[4, 2, 2, 8, 3]

Output:
[2, 2, 3, 4, 8]

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

| Case | Time Complexity |
|-----|-----|
| Best | O(n + k) |
| Average | O(n + k) |
| Worst | O(n + k) |

---

# 🪣 7. Bucket Sort

Bucket Sort distributes elements into buckets, sorts each bucket, then merges them.

### Example

Input:
[0.42, 0.32, 0.23, 0.52, 0.25]

Output:
[0.23, 0.25, 0.32, 0.42, 0.52]

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

| Case | Time Complexity |
|-----|-----|
| Best | O(n + k) |
| Average | O(n + k) |
| Worst | O(n²) |

---

# 🧠 Algorithm Comparison

| Algorithm | Best | Average | Worst |
|------|------|------|------|
| Bubble Sort | O(n) | O(n²) | O(n²) |
| Insertion Sort | O(n) | O(n²) | O(n²) |
| Selection Sort | O(n²) | O(n²) | O(n²) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) |
| Quick Sort | O(n log n) | O(n log n) | O(n²) |
| Counting Sort | O(n+k) | O(n+k) | O(n+k) |
| Bucket Sort | O(n+k) | O(n+k) | O(n²) |

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
