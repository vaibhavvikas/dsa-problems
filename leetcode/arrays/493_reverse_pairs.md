## 493. Reverse Pairs

Given an integer array nums, return the number of reverse pairs in the array.
A reverse pair is a pair (i, j) where 0 <= i < j < nums.length and nums[i] > 2 * nums[j].

### Merge Sort Algorithm:
```
If at any point arr[i] <= 2*arr[j],
we add 1  to the answer as this pair
has a contribution to the answer.

TC: O(nlogn) + O(n) + O(n)
SC: O(n)
```

### Solution
```python
def reversePairs(nums):
    def merge_sort(arr, temp_arr, left, right):
        pairs = 0
        
        if left < right:
            mid = (left + right)//2
            pairs += merge_sort(arr, temp_arr, left, mid)
            pairs += merge_sort(arr, temp_arr, mid + 1, right)
            pairs += merge(arr, temp_arr, left, mid, right)
        return pairs
    
    def merge(arr, temp_arr, left, mid, right):
        j = mid + 1
        pairs = 0
        
        for i in range(left, mid + 1):
            while j <= right and arr[i] > 2 * arr[j]:
                j += 1
            pairs += j - (mid + 1)
        
        i, j, k = left, mid + 1, left
        
        while i <= mid and j <= right:
            if arr[i] < arr[j]:
                temp_arr[k] = arr[i]
                i += 1
                k += 1
            else:
                temp_arr[k] = arr[j]
                j += 1
                k += 1
        
        while i <= mid:
            temp_arr[k] = arr[i]
            i += 1
            k += 1
        
        while j <= right:
            temp_arr[k] = arr[j]
            j += 1
            k += 1
            
        for i in range(left, right+1):
            arr[i] = temp_arr[i]
            
        return pairs
    
    temp_arr = [0]*len(nums)
    pairs = merge_sort(nums, temp_arr, 0, len(nums)-1)
    return pairs
```