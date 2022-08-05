## 4. Median of two sorted arrays

Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays.

### Brute Force
```
TC: O(m+n)
SC: O(m+n)
```

### Solution
```python
def findMedian(nums1, nums2):
    merged_arr = [0]*(len(nums1) + len(nums2))
    i, j, k = 0, 0, 0

    while i < len(nums1) and j < len(nums2):
        if nums1[i] <= nums2[j]:
            merged_arr[k] = nums1[i]
            i += 1
            k += 1
        else:
            merged_arr[k] = nums2[j]
            j += 1
            k += 1

    while i < len(nums1):
        merged_arr[k] = nums1[i]
        i += 1
        k += 1

    while j < len(nums2):
        merged_arr[k] = nums2[j]
        j += 1
        k += 1
    
    print(merged_arr)
    
    if len(merged_arr)%2 == 0:
        return (merged_arr[len(merged_arr)//2] + merged_arr[len(merged_arr)//2 - 1]) / 2

    return merged_arr[len(merged_arr)//2]
```

### Binary Search Approach
```
TC: O(log(m+n))
SC: O(1)
```

### Solution
```python
def findMedianSortedArrays(self, nums1, nums2):
    n1, n2 = len(nums1), len(nums2)
    
    if n2 < n1:
        return self.findMedianSortedArrays(nums2, nums1)
    
    partition = (n1 + n2 + 1)//2
    
    low, hi = 0, n1
    
    while low <= hi:
        cut1 = (low + hi) // 2
        cut2 = partition - cut1
        
        l1, l2, r1, r2 = -math.inf, -math.inf, math.inf, math.inf
        
        if cut1 != 0: l1 = nums1[cut1-1]
        if cut2 != 0: l2 = nums2[cut2-1]
        
        if cut1 != n1: r1 = nums1[cut1]
        if cut2 != n2: r2 = nums2[cut2]
        
        if l1 <= r2 and l2 <= r1:
            if (n1 + n2) % 2 == 0:
                return (max(l1, l2) + min(r1, r2)) / 2
            return max(l1, l2)
        
        if l1 > r2:
            hi = cut1 - 1
        else:
            low = cut1 + 1
            
    return 0
```