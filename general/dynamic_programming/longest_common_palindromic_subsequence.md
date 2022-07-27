## Longest Common Palindromic Subsequence

Find the longest common palindromic subsequence.

### Algorithm:
```python
Tabulation: Bottom Up
Step 1: Copy the base cases:
    for that we incremented the index of dp
    i.e. we took the size of len(string) + 1
    i.e Shifting right

Step 2: Changing params in opp manner:
    Start from 1 to len(string) + 1

Step 3: Copy the recurrence:
    If matches increment both
    else: decrement either and return max
```
```python
TC ~> O(n^2)
SC ~> O(n^2)
```

### Solution:

```python
def lcps(s):
    n = len(s)
    t = s[::-1]
    dp = [[0]*(n+1) for _ in range(n+1)]
    
    for i in range(1, n+1):
        for j in range(1, n+1):
            if s[i-1] == t[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[-1][-1]
```
