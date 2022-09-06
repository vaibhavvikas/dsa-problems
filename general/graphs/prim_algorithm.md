## Prim's Algorithm - Minimum Spanning Tree

Given a weighted, undirected, and connected graph of V vertices and E edges. The task is to find the sum of weights of the edges of the Minimum Spanning Tree.
**Definition:** A minimum spanning tree consists of N nodes and N-1 edges connecting all the nodes which have the minimum cost(sum of edge weights).

### Brute Force
```
TC: O(n^2)
SC: O(n)
```
### Solution
```python
def prims_algorithm(n, edges):
    adj = {i: [] for i in range(n)}

    for x, y, weight in edges:
        adj[x].append((x, weight))
        adj[y].append((y, weight))

    key = [math.inf for _ in range(n)]
    mst = [False for _ in range(n)]
    parent = [-1 for _ in range(n)]
    
    key[0] = 0
    u = 0

    for i in range(n):
        mini = math.inf
        for j in range(n):
            if not mst[j] and key[j] < mini:
                u = j
                mini = key[j]

        mst[u] = True

        for nei, cost in adj[u]:
            if cost < key[nei] and not mst[nei]:
                key[nei] = cost
                parent[nei] = u
    
    return parent
```

### Heap Implementation

```bash
TC: O(nlogn)
SC: O(n)
```

### Solution
```python
def prims_algorithm(n, edges):
    adj = {i: [] for i in range(n)}

    for x, y, weight in edges:
        adj[x].append((y, weight))
        adj[y].append((x, weight))

    
    key = [math.inf for _ in range(n)]
    mst = [False for _ in range(n)]
    parent = [-1 for _ in range(n)]
    
    key[0] = 0
    heap = [(0, key[0])]

    while heap:
        weight, u = heapq.heappop(heap)

        mst[u] = True

        for nei, cost in adj[u]:
            if cost < key[nei] and not mst[nei]:
                key[nei] = cost
                parent[nei] = u
                heapq.heappush(heap, (key[nei], nei))

    return parent
```
