## 60. Kth Permutation

The set [1, 2, 3, ..., n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for n = 3:
1:"123" 2:"132" 3:"213" 4:"231" 5:"312" 6:"321"
Given n and k, return the kth permutation sequence.


### Brute Force: Generate All Permutations
```
TC: O(n!*n) + O(n!logn!)
SC: O(n!) ~> res array
```

### Solution
```python
def kth_permutation(n, k):
    arr = [str(i+1) for i in range(n)]
    res = []

    def recurse(ind):
        if ind == n:
            res.append(''.join(arr))
            return

        for i in range(ind, n):
            arr[i], arr[ind] = arr[ind], arr[i]
            recurse(ind+1)
            arr[i], arr[ind] = arr[ind], arr[i]

    recurse(0)
    return sorted(res)[k]

print(next_permutation(6))
```

### Optimized
```bash
lets say n = 4, k = 17
arr = [1, 2, 3, 4]

We know we can have total of
4! = 24 permutations
which implies => 3! with each
element 1, 2, 3, and 4

We use this to get our permutation
we reduce k by 1 as we are using 0
based indexing

Dividing k by 3! we get 2 i.e we
need to choose index 2 as first
element

res = "3"
arr = [1, 2, 4]
k = 16 % 6 = 4
fact = 2

Now we choose 4//2 = 2
res = "34"
arr = [1, 2]
k = 4%2 = 0
fact = 1

and so one

we get "3412" as the 17th perm
```

```bash
TC: O(n*n)
SC: O(n)
```

### Solution
```python
def getPermutation(n, k):
    arr = [str(i+1) for i in range(n)]
    fact = math.factorial(n-1)
    k -= 1
    res = ""
    
    while True:
        res += arr[k//fact]
        del arr[k//fact]
        
        if not arr:
            return res
        
        k %= fact
        fact //= len(arr)
```
