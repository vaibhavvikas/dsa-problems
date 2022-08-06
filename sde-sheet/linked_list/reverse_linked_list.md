## Reverse Linked List

```
TC: O(n)
SC: O(1)
```

### Solution
```python
def reverseList(head):
    prev = forw = None
    curr = head
    
    while curr:
        forw = curr.next
        curr.next = prev
        prev = curr
        curr = forw
    
    return prev    
```
```python
def reverseList(head):
    end = None
    
    while head:
        prev, head.next, head = head, prev, head.next
    
    return prev
```
