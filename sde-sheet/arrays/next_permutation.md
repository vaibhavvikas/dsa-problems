## Next Permutation

**Problem Statement:** Given an array Arr[] of integers, rearrange the numbers of the given array into the lexicographically next greater permutation of numbers. If such an arrangement is not possible, it must rearrange it as the lowest possible order (i.e., sorted in ascending order).

```bash
Example:
Input: [1, 9, 5, 6, 3, 2, 1]
Output: [1, 9, 6, 1, 2, 3, 5]
```

### Algorithm
```bash
1 9 5 6 3 2 1

We start from end and traverse till
we get the increasing pair
i from n - 2
we reach i = 2 (i.e. number 5)

then we find the the nummber just
greater than the current number and
swap them
we find j = 3, (number 6) and swap
we get: 1 9 6 5 3 2 1

And reverse all the numbers after that
index
1 9 6 5 + reverse(3 2 1)
1 9 6 5 1 2 3 

```
```bash
TC: O(n) + O(n) + O(n)
SC: O(1)
```

### Solution
```python
def next_permutation(arr):
    i = len(arr) - 2

    while i >= 0 and arr[i] > arr[i+1]:
        i -= 1

    if i < 0:
        return arr[::-1]

    j = len(arr) - 1

    while j > i:
        print(i, j)
        if arr[j] > arr[i]:
            arr[i], arr[j] = arr[j], arr[i]
            break
        j -= 1

    return arr[:i+1] + arr[:i:-1] # reversed(arr[i+1:])
```
