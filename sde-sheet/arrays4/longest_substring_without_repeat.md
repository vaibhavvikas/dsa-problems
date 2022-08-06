## Length of Longest Substring without any Repeating Character


### Sliding Window Technique
```
if string[j] is in array.
that means we need remove
element from index i till j
unless we dont find the element
at index j inside set

then we add the curr element and 
update max len
```
```
TC: O(n)
SC: O(n)
```

### Solution
```python
def long_subs(string):
    if not string:
        return 0

    i, max_len = 0, 1
    n = len(string)
    curr_set = set([string[0]])

    for j in range(n):
        if string[j] in curr_set:
            while i < j and string[j] in curr_set:
                curr_set.remove(string[i])
                i += 1

        curr_set.add(string[j])
        max_len = max(max_len, len(curr_set))

    return max_len
```
