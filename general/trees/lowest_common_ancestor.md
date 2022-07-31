## Lowest Common Ancestor

### Algortihm
```
TC: O(n)
SC: O(1)
```

### Solution
```python
def lca(root, p, q):
    if not root or root == p or root == q:
        return root
    
    left = lca(root.left, p, q)
    right = lca(root.right, p, q)
    
    if not left:
        return right
    elif not right:
        return left

    return root
```