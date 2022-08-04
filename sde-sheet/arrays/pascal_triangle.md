## Pascal's Triangle

**Problem Statement:** Given an integer N, return the first N rows of Pascal’s triangle.

```bash
Input: N = 5

Output:
    1
   1 1
  1 2 1
 1 3 3 1
1 4 6 4 1
```

### Algorithm
```python
TC: O(n^2)
SC: O(n^2)
```

### Solution
```python
def pascal_triangle(n):
    if n < 1:
        return []

    res = [[1]]

    for i in range(1, n):
        temp = [-1]*(i+1)
        temp[0] = temp[i] = 1

        for j in range(1, i):
            temp[j] = res[i-1][j-1] + res[i-1][j]

        res.append(temp)

    return res
```
