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
            if top1 == top2:
                first = top1
            else:
                break

        return first
```

# 解答二

