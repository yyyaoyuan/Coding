# 题目描述

一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

# 解答一

使用python内置的count函数。

```python
class Solution:
    # 返回[a,b] 其中ab是出现一次的两个数字
    def FindNumsAppearOnce(self, array):
        # write code here
        res = []
        for i in array:
            if array.count(i) == 1:
                res.append(i)
        return res
```

# 解答二

使用python内置的remove函数。

```python
class Solution:
    # 返回[a,b] 其中ab是出现一次的两个数字
    def FindNumsAppearOnce(self, array):
        # write code here
        res = []
        while len(array):
            a = array[0]
            array.remove(a)
            if a not in array:
                res.append(a)
            else:
                array.remove(a)       # 注意这里需要remove一下，因此只能适用于两个重复元素的问题
        return res
```

# 解答三

hashmap解法：利用一个字典进行封装，然后统计每个元素出现的次数。

```python
class Solution:
    # 返回[a,b] 其中ab是出现一次的两个数字
    def FindNumsAppearOnce(self, array):
        # write code here
        dictA = {}
        for a in array:
            if a in dictA:
                dictA[a] += 1
            else:
                dictA[a] = 1
        res = []
        for d in dictA:
            if dictA[d] == 1:
                res.append(d)
        return res
```

# 解答四

位运算：
