## Minimum Time to Burn Binary Tree

### Algorithm
```
TC: O(n)
SC: O(n)
```

### Solution

```python
def timeToBurnTree(root, start):

    max_time_to_burn = 0
    if not root:
        return max_time_to_burn
    
    parent_map = {}
    q = deque([root])
    start_node = None
    
    while q:
        for _ in range(len(q)):
            node = q.popleft()
            
            if node.data == start:
                start_node = node
            if node.left:
                parent_map[node.left] = node
                q.append(node.left)
            if node.right:
                parent_map[node.right] = node
                q.append(node.right)
                
    visited = {}
    
    queue = deque([[start_node, 0]])
    visited[start_node] = True
    
    while queue:
        for _ in range(len(queue)):
            element = queue.popleft()
            max_time_to_burn = max(element[1], max_time_to_burn)

            if element[0].left and element[0].left not in visited:
                visited[element[0].left] = True
                queue.append([element[0].left, element[1] + 1])
                
            if element[0].right and element[0].right not in visited:
                visited[element[0].right] = True
                queue.append([element[0].right, element[1] + 1])
                
            if element[0] in parent_map and parent_map[element[0]] not in visited:
                visited[parent_map[element[0]]] = True
                queue.append([parent_map[element[0]], element[1] + 1])
                
    return max_time_to_burn
```
