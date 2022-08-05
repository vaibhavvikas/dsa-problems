## 295. Median of two data stream.

### Heap Approach
```bash
TC: AddNum: O(logn) + O(logn)
    findMedian: O(1)
SC: O(n)
```

### Solution
```python
class MedianFinder:
    def __init__(self):
        self.small = []
        self.large = []

    def addNum(self, num: int) -> None:
        heapq.heappush(self.small, -num)
        
        if self.small and self.large and\
            -self.small[0] > self.large[0]:
                element = -heapq.heappop(self.small)
                heapq.heappush(self.large, element)
        
        if len(self.small) > len(self.large) + 1:
            element = -heapq.heappop(self.small)
            heapq.heappush(self.large, element)
        
        if len(self.large) > len(self.small) + 1:
            element = heapq.heappop(self.large)
            heapq.heappush(self.small, -element)
                
    def findMedian(self) -> float:
        if len(self.small) > len(self.large):
            return -self.small[0]
        if len(self.large) > len(self.small):
            return self.large[0]
        return (-self.small[0] + self.large[0]) / 2
```
