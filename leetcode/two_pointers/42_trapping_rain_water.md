## 42. Trapping Rain Water

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.


### Two Pointer Approach

```bash
1. Water units trapped in each index of the
   array is calculated and added individually.

2. Water level at an index is determined by
   the lower of max_left and max_right for any
   bar, i.e. essentially water trapped in bar i
   depends on min(max_left, right_left).

3. Water trapped in index
   i = min(max_left, max_right) - height[i].

4. Therefore if max_left < max_right, we fill the
   left index up to max_left, and advance the left
   pointer; and vice versa. If max_left equals
   max_right, moving either pointer would work.
```
```
TC: O(n)
SC: O(1)
```

**Solution:**
```python
def trap(self, height: List[int]) -> int:
    res, n = 0, len(height)
    
    i, j = 1, n-2
    lmax, rmax = height[0], height[-1]

    while i <= j:
        if height[i] > lmax:
            lmax = height[i]

        if height[j] > rmax:
            rmax = height[j]

        if lmax < rmax:
            res += lmax - height[i]
            i += 1

        else:
            res += rmax - height[j]
            j -= 1
        
    return res
```

### DP Approach


```bash
1. Water stored at any level is:
   max from left_max, right_max (excluding current)
   and then subtracting the height from min of both

2. We create left arr from 1 -> n with
   left[0] = height[0]
   Each element => max(left[i-1], height[i])

3. We crete right arr from n-2 -> 0 with
   right[n-1] = height[n-1]
   Each element => max(height[i], right[i+1])

4. For calculating water trapped, each will store
   min(left[i], right[i]) - height[i]
```
```bash
Example: 
height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
left =   [0, 1, 1, 2, 2, 2, 2, 3, 3, 3, 3, 3]
right =  [3, 3, 3, 3, 3, 3, 3, 3, 2, 2, 2, 1]
res =    [0, 0, 1, 0, 1, 2, 1, 0, 0, 1, 0, 0]
```
```bash
    left  right   res
TC: O(n) + O(n) + O(n)
SC: O(n) + O(n) + O(n)
```

**Solution:**
```python
def trap(self, height: List[int]) -> int:
    res, n = 0, len(height)
    left, right = [0]*n, [0]*n
    
    left[0] = height[0]
    
    for i in range(1, n):
        left[i] = max(left[i-1], height[i])
        
    right[-1] = height[-1]
    
    for i in range(1, n):
        right[~i] = max(right[~i + 1], height[~i])
        
    res = sum([min(left[i], right[i]) \
        - height[i] for i in range(n)])
    
    return res
```