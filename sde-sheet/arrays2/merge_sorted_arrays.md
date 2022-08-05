## Merge Two Sorted Arrays

### Gap Method
```bash
TC: O(nlogn)
SC: O(1)
```
### Solution
```python
def merge(arr1, arr2):
    m = len(arr1)
    n = len(arr2)

    gap = math.ceil((m + n)/2)

    while gap >= 1:
        i = 0
        j = gap

        while j < (n + m):
            if j < m and arr1[i] > arr1[j]:
                arr1[i], arr1[j] = arr1[j], arr1[i]
            elif i < m and j >= m and arr1[i] > arr2[j-m]:
                arr1[i], arr2[j-m] = arr2[j-m], arr1[i]
            elif i >= m and j >= m and arr2[i-m] > arr2[j-m]:
                arr2[i-m], arr2[j-m] = arr2[j-m], arr2[i-m]
            i += 1
            j += 1

        if gap == 1:
            gap = 0
        else:
            gap = math.ceil(gap/2)
```
