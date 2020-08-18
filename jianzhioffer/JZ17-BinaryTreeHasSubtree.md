# 题目描述

输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

# 解答一

首先写一个前序遍历的函数，然后将A和B的前序遍历的序列AList，BList写出来，**因为它们都是有序的**，所以接下来只需要判断BList是否在AList中即可。
具体代码如下：

```python
class Solution:
    def HasSubtree(self, pRoot1, pRoot2):
        # write code here
        if not pRoot2:
            return False
        pList1 = self.preTraversal(pRoot1, [])
        pList2 = self.preTraversal(pRoot2, [])
        res = [1 for i in pList2 if i not in pList1]     # 记住这样的代码，非常的简介和优美！
        if res:
            return False
        return True
        
    def preTraversal(self, root, List):
        if not root:
            return List
        List.append(root.val)
        self.preTraversal(root.left, List)
        self.preTraversal(root.right, List)
        return List
```

# 解答一有问题！！！！在牛客网上看到了反例，真正考试的时候这样做不知道能不能过去，但是即使可以过去，也是错的。。。。。。接下来看一下正确的解答。

