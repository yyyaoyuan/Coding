# 二叉树中的最大路径和

给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。


# 解答：深度优先遍历






```python
class Solution:
    def __init__(self):
        self.res = float('-inf')

    def maxPathSum(self, root: TreeNode) -> int:
        self.dfs(root)
        return self.res
    
    def dfs(self, node):
        if not node:
            return 0
        left = max(0, self.dfs(node.left))
        right = max(0, self.dfs(node.right))
        self.res = max(self.res, left+right+node.val)
        return max(left, right) + node.val
```
