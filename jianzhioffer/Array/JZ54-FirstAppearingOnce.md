# 题目描述

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。
当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。

## 输出描述:

如果当前字符流没有存在出现一次的字符，返回#字符。

# 解答一

这里使用两个队列保存状态：
* 一个按顺序保存所有出现一次的字符：self.s1
* 一个按顺序保存所有出现过的字符：self.s2

```python
class Solution:
    # 返回对应char
    def __init__(self):
        self.s = ''
        self.s1 = []               # 按顺序保存所有出现一次的字符
        self.s2 = []               # 按顺序保存所有出现过的字符
    def FirstAppearingOnce(self):
        # write code here
        if self.s1:
            return self.s1[0]
        return '#'
    def Insert(self, char):
        # write code here
        self.s += char
        if char in self.s1:
            self.s1.pop(self.s1.index(char))
        elif char not in self.s2:
            self.s1.append(char)
            self.s2.append(char)
```

# 感想

这道题完全不知道怎么入手，因为涉及到了两个函数，最后理解的意思是这里是个动态的过程，需要在字符到来的过程中做判断，不是静态的。。。。继续加油！！！！
