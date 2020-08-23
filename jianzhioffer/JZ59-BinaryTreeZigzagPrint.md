#题目描述

请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

# 解答一

该题思路比较直接，只需要层次遍历，然后根据奇偶性判断是顺序还是逆序存储即可。

```python
class Solution:
    def Print(self, pRoot):
        # write code here
        if not pRoot:
            return []
        res = []
        Node = [pRoot]
        t = 0
        while Node:
            tmpNode = []
            tmpValue = []
            for n in Node:
                tmpValue.append(n.val)
                if n.left:
                    tmpNode.append(n.left)
                if n.right:
                    tmpNode.append(n.right)
            if t % 2 == 0:
                res.append(tmpValue)
            else:
                res.append(tmpValue[::-1])
            t += 1
            Node = tmpNode
        return res
```

# 感想
这道题最主要的问题是不清楚返回的方式是如何的，面试中一定要问清楚面试官究竟是打印还是以列表的方式返回。另外，需要记住列表反转的方法，这里有两种：
```python
A = [1,2,3]
B = list(reversed(A)) # B = [3,2,1]
C = A[::-1] # C = [3,2,1]，重点学习！！！
D = A[1::-1] # D = [2,1]，从下标为1的位置逆序输出。
```
