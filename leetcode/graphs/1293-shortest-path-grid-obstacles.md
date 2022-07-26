## 1293. Shortest path in a grid with obstacles elimination

[1293. Leetcode](https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/)

**Given:**
A grid of size m * n with each cell with 0 (empty) or 1 (obstacle)
and k = max number of obstacles that can be removed.

**Objective:**
Find min number off steps to reach from (0, 0) to (m-1, n-1).

```python
Constraints:

m == grid.length
n == grid[i].length
1 <= m, n <= 40
1 <= k <= m * n
grid[i][j] is either 0 or 1.
grid[0][0] == grid[m - 1][n - 1] == 0
```

### Algorithm

```
We can do DFS or BFS. But we choose BFS as with BFS we wont have to go back and
then visit again. Also, we can store the visited values as 
(row_ind, col_ind, remaining_k) and never go back to this condition.

Step 1. Corner Cases. if k is greater than n - 1 + m - 1 means we can simply 
        traverse the edges return n - 1 + m - 1
        If only one cell is there means return 0

Step 2. We have 4 paths and on each path we have two conditions i.e. obstacle or
        non-obstacle.
        1. If obstacle remove only if k > 0
        2. if not obstacle. check:
           if we reached end return steps + 1
           else: traverse
```
```python
TC: O(mnk) ~> We have to check each m, n for each k
SC: O(mnk) ~> Size of visited and queue
```


### Solution

```python
class Solution:
    def shortestPath(self, grid: List[List[int]], k: int) -> int:
        m, n = len(grid), len(grid[0])
        
        if m == 1 and n == 1:
            return 0
        
        if k > m - 1 + n - 1:
            return m - 1 + n - 1
        
        def is_valid(i, j):
            return 0 <= i < m and 0 <= j < n
        
        queue = deque([(0, 0, k, 0)])
        visited = set([(0, 0, k)])
            
        while queue:
            i, j, elim, steps = queue.popleft()
            
            for x, y in [(i+1, j), (i-1, j), (i, j+1), (i, j-1)]:
                if is_valid(x, y):
                    if grid[x][y] == 1 and elim > 0 and (x, y, elim-1) not in visited:
                        visited.add((x, y, elim-1))
                        queue.append((x, y, elim-1, steps+1))
                    if grid[x][y] == 0 and (x, y, elim) not in visited:
                        if x == m-1 and y == n-1:
                            return steps + 1
                        visited.add((x, y, elim))
                        queue.append((x, y, elim, steps+1))
    
        return -1
```