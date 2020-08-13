# 题目描述

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

# 解答

这个问题有很多小的知识点，首先先看一下二叉树的前序遍历、中序遍历以及后序遍历的方式：
* 前序遍历：根，左，右
* 中序遍历：左，根，右
* 后序遍历：左，右，根

根据上面可知，前序遍历的第一个节点一定是根节点，并且可以根据根节点在中序遍历中的位置，将左右子树划分开来，即中序遍历中，根结点前面的所有节点一定是左子树，后面的所有节点一定是右子树。
因此，解答此问题的思路为：
* 首先判断是否有根结点，如果没有，则return None，如果有，执行下面的步骤；
* 记录根结点的值；
* 寻找到根结点在中序遍历中的索引；
* 根据索引，找出对应的左、右子树的前序和中序遍历序列，然后便可递归调用该重构函数，进一步构造左右子树。

具体代码如下：
```python
class Solution:
    # 返回构造的TreeNode根节点
    def reConstructBinaryTree(self, pre, tin):
        # write code here
        if not pre:
            return None
        root = TreeNode(pre[0])
        l = tin.index(pre[0])
        root.left = self.reConstructBinaryTree(pre[1:l+1], tin[0:l])
        root.right = self.reConstructBinaryTree(pre[l+1:], tin[l+1:])
        return root
```

### 注意
这里牵扯到了列表索引，所以需要小心列表的范围，为了避免出错，可以在草稿纸上想清楚究竟从哪里开始取，以及**一定要记得python的索引下标是从0开始的，并且list[1:3]是从索引1开始，取3-1个元素**。
有人巧妙地利用了列表的pop函数，尽量避免了索引的使用，在该情况下，只需考虑中序遍历的索引即可。具体代码如下：

```python
class Solution:
    # 返回构造的TreeNode根节点
    def reConstructBinaryTree(self, pre, tin):
        # write code here
        if not tin:                                # 这里用的tin，因为在这种情况下pre的长度比tin长
            return None
        root = TreeNode(pre.pop(0))                # 调用了pop函数
        index = tin.index(root.val)                # 因为pre已经弹出了刚才根结点的值，所以这里利用root.val寻找索引
        root.left = self.reConstructBinaryTree(pre, tin[:index])
        root.right = self.reConstructBinaryTree(pre, tin[index + 1:])
        return root
```

# 感想

一开始看到这道题还是没有太大思路，一个是因为不知道如何初始化类的实例，一个是没有想到递归调用。在网上简单看了一下初始化后，便开始自己动手编，首先按照递归的模式写出来，然后自己开始有思路，只需要找到索引即可，但是这个时候遇到的问题是，不知道python中list类型如何按值查找索引，虽然自己之前过了一遍python语法，不过很明显自己并没有记住。这里既然用到了list类型，下面便将list中的默认函数记录一下，希望自己可以记住：

### 列表脚本操作符

* len([1,2,3]) = 3，功能
