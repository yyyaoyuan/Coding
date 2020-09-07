# 题目描述

输入一个链表，反转链表后，输出新链表的表头。

# 解答

* 边界条件：当前节点或者当前节点的下一个节点是否为空，是的话，返回当前节点
* 需要三个指针进行记录：
  * pre：记录当前节点的前一个节点
  * cur：记录当前节点
  * tmp：记录当前节点的下一个节点

```python
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
class Solution:
    # 返回ListNode
    def ReverseList(self, pHead):
        # write code here
        if not pHead or not pHead.next:
            return pHead
        pre = None
        cur = pHead
        while cur:
            tmp = cur.next    # 首先记录当前节点的下一个节点
            cur.next = pre    # 然后将当前节点的下一个节点指向当前节点的前一个节点
            pre = cur         # 更新当前节点的当前节点为cur
            cur = tmp         # 更新当前节点为tmp
        return pre            # 注意最后返回的是pre，因为cur为空时结束循环，表示当前节点的前一个节点就是最后一个节点
```

# 感想

第一次做链表题，经验不足，不会做，这里需要学习的是指针（索引）的使用，需要多少个指针，分别怎么更新，需要弄清楚才行。
