## Rotate Matrix

Rotate the given square matrix by 90 degrees

## Algorithm

```bash
Find transpose of the matrix
reverse each row
```
```
TC: O(n^2) + O(n^2)
SC: O(1)
```

## Solution
```python
def rotate_matrix(matrix):

    for i in range(len(matrix)):
        for j in range(len(matrix)):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

    for i in range(len(matrix)):
        matrix[i] = matrix[i][::-1]

    return matrix
```
