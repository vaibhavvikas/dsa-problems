## Merge Two Sorted Arrays

### Without using Space
```
TC: O(m*n)
SC: O(1)
```
```python
def merge(arr1, arr2):
    m = len(arr1)
    n = len(arr2)

    for i in range(m):
        if arr1[i] > arr2[0]:
            arr1[i], arr2[0] = arr2[0], arr1[i]
            j = 0
            while j < n-1:
                if arr2[j] > arr2[j + 1]:
                    arr2[j], arr2[j+1] = arr2[j+1], arr2[j]
                    j += 1
                else:
                    break
```

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
