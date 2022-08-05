## Find Min cost to combine n gold bars

```python
def min_min_sum(weights):
    cost = 0
    heapq.heapify(weights)

    while len(weights) > 1:
        a = heapq.heappop(weights)
        b = heapq.heappop(weights)
        cost += a + b
        heapq.heappush(weights, a + b)
    
    return cost
```