# 最长同值路径

给定一个二叉树，找到最长的路径，这个路径中的每个节点具有相同值。 这条路径可以经过也可以不经过根节点。

注意：两个节点之间的路径长度由它们之间的边数表示。

# 解答：深度优先遍历

该题仍然是二叉树的深度优先遍历解法，解题思路如下：

* 首先遍历当前节点的左右子树，分别求出左右子树的最大同值路径
* 然后，根据当前节点的左（右）子树的节点值与当前节点值是否相同，决定是否丢低该子树。


```python
class Solution:
    def __init__(self):
        self.res = 0
    
    def longestUnivaluePath(self, root: TreeNode) -> int:
        self.dfs(root)
        return self.res
    
    def dfs(self, node):
        if not node:
            return 0
        left = self.dfs(node.left)
        right = self.dfs(node.right)
        if node.left and node.left.val == node.val:  # 如果相同，则加1
            left += 1
        else:                                        # 否则丢弃
            left = 0
        if node.right and node.right.val == node.val:
            right += 1
        else:
            right = 0
        self.res = max(self.res, left+right)
        return max(left, right)
```

# 感想

大概先记住这种类型题的解题套路，加油！！！！！！
