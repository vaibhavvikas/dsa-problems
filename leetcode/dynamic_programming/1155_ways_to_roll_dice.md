## 1155. Number of ways to roll a dice

You have n dice and each die has k faces numbered from 1 to k.

Given three integers n, k, and target, return the number of possible ways to roll the dice so the sum of the face-up numbers equals target.

Return answer % 10**9 + 7


### Top Down Approach: Memoization

#### Algorithm

```bash
Base Case: 
If n == 0:
    if target == 0:
        return 1
    else return 0

For each case we have two options
1. We run a loop from 1 to 
min(k + 1, desired_sum)
and each time decrement the index
and also the desired_val
```
```
TC: O(N∗T∗K)
SC: O(N*T) + Stack O(N)
```

#### Solution

```python
def numRollsToTarget(n: int, k: int, target: int)
    dp = {}
    
    def helper(ind, desired_sum):
        if ind == 0:
            return desired_sum == 0
        
        if (ind, desired_sum) in dp:
            return dp[(ind, desired_sum)]
        
        req_sum = 0
        
        # we cannot exceed our desired_value so we keep
        # it under limit by using min
        for value in range(1, min(k+1, desired_sum + 1)):
            req_sum += helper(ind - 1, desired_sum-value)
            
        dp[(ind, desired_sum)] = req_sum % (10**9 + 7)
        return dp[(ind, desired_sum)]
    
    return helper(n, target)
```

### Bottom Up - Tabulation

#### Algorithm
```bash
Step 1: Initialize DP

set base case i.e. dp[0][0] = 1

Now convert it to tabulation
```
```
TC: O(N∗T∗K)
SC: O(N*T)
```
#### Solution
```python
def numRollsToTarget(n: int, k: int, target: int)
    dp = [[0]*(target+1) for _ in range(n+1)]
    MOD = 10**9 + 7
    
    dp[0][0] = 1
    
    for ind in range(1, n+1):
        for desired in range(1, target+1):
            for value in range(1, min(desired, k)+1):
                dp[ind][desired] += dp[ind-1][desired-value] % MOD
                
    return dp[-1][-1] % MOD
```