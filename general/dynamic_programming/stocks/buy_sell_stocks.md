## Buy and Sell Stock I

Given a list of stock prices on different days.
Find the best possible profit you can get if you can buy and sell stock only once.

```bash
Example:
input: [7, 1, 5, 3, 6, 4]
output: 5
```

### Algorithm
```bash
On each step we check 
the min so far and
calculate the maxprofit
```
```bash
TC: O(n)
SC: O(1)
```

### Solution

```python
def buy_sell(prices):
    max_profit, min_price = 0, math.inf

    for price in prices:
        min_price = min(min_price, price)
        max_profit = max(max_profit, price - min_price)

    return max_profit
```
