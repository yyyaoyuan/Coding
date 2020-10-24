# 题目描述

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针random指向一个随机节点），请对此链表进行深拷贝，并返回拷贝后的头结点。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

# 解答一：递归实现

不确定对不对，不过暂时先按照该方法记忆吧。

```python
class Solution:
    # 返回 RandomListNode
    def Clone(self, head):
        # write code here
        if not head: 
            return
        newNode = RandomListNode(head.label)    # 新建一个节点
        newNode.random = RandomListNode(head.random.label) if head.random else None # 新建一个节点
        newNode.next = self.Clone(head.next)
        return newNode
```
