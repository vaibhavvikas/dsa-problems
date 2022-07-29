## 1579. Remove edges to keep graph fully traversal

Alice and Bob have an undirected graph of n nodes and 3 types of edges:

Type 1: Can be traversed by Alice only.
Type 2: Can be traversed by Bob only.
Type 3: Can by traversed by both Alice and Bob.

Return the maximum number of edges you can remove, or return -1 if it's impossible for the graph to be fully traversed by Alice and Bob.

### Algorithm
```bash
Union Find:

Step 1. Use type 3 to create a union find for A

Step 2. Copy the union find for B from A

Step 3. Now for each edge
    if its type 1 or type 2, we check if there
    is already a conection to root from both
    vertices.
    if yes skip it otherwise add it to union find

Step 4. Check if both a and b has same number of edges
    if yes return res other wise -1 as there is 
    a non-connected component
```
```
TC: O(nα) α is inverse Ackermann 
SC: O(n)
```

### Solution

```python
class UnionFind:
    def __init__(self, n):
        self.parents = [i for i in range(n+1)]
        self.rank = [0]*(n+1)
        
    def find(self, i):
        if self.parents[i] != i:
            self.parents[i] = self.find(self.parents[i])
            
        return self.parents[i]
    
    def union(self, a, b):
        root_a, root_b = self.find(a), self.find(b)
        
        if root_a == root_b:
            return False
        
        if self.rank[root_a] < self.rank[root_b]:
            self.parents[root_a] = self.parents[root_b]
        else:
            self.parents[root_b] = self.parents[root_a]
            
        return True
    
    def copy(self):
        uf = UnionFind(0)
        uf.parents = self.parents.copy()
        uf.rank = self.rank.copy()
        return uf

class Solution:
    def maxNumEdgesToRemove(self, n, edges):
        if len(edges) < n-1:
            return -1
        
        b_union_find = UnionFind(n)
        b_edges = a_edges = res = 0
        
        for type, start, end in edges:
            if type == 3:
                if b_union_find.union(start, end):
                    b_edges += 1
                    a_edges += 1
                else:
                    res += 1
                    
        a_union_find = b_union_find.copy()
        
        for type, start, end in edges:
            if type == 1:
                if a_union_find.union(start, end):
                    a_edges += 1
                else:
                    res += 1
                    
            if type == 2:
                if b_union_find.union(start, end):
                    b_edges += 1
                else:
                    res += 1
                    
        return res if a_edges == b_edges == n-1 else -1    
```