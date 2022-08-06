## Longest Subarray with Zero Sum

### Prefis Sum Approach 
```bash
We start from first element
and add it into the arr with its index

Two cases comes:
Case 1:
if prefix_sum = 0 that means sum from
index 0 to curr_index is 0 so max_len
is index + 1

Case 2:
We check if prefix_sum is already present
that means sum of elements from that index
to curr_ind is zero so we take that len

In any case we add the the prefix_sum
in the dict with their index
```
```bash
TC: O(n)
SC: O(n)
```
### Solutions
```python
def max_len(nums):
    curr_sum = 0
    pref_sum = {}
    max_len = 0

    for i in range(len(nums)):
        curr_sum += nums[i]

        if curr_sum == 0:
            max_len = i + 1

        else:
            if curr_sum in pref_sum:
                max_len = max(max_len, i - pref_sum[curr_sum])
            else:
                pref_sum[curr_sum] = i

    return max_len
```