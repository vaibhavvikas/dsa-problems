## Topological Sort


### Kahn's Algorithm
```
Maintain indegree:
At least one element with indegree 0
will be present
```
```
TC: O(V+E)
SC: O(V) + O(V) ~> queue + indegree
```

#### Solution
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
    
    cnt = 0
    while queue:
        node = queue.popleft()
        res.append(node)
        cnt += 1
        for each in adj[node]:
            indegree[each] -= 1
            if indegree[each] == 0:
                queue.append(each)
    
    if cnt != V:
        return [] # Cycle present
    return res
```