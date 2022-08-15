## 1631. Path With Minimum Effort

You are given heights, a 2D array of size rows x columns, where heights[row][col] represents the height of cell (row, col). You are situated in the top-left cell, (0, 0), and you hope to travel to the bottom-right cell.
A route's effort is the maximum absolute difference in heights between two consecutive cells of the route.

Return the minimum effort required to travel from the top-left cell to the bottom-right cell.

```bash
Example:

Input: 
heights = [[1, 2, 2],
           [3, 8, 2],
           [5, 3, 5]]
Output: 2
Path: 1, 3, 5, 3, 5
```

### Dijkstra Approach
```bash
We create a min heap to store the min effort
and traverse the grid based on the min effort

Once we reach the end thats what we wanted
```
```bash
TC: O(m*n)
SC: O(m*n)
```

### Solution
```python
def minimumEffortPath(heights):
    heap = [(0, 0, 0)]
    res = 0
    m, n = len(heights), len(heights[0])
    visited = set()
    
    while heap:
        d, x, y = heapq.heappop(heap)
        
        res = max(res, d)
        
        if (x, y) == (m-1, n-1):
            return res
        
        visited.add((x, y))
        
        for nx, ny in [(x-1, y), (x+1, y), (x, y-1), (x, y+1)]:
            if 0 <= nx < m and 0 <= ny < n and (nx, ny) not in visited:
                element = (abs(heights[x][y] - heights[nx][ny]), nx, ny)
                heapq.heappush(heap, element)
```
