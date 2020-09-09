# 题目描述

输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

# 解答一

递归解法：
* 首先判断边界条件，如果有一个链表为空，只需要返回剩余的链表即可，如果两个均为空，返回None；
* 然后判断第一个链表的值是否小于第二个链表的值，是的话只需要考虑第一个链表下一个节点是谁即可，采用递归公式；反之亦然。

```python
class Solution:
    # 返回合并后列表
    def Merge(self, pHead1, pHead2):
        # write code here
        if not pHead1 and not pHead2:
            return None
        if not pHead1:
            return pHead2
        if not pHead2:
            return pHead1
        if pHead1.val <= pHead2.val:
            pHead1.next = self.Merge(pHead1.next, pHead2) # 注意体会这里，递归的优点
            return pHead1                                 # 这里只需返回pHead1即可，因为是从pHead1开始链接的。
        else:
            pHead2.next = self.Merge(pHead1, pHead2.next) 
            return pHead2
```

# 解答二

非递归解法：
* 首先初始化一个新的节点 pHead = ListNode(0)，然后使用一个指针指向该节点，目的是记录链表的头部；
* 接下来进行循环判断，终止条件为一个链表为空，哪个链表的值小就将该值添加在新的链表的后面，注意更新链表。

```python
class Solution:
    # 返回合并后列表
    def Merge(self, pHead1, pHead2):
        # write code here
        if not pHead1 and not pHead2:
            return None
        if not pHead1:
            return pHead2
        if not pHead2:
            return pHead1
        pHead = ListNode(0)   # 初始化新节点
        res = pHead           # 记录链表的头部
        while pHead1 and pHead2:
            if pHead1.val <= pHead2.val:
                pHead.next = pHead1   # 谁的值小就将该节点添加进来
                pHead1 = pHead1.next
            else:
                pHead.next = pHead2
                pHead2 = pHead2.next
            pHead = pHead.next     # 注意更新pHead
        if pHead1:
            pHead.next = pHead1
        if pHead2:
            pHead.next = pHead2
        return res.next
```

# 感想

递归思路真的很优美，可是自己独立却想不出来，还需要努力，加油！加油！加油！
