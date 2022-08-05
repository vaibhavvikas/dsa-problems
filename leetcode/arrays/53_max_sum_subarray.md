## 53. Max Sum Subarray

### Kadane's Algorithm
```bash
TC: O(n)
SC: O(1)
```

### Solution
```python
def maxSubArray(self, A):

    curSum = maxSum = A[0]
    for num in A[1:]:
        curSum = max(num, curSum + num)
        maxSum = max(maxSum, curSum)

    return maxSum
```