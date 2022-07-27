## 200. Number of islands

Given an m x n grid which represents a map of '1' (land) and '0' (water), return the number of islands.

### Algorithm
```bash
Step 1. Traverse the graph, 
    if 1 found means island found
    res += 1

Step 2. Call DFS and change all the connected
    and mark it something else so
    that we dont touch those again
```
```bash
TC: O(rows*columns)
SC: O(1) ~> Changing the initial grid
```

### Solution

```python
def numIslands(grid: List[List[str]]) -> int:
    res = 0
    
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] != "1":
                continue
            else:
                res += 1
                dfs(i, j, grid)
    
    return res
                
    
def dfs(i, j, grid):
    if i < 0 or j < 0 or i == len(grid) or j == len(grid[0]):
        return
    
    if grid[i][j] == "1":
        grid[i][j] += "1"
        dfs(i+1, j, grid)
        dfs(i, j+1, grid)
        dfs(i-1, j, grid)
        dfs(i, j-1, grid)

    return
```