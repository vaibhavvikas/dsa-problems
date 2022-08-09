## Union Find with Path Compression

```bash
TC:
Union O(4alpha)
Find O(4alpha)

SC: O(n) + O(n)
```
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

```