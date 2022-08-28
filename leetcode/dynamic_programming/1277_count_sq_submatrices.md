## 1277. Count Square Submatrices

Given a m * n matrix of ones and zeros, return how many square submatrices have all ones.

```bash
Example
Input: matrix =
[
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
Output: 15
```

### Algorithm
```bash
The first row and firs column will
be as it is

Now for each element the number of
sq will be min of its adjent 3 edges
+ 1
```
```
TC: O(m*n)
SC: O(m*n)
```

### Solution
```python
def countSquares(matrix):
    m, n = len(matrix), len(matrix[0])
    dp = [[0]*n for _ in range(m)]
    res = 0
    
    dp[0] = matrix[0]
    res = sum(dp[0])
    
    for i in range(1, m):
        dp[i][0] = matrix[i][0]
        res += dp[i][0]

    for i in range(1, m):
        for j in range(1, n):
            if matrix[i][j]  == 1:
                dp[i][j] = min(dp[i-1][j-1], \
                           dp[i-1][j], dp[i][j-1]) + 1
                res += dp[i][j]
                    
    return res
```
