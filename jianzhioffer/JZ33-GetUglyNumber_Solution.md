# 题目描述

把只包含质因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。

# 解答一

一个丑数的因子只有2,3,5，那么丑数p = 2^x * 3^y * 5^z，换句话说一个丑数一定由另一个丑数乘以2或者乘以3或者乘以5得到。
因此可以使用三个列表分别进行存储，具体步骤如下：
* 首先按照顺序找最小的丑数，按照定义为1；
* 然后分别将1*2，1*3，1*5存入三个数组，并从中找到最小值，存入结果列表，并将最小值从3个列表中移除；
* 然后将当前的最小值在分别乘上2，3，5，存入上述三个数组；
* 上述过程重复N次即可得到结果。

```python
class Solution:
    def GetUglyNumber_Solution(self, index):
        # write code here
        if index < 7:
            return index
        res = []
        tmp2 = [1]   # 当前丑数乘2的结果列表
        tmp3 = [1]   # 当前丑数乘3的结果列表
        tmp5 = [1]   # 当前丑数乘5的结果列表 
        for i in range(0, index):
            minNum = min(min(tmp2), min(min(tmp3), min(tmp5)))  # 寻找最小值
            res.append(minNum)   # 将当前最小值存入结果列表
            if minNum in tmp2:
                tmp2.remove(minNum) # 移除最小值
            if minNum in tmp3:
                tmp3.remove(minNum)
            if minNum in tmp5:
                tmp5.remove(minNum)
            tmp2.append(minNum*2)  # 计算当前丑数乘2的结果，因为丑数是有序的，所以按照顺序进行计算不会出现遗漏
            tmp3.append(minNum*3)
            tmp5.append(minNum*5)
        return res[-1]
```

# 解答二

三指针解法，节省空间

```python
class Solution:
    def GetUglyNumber_Solution(self, index):
        # write code here
        if index < 7:
            return index
        res = [1]
        t2 = t3 = t5 = 0
        for i in range(1, index):
            minNum = min(res[t2]*2, min(res[t3]*3, res[t5]*5))
            res.append(minNum)
            if res[i] == res[t2] * 2:
                t2 += 1
            if res[i] == res[t3] * 3:
                t3 += 1
            if res[i] == res[t5] * 5:
                t5 += 1
        return res[index-1]
```
