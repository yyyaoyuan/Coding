# 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

# 解法

需要利用一个辅助栈进行解决，**该辅助栈需要将每次的最小值保存下来**，并且需要保持和原始栈相同的高度。

```python
class Solution:
    def __init__(self):
        self.stack = []
        self.assist = []                    # 辅助栈
    def push(self, node):
        # write code here
        minVal = self.min()                 # 核心代码块，需要每次找到最小值
        if not minVal or node < minVal:     # 这里需要特别注意minVal为空的情况，表明初始状态
            self.assist.append(node)
        else:
            self.assist.append(minVal)
        return self.stack.append(node)
    def pop(self):
        # write code here
        if self.stack:
            self.assist.pop()
        return self.stack.pop()
    def top(self):
        # write code here
        if self.stack:
            return self.stack[-1]
    def min(self):
        # write code here
        if self.stack:
            return self.assist[-1]
```

# 感想

这道题自己是没有任何思路的，怎么也不会联想到利用一个辅助栈，还是需要多见题型，多多练习，加油！！！
