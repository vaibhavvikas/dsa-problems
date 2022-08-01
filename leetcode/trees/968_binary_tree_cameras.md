## 968. Binary Tree Cameras

### Greedy Algorithm

If a node's children are not covered by a camera, then we must place a camera. Additionally, if a node has no parent and it is not covered, we must place a camera here.
```
TC: O(N)
SC: O(H) ~> Recursion Stack Space
```

```python
def minCameraCover(root):
    self.ans = 0
    covered = {None} # Constant Sapce

    def dfs(node, par = None):
        if node:
            dfs(node.left, node)
            dfs(node.right, node)

            if (par is None and node not in covered or
                    node.left not in covered or node.right not in covered):
                self.ans += 1
                covered.update({node, par, node.left, node.right})

    dfs(root)
    return self.ans
```