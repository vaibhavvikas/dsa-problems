## Detect Cycle in a Linked List


### Slow anf Fast Pointer Approach

```python
def hasCycle(head):
    if not head:
        return False
    
    slow, fast = head, head
    
    while slow and fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
        
    return False
```