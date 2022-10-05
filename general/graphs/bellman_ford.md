## Bellman Ford's Algorithm

Bellman Ford Algorithm states that we gonna relax the graph N - 1 times (N is number of nodes in the graph), then we will have the shortest disance for the graph. Afer N - 1 times, we do the relaxation one more time. If a that time the distance array is reduces that implies there is a negative cycle in the graph.

### Algorithm

```bash
Step 1. Create a distance array of size N
initialize everything except the first
node as inf.

Step 2. For N - 1 time we traverse through
all the edges and update the distance
if dis[u] + wt > dis[v]:
    dis[v] = dis[u] + wt

Step 3. After N - 1 times, we relax one
more time. If the dis array changes, that
means there is a negative cycle
```
```
TC: O(n*e)
SC: O(n)
```

### Solution

```python

def bellman_ford(adj, n):
    dis = [math.inf] * n
    dis[0] = 0

    for _ in range(n-1):
        for start in adj:
            for end, wt in adj[start]:
                if dis[start] + wt < dis[end]:
                    dis[end] = dis[start] + wt

    flag = 0
    for start in adj:
        for end, wt in adj[start]:
            if dis[start] + wt < dis[end]:
                return True, [] # Negative Cycle Exists

    return False, dis 
```