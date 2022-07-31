## Diameter of a binary tree

### Algprithm
```
TC: O(n)
SC: o(1)
```

### Solution
```python
def diameterOfBinaryTree(root) -> int:
    self.res = 0
    if not root:
        return 0
    
    def height(node):
        if not node:
            return 0
        ld, rd = height(node.left), height(node.right)
        self.res = max(self.res, ld + rd)
        return max(ld, rd) + 1
    
    height(root)
    return self.res
```