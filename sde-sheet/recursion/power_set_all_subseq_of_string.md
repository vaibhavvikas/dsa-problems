## Power Set

Print all the possible subsequences of the String

### Recursion + Backtracking
```bash
On each step we have two options
take or not take

Once we reach the enf of index,
we append the curr_string to res
and break the recursion
```
```bash
TC: O(2^n)
SC: O(n) ~> Recursion stack
```

### Solution
```python
def all_substrings(s):
    res, n = [], len(s)

    def recurse(ind, curr_str):
        if ind == n:
            res.append(curr_str)
            return

        recurse(ind+1, curr_str + s[ind])
        recurse(ind+1, curr_str)
    
    recurse(0, "")
    return sorted(res)
```
