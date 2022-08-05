## 36. Valid Sudoku

```
TC: O(m*n)
SC: O(1) ~> Max len of set can be 9
```

### Solution

```python
def isValidSudoku(self, board: List[List[str]]) -> bool:
    rows, cols, boxes = set(), set(), set()
    
    for i, x in enumerate(board):
        for j, y in enumerate(x):
            if y == ".":
                continue
            if (i, y) in rows or (j, y) in cols or (i//3, j//3, y) in boxes:
                return False
            else:
                rows.add((i, y))
                cols.add((j, y))
                boxes.add((i//3, j//3, y))

    return True
```