## 493. Reverse Pairs

Given an integer array nums, return the number of reverse pairs in the array.
A reverse pair is a pair (i, j) where 0 <= i < j < nums.length and nums[i] > 2 * nums[j].

### Merge Sort Algorithm:
```bash
If at any point arr[i] <= 2*arr[j],
we add 1  to the answer as this pair
has a contribution to the answer.

every part will be sorted,
so we start i = 0 for left side
and j = 0 for right side

lets take
12 19 25 40 and 2 6 9
initial i = 0 and j = 0

for each i we increment j 
till arr[i] > 2*arr[j]

and once the codintion fails we
add the j current value to res

i at 12, j at 2
we incremnt j by 1
add 1 to res

now i at 19 we incremnt j and reach
j at end i.e. for every number at i
we have to add current j val to res
```
```bash
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