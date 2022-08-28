## Count Subset with target Sum

### Algortihm
```bash
Continuing knapsack Approach
Number will be take + not_take
```
```bash
TC: O(n*target)
SC: O(n*target)
```

### Solution
```python
def perfectSum(arr, n, target):
    dp = [[-1]*(target+1) for _ in range(n)]
    MOD = 10**9 + 7
    
    def recurse(ind, curr):
        if ind == n:
            if curr == target:
                return 1
            return 0
        
        if dp[ind][curr] != -1:
            return dp[ind][curr]
        
        take = 0
        if curr + arr[ind] <= target:
            take = recurse(ind+1, curr + arr[ind])
            
        not_take = recurse(ind+1, curr)
        
        dp[ind][curr] = (take + not_take)%MOD
        return dp[ind][curr]
        
    return recurse(0, 0)
```
