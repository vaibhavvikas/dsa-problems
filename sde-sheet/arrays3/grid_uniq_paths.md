## Grid Unique Paths

### Maths
```
TC: O(min(m, n))
SC: O(1)
```
```python
def uniquePaths(m, n):
    N = n + m - 2
    r = min(n, m) - 1
    return comb(N, r)
```

### Dynamic Programming
```bash
TC: O(m*n)
SC: O(m*n)
```
```python
def uniquePaths(m, n):
    res = [[1]*n for _ in range(m)]

    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i][j-1] + dp[i-1][j]

    return dp[-1][-1]
```