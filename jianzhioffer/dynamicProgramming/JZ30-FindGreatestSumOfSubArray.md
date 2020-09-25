# 题目描述

HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。
今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。
但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？
例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。
给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1)

# 解答一：暴力求解

两重循环进行遍历所有可能的和，记录结果最大的。

```python
class Solution:
    def FindGreatestSumOfSubArray(self, array):
        # write code here
        n = len(array)
        if n == 1:
            return array[0]
        maxVal = -10000
        for i in range(0, n):
            sumVal = array[i]
            maxVal = max(maxVal, sumVal)
            for j in range(i+1, n):
                sumVal += array[j]
                maxVal = max(maxVal, sumVal)
        return maxVal
```

# 解答二：动态规划

F(i)：以array[i]为末尾元素的子数组的和的最大值，子数组的元素的相对位置不变；
* F(i) = max(F(i-1) + array[i], array[i])

res：所有子数组的和的最大值；
* res = max(res，F(i))。

```python
class Solution:
    def FindGreatestSumOfSubArray(self, array):
        # write code here
        resVal = array[0]   //记录当前所有子数组的和的最大值
        maxVal = array[0]   //包含array[i]的连续数组最大值
        for i in range(1, len(array)):
            maxVal = max(maxVal+array[i], array[i])
            resVal = max(resVal, maxVal)
        return resVal
```

# 感想

这题还是不知道怎么用动态规划进行求解，动态规划两个最主要的元素，状态和状态转移方程。
* 状态：F(i)：以array[i]为末尾元素的子数组的和的最大值，子数组的元素的相对位置不变；res：所有子数组的和的最大值
* 状态转移方程：F(i) = max(F(i-1) + array[i], array[i])；res = max(res，F(i))
