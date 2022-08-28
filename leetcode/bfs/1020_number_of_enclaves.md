## 1020. Number of enclaves

You are given an m x n binary matrix grid, where 0 represents a sea cell and 1 represents a land cell.
A move consists of walking from one land cell to another adjacent (4-directionally) land cell or walking off the boundary of the grid.
Return the number of land cells in grid for which we cannot walk off the boundary of the grid in any number of moves.

```python
def numEnclaves(grid):  
    n, m = len(grid), len(grid[0])
    dirs = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    q = deque()
    count = 0
    for i in range(n):
        for j in range(m):
            if grid[i][j]:
                if i in (0, n - 1) or j in (0, m - 1):
                    q.append((i, j))
                    grid[i][j] = 0
                count += 1
    while q:
        i, j = q.popleft()
        count -= 1
        for di, dj in dirs:
            if 0 <= i + di < n and 0 <= j + dj < m and grid[i + di][j + dj]:
                grid[i + di][j + dj] = 0
                q.append((i + di, j + dj))
    return count
```