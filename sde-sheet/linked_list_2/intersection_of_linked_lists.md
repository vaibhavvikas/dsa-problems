## Intersection of Two Linked Lists

### Difference of Length Method
```bash
the idea is if you switch head,
the possible difference between
length would be countered. 
On the second traversal, they either
hit or miss. 
if they meet, pa or pb would be 
the node we are looking for, 
if they didn't meet, they will hit
the end at the same iteration,
pa == pb == None, return either,
None
```

### Solution
```python
def getIntersectionNode(self, headA, headB):
    if headA is None or headB is None:
        return None

    pa = headA
    pb = headB

    while pa is not pb:
        pa = headB if pa is None else pa.next
        pb = headA if pb is None else pb.next

    return pa
```