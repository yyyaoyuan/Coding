# 题目描述

从上往下打印出二叉树的每个节点，同层节点从左至右打印。

# 解答

基本的层次遍历问题，解答此问题需要主要边界条件以及返回的具体形式，**如果在面试中记得问清楚面试官，返回的是一个list（如[1,2,3]），
还是一个大的list中嵌套每一层的list（如[[1],[2,3]]）**，此外注意根结点为空时返回的是[]而不是None。

思想：
* 首先判断是否根结点为空，是则返回[]，否则执行接下来的步骤。
* 需要一个列表存放当前层的节点（node=[root]），然后进入while循环主体。
* 需要一个临时的列表存放当前层的所有孩子节点（tmpNode=[]）,利用for循环遍历node列表中的所有节点，需要将当前节点的值装入res中，然后依次遍历该节点的左右孩子，如果有节点，便将其装入tmpNode中。
* 当for循环执行完以后，利用tmpNode列表更新node列表
* 最后，退出while循环，返回res。

具体代码如下：
```python
class Solution:
    # 返回从上到下每个节点值列表，例：[1,2,3]
    def PrintFromTopToBottom(self, root):
        # write code here
        if not root:
            return []
        res = []
        node = [root]
        while node:
            tmpNode = []
            for n in node:
                res.append(n.val)
                if n.left:
                    tmpNode.append(n.left)
                if n.right:
                    tmpNode.append(n.right)
            node = tmpNode
        return res
```

# 感想
现在在做这样的题感觉非常简单，但是我仍然犯了两个错误，第一个错误是边界条件的判断，应该返回[]而不是None，第二个是应该是将res.append(n.val)错写成res.append(root.val)，下次一定不能再错了，真正考试的时候只有一次机会！！！
