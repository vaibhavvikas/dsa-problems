## Delete a node

### O(1) Approach
```
copy the next data to current node
and mark next of current of next.next
```
```
TC: O(1)
SC: O(1)
```

### Solution
```python
def del_node(node):
    if not node.next:
        node = None
        return

    node.data = node.next.data
    node.next = node.next.next
```