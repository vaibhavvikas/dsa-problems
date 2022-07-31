## Add two numbers using Bitwise Operators

### Algorithm

```bash
Half Adder Logic
A B C D
0 0 0 0
1 0 0 1
0 1 0 1
1 1 1 0
```
```bash
TC: O(logn)
SC: O(logn) ~> Recursion Stack
```

### Solution
```python
def add(x, y):
    keep = (x & y) << 1
    res = x^y
  
    # If bitwise & is 0, then there
    # is not going to be any carry.
    # Hence result of XOR is addition.
    if (keep == 0):
        return res
  
    return add(keep, res)

# Driver code
print(add(15, 38))
```
