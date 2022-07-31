## Cycle in Directed Graph

### DFS

```python
def isCyclic(V, adj):
    self.visited = [False]*V
    self.dfs_visited = [False]*V
    
    for i in range(V):
        if not self.visited[i]:
            if self.dfs_cycle(i, adj):
                return True
    return False
    
def dfs_cycle(self, node, adj):
    self.visited[node] = True
    self.dfs_visited[node] = True
    
    for each in adj[node]:
        if not self.visited[each]:
            if self.dfs_cycle(each, adj):
                return True
        elif self.dfs_visited[each]:
            return True
                
    self.dfs_visited[node] = False
    return False
```

### BFS Using Kah's Algorithm

```python
def detectCycle(self, V, adj):
    res = []
    indegree = [0]*V
    
    for i in range(V):
        for each in adj[i]:
            indegree[each] += 1
            
    queue = deque([])
    
    for i in range(V):
        if indegree[i] == 0:
            queue.append(i)
    
    cnt = 0
    while queue:
        cnt += 1
        node = queue.popleft()
        res.append(node)
        
        for each in adj[node]:
            indegree[each] -= 1
            if indegree[each] == 0:
                queue.append(each)
        
    return cnt == V
```