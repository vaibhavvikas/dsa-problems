## Rat in a Maze

Consider a rat placed at (0, 0) in a square matrix of order N * N. It has to reach the destination at (N - 1, N - 1). Find all possible paths that the rat can take to reach from source to destination. The directions in which the rat can move are 'U'(up), 'D'(down), 'L' (left), 'R' (right). Value 0 at a cell in the matrix represents that it is blocked and rat cannot move to it while value 1 at a cell in the matrix represents that rat can be travel through it.

```bash
Example:
N = 4
m[][] = {{1, 0, 0, 0},
         {1, 1, 0, 1}, 
         {1, 1, 0, 0},
         {0, 1, 1, 1}}
Output:
DDRDRR DRDDRR
```

### Algorithm
```
TC: O(4^(m*n))
SC: O(m*n)
```

### Solution
```python
def findPath(self, m, n):
    res = []
    visited = set()
    
    def dfs(i, j, curr_path):
        if i < 0 or i >=n or j < 0 or j >= n or \
            m[i][j] == 0 or (i, j) in visited:
            return
        
        if i == n-1 and j == n-1:
            res.append(curr_path)
            return
        
        visited.add((i, j))
        
        dfs(i, j-1, curr_path + "L")
        dfs(i, j+1, curr_path + "R")
        dfs(i+1, j, curr_path + "D")
        dfs(i-1, j, curr_path + "U")
        
        visited.remove((i,j))

    dfs(0, 0, "")
    return res
```