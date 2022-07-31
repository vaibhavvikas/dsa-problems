## Detect Cycle in Undirected Graph


### BFS

```python
def isCycle(V, adj):
    visited = [False]*V
    
    for i in range(V):
        if not visited[i]:
            queue = deque([[i, -1]])
            visited[i] = True
            
            while queue:
                curr_node, parent = queue.popleft()
                
                for node in adj[curr_node]:
                    if node != parent and visited[node]:
                        return True
                        
                    else:
                        if not visited[node]:
                            queue.append([node, curr_node])
                            visited[node] = True
    return False
```

### DFS

```python
def isCycle(self, V, adj):
    visited = [False]*V

    def check_cycle_dfs(node, parent):
        visited[node] = True
        
        for each in adj[node]:
            if parent != each:
                if visited[each]:
                    return True

                if check_cycle_dfs(each, node):
                    return True
                
        return False

    for i in range(V):
        if not visited[i]:
            if check_cycle_dfs(i, -1):
                return True
    return False
```
