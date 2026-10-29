
# Implement BFT and DFT for a Graph

Implement Breadth First Traversal (BFT) and Depth First Traversal (DFT) using:

1. Adjacency Matrix
2. Adjacency List

## A) Adjacency Matrix

### Python Code

```python
from collections import deque

graph = [
    [0, 1, 1, 0],
    [1, 0, 0, 1],
    [1, 0, 0, 1],
    [0, 1, 1, 0]
]

def bft(graph, start):
    n = len(graph)
    visited = [False] * n
    q = deque([start])
    visited[start] = True

    while q:
        v = q.popleft()
        print(v, end=" ")

        for i in range(n):
            if graph[v][i] == 1 and not visited[i]:
                q.append(i)
                visited[i] = True

def dft(graph, start, visited=None):
    if visited is None:
        visited = [False] * len(graph)

    visited[start] = True
    print(start, end=" ")

    for i in range(len(graph)):
        if graph[start][i] == 1 and not visited[i]:
            dft(graph, i, visited)

print("BFT (Adjacency Matrix):")
bft(graph, 0)

print("\nDFT (Adjacency Matrix):")
dft(graph, 0)
```

### Output

```text
BFT (Adjacency Matrix):
0 1 2 3
DFT (Adjacency Matrix):
0 1 3 2
```

## B) Adjacency List

### Python Code

```python
from collections import deque

graph = {
    0: [1, 2],
    1: [0, 3],
    2: [0, 3],
    3: [1, 2]
}

def bft(graph, start):
    visited = [False] * len(graph)
    q = deque([start])
    visited[start] = True

    while q:
        v = q.popleft()
        print(v, end=" ")

        for i in graph[v]:
            if not visited[i]:
                q.append(i)
                visited[i] = True

def dft(graph, start, visited=None):
    if visited is None:
        visited = [False] * len(graph)

    visited[start] = True
    print(start, end=" ")

    for i in graph[start]:
        if not visited[i]:
            dft(graph, i, visited)

print("BFT (Adjacency List):")
bft(graph, 0)

print("\nDFT (Adjacency List):")
dft(graph, 0)
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 5. Implement Quick Sort and Merge Sort

Implement Quick Sort and Merge Sort and observe their execution time for different input sizes in Average, Best, and Worst cases.

## Python Code

```python
import random
import time

def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]

    return quick_sort(left) + middle + quick_sort(right)


def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    return merge(left, right)


def merge(left, right):
    result = []
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    result.extend(left[i:])
    result.extend(right[j:])
    return result


def measure_time(sort_func, arr):
    start = time.time()
    sort_func(arr)
    end = time.time()
    return end - start


sizes = [1000, 5000, 10000]
cases = ["Average", "Best", "Worst"]

for size in sizes:
    print(f"\nInput size: {size}")

    arr_avg = [random.randint(0, size) for _ in range(size)]
    arr_best = sorted(arr_avg)
    arr_worst = sorted(arr_avg, reverse=True)

    for case, arr in zip(cases, [arr_avg, arr_best, arr_worst]):
        time_quick = measure_time(quick_sort, arr.copy())
        time_merge = measure_time(merge_sort, arr.copy())

        print(
            f"{case} Case - Quick Sort: {time_quick:.5f}s, "
            f"Merge Sort: {time_merge:.5f}s"
        )
```

## Sample Output

*Execution times vary depending on the computer and system load.*

```text
Input size: 1000
Average Case - Quick Sort: 0.00229s, Merge Sort: 0.00594s
Best Case - Quick Sort: 0.00131s, Merge Sort: 0.00384s
Worst Case - Quick Sort: 0.00126s, Merge Sort: 0.00267s

Input size: 5000
Average Case - Quick Sort: 0.01103s, Merge Sort: 0.02673s
Best Case - Quick Sort: 0.00829s, Merge Sort: 0.01253s
Worst Case - Quick Sort: 0.01002s, Merge Sort: 0.01602s

Input size: 10000
Average Case - Quick Sort: 0.02439s, Merge Sort: 0.03977s
Best Case - Quick Sort: 0.02247s, Merge Sort: 0.03548s
Worst Case - Quick Sort: 0.01557s, Merge Sort: 0.02738s
```

## Time Complexity

| Algorithm | Best Case | Average Case | Worst Case |
|---|---|---|---|
| Quick Sort | O(n log n) | O(n log n) | O(n²) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) |

## Explanation

- **Quick Sort:** Selects a pivot and partitions elements into smaller and larger groups, then sorts them recursively.
- **Merge Sort:** Divides the array into halves, sorts each half recursively, and merges the sorted halves.
- **Execution time:** Measured using Python's `time` module.
- **Input sizes:** 1,000, 5,000, and 10,000 elements.
- **Conclusion:** Merge Sort has predictable O(n log n) time complexity. Quick Sort can be efficient in practice, but its worst-case time complexity is O(n²).

**Note:** The program uses random arrays, sorted arrays, and reverse-sorted arrays as the three test cases. These are practical test inputs, but they do not guarantee the theoretical best and worst cases for this particular Quick Sort implementation.

