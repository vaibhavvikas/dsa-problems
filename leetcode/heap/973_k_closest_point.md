## 973. K Closest Point

Given a set of points and k, find k points which are closest to origin.

### Algorithm

```bash
We maintain a max heap of size k
with the distance as the calcualtion
factor
```
```
TC: O(nlogk) 
SC: O(k)
```

### Solution
```python
def k_closest(points, k):
    heap = []
    
    for x, y in points:
        # - sign for max heap
        dist = -(x**2 + y**2)
        if len(heap) == k:
            heapq.heappushpop(heap, (dist, x, y))
        else:
            heapq.heappush(heap, (dist, x, y))

    return [(x, y) for (dist, x, y) in heap]
```
