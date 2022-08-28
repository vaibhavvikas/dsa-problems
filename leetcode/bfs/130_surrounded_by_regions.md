## 130. Surrounded by regions

Given an m x n matrix board containing 'X' and 'O', capture all regions that are 4-directionally surrounded by 'X'.
A region is captured by flipping all 'O's into 'X's in that surrounded region.

```bash
Input: [["X","X","X","X"],
        ["X","O","O","X"],
        ["X","X","O","X"],
        ["X","O","X","X"]]

Output: [["X","X","X","X"],
         ["X","X","X","X"],
         ["X","X","X","X"],
         ["X","O","X","X"]]

Explanation: Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
The bottom 'O' is on the border, so it is not flipped.
The other three 'O' form a surrounded region, so they are flipped.
```

### Multi Source BFS Solution
```bash
The intuition is to add the boundary
to a queue if it is 'O'.

Start the bfs from the nodes added
and since youre using queue(FIFO)
this bfs will check for inner matrix
elements and if they are also 'O' just start

convertin all these 'O's to 'V's. 
i.e. they are connected to boundary
and should not be converted

The last step is to traverse the matrix
and if the element is still 'O' turn it
to 'X' if it is 'V' turn it to 'O' and
we get our answer.
```
```bash
TC: O(m*n)
SC: O(m*n)
```

### Solution
```python
def solve(board):
    queue = deque()
    r, c = len(board), len(board[0])
    
    def is_valid(nr, nc):
        return 0 <= nr < r and 0 <= nc < c
    
    directions = [(-1, 0), (0, -1), (1, 0), (0, 1)]
    
    for i in range(r):
        if board[i][0] == "O":
            queue.append((i, 0))
        if board[i][c-1] == "O":
            queue.append((i, c-1))
            
    for i in range(1, c-1):
        if board[0][i] == "O":
            queue.append((0, i))
        if board[r-1][i] == "O":
            queue.append((r-1, i))
            
    visited = set()
    
    while queue:
        nr, nc = queue.popleft()
        board[nr][nc] = "V"
        
        for i, j in directions:
            ri, ci = nr + i, nc + j
            if is_valid(ri, ci) and (ri, ci) not in visited and board[ri][ci] == "O":
                queue.append((ri, ci))
                visited.add((ri, ci))
                
    for i in range(r):
        for j in range(c):
            if board[i][j] == "O":
                board[i][j] = "X"
            if board[i][j] == "V":
                board[i][j] = "O"
```
