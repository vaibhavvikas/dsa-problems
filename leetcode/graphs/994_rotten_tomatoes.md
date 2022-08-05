## 994. Rotten Tomatoes

You are given a grid where each cell can have:

0 - empty cell,
1 - fresh orange, or
2 rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes until no cell has a fresh orange. If this is impossible, return -1.

### Algortihm
```bash
TC: O(m*n)
SC: O(m*n)
```

### Solution
```python
def orangesRotting(self, grid) -> int:
    queue = deque([])
    oranges = 0
    res = 0
    
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == 0:
                continue
            if grid[i][j] == 2:
                queue.append([i, j])
            else:
                oranges += 1
    
    if oranges == 0:
        return 0
    
    while queue:
        for _ in range(len(queue)):
            a, b = queue.popleft()
            for i, j in [(a-1, b), (a, b+1), (a+1, b), (a, b-1)]:
                if j < len(grid[0]) and j >= 0 and i >= 0 \
                    and i < len(grid) and grid[i][j] == 1:
                    grid[i][j] = 2
                    oranges -= 1
                    queue.append([i, j])
        res += 1
        
    if oranges == 0:
        return res - 1 if res > 0 else 0
    return -1
```