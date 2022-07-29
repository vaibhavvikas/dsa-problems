## 778. Swimming in Rising Water

An n x n integer matrix grid where, grid[i][j] is elevation at that point
Return the least time until you can reach the bottom right square (n - 1, n - 1) if you start at the top left square (0, 0).

### DFS + Binary Search

#### Algorithm
```bash
We use binary search and only traverse
the nodes which have an element <= val

If we reach we go to left half else
right half
```
```bash
TC: O(n*2 logn)
SC: O(n^2)
```
#### Solution

```python
def is_valid_path(i, j):
    return i >= 0 and i < len(grid) \
        and j >= 0 and j < len(grid[0])


def dfs(i, j, val):
    if i == len(grid) - 1 and \
        j == len(grid[0]) - 1 and \
        grid[i][j] <= val:
        return True

    if not is_valid_path(i, j) or \
        visited[i][j] or grid[i][j] > val:
        return False

    visited[i][j] = True
    
    res = dfs(i, j-1, val) or \
            dfs(i, j+1, val) or \
            dfs(i-1, j, val) or \
            dfs(i+1, j, val)
    return res


def swimInWater(self, grid: List[List[int]]) -> int:
    left = max(grid[0][0], grid[-1][-1]), 
    right = len(grid)*len(grid[0]) - 1
    min_ele = right

    while left <= right:
        mid = left + (right - left)//2
        visited = [[False]*(len(grid[0])) for _ in range(len(grid))]
    
        if dfs(0, 0, mid):
            min_ele = min(min_ele, mid)
            right = mid - 1
        else:
            left = mid + 1
            
    return min_ele
```

### BFS

#### Algorithm

```python
We use priority queue (heap)
and push based on elevation

we maintain visited so we dont
use them again.

As soon as we reached end we are
done.
```
```bash
TC: O(n^2 logn)
SC: O(n^2)
```

#### Solution
```python
def swimInWater(self, grid: List[List[int]]) -> int:   
    def is_valid(i, j):
        return 0 <= i < len(grid) and 0 <= j < len(grid)
    
    heap = [(grid[0][0], 0, 0)]
    visited = set((0, 0))
    
    while heap:
        elevation, i, j = heapq.heappop(heap)
        
        if i == j == len(grid)-1:
            return elevation
        
        for x, y in [(i, j+1), (i, j-1), (i+1, j), (i-1, j)]:
            
            if is_valid(x, y):
                new_ele = max(elevation, grid[x][y])
                if (x, y) not in visited:
                    heapq.heappush(heap, (new_ele, x, y))
                    visited.add((x, y))
```
