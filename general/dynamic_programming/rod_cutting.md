## Rod Cutting Problem

Given a rod of length "N", that can be cut into different sizes.
Cut the rod in such a way so that it gives the max value

```bash
Example:
Input: N= 5, val = [2 5 7 8 10]
Output: 12
```

### Recursion

#### Algorithm
```bash
Base Cases:

At any index:
the rod length is ind + 1

at index == 0, rod_length == 1

Therefore,
we have two options

take only if the ind + 1 <= rem_len
than we can: 
```
```bash
TC: (2^n) ~> Exponential 
SC: O(n) ~> Stack Space
```

#### Solution
```python
def cut_rod(target, price):

    def recurse(ind, rem_len):
        if ind == 0:
            return rem_len * price[ind]

        take = 0
        if ind < rem_len:
            take = price[ind] + recurse(ind, rem_len - ind - 1)
        
        not_take = recurse(ind - 1, rem_len)
        return max(take, not_take)

    return recurse(target, target)
```


### Recursion + Memoization
```bash
TC: (n^2) 
SC: O(n^2) + O(n) ~> Stack Space
```

#### Solution
```python
def cut_rod(target, price):
    dp = [[-1]*(target+1) for _ in range(target+1)]

    def recurse(ind, rem_len):
        if ind == 0:
            dp[ind][rem_len] = rem_len * price[ind]
            return dp[ind][rem_len]

        if dp[ind][rem_len] != -1:
            return dp[ind][rem_len]

        take = 0
        if ind < rem_len:
            take = price[ind] + recurse(ind, rem_len - ind - 1)
        
        not_take = recurse(ind - 1, rem_len)
        dp[ind][rem_len] = max(take, not_take)
        return dp[ind][rem_len]

    recurse(target, target)
    return dp[-1][-1]
```


### Tabulation
```bash
TC: (n^2) 
SC: O(n^2)
```

#### Solution
```python
def cut_rod(target, price):
    dp = [[0]*(target+1) for _ in range(target+1)]

    for i in range(target+1):
        dp[0][i] = i * price[0]

    for ind in range(1, target+1):
        for rod_len in range(1, target+1):
            take = 0
            if ind < rod_len:
                take = price[ind] + dp[ind][rod_len - ind - 1]

            not_take = dp[ind-1][rod_len]
            dp[ind][rod_len] = max(take, not_take)

    return dp[-1][-1]
```
