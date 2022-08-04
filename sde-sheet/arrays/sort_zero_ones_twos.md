## Sort Array of 0, 1 and 2

### Algorithm
```bash
Two Pointer Approach

TC: O(n)
SC: O(1)
```

### Solution
```python
def sort_zero_one_two(nums):
    i, j, k = 0, 0, len(nums) - 1

    while j <= k:
        if nums[j] == 1:
            j += 1
        
        elif nums[j] == 0:
            nums[i], nums[j] = nums[j], nums[i]
            i += 1
            j += 1

        else:
            nums[j], nums[k] = nums[k], nums[j]
            k -= 1

    return nums
```
