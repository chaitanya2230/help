
# BFT and DFT for a Graph

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
```

### Output

```text
BFT (Adjacency List):
0 1 2 3
DFT (Adjacency List):
0 1 3 2
```

## Key Concepts

- **BFT (Breadth First Traversal):** Uses a queue to visit vertices level by level.
- **DFT (Depth First Traversal):** Uses recursion to explore deeply before backtracking.
- **Visited Array:** Prevents visiting the same vertex repeatedly.
- **Adjacency Matrix:** Checks edges using `graph[v][i] == 1`.
- **Adjacency List:** Visits neighbors directly using `graph[v]`.

## Time Complexity

| Representation | BFT | DFT |
|---|---|---|
| Adjacency Matrix | O(V²) | O(V²) |
| Adjacency List | O(V + E) | O(V + E) |

Where `V` is the number of vertices and `E` is the number of edges.

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

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Job Sequencing with Deadlines Using Greedy Algorithm

## Python Code

```python
class Job:
    def __init__(self, job_id, deadline, profit):
        self.id = job_id
        self.deadline = deadline
        self.profit = profit


def job_sequencing(jobs):
    jobs.sort(key=lambda x: x.profit, reverse=True)

    n = max(job.deadline for job in jobs)
    result = [None] * n
    total_profit = 0

    for job in jobs:
        for slot in range(job.deadline - 1, -1, -1):
            if result[slot] is None:
                result[slot] = job.id
                total_profit += job.profit
                break

    scheduled_jobs = [
        job_id for job_id in result if job_id is not None
    ]

    return scheduled_jobs, total_profit


if __name__ == "__main__":
    jobs = [
        Job('A', 7, 15),
        Job('B', 2, 20),
        Job('C', 5, 30),
        Job('D', 3, 18),
        Job('E', 4, 18),
        Job('F', 5, 10),
        Job('G', 2, 23),
        Job('H', 7, 16),
        Job('I', 3, 25)
    ]

    scheduled_jobs, total_profit = job_sequencing(jobs)

    print("Scheduled jobs:", scheduled_jobs)
    print("Total profit:", total_profit)
```

## Sample Output

```text
Scheduled jobs: ['C', 'I', 'G', 'E', 'A']
Total profit: 114
```

## Algorithm

1. Sort all jobs in decreasing order of profit.
2. Find the maximum deadline and create empty time slots.
3. For each job, search for an empty slot from its deadline backward.
4. Schedule the job if a slot is available.
5. Add the job's profit to the total profit.
6. Return the scheduled jobs and maximum profit.

## Time Complexity

- **Sorting:** O(n log n)
- **Scheduling:** O(n × d), where `d` is the maximum deadline.
- **Overall:** O(n log n + n × d)

## Key Concept

The Greedy Algorithm selects higher-profit jobs first and schedules each job in the latest available slot before its deadline.
=====================================================================================================================================================================================================================================

# 9. 0/1 Knapsack Problem Using Dynamic Programming

## Python Code

```python
def knapsack_dp(values, weights, capacity):
    n = len(values)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            if weights[i - 1] <= w:
                dp[i][w] = max(
                    dp[i - 1][w],
                    values[i - 1] + dp[i - 1][w - weights[i - 1]]
                )
            else:
                dp[i][w] = dp[i - 1][w]

    return dp[n][capacity]


values = [60, 100, 120]
weights = [10, 20, 30]
W = 50

print("Maximum value in Knapsack =", knapsack_dp(values, weights, W))
```

## Output

```text
Maximum value in Knapsack = 220
```

## Algorithm

1. Create a DP table initialized with zeros.
2. Iterate through each item and each capacity.
3. If the item fits, choose the maximum value between including and excluding it.
4. If the item does not fit, copy the value from the previous row.
5. Return `dp[n][capacity]`.

## Time and Space Complexity

- **Time Complexity:** O(n × W)
- **Space Complexity:** O(n × W)

Where `n` is the number of items and `W` is the knapsack capacity.

## Explanation

The 0/1 Knapsack problem selects items to maximize total value without exceeding the capacity. Each item can be selected at most once.

For the given input, items with weights 20 and 30 provide the maximum value of **220**, with a total weight of 50.
==========================================================================================================================================================================================================================

# 11. 0/1 Knapsack Problem Using Backtracking

## Python Code

```python
def knapsack_backtrack(values, weights, capacity, n):
    if n == 0 or capacity == 0:
        return 0

    if weights[n - 1] > capacity:
        return knapsack_backtrack(
            values, weights, capacity, n - 1
        )
    else:
        return max(
            values[n - 1] + knapsack_backtrack(
                values, weights, capacity - weights[n - 1], n - 1
            ),
            knapsack_backtrack(
                values, weights, capacity, n - 1
            )
        )


values = [60, 100, 120]
weights = [10, 20, 30]
W = 50

max_value = knapsack_backtrack(
    values, weights, W, len(values)
)

print("Maximum value in Knapsack =", max_value)
```

## Output

```text
Maximum value in Knapsack = 220
```

## Algorithm

1. Check whether there are no items left or the capacity is zero.
2. If the current item exceeds the capacity, skip it.
3. Otherwise, calculate two possibilities:
   - Include the item and reduce the remaining capacity.
   - Exclude the item and continue with the remaining items.
4. Return the maximum value from both possibilities.

## Time and Space Complexity

- **Time Complexity:** O(2ⁿ)
- **Space Complexity:** O(n), due to recursive calls.

## Explanation

The 0/1 Knapsack problem selects items to maximize total value without exceeding the bag's capacity. Backtracking explores both including and excluding each item.

For the given input, the maximum value is **220**, obtained by selecting the items with weights 20 and 30.

