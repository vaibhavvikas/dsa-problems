## Postorder Traversal

### Solution
```python
def postOrderIterative(root):
 
    if root is None:
        return       
     
    stack = []
    res = []
     
    stack.append(root)

    while stack:
        node = stack.pop()
        res.append(node.val)

        if node.left:
            stack.append(node.left)
        if node.right:
            stack.append(node.right)
 
    return res[::-1]
```
