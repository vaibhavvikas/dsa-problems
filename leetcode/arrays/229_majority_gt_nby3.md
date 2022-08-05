## 229. Majority Element II

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

```bash
TC: O(n) + O(n)
SC: O(1)
```

```python
def majorityElement(nums: List[int]):
    candidate1, candidate2 = None, None
    count1, count2 = 0, 0

    for num in nums:
        if candidate1 == num:
            count1 += 1
        elif candidate2 == num:
            count2 += 1
        elif count1 == 0:
            candidate1 = num
            count1 = 1
        elif count2 == 0:
            candidate2 = num
            count2 = 1
        else:
            count1 -= 1
            count2 -= 1

    return [n for n in (candidate1, candidate2) \
            if nums.count(n) > len(nums)//3]
```
