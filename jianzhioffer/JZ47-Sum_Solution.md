# 题目描述

求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

如果a and b，**a, b都不为0返回b**；a为0返回a也就是0；a不为0，b为0返回b，也就是0。

# 解答一

这个问题主要难点在于不能使用语句，所以需要运用到逻辑运算符and进行短路操作。

```python
class Solution:
    def Sum_Solution(self, n):
        # write code here
        return n and n + self.Sum_Solution(n-1)
```

# 感想

这道题主要学习逻辑运算符and的使用。
