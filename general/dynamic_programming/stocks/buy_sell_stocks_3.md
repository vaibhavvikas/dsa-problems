## Buy and Sell Stocks with max k transactions


```
TC: O(n*2*k)
SC: O(n*2*k)
```
```python
def buy_sell(prices, n):
    dp = [[[-1]*(k+1) for _ in range(2)] for i in range(n)]

    def max_profit(ind, buy, k):
        if ind == n or k == 0:
            return 0

        if dp[ind][buy][k] != -1:
            return dp[ind][buy][k]

        if buy:
            do_nothing = max_profit(ind + 1, buy, k)
            buy_stock = -prices[ind] + max_profit(ind + 1, 0, k)
            profit = max(do_nothing, buy_stock)

        else:
            do_nothing = max_profit(ind + 1, buy, k)
            sell_stock = prices[ind] + max_profit(ind + 1, 1, k-1)
            profit = max(do_nothing, sell_stock)

        dp[ind][buy][k] = profit
        return dp[ind][buy][k]

    return max_profit(0, 1, k)
```
