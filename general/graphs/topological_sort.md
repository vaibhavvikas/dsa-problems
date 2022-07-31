## Topological Sort

### Kahn's Algorithm
```python
def topoSort(V, adj):
    res = []
    indegree = [0]*V
    
    for i in range(V):
        for each in adj[i]:
            indegree[each] += 1
            
    queue = deque([])
    
    for i in range(V):
        if indegree[i] == 0:
            queue.append(i)
    
    while queue:
        node = queue.popleft()
        res.append(node)
        
        for each in adj[node]:
            indegree[each] -= 1
            if indegree[each] == 0:
                queue.append(each)
        
    return res
```