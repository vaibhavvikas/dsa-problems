## Find width of a binary tree

```python
def widthOfBinaryTree(root):
    if not root: return 0
    
    width = 0
    queue = deque([[root, 0]])
    res = 0
    
    while queue:
        n = len(queue)
        level_min = queue[0][1]
        first, last = None, None
        
        for i in range(n):
            element = queue.popleft()
            curr_id = element[1] - level_min
            if i == 0:
                first = curr_id
            if i == n - 1:
                last = curr_id
            
            if element[0].left:
                queue.append([element[0].left, 2*curr_id + 1])

            if element[0].right:
                queue.append([element[0].right, 2*curr_id + 2])
            
        res = max(res, last - first + 1)
        
    return res
```