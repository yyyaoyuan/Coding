# 题目描述

操作给定的二叉树，将其变换为源二叉树的镜像。

# 解答
此问题为二叉树的经典问题，有关二叉树的问题基本都离不开递归解答，并且一旦熟悉了解题思路，编写代码相对比较容易。本题的解题思路为：
**首先判断根结点是否为空，如果为空直接返回即可，否则，执行如下步骤：（1）首先反转根结点的左孩子和右孩子（在反转左孩子节点的时候，相当于反转左子树，右孩子节点同理）；（2）调用self.Mirror反转根结点的左孩子；（3）调用self.Mirror反转根结点的右孩子。**

```python

class Solution:
    def Mirror(self , pRoot ):
        # write code here
        if pRoot:
            pRoot.left, pRoot.right = pRoot.right, pRoot.left
            self.Mirror(pRoot.left)
            self.Mirror(pRoot.right)
        else:
            return
```
