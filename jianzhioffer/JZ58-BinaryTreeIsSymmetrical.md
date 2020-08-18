# 题目描述

请实现一个函数，用来判断一棵二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。

# 解答一

看到该题的第一思路是，暴力对比。具体思路如下：
* 首先将原始的二叉树复制一份，此时需要一个函数对二叉树进行复制（进行复制的原因在于后面需要求二叉树的镜像，python函数中默认是传入引用，所以会改变原始二叉树的值）。
* 然后将原始的二叉树进行镜像反转，得到一颗新的二叉树，此时需要一个函数对二叉树进行镜像反转。
* 最后将复制的原始二叉树和镜像二叉树进行层次遍历，得到每一层所有节点的值，然后进行比较（这里只能进行值的比较，不能进行节点的比较，**并且需要注意值为None时的情况，非常重要！！！**），如果有一层的值不同，直接返回False，否则遍历完所有层后返回True。

具体代码如下：
```python
class Solution:
    def isSymmetrical(self, pRoot):
        # write code here
        if not pRoot:
            return True
        cRoot = self.copy(pRoot)
        qRoot = self.mirror(pRoot)
        qNode, cNode = [qRoot], [cRoot]
        while qNode and cNode:
            qTmpNode, qTmpVal = self.findNode(qNode)
            cTmpNode, cTmpVal = self.findNode(cNode)
            if qTmpVal != cTmpVal:
                return False
            qNode, cNode = qTmpNode, cTmpNode
        return True
        
    def mirror(self, pRoot):                         # 镜像反转二叉树
        if not pRoot:
            return None
        pRoot.left, pRoot.right = pRoot.right, pRoot.left
        self.mirror(pRoot.left)
        self.mirror(pRoot.right)
        return pRoot
        
    def findNode(self, Node):                        # 遍历二叉树中下一层所有的节点
        TmpNode = []                                 # 用来装下一层的节点
        TmpVal = []                                  # 用来装下一层的值，存储值的作用在于进行对比是否二叉树对称
        for n in Node:
            TmpVal.append(n.val)
            if n.left:
                TmpNode.append(n.left)
                TmpVal.append(n.left.val)
            else:
                TmpVal.append(None)
            if n.right:
                TmpNode.append(n.right)
                TmpVal.append(n.right.val)
            else:
                TmpVal.append(None)
        return TmpNode, TmpVal
        
    def copy(self, root):                             # 复制一颗二叉树的函数
        if not root:
            return None
        cRoot = TreeNode(root.val)                    # 利用根结点的值初始化一个新的根结点
        cRoot.left = self.copy(root.left)             # 递归复制根结点的左子树
        cRoot.right = self.copy(root.right)           # 递归复制根结点的右子树
        return cRoot
```

# 解答二

解答一是一种很直观的暴力搜索的方法，使用解答一回顾了很多二叉树的基本代码，这些对于复习之前的知识是很有帮助的，但是还是需要掌握一下高级的解法。
具体思路如下：
