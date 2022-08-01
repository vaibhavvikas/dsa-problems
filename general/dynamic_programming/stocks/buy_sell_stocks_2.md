## 122. Buy And Sell Stock 2

### Peak - Valley Approach

```
We use peak value approach 
to solve this question.
```
```
TC: O(n)
SC: O(1)
```

### Solution

```python
def maxProfit(prices: List[int]) -> int:
    res = 0
    for i in range(1, len(prices)):
        res += max(prices[i]-prices[i-1], 0)
    return res
```

```python
def maxProfit(prices: List[int]):
    valley = prices[0]
    peak = prices[0]

    i, max_profit = 0, 0

    while i < len(prices) - 1:
        while i < len(prices) - 1 and prices[i] >= prices[i+1]:
            i += 1
        valley = prices[i]
        
        while i < len(prices) - 1 and prices[i] <= prices[i+1]:
            i += 1
        peak = prices[i]
        max_profit += peak - valley
        
    return max_profit
```

### Dynamic Programming
```
Recursion
TC: O(2^n)
SC: O(n) Stack Space
```
#### Solution

```python
def buy_sell(prices):
    def get_profit(ind, buy):
        if ind == n:
            return 0

        if buy:
            do_nothing = get_profit(ind - 1, buy)
            buy_stock = -prices[ind] + get_profit(ind - 1, not buy)
            profit = max(do_nothing, buy_stock)
        
        else:
            do_nothing = get_profit(ind - 1, buy)
            sell_stock = prices[ind] + get_profit(ind - 1, not buy)
            profit = max(do_nothing, sell_stock)

        return profit

    return get_profit(0, True)
```

### DP + Memoization
```
TC: O(2*n)
SC: O(2*n) + O(n) ~> Recusion Stack
```
```python
def buy_sell(prices):
    dp = [[-1, -1] for _ in range(len(prices))]

    def get_profit(ind, buy):
        if ind == len(prices):
            return 0

        if dp[ind][buy] != -1:
            return dp[ind][buy]

        if buy:
            do_nothing = get_profit(ind + 1, buy)
            buy_stock = -prices[ind] + get_profit(ind + 1, 0)
            profit = max(do_nothing, buy_stock)

        else:
            do_nothing = get_profit(ind + 1, buy)
            sell_stock = prices[ind] + get_profit(ind + 1, 1)
            profit = max(do_nothing, sell_stock)

        dp[ind][buy] = profit
        return dp[ind][buy]

    return get_profit(0, 1)
```

### Tabulation
```
TC: O(2*n)
SC: O(2*n) ~> Optimize to O(1)
```

```python

def buy_sell(prices):
    n = len(prices)
    dp = [[-1, -1] for _ in range(n+1)]
    dp[n][0] = dp[n][1] = 0

    for ind in range(n-1, -1, -1):
        for buy in range(2):
            if buy:
                do_nothing = dp[ind + 1][buy]
                buy_stock = -prices[ind] + dp[ind + 1][0]
                dp[ind][buy] = max(do_nothing, buy_stock)

            else:
                do_nothing = dp[ind + 1][buy]
                sell_stock = prices[ind] + dp[ind + 1][1]
                dp[ind][buy] = max(do_nothing, sell_stock)
    
    return dp[0][1] # In the starting buy should be 1
```
