## Boundary view of a binary tree

### Algorithm
```bash
Step 1: Print left view
Step 2: Print leaves
Step 3: Print right in reverse
```

### Solution
```python
def traverseBoundary(root):
    if not root:
       return []
    
    res = []
    def is_leaf(node):
        return not node.left and not node.right
    
    def left_traversal(node):
        curr = node.left
        while curr:
            if not is_leaf(curr):
                res.append(curr.data)
            if curr.left: curr = curr.left
            else: curr = curr.right
        
    def add_leaves(node):
        if is_leaf(node):
            res.append(node.data)
            return
        if node.left: add_leaves(node.left)
        if node.right: add_leaves(node.right)
    
    def add_right(node):
        temp_stack = []
        curr = node.right
        while curr:
            if not is_leaf(curr):
                temp_stack.append(curr.data)
            if curr.right: curr = curr.right
            else: curr = curr.left
        res.extend(temp_stack[::-1])
    
    if not is_leaf(root):
        res.append(root.data)

    left_traversal(root)
    add_leaves(root)
    add_right(root)
    return res
```