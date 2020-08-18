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

正确的解答写的很简洁，但是很难理解，接下来大概写一下我个人的理解：
首先第一个函数逻辑比较简单，因为题目中已经说了，空树不是任意一颗树的子结构，所以如果两棵树中有任意一颗为空树，直接返回False即可，否则返回一个递归函数的值，该递归函数用于判断是否有子树。
递归函数两个重要的概念，递归终止条件和递归主体，接下来看一下isSubtree函数的这两个内容：
* 递归终止条件：XXX
* 递归主体： XXX

```python
class Solution:
    def HasSubtree(self, pRoot1, pRoot2):
        # write code here
        if pRoot1 == None or pRoot2 == None:
            return False
        return self.isSubtree(pRoot1, pRoot2)

    def isSubtree(self, p1, p2):
        if p2 == None:
            return True
        if p1 == None:
            return p1 == p2
        res = False
        if p1.val == p2.val:
            res = self.isSubtree(p1.left, p2.left) and self.isSubtree(p1.right, p2.right)
        return res or self.isSubtree(p1.left, p2) or self.isSubtree(p1.right, p2)
```

