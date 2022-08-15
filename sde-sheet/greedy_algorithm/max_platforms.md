## Max number of Platforms

Given arrival and departure times of all trains that reach a railway station. Find the minimum number of platforms required for the railway station so that no train is kept waiting.

```bash
Example:

Input: n = 6 
arr = {0900, 0940, 0950, 1100, 1500, 1800}
dep = {0910, 1200, 1120, 1130, 1900, 2000}

Output: 3
```

### Approach
```
We sort both the arrays
if a train comes we increment
the count and if train leaves
we decrement the count
```

### Solution
```python
def minimumPlatform(n, arr, dep):
    arr.sort()
    dep.sort()
    
    i, j = 0, 0
    res, curr = 0, 0
    
    while i < n and j < n:
        if arr[i] <= dep[j]:
            curr += 1
            i += 1
        else:
            curr -= 1
            j += 1

        res = max(res, curr)
    
    return res
```
