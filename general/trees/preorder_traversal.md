## Preorder Traversal

### Algorithm
```
Pop all items one by one.
Do following for every popped item
a) print it
b) push its right child
c) push its left child
Note that right child is pushed first
so that left is processed first
```

### Solution
```python
def iterativePreorder(root):
    if root is None:
        return
 
    nodeStack = []
    nodeStack.append(root)
    while(len(nodeStack) > 0):
        node = nodeStack.pop()
        print (node.data, end=" ")
        if node.right is not None:
            nodeStack.append(node.right)
        if node.left is not None:
            nodeStack.append(node.left)
```