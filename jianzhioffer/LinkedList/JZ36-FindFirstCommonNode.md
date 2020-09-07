# 题目描述

输入两个链表，找出它们的第一个公共结点。（注意因为传入数据是链表，所以错误测试数据的提示是用其他方式显示的，保证传入数据是正确的）

# 解答一

这里需要注意一点，其实看题目看不出来，两个链表如果有公共节点，**那么表示两个链表一定从公共节点到尾节点是重叠的**。

利用两个栈分别存储链表中的每个节点，根据上述分析，两个链表的尾部一定是相同的，那么入栈后便是头部一定有部分是重叠，只需要按照顺序出栈，直到找到最后相同的结点便是第一个公共结点。

```python
class Solution:
    def FindFirstCommonNode(self, pHead1, pHead2):
        # write code here
        if not pHead1 and not pHead2:
            return None

        stack1 = []
        stack2 = []

        while pHead1:
            stack1.append(pHead1)
            pHead1 = pHead1.next
            
        while pHead2:
            stack2.append(pHead2)
            pHead2 = pHead2.next

        first = None
        while stack1 and stack2:
            top1 = stack1.pop()
            top2 = stack2.pop()
            if top1 is top2:
                first = top1
            else:
                break

        return first
```

# 解答二

先计算两个链表的深度，如果谁的深度比较长，就让谁先多走几步，直到深度相同，然后再一起遍历，直到找到第一个相同的结点为止。

```python
class Solution:
    def FindFirstCommonNode(self, pHead1, pHead2):
        # write code here
        if not pHead1 and not pHead2:
            return None
        
        deep1 = 0
        deep2 = 0
        
        p1, p2 = pHead1, pHead2   # 注意进行赋值操作
        
        while p1:                 # 计算第一个链表的长度
            deep1 += 1
            p1 = p1.next

        while p2:                 # 计算第二个链表的长度
            deep2 += 1
            p2 = p2.next
        
        if deep1 > deep2:
            h = deep1 - deep2
            while h:
                pHead1 = pHead1.next
                h -= 1
        elif deep2 > deep1:
            h = deep2 - deep1
            while h:
                pHead2 = pHead2.next
                h -= 1
        else:
            return pHead1
        
        while pHead1 and pHead2:
            if pHead1 is pHead2:
                return pHead1
            pHead1 = pHead1.next
            pHead2 = pHead2.next
        
        return None
```
