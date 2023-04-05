### 2439. Minimize Maximum of Array

#### Intution
```
the best we can get is averaging the values at each index.
```

```python
def minimizeArrayValue(self, nums: List[int]) -> int:
    total_sum = 0
    res = 0

    for index in range(len(nums)):
        total_sum += nums[index]
        avg = math.ceil(total_sum / (index + 1))

        res = max(res, avg)

    return res
```