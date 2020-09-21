# 题目描述

汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。
对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,
要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

# 解答一

首先将字符串转成列表，然后利用pop函数和append函数进行求解，最后将结果列表转成字符串。

```python
class Solution:
    def LeftRotateString(self, s, n):
        # write code here
        if not s:
            return ''
        if n == 0 or n == len(s):
            return s
        count = n % len(s)
        A = list(s)
        while count:
            A.append(A.pop(0))
            count -= 1
        return ''.join(A)
```

# 解答二

利用索引，非常巧妙！！！！

```python
class Solution:
    def LeftRotateString(self, s, n):
        # write code here
        if not s:
            return ''
        n = n % len(s)
        return s[n:] + s[:n]    # 非常巧妙的代码，太赞了！！！！！！！
```

# 感想

这里需要学习两个知识点：
* A = ['1', '2'], B = ''.join(A)。B = '12'。    # join函数的使用，如何将字符串列表变成字符串，需要记住，用的很多
* s[n:]+s[:n]    # 这个写法也太优雅了！！！
