Implement Breadth First Traversal (BFT) and Depth First Traversal (DFT) using:
1. Adjacency Matrix
2. Adjacency List
A) Adjacency Matrix
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

print("\\nDFT (Adjacency Matrix):")
dft(graph, 0)
Output
BFT (Adjacency Matrix):
0 1 2 3
DFT (Adjacency Matrix):
0 1 3 2
B) Adjacency List
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

print("\\nDFT (Adjacency List):")
dft(graph, 0)
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
