## Bipartite Graph

### BFS
```python
def isBipartite(V, adj):
    colors = [-1]*V
    
    for i in range(V):
        if colors[i] == -1:
            queue = deque([[i, 0]])
            colors[i] = 0
            
            while queue:
                node, color = queue.popleft()
                for each in adj[node]:
                    if colors[each] == -1:
                        queue.append([each, 1-color])
                        colors[each] = 1-color
                    elif colors[each] == color:
                        return False

    return True
```
