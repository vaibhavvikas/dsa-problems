## 366. Remove leaves of a binary tree

**Given:**
Root of a binary tree

**Objective:**
Remove all leaves till tree is empty.

```python
Input: [1,2,3,4,5]
 
          1
         / \
        2   3
       / \
      4   5

Output: [[4,5,3],[2],[1]]
```

### Algorithm

```python
1. Find height of each node
2. Based on heights remove the nodes.
```
```python
TC: O(n) ~> Since we are traversing each node once 
SC: O(logn) ~> Height of tree = log(n) which is the dict size
```

### Solution

```python
class Solution:
    def remove_leaves(self, root: TreeNode) -> list:
        if not root:
            return []

        node_height = defaultdict(list)

        def get_heights(node):
            if not node:
                return -1

            left = get_heights(node.left)
            right = get_heights(node.right)
            
            node_height[max(left, right) + 1].append(node.val)
            return max(left, right) + 1

        get_heights(root)

        return [node_height[each] for each in node_height]
```