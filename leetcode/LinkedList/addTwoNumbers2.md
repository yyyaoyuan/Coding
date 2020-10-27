# 两数相加 II

给你两个非空链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。
你可以假设除了数字 0 之外，这两个数字都不会以零开头。

## 进阶：

如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

## 示例：

输入：(7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 8 -> 0 -> 7

# 解答一：非进阶

首先翻转链表，然后按照顺序相加的方法进行计算，最后将结果翻转后输出。

```python
class Solution: 
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        p = self.reverseList(l1)
        q = self.reverseList(l2)
        res = ListNode(-1)
        ans = res
        sumVal = 0
        while True:
            if p:
                sumVal += p.val
                p = p.next
            if q:
                sumVal += q.val
                q = q.next
            tmpVal = sumVal % 10
            sumVal //= 10
            res.next = ListNode(tmpVal)
            res = res.next
            if not p and not q and sumVal == 0:
                break
        return self.reverseList(ans.next)   # 注意需要翻转链表
    
    def reverseList(self, l):           # 翻转链表
        if not l:
            return l
        pre = None
        cur = l 
        while cur:
            tmp = cur.next
            cur.next = pre
            pre = cur
            cur = tmp
        return pre         # 注意这里是返回的pre，这里错了好多次！！！！
```

# 解答二：进阶

使用栈进行解决。

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        p1, p2 = [], []
        while l1:
            p1.append(l1.val)
            l1 = l1.next
        while l2:
            p2.append(l2.val)
            l2 = l2.next
        sumVal = 0
        ans = None      # 记录答案
        while p1 or p2 or sumVal != 0:
            a = 0 if not p1 else p1.pop()
            b = 0 if not p2 else p2.pop()
            sumVal = a + b + sumVal
            tmpVal = sumVal % 10
            sumVal //= 10
            curNode = ListNode(tmpVal)   # 注意这里新建一个节点
            curNode.next = ans           # 然后指向前一个节点
            ans = curNode                # 修改ans节点
        return ans
```

# 感想

面试时遇到了这道题，个人感觉还是

