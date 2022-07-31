## Coin Change

Given a list of coins,
Find the min number of coins required to reach a target value

```bash
Input:
target = 22
coins = [1 3 4 5]

Output:
5
```

### Recursion Bottom Up

#### Algorithm
```
Taking the Knapsack
we extend it to unbounded knapsack
```
```bash
TC: O(2^n)
SC: O(n) Stack Space 
```

#### Solution
```python
def min_coins(target, coins):

    def recurse(ind, val):
        if ind == 0:
            if val % coins[ind] == 0:
                return val//coins[ind]
            return math.inf

        take = math.inf
        if coins[ind] <= val:
            take = 1 + recurse(ind, val - coins[ind])
        not_take = recurse(ind - 1, val)

        return min(take, not_take)

    return recurse(len(coins)-1, target)
```

### Recursion + Memoization

```bash
TC: O(n^2)
SC: O(n^2) + O(n)
```

#### Solution
```python
def min_coins(target, coins):

    dp = [[-1]*(target+1) for _ in range(len(coins))]

    def recurse(ind, val):
        if ind == 0:
            if val % coins[ind] == 0:
                return val//coins[ind]
            return math.inf

        if dp[ind][val] != -1:
            return dp[ind][val]

        take = math.inf
        if coins[ind] <= val:
            take = 1 + recurse(ind, val - coins[ind])
        not_take = recurse(ind - 1, val)

        dp[ind][val] = min(take, not_take)
        return dp[ind][val]

    return dp[-1][-1] if dp[-1][-1] != math.inf else -1
```

### Tabulation

```bash
TC: O(n^2)
SC: O(n^2)
```

#### Solution
```python
def min_coins(target, coins):
    dp = [[0]*(target+1) for _ in range(len(coins))]

    for val in range(0, target + 1):
        dp[0][val] = val // coins[0] if val % coins[0] == 0 else math.inf

    for ind in range(1, len(coins)):
        for val in range(1, target+1):
            take = math.inf

            if coins[ind] <= val:
                take = 1 + dp[ind][val - coins[ind]]
            
            not_take = dp[ind - 1][val]
            dp[ind][val] = min(take, not_take)

    return dp[-1][-1] if dp[-1][-1] != 0 else -1
```
