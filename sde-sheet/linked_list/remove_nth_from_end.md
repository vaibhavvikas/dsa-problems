## Remove nth node from end

### Approach
```bash
Take two dummy nodes, who’s next
will be pointing to the head.

Take another node to store the head,
initially,s a dummy node(start), and the
next node will be pointing to the head.
The reason why we are using this extra
dummy node is that there is an edge case.
If the node is equal to the length of the
LinkedList, then this slow will point to
slow’s next→ next. And we can say our
dummy start node will be broken and will
be connected to the slow next→ next.

Start traversing until the fast
pointer reaches the nth node.
```
```bash
TC: O(n)
SC: O(1)
```

### Solution
```python
def removeNthFromEnd(head, n):
    first, second = head, head
    
    for i in range(n):
        if not second.next:
            if i == n-1:
                head = head.next
                return head
        second = second.next

    while second.next:
        first = first.next
        second = second.next
        
    first.next = first.next.next
    return head
```

### Another Approach

Another Approach is we can count total nodes in one go and in another go we traverse to total - n nodes.
