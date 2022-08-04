## Set Matrix Zeroes

**Problem Statement:** Given a matrix if an element in the matrix is 0 then you will have to set its entire column and row to 0 and then return the matrix.

### Algorithm
```
TC: O(m*n)
SC: O(m + n)
```

### Solution
```python
def set_matrix_zeroes(matrix):
    rows, cols = set(), set()

    for i in range(len(matrix)):
        for j in range(len(matrix[0])):
            if matrix[i][j] == 0:
                rows.add(i)
                cols.add(j)

    for i in range(len(matrix)):
        for j in range(len(matrix[0])):
            if i in rows or j in cols:
                matrix[i][j] = 0
```
