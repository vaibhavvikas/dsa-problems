## O-1 Knapsack Problem

Given a list of items, their weight and their value
Find the max value someone can get with a constraint
of total weight W.

```bash
Input:
W = 5 
val = [1 2 4 5]
wi = [5 4 8 6]

Output:
13
```

### Recursion + Top Down

#### Algorithm
```bash
We have two cases take or not_take
take if only curr_weight allows 
else skip

Base case if ind == 0:
    take only if e can
```
```bash
TC: (2^n) ~> Exponential 
SC: O(n) ~> Stack Space
```

#### Solution
```python
def find_max_profit(W, wei, val):

    def recurse(ind, rem_weight):
        if ind == 0:
            if rem_weight >= wei[ind]:
                return val[ind]
            return 0

        take = 0
        if wei[ind] <= rem_weight:
            take = val[ind] + recurse(ind-1, rem_weight-wei[ind])

        not_take = recurse(ind-1, rem_weight)

        return max(take, not_take)
    
    return recurse(len(wei)-1, W)
```

### Memoization + Recursion + Top Down

#### Algorithm
```bash
We have two cases take or not_take
Take the above cases and memoize it
```
```bash
TC: O(n^2) 
SC: O(n^2) + O(n) Stack Space
```

#### Solution
```python
def find_max_profit(W, wei, val):

    dp = [[-1]*(W+1) for _ in range(len(val))]

    def recurse(ind, rem_weight):
        if ind == 0:
            if rem_weight >= wei[ind]:
                dp[ind][rem_weight] = val[ind]
                return dp[ind][rem_weight]
            dp[ind][rem_weight] = 0
            return dp[ind][rem_weight]
        
        if dp[ind][rem_weight] != -1:
            return dp[ind][rem_weight]

        take = 0
        if wei[ind] <= rem_weight:
            take = val[ind] + recurse(ind-1, rem_weight-wei[ind])

        not_take = recurse(ind-1, rem_weight)

        dp[ind][rem_weight] = max(take, not_take)
        return dp[ind][rem_weight]
    
    return recurse(len(wei)-1, W)
```


### Tabulation + Bottom Down

#### Algorithm
```bash
Base Case:
if ind == 0:
    if rem_weight >= wei[ind]:
        return val[ind]
    return 0

converting it to Tabulation:
we know it is called only if ind == 0
abut rem_weight can be any in the range Weights
also the min wt can be wt[0]

```
```bash
TC: O(n^2) 
SC: O(n^2)
```

#### Solution
```python
def find_max_profit(n, max_weight, wt, val):
    dp = [[0]*(max_weight+1) for _ in range(len(val))]

    for w in range(wt[0], max_weight+1):
        dp[0][w] = val[0]

    for ind in range(1, n):
        for w in range(1, max_weight+1):
            take = 0
            if wt[ind] <= w:
                take = val[ind] + dp[ind-1][w-wt[ind]]
            not_take = dp[ind-1][w]

            dp[ind][w] = max(take, not_take)

    return dp[-1][-1]
```

### Space Optimization

```bash
We knoe the look up table is only
the prev row. 

So convert dp = 1D array and create 
a new 1D array each time for the
second loop and replace it

TC: O(n^2)
SC: O(n)
```
