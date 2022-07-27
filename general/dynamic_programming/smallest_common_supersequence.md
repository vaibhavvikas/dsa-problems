## Smallest Common Supersequence

A supersequence is a sequence from which we can obtain both the sequences.

### Algorithm
```bash
Step 1. Make Tabulation to find
    max common sub sequence.
Step 2. Start from end.
Step 3. If match then decrement both i, j
    adding a[i] to res
    else: We check if dp[i-1][j] > dp[i][j-1]
    and we shift accordingly adding the
    other element to res

    if dp[i-1][j] > dp[i][j-1] ~> Shift Up
    else: shift left
```
```bash
TC: O(mn) + O(m+n) ~> Tabulation and Printing
SC: O(mn) + res_size ~> O(m + n - len(lcs))
```


### Solution
```python
def shortestSupersequence(a: str, b: str) -> str:
    m, n  = len(a), len(b)
    
    dp = [[0]*(n+1) for _ in range(m+1)]
    
    for i in range(1, m+1):
        for j in range(1, n+1):
            if a[i-1] == b[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    res = ""
    i, j = m, n
    
    while i > 0 or j > 0:

        if i == 0:
            res += b[j-1]
            j -= 1
            continue

        if j == 0:
            res += a[i-1]
            i -= 1
            continue

        if a[i-1] != b[j-1]:
            if dp[i-1][j] > dp[i][j-1]:
                res += a[i-1]
                i -= 1
            else:
                res += b[j-1]
                j -= 1
        else:
            res += a[i-1]
            i -= 1
            j -= 1

    return res[::-1]
```