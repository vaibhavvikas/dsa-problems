## Reverse Linked List in Group of size K

[Leetcode 25](https://leetcode.com/problems/reverse-nodes-in-k-group/)

Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.
k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.
You may not alter the values in the list's nodes, only nodes themselves may be changed.

```bash
Example
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

### Recursion Approach
```bash
We check if the current len of linked
list starting from head is <= k

In other case, we reverse till len k
and call the recursion fucntion to
reverse the curr array
```
```bash
TC: O(n)
SC: O(1)
```

### Solution
```python
def reverseKGroup(head, k):
    node, count = head, 0
    while node and count < k:
        node = node.next
        count += 1
        
    if count < k:
        return head
    
    prev = None
    temp = head
    
    for i in range(k):
        nxt = head.next
        head.next = prev
        prev = head
        head = nxt
        
    temp.next = reverseKGroup(head, k)
    
    return prev
```
