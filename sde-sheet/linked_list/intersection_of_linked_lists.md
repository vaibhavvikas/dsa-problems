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
if they didnt meet, they will hit
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

### Difference of length detailed method
```
TC: O(n)
SC: O(1)
```
```python
def getIntersectionNode(headA, headB): 
    lengthA = 0
    lengthB = 0 
    
    tempHeadA = headA 
    tempHeadB = headB 
    
    while(tempHeadA != None):
        lengthA += 1 
        tempHeadA = tempHeadA.next 
    
    while(tempHeadB != None):
        lengthB += 1 
        tempHeadB = tempHeadB.next 
    
    if lengthA > lengthB:
        extra = lengthA - lengthB 
        
        while(extra > 0):
            headA = headA.next  
            extra -= 1
    else:
        extra = lengthB - lengthA 
        
        while(extra > 0):
            headB = headB.next 
            extra -= 1
    
    while(headA != None and headB != None):
        if(headA == headB):
            return headA  
        
        headA = headA.next 
        headB = headB.next

    return None
```