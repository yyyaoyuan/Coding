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
递归函数有两个重要的概念，递归终止条件和递归主体，接下来看一下isSubtree函数的这两个内容：
* 递归终止条件：
    * 如果p2为空（此时需要注意，p2不可能在第一次调用时为空，因为HasSubtree函数已经排除掉pRoot2为空的情况，并且最低是在第二次迭代调用时访问的，因此此时可以保证p1.val == p2.val），表明在p1.val == p2.val的情况下p2的孩子节点为空，因此此时返回True。
    * 如果p1为空，看一下p2是否为空，是的话返回True，否则返回False。
* 递归主体：
    * 首先让res默认设置为False。
    * 然后判断是否p1.val == p2.val，是的话则进一步递归判断（p1.left和p2.left）and递归判断（p1.right和p2.right）（**这里没有搞懂**），否则进行下一步。
    * 递归判断res or（p1.left和p2） or (p1.right和p2)（**这里也没有搞懂**）。

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

# 感想

按照思路二来求解，我还是很多地方没有弄明白，不懂为什么这里是and：(p1.left, p2.left) and (p1.right, p2.right)？
为什么这里是or：(p1.left, p2) or (p1.right, p2)？
