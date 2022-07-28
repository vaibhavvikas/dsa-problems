## 79. Word Search

Given an m x n grid of characters board and a string word,
return true if word exists in the grid.

### Algorithm
```bash
We call dfs for each word in grid.

Use DFS:
Step 1. For each word we have 4 directions.
Step 2. We mark the current index as visited
    and call all 4 with increment in curr len
Step 3. If any case fails return False
Step 4. If DFS return True means found.
```
```
TC: O(R*C*n)
SC: O(R*C)
```


### Solution
```python
def exist(board: List[List[str]], word: str):
    ROWS, COLS = len(board), len(board[0])
    WORD = len(word)
    
    visited = set()
    
    def dfs(i, j, l):
        if l == WORD:
            return True

        if i < 0 or i >= len(board) or j < 0 or \
            j >= len(board[0]) or \
            (i, j) in visited or \
            board[i][j] != word[l]:
            return False
        
        visited.add((i, j))
        res = dfs(i+1, j, l+1) or\
                dfs(i-1, j, l+1) or\
                dfs(i, j-1, l+1) or\
                dfs(i, j+1, l+1)

        visited.remove((i, j))
        return res
    
    for i in range(len(board)):
        for j in range(len(board[0])):
            if dfs(i, j, 0):
                return True
    return False
```