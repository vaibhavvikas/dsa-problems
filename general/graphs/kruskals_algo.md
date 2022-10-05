## Kruskal's Algorruthm

Min Spanning Tree

1. Sort all the edges in non-decreasing order of their weight. 
2. Pick the smallest edge. Check if it forms a cycle with the spanning tree formed so far. If cycle is not formed, include this edge. Else, discard it. 
3. Repeat step 2 until there are (V-1) edges in the spanning tree.

### Solution

```python
class UnionFind:
    def __init__(self, V):
        self.parent = {v:v for v in range(V)}
        self.rank = {v:0 for v in range(V)}

    def find(self, node):
        if self.parent[node] != node:
            self.parent[node] = self.find(self.parent[node])
        
        return self.parent[node]

    def union(self, a, b):
        root_a = self.find(a)
        root_b = self.find(b)

        if root_a == root_b:
            return False

        if self.rank[root_a] < self.rank[root_b]:
            self.parent[root_a] = self.parent[root_b]
        elif self.rank[root_a] > self.rank[root_b]:
            self.parent[root_a] = self.parent[root_b]
        else:
            self.parent[root_b] = self.parent[root_a]
            self.rank[root_a] += 1

        return True


def kruskals_algo(adj):
    heap = []

    visited = set()

    for start in adj:
        for dest, cost in adj[start]:
            if (start, dest) not in visited:
                heapq.heappush(heap, (cost, min(start, dest), max(start, dest)))
                visited.add((start, dest))
                visited.add((dest, start))

    uf = UnionFind(len(adj))

    total_cost = 0

    while heap:
        cost, start, end = heapq.heappop(heap)
        if uf.union(start, end):
            total_cost += cost
            print(start, end, cost)

    print(total_cost)
```