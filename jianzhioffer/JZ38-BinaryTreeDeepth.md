# 题目描述

输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

# 解答

思路：**首先判断是否当前结点为空节点，如果是空，表明树的深度为0，则返回0；然后分别计算当前节点左子树和右子树的深度，注意总的深度需要加1（算上当前节点）；最后返回按照左右子树分别计算的深度的最大值。**

```python
class Solution:
    def TreeDepth(self, pRoot):
        # write code here
        if not pRoot:
            return 0
        l = self.TreeDepth(pRoot.left) + 1
        r = self.TreeDepth(pRoot.right) + 1
        return max(l,r)
```
