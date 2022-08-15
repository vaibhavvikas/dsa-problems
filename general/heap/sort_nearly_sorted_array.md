## Sort a k - Array (Nearly Sorted Array)

Given an array of n elements, where each element is at most k away from its target position, devise an algorithm that sorts in O(n log k) time.

```bash
Example:

Input:
arr = {6, 5, 3, 2, 8, 10, 9}
k = 3 

Output:
arr = {2, 3, 5, 6, 8, 9, 10}
```

### Heap Approach

```bash
We take a heap of size k
Traverse the array and replace
the first element by the top
of heap and add the next element
inside the heap 
```
```bash
TC: O(nlogk)
SC: O(k)
```

### Solution
```python
from heapq import heapify, heappop, heappush

def nearly_sorted(arr, k):
    heap = arr[:k+1]
    heapify(heap)
    n = len(arr)

    print(heap)

    for i in range(n - k - 1):
        arr[i] = heappop(heap)
        heappush(heap, arr[i+k+1])
    
    for i in range(n-k-1, n):
        arr[i] = heappop(heap)
```