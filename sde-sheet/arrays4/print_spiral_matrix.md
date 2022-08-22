## Print Spiral Matrix:

```bash
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

### Solution
```python
def spiralOrder(self, matrix, m, n):
    top, bottom, right, left = 0, m-1, n-1, 0
    
    res = []
    
    while top <= bottom and left <= right:
        for i in range(left, right+1):
            res.append(matrix[top][i])
            
        top += 1
        
        for i in range(top, bottom+1):
            res.append(matrix[i][right])
            
        right -= 1
        
        if top <= bottom:
            for i in range(right, left-1, -1):
                res.append(matrix[bottom][i])
        
        bottom -= 1
        
        if left <= right:
            for i in range(bottom, top-1, -1):
                res.append(matrix[i][left])
            
        left += 1
        
    return res
```
