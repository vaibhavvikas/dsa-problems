## Find repeating and missing element from array

### Maths
```
TC: O(n)
SC: O(1)
```
### Solution
```python
def find(nums):
    n = len(nums)

    sn = (n * (n + 1)) // 2
    pn = (n * (n + 1) * (2*n + 1)) // 6

    for num in nums:
        sn -= num
        pn -= num**2

    missing_num = (sn + (pn // sn)) // 2
    repeating_num = missing_num - sn
    
    return missing_num, repeating_num
```