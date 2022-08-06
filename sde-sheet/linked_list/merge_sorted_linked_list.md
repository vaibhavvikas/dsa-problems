## Merge Sorted Linked List

### No extra space
```bash
Step 1. Assign first to the lowest 
val list

Now we traverse first taking temp as 
prev of first until we reach the case
that second val is less.
once we recah that we assign temp.next 
to second and make second as first

then vice versa.
```
```
TC: O(n)
SC: O(1)
```
### Solution
```python
def mergeTwoLists(first, second):
    if not first:
        return second
    
    if not second:
        return first
    
    if first.val > second.val:
        first, second = second, first
    
    res = first
    
    while first != None and second != None:
        temp = None
        
        while first and first.val <= second.val:
            temp = first
            first = first.next
        
        temp.next = second
        first, second = second, first
            
    return res
```