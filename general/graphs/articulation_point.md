## Articulation Point

### Algorithm
```bash
Expanding the bridges algo,

the condition will be low[next] >= tin[curr]
and parent != None it will be articulation
point

also in the case the first node has multiple 
disconnected points in that case it will be 
an articualtion point, so we need to check
that too.
```

## Solution

```python
def art(adj, n):
    tin = [None] * n
    low = [None] * n
    
    def dfs(curr, timer, prev):
        tin[curr] = timer
        low[curr] = timer
        child = 0

        for next in adj[curr]:
            if next == prev:
                continue

            if tin[next] == None:
                dfs(next, timer+1, curr)
                low[curr] = min(low[curr], low[next])

                if low[next] >= tin[curr] and prev != None:
                    res.add(curr)
                child += 1
            else:
                low[curr] = min(low[curr], low[next])

        if child > 1 and prev == None:
            res.add(curr)

    res = set()

    for i in range(1, n):
        if tin[i] == None:
            dfs(i, 1, None)

    print(res)
```
