## Bridges in an undirected graph

Example:
adj = {1:[2, 4], 2:[1, 3], 3:[2, 4], 4:[1, 3, 5], 5:[4, 6], 6:[5, 7, 9], 7:[6, 8], 8:[7, 9, 10], 9:[6, 8], 10:[8, 11, 12], 11:[10, 12], 12:[10, 11]}
bridges = [(8, 10), (5, 6), (4, 5)]


### Algorithm
```bash
Step 1. We create two lists,
time of insertion and low

Step 2. Everytime we visit the node
for the first time we mark its tin and low
as same as current timer.

Step 3. Now for each adj nodes, we call dfs
and update low[curr] as min of it and low[next]

Step 4. if low[next] > tin[curr] means its a bridge
```

### Solution
```python
def bridges(adj, n):
    tin = [None] * n
    low = [None] * n

    def dfs(curr, timer, prev):
        tin[curr] = timer
        low[curr] = timer

        for next in adj[curr]:
            if next == prev:
                continue

            if tin[next] == None:
                dfs(next, timer+1, curr)
                low[curr] = min(low[curr], low[next])

                if low[next] > tin[curr]:
                    res.append((curr, next))
            else:
                low[curr] = min(low[curr], low[next])

    res = []
    
    for i in range(1, n):
        if tin[i] == None:
            dfs(i, 1, None)

    print(res)
```