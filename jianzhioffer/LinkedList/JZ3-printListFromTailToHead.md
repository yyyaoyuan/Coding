# 题目描述

输入一个链表，按链表从尾到头的顺序返回一个ArrayList。

# 解答一

首先将链表按照顺序入栈，然后从栈顶依次弹出即可。

```python
class Solution:
    # 返回从尾部到头部的列表值序列，例如[1,2,3]
    def printListFromTailToHead(self, listNode):
        # write code here
        if not listNode:
            return []
        stack = []
        res = []
        while listNode:
            stack.append(listNode)
            listNode = listNode.next
        while len(stack):
            res.append(stack.pop().val)
        return res
```

# 解答二

首先反转链表，然后依次打印即可。

```python
class Solution:
    # 返回从尾部到头部的列表值序列，例如[1,2,3]
    def printListFromTailToHead(self, listNode):
        # write code here
        if not listNode:
            return []
        pre = None       # 注意这里是None
        cur = listNode
        while cur:
            tmp = cur.next
            cur.next = pre # 注意更新这里
            pre = cur
            cur = tmp
        res = []
        while pre:
            res.append(pre.val)
            pre = pre.next
        return res
```

# 解答三

递归操作，采用递归的特性，递归到最深处才开始返回，注意这一点。

```python
class Solution:
    # 返回从尾部到头部的列表值序列，例如[1,2,3]
    def printListFromTailToHead(self, listNode):
        # write code here
        if not listNode:
            return []
        return self.printListFromTailToHead(listNode.next) + [listNode.val]   # 这里注意python的list类型可以使用+，如[1]+[2]=[1,2]
```

# 感想

这里特别需要学习的是递归版本，递归到深处后开始逐层返回，只需要加上每层的val即可，并且**需要记住python中list类型可以+**。
