## 554. Brick Wall

There is a rectangular brick wall in front of you with n rows of bricks.
Draw a vertical line from the top to the bottom and cross the least bricks. 

### Algorithm
```
TC: O(m*n)
SC: O(m*n)
```

### Solution
```python
def leastBricks(self, wall: List[List[int]]) -> int:
    bricks_edges = defaultdict(int)
    max_edges = 0
    
    for row in wall:
        for brick in accumulate(row[:-1]):
            bricks_edges[brick] += 1
            max_edges = max(max_edges, bricks_edges[brick])
            
    return len(wall) - max_edges
```