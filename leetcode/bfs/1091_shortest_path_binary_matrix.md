## 1091. Shortest path binary matrix

Given an n x n binary matrix grid, return the length of the shortest clear path in the matrix. If there is no clear path, return -1.

A clear path in a binary matrix is a path from the top-left cell (i.e., (0, 0)) to the bottom-right cell (i.e., (n - 1, n - 1)) such that:

All the visited cells of the path are 0.
All the adjacent cells of the path are 8-directionally connected (i.e., they are different and they share an edge or a corner).
The length of a clear path is the number of visited cells of this path.

```bash
Example
Input: grid = [["0",  1],
               [1  ,"0"]]
Output: 2
```
```bash
TC: O(m*n)
SC: O(m*n)
```

### Solution
```python
def shortestPathBinaryMatrix(grid):
    m, n = len(grid), len(grid[0])
    def get_neighbors(i, j):
        return [(i+1,j), (i-1,j), (i,j+1), (i,j-1), 
                (i-1,j-1), (i+1,j+1), (i+1,j-1),(i-1,j+1)]
    
    def is_valid(i, j):
        if 0 <= i < m and 0 <= j < n:
            return True
        return False
    
    def bfs():
        visited = set()
        que = deque()
        if not grid[0][0]:
            que.append((0,0))
            visited.add((0,0))
        count = 1
        while len(que):
            for _ in range(len(que)):
                i,j = que.popleft()
                if i == m-1 and j == n-1:
                    return count
                for nei in get_neighbors(i,j):
                    x, y = nei
                    if is_valid(x, y) and grid[x][y] == 0 and (x,y) not in visited:
                        visited.add((x,y))
                        que.append((x,y))
            count+=1
        return -1
    return bfs()
```