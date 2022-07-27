## 2096. Step-By-Step Directions From a Binary Tree Node to Another

**Given:**
root of binary tree, start_val, end_val

**Objective:**
Shortest fast from start to end with directions as:
L means go to left child
R means to to right child
U means go up to parent

### Algorithm

```bash
1. Find LCA as we dont need anything else.
2. once we find the lca, we only need to focus
   on the subtree with lca as root.
3. Using BFS we find the path.
```
```python
TC: O(n) ~> for LCA and O(n) ~> for queue path
SC: O(n) ~> Queue size
```

### Solution

```python
def getDirections(root, startValue, destValue):
    def lca(node):
        if not node:
            return None
        
        if node.val == startValue or node.val == destValue:
            return node
        
        left = lca(node.left)
        right = lca(node.right)
        
        if left and right:
            return node
        
        return left if left else right
    
    common_root = lca(root)
    
    queue = deque([(common_root, "")])
    position_start, position_end = "", ""

    while queue:
        node, path = queue.popleft()
        
        if node.val == startValue:
            position_start = path    
        if node.val == destValue:
            position_end = path

        if node.left:
            queue.append((node.left, path + "L"))                
        if node.right:
            queue.append((node.right, path + "R"))
            
    return "U"*len(position_start) + position_end
```