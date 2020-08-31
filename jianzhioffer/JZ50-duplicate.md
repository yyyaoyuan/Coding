# 题目描述

在一个长度为n的数组里的所有数字都在0到n-1的范围内。
数组中某些数字是重复的，但不知道有几个数字是重复的。
也不知道每个数字重复几次。请找出数组中任意一个重复的数字。
例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。

# 解答一

暴力求解，采用两重for循环进行查找，时间复杂度为O(n^2)。

```python
def duplicate(self, numbers, duplication):
        # write code here
        n = len(numbers)
        for i in range(n):
            for j in range(i+1,n):
                if numbers[i] == numbers[j]:
                    duplication[0] = numbers[i]
                    return True
        return False
```

# 解答二

利用字典，首先循环统计每一个数字出现的次数，然后找到次数不等于1的数字即可，时间复杂度为O(n)。

```python
def duplicate(self, numbers, duplication):
        dict = {}
        for n in numbers:
            if not n in dict:
                dict[n] = 1
            else:
                dict[n] += 1
        for n in numbers:
            if dict[n] != 1:
                duplication[0] = n
                return True
        return False
```
上述方法可以进一步简化，在循环统计每一个数字出现的次数时，如果有count>2，便可以结束了。

```python
def duplicate(self, numbers, duplication):        
        dict = {}
        for n in numbers:
            if not n in dict:
                dict[n] = 1
            else:
                dict[n] += 1
                duplication[0] = n
                return True
        return False
```
# 感想

从这道题中可以学习到字典的使用，以后在面试中如果遇到需要进行计数统计的，可以采用这种方式，一定要掌握住。加油！加油！加油！
