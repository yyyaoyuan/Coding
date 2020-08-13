# 题目描述

输入一棵二叉树，判断该二叉树是否是平衡二叉树。在这里，我们只需要考虑其平衡性，不需要考虑其是不是排序二叉树。

# 解答一
最直接的逻辑是借助一个辅助计算二叉树深度的函数，然后直接通过计算当前节点的左右子树的高度差的绝对值是否小于等于1进行判断，这里需要注意一点，**上述过程只能判断当前节点的左右子树是平衡的，无法判断每个子树内部是否平衡，为了进一步判断左右子树内部是否平衡，只需要递归调用该函数即可**。
（这里需要注意的一点是，如果当前节点为空，是否判断为平衡二叉树，这里默认是返回的True。）
具体代码如下：
```python
class Solution:
    def depth(self, pRoot):
        if not pRoot:
            return 0
        return max(self.depth(pRoot.left),self.depth(pRoot.right)) + 1

    def IsBalanced_Solution(self, pRoot):
        # write code here
        if not pRoot:
            return True
        return (abs(self.depth(pRoot.left) - self.depth(pRoot.right)) <= 1
            and self.IsBalanced_Solution(pRoot.left)
            and self.IsBalanced_Solution(pRoot.right))
```

# 错误记录

这里我编程时，忘记了绝对值，导致第一次编译没有通过（**一定要注意求差需要绝对值**）。
