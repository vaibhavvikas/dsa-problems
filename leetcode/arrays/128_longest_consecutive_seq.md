## Longest Consecutive Seq in an Array

**Problem Statement:** You are given an array of ‘N’ integers. You need to find the length of the longest sequence which contains the consecutive elements.

```bash
Example:

Input: [100, 200, 1, 3, 2, 4]
Output: 4
Explanation: The longest consecutive
    subsequence is 1, 2, 3, and 4
```

### Set Approach
```
We use a set and all items in set
Now we run a loop through each items
of the arr. If the num - 1 is not there,
then we run a loop till num + 1 is not there
and count numbers
```
```python
TC: O(n) ~> We only traverse once
SC: O(n) ~> Set
```

### Solution
```python
def longestConsecutive(nums):
    nums_set = set(nums)
    res = 0

    for num in nums:
        if num - 1 not in nums_set:
            streak = 0
            while num in nums_set:
                num += 1
                streak += 1
            
            res = max(res, streak)

    return res
```
