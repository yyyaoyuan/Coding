# 两数相加

给出两个非空的链表用来表示两个非负的整数。其中，它们各自的位数是按照逆序的方式存储的，并且它们的每个节点只能存储一位数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

## 示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

# 解答

该题重点是考虑进位，注意相加后取模和整除。

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        res = ListNode(-1)             # 注意学习初始化链表节点的写法
        ans = res
        sumVal = 0                     # 每一位相加的和，初始为0
        while True:
            if l1:
                sumVal += l1.val
                l1 = l1.next
            if l2:
                sumVal += l2.val
                l2 = l2.next
            tmpVal = sumVal % 10      # 注意取模
            sumVal //= 10             # 这里计算得到的是进位
            res.next = ListNode(tmpVal)  # 建立下一个节点
            res = res.next
            if not l1 and not l2 and sumVal == 0:  # 终止条件，注意sumVal == 0这个条件
                break
        return ans.next    # 返回的是ans.next节点
```

# 感想

没想到字节的面试出现了链表题，凑着复习一下吧。
