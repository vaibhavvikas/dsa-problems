## Kosaraju's Algorithm

This algorithm is used to find strongly connected components in a directed graph.

A strongly component is a component where we can reach all other vertices from a vertex

### Algorithm

```bash
Step 1. Find stack using DFS Topo Sort
Step 2. Transpose he graph i.e. reverse edges
Step 3. Find DFS using stacl from step 1
```

### Solution
```python
from collections import defaultdict, deque

def topoSortDFS(V, adj):
    visited = [None] * V
    res = []

    def dfs(node):
        visited[node] = True
        if node in adj:
            for nei in adj[node]:
                if visited[nei] == None:
                    dfs(nei)

        res.append(node)

    dfs(0, visited, adj, [])
    return res

def transpose_adj(adj):
    transposed = defaultdict(list)

    for start in adj:
        for end in adj[start]:
            transposed[end].append(start)

    return transposed

def DFS(node, visited, transposed_adj, res):
    visited.add(node)

    for nei in transposed_adj[node]:
        if nei not in visited:
            DFS(nei, visited, transposed_adj, res)
    
    res.append(node)
    return res

def kosaraju(adj):
    stack = topoSortDFS(5, adj)
    transposed_adj = transpose_adj(adj)
    visited = set()

    print(transposed_adj)
    scc = []
    
    while stack:
        curr_node = stack.pop()
        if curr_node not in visited:
            scc.append(DFS(curr_node, visited, transposed_adj, []))

    print(scc)
```