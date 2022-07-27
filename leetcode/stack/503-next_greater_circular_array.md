## 503. Next Greater Element II

Find next greater eleemnt in a circular array.

Example:
```
Input: nums = [1,2,3,4,3]
Output: [2,3,4,-1,4]
```
### Algorithm
```
Add the arr to itself, since we need,
to traverse back.

Use next larger algo.
```
```
TC ~> O(2n) 
SC ~> O(2n) 
```

### Solution
```python
def nextGreaterElements(self, nums):
    arr = nums + nums
    stack = []
    
    res = [None]*len(arr)
    
    for i in range(len(arr)-1, -1, -1):
        while stack and stack[-1] <= arr[i]:
            stack.pop()
        if not stack:
            stack.append(arr[i])
            res[i] = -1
            continue
        res[i] = stack[-1]
        stack.append(arr[i])
            
    return res[:len(nums)]
```
