## 120. Buy And Sell Stock 2

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