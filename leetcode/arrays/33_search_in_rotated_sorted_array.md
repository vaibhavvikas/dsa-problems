## 33. Search in rotated sorted array

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(logn) runtime complexity.

### Binary Search
```
We can perform a Binary Search.
If A[mid] is bigger than A[left]
we know the inflection point will be to the
right of us, meaning values from
a[left]...a[mid] are ascending.

So if target is between that range we just
cut our search space to the left.
Otherwise go right.

The other condition is that A[mid] is not
bigger than A[left] meaning a[mid]...a[right]
is ascending.

In the same manner we can check if target is
in that range and cut the search space
correspondingly.
```
```
TC: O(logn)
SC: O(1)
```

### Solution
```python
def search(nums, target):
    low, high = 0, len(nums)-1

    while low <= high:
        mid = low + (high - low) // 2
        if nums[mid] == target:
            return mid

        # inflection point to the right. Left is strictly increasing
        if nums[mid] >= nums[low]:
            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1
        
        # inflection point to the left. right is strictly increasing
        else:
            if nums[mid] <= target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1

    return -1
```
