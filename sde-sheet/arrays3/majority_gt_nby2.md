## Majority Element that occurs more than N/2 times

**Problem Statement:** Given an array of N integers, write a program to return an element that occurs more than N/2 times in the given array. You may consider that such an element always exists in the array.

### Moore's Voting Algorithm
```bash
TC: O(n)
SC: O(1)
```

### Solution
```python
def majorityElement(nums):
    count = 0
    candidate = None

    for num in nums:
        if count == 0:
            candidate = num

        if num == candidate:
            count += 1
        else:
            count -= 1

    return candidate
```
