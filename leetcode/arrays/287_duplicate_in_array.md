## 287. Duplicate in Array

## Cycle Detection Algo
```
TC: O(n)
SC: O(1)
```
```python
def findDuplicate(nums):
    slow, fast = nums[0], nums[0]
    
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        
        if slow == fast:
            break
            
    fast = nums[0]
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]
        
    return slow
```

### Using array as hash
```
TC: O(n)
SC: O(1)
```
```python
def findDuplicate(nums):
    while nums[0] != nums[nums[0]]:
        nums[nums[0]], nums[0] = nums[0], nums[nums[0]]
    return nums[0]
```
d