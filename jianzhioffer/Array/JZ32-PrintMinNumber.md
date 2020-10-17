# 题目描述

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

# 解答

解决该问题的最核心思想是找到规律进行排序，相当于高级的排序算法。

核心思想：比较两个字符串s1, s2大小的时候，先将它们拼接起来，比较s1+s2,和s2+s1那个大，如果s1+s2大，那说明s2应该放前面，所以按这个规则，s2就应该排在s1前面。

## 选择排序

```python
class Solution:
    def PrintMinNumber(self, numbers):
        # write code here
        if not numbers:
            return ''
        n = len(numbers)
        
        for i in range(n):           # 选择排序核心代码块
            for j in range(i+1, n):
                if int(str(numbers[i])+str(numbers[j])) > int(str(numbers[j])+str(numbers[i])):
                    numbers[i], numbers[j] = numbers[j], numbers[i]
        
        res = ''
        for i in numbers:
            res += str(i)
        return int(res)
```

## 冒泡排序

```python
class Solution:
    def PrintMinNumber(self, numbers):
        # write code here
        if not numbers:
            return ''
        n = len(numbers)
        
        for i in range(n-1, 0, -1):                     # 冒泡排序核心代码块
            for j in range(i):
                if int(str(numbers[j])+str(numbers[j+1])) > int(str(numbers[j+1])+str(numbers[j])):
                    numbers[j], numbers[j+1] = numbers[j+1], numbers[j]
                    
        res = ''
        for i in numbers:
            res += str(i)
        return int(res)
```

# 感想

解这道题最主要的关键是找到规律进行排序，这个真的很难。。。。。。。。。。加油！！！
