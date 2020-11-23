# 二叉树中的最大路径和

给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。


# 解答：深度优先遍历

对于任意一个节点, 如果最大和路径包含该节点, 那么只可能是两种情况: 

* 其左右子树中所构成的和路径值较大的那个加上该节点的值后向父节点回溯构成最大路径；
* 左右子树都在最大路径中, 加上该节点的值构成了最终的最大路径。



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
        left = max(0, self.dfs(node.left))    # 如果左子树路径和为负则应当置0表示最大路径不包含左子树
        right = max(0, self.dfs(node.right))  # 如果右子树路径和为负则应当置0表示最大路径不包含右子树
        self.res = max(self.res, left+right+node.val)  # 以当前节点为根节点,判断在该节点包含左右子树的路径和是否大于当前最大路径和
        return max(left, right) + node.val   # 当前节点作为父节点的一个子节点和父节点连接的话则需取【单端的最大值】返回
```

# 感想

这道题也是二叉树上的深度优先遍历，但是对大难有些似懂非懂，先放在这里吧，继续加油！！！
