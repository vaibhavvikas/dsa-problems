## Given root of a binary tree. Find the path with max sum

```python
def maxPathSum(self, root: TreeNode) -> int:     
    self.res = root.val
    
    def max_path(node):
        if not node:
            return 0
        
        ld, rd = max_path(node.left), max_path(node.right)
        self.res = max(self.res, node.val + ld + rd,\
             ld + node.val , rd + node.val, node.val)
        
        return max(node.val + max(ld, rd), node.val)
    
    max_path(root)
    return self.res
```