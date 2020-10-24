# 题目描述

给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4

# 解答

因为是二叉搜索树，所以只需要中序遍历该树，得到的序列便是从小到大有序的，此时只需要按照索引输出第k个**节点**即可。

**注意题目要求输出是节点，此外注意判断k的范围是否合法**

```python
class Solution:
    # 返回对应节点TreeNode
    def __init__(self):
        self.res = []
    def KthNode(self, pRoot, k):
        # write code here
        if not pRoot or k <= 0:
            return
        self.dfs(pRoot)
        return self.res[k-1] if k <= len(self.res) else None
    def dfs(self, pRoot):
        if not pRoot:
            return
        self.dfs(pRoot.left)
        self.res.append(pRoot)
        self.dfs(pRoot.right)
```

# 感想

关于二叉树相关的程序有些忘记了，后面还需要集中训练，加油！！！
