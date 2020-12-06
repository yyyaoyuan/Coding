# 题目描述

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。
假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，
但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）


# 解答一

按照递归的思路进行求解。

```python
class Solution:
    def IsPopOrder(self, pushV, popV):
        # write code here
        if len(pushV) != len(popV):
            return False
        if not pushV and not popV:
            return True
        if len(pushV) == 1 and len(popV) == 1:
            return pushV == popV
        first = popV[0]
        idx = pushV.index(first)
        lPushV = pushV[:idx]                 # 注意索引
        lPopV = popV[len(popV)-idx:]         # 注意索引
        rPushV = pushV[idx+1:]               # 注意索引
        rPopV = popV[1:len(popV)-idx]        # 注意索引   
        lPopV.reverse()                      # 这个函数会改变原始的列表，所以需要单独写一行
        lFlag = lPushV == lPopV              # 对于左边按照正常的出栈顺序进行判断
        rflag = self.IsPopOrder(rPushV, rPopV) # 对于右边需要进行递归求解
        return lFlag and rflag
```

# 解答二

利用一个辅助栈模拟整个过程

```python
class Solution:
    def IsPopOrder(self, pushV, popV):
        # write code here
        stack = []
        while popV: # 下面if语句的顺序不能颠倒！！！
            if stack and stack[-1] == popV[0]:       # 核心代码块：模拟整个过程，如果stack的最后一个元素与popV中第一个元素相等，将两个元素都弹出
                stack.pop()
                popV.pop(0)                          # popV弹出第一个元素
            elif pushV:
                stack.append(pushV.pop(0))           # 如果pushV中有数据，压入stack
            else:
                return False
        return True
```
