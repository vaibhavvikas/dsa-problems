## 138. Clone Linked List with Random Pointers

Given a linked list having two pointers in each node. The first one points to the next node of the list, however, the other pointer is random and can point to any node of the list. Write a program that clones the given list

### Algortihm
```bash
Step 1: Insert Additional Node
Step 2: Copy randome
Step 3: Detach Dup from Orig
```
```bash
TC: O(n)
SC: O(1)
```

### Solution
```python
def copyRandomList(head):
    if not head:
        return head
    
    curr = head
    while curr:
        new = Node(curr.val)
        new.next = curr.next
        curr.next = new
        curr = curr.next.next
    
    curr = head
    while curr:
        if curr.random:
            curr.next.random = curr.random.next
        curr = curr.next.next

    curr = head
    dup_head = head.next
    while curr.next:
        temp = curr.next
        curr.next = curr.next.next
        curr = temp

    return dup_head
```