# 题目描述

输入一个链表，输出该链表中倒数第k个结点。

# 解答一

首先将链表装入栈中，然后计算栈的长度，再根据k计算应该弹出的节点的索引，找到对应的节点弹出即可。

```python
class Solution:
    def FindKthToTail(self, head, k):
        # write code here
        if not head:
            return None
        stack = []
        while head:
            stack.append(head)
            head = head.next
        l = len(stack)
        if 0 < k <= l:               # 注意这里的判断条件
            return stack.pop(l-k)    # 注意这里的索引
        return None
```

# 解答二

首先遍历一遍链表求出长度，然后根据k求出对应的索引位置，再遍历一遍即可。

```python
class Solution:
    def FindKthToTail(self, head, k):
        # write code here
        if not head:
            return None
        depth = 0
        h = head
        while h:
            h = h.next
            depth += 1
        idx = depth - k + 1
        if idx > 0:
            for i in range(1, idx):
                head = head.next
            return head
        else:
            return None
```

# 解答三

双指针法：使用两个指针，另两个指针的长度差为k-1，当最后面的指针为最有一个节点时，第一个节点便是所需要求的节点，返回即可。

```python
class Solution:
    def FindKthToTail(self, head, k):
        # write code here
        if not head:
            return None
        first = head
        last = head
        if k <= 0:       # 注意这个判断条件
            return None
        for _ in range(1, k): # 注意这里是range(1, k)
            last = last.next
            if not last:
                return None
        while last.next:
            first = first.next
            last = last.next
        return first
```

# 感想

这道题最主要的是注意索引，以及边界条件，**特别是k<=0不要忘记**，以及k超出链表长度。另外，需要学习一下双指针的思想，确实很巧妙，
可是自己真的想不出来这种解法，希望以后遇到类似的题可以想到**双指针的解法**。
