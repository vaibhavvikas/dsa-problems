## Edit Distance

```bash
Example:
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

### Recursion + Memoization
```bash
TC: O(m*n)
SC: O(m*n) + O(min(m, n))
```

```python
def edit_distance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[-1]*n for _ in range(m)]
    
    def recurse(ind1, ind2):
        if ind1 < 0:
            return ind2 + 1
        
        if ind2 < 0:
            return ind1 + 1
        
        if dp[ind1][ind2] != -1:
            return dp[ind1][ind2]
        
        if word1[ind1] == word2[ind2]:
            dp[ind1][ind2] = recurse(ind1-1, ind2-1)
            return dp[ind1][ind2]
        
        dp[ind1][ind2] = 1 + min(recurse(ind1, ind2-1), 
                                 recurse(ind1-1, ind2),
                                 recurse(ind1-1, ind2-1))
        
        return dp[ind1][ind2]
    
    return recurse(m-1, n-1)
```

### Tabulation

```python
def minDistance(word1, word2):
    m, n = len(word1), len(word2)
    dp = [[-1]*(n+1) for _ in range(m+1)]
    
    for ind1 in range(m+1):
        dp[ind1][0] = ind1
        
    for ind2 in range(n+1):
        dp[0][ind2] = ind2
    
    for ind1 in range(1, m+1):
        for ind2 in range(1, n+1):
            if word1[ind1-1] == word2[ind2-1]:
                dp[ind1][ind2] = dp[ind1-1][ind2-1]
            
            else:
                dp[ind1][ind2] = 1 + min(dp[ind1][ind2-1], 
                                         dp[ind1-1][ind2],
                                         dp[ind1-1][ind2-1])

    return dp[-1][-1]
```
