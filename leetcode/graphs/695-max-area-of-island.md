## 695. Max area of island

Given an m x n grid which represents a map of '1' (land) and '0' (water).
The area of an island is the number of cells with a value 1 in the island.

### Algrithm
```bash
Follow up for Number of Islands

Start same but in DFS return number
of points changed from 1 to something else

Fianlly return max value formed 
```
```bash
TC: O(rows*columns)
SC: O(1) ~> Changing the initial grid
```


```python
def maxAreaOfIsland(self, grid) -> int:
    res = 0

    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == 1:
                res = max(res, dfs(i, j, grid))
                
    return res


def dfs(i, j, grid):
    if i < 0 or i >= len(grid) \
        or j < 0 or j >= len(grid[0]):
        return 0

    if grid[i][j] != 1:
        return 0
    
    grid[i][j] += 1
    
    return 1 + dfs(i, j-1, grid) \
        + dfs(i, j+1, grid) \
        + dfs(i+1, j, grid) \
        + dfs(i-1, j, grid)
```