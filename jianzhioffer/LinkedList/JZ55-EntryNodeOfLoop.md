# 题目描述

给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。

# 解答一

使用一个字典存储所有的节点，一但出现发现有节点已经存在于字典中，那么该节点一定是环的入口节点。

```python
class Solution:
    def EntryNodeOfLoop(self, pHead):
        # write code here
        dic = {}
        while pHead:
            if pHead not in dic:
                dic[pHead] = 1
            else:
                return pHead
            pHead = pHead.next
        return None
```

# 解答二

采用双指针方法进行求解，有点不好理解，大概的意思是：
* 分别用slow，fast指向链表头部，slow每次走一步，fast每次走二步，直到slow==fast找到二者在环中的相汇点。
* 当slow==fast时，fast所经过节点数为2x, slow所经过节点数为x, 
  * 设从起始点到环的入口点到相遇点距离为a；从环的入口点到相遇点距离为c，从相遇点到环的入口点到距离为d;
  * x = a + c; 2x = a + c + d + c; 
  * 根据上式可得**d == a**;   * x = a + c; 2x = a + c + d + c; （这里做了化简，只考虑快指针在环里转了一圈的情况，如果转了很多圈也可以得到同样的结论，这个需要好好理解理解）
* 因此，再让fast指向链表头部，slow位置不变，slow, fast每次走一步直到slow==fast，此时slow指向环的入口。

```python
class Solution:
    def EntryNodeOfLoop(self, pHead):
        # write code here
        fast = pHead
        slow = pHead
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                fast = pHead
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
        return None
```

# 感想

这道题不管我怎么想肯定都是想不出来怎么解决的，需要学习的有两点
        return None
