## Search in sorted 2D Matrix

**Problem Statement:** Given an m*n 2D matrix and an integer, write a program to find if the given integer exists in the matrix.

Given matrix has the following properties:
1. Integers in each row are sorted from left to right.
2. The first integer of each row is greater than the last integer of the previous row

### Binry Search
```bash
See 2D matrix as one long array
a 3x4 matrix will be read as:

0 1 2 3
4 5 6 7
8 9 10 11

lo = 0, hi = 11
apply binary search
```
```bash
TC: O(logn)
SC: O(1)
```

### Solution
```python
def find_num(num, matrix):
    m = len(matrix)
    n = len(matrix[0])

    lo, hi = 0, (m*n - 1)

    while lo <= hi:
        mid = lo + (hi - lo)//2
        if matrix[mid//n][min%n] == num:
            return True
        elif matrix[mid//n][min%n] < num:
            lo = mid + 1
        else:
            hi = mid - 1

    return False
```