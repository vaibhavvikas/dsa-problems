## Count Inversions

Count number of inversions in an array to make it sorted.

### Brute Force
```
TC: O(n**2)
SC: O(1)
```
### Solution
```python
def getInvCount(arr, n):
    inv_count = 0
    for i in range(n):
        for j in range(i + 1, n):
            if (arr[i] > arr[j]):
                inv_count += 1

    return inv_count
```


### Modified Merge Sort
```bash
Modified MergeSort Function:
If arr[i] <= arr[j] No inversion
else: 
    inv_count += mid - i + 1
```
```bash
TC: O(nlogn) ~> Divide and Conquer n levels
SC: O(n) ~> Temp Arr
```


### Solution
```python
def mergeSort(arr, n):
    temp_arr = [0]*n
    return _mergeSort(arr, temp_arr, 0, n-1)
  

def _mergeSort(arr, temp_arr, left, right):
    inv_count = 0

    if left < right:
        mid = (left + right)//2

        inv_count += _mergeSort(arr, temp_arr,
                                left, mid)

        inv_count += _mergeSort(arr, temp_arr,
                                mid + 1, right)
  
        inv_count += merge(arr, temp_arr, left, mid, right)

    return inv_count


def merge(arr, temp_arr, left, mid, right):
    i = left     # Starting index of left subarray
    j = mid + 1  # Starting index of right subarray
    k = left     # Starting index of to be sorted subarray
    inv_count = 0

    while i <= mid and j <= right:

        if arr[i] <= arr[j]:
            temp_arr[k] = arr[i]
            k += 1
            i += 1
        else:
            # Inversion will occur.
            temp_arr[k] = arr[j]
            inv_count += (mid-i + 1)
            k += 1
            j += 1

    while i <= mid:
        temp_arr[k] = arr[i]
        k += 1
        i += 1

    while j <= right:
        temp_arr[k] = arr[j]
        k += 1
        j += 1

    for k in range(left, right + 1):
        arr[k] = temp_arr[k]

    return inv_count


arr = [1, 20, 6, 4, 5]
n = len(arr)
result = mergeSort(arr, n)
print("Number of inversions are", result)
```