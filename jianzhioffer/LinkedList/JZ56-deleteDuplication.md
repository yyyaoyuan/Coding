# 题目描述

在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5。

# 解答一：递归

核心思想：

* 递归终止条件，当前节点为空或者当前节点的下一个节点为空，此时返回当前节点
* 递归主体：
  * 当pHead.val == pHead.next.val时，说明当前节点存在重复，一直删除到第一个不等于该值的节点A处，然后递归调用该函数，输入为A；
  * 当pHead.val != pHead.next.val时，说明当前节点不存在重复，递归调用该函数，输入为pHead.next，赋值给pHead.next，然后返回pHead。
  
```python
class Solution:
    def deleteDuplication(self, pHead):
        # write code here
        if not pHead or not pHead.next:  # 递归终止条件，注意判断pHead.next，以及需要返回pHead
            return pHead
        if pHead.val == pHead.next.val:  # 递归主体，两种情况，分别进行判断，满足==条件时，一直递归到最后一个不重复的节点为止
            tmp = pHead.next
            while tmp and tmp.val == pHead.val:
                tmp = tmp.next
            return self.deleteDuplication(tmp)  # 递归调用该函数
        else:                            # 不满足==条件时，对pHead.next递归调用该函数，用于删除重复的节点
            pHead.next = self.deleteDuplication(pHead.next)
            return pHead                 # 返回pHead，此时pHead肯定不是重复的，并且一定是头节点
```

# 感想

突然发现还是有一点不理解，先放着，回过头来再看！！！

