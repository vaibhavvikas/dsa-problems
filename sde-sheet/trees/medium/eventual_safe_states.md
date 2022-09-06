## Eventual Safe States

[GFG Link](https://practice.geeksforgeeks.org/problems/eventual-safe-states/1)

A directed graph of V vertices and E edges is given in the form of an adjacency list adj. Each node of the graph is labelled with a distinct integer in the range 0 to V - 1.
A node is a terminal node if there are no outgoing edges. A node is a safe node if every possible path starting from that node leads to a terminal node.
You have to return an array containing all the safe nodes of the graph. The answer should be sorted in ascending order.

### DFS Solutiom

```python    
def eventualSafeNodes(self, V, adj):
    visited = [0]*(V)
    path_vis = [0]*(V)
    safe = [0]*(V)
    
    def dfs(node):
        visited[node] = 1
        path_vis[node] = 1
        safe[node] = 0

        for nei in adj[node]:
            if not visited[nei]:
                if dfs(nei):
                    return True

            elif path_vis[nei]:
                return True
                
        path_vis[node] = 0
        safe[node] = 1
        return False
        
    for node in range(V):
        if not visited[node]:
            dfs(node)
    
    res = []
    for node in range(V):
        if safe[node]:
            res.append(node)

    return res
```