## Given root find a path from root to a node

### Algorithm
```bash
Step 1. Traverse and add curr to res
Step 2. Check its value
    if equal return True
    else check both left and right
    if either returns True return True
    else: it means neither side has it
    so, pop from res
    and return False
```

### Solution

```python
def solve(A: TreeNode, B: int):
    if not A:
        return []

    if A.val == B:
        return [B]

    self.res = []

    def get_path(node, B):
        if not node:
            return False
        
        self.res.append(node.val)

        if node.val == B:
            return True

        left_trav = get_path(node.left, B)
        right_trav = get_path(node.right, B)

        if left_trav or right_trav:
            return True

        self.res.pop()
        return False

    get_path(A, B)
    return self.res
```