# 题目描述

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。
例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

# 解答一：使用内部函数求解

使用count函数求解。

```python
class Solution:
    def MoreThanHalfNum_Solution(self, numbers):
        # write code here
        for n in numbers:
            if numbers.count(n) > len(numbers) // 2:
                return n
        return 0
```

# 解答二：hashMap

使用一个字典进行统计次数，**注意数组长度为1的情况**。

```python
class Solution:
    def MoreThanHalfNum_Solution(self, numbers):
        # write code here
        if len(numbers) == 1:          # 需要特别注意此种情况，边界条件的判断，非常重要！！！！
            return numbers[0]
        dic = {}
        for n in numbers:
            if n in dic:               # 复习字典的使用
                dic[n] += 1
                if dic[n] > len(numbers) // 2:
                    return n
            else:
                dic[n] = 1
        return 0
```

