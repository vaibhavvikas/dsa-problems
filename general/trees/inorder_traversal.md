## Inorder Traversal

```python
def inOrder(root):
    current = root 
    stack = []
      
    while True:
        if current is not None:
            stack.append(current)
            current = current.left 

        elif(stack):
            current = stack.pop()
            print(current.data, end=" ")
            current = current.right
        
        else:
            break
```