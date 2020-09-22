# 题目描述

输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序。

# 解答一：滑动窗口

这道题我怎么都不会想到滑动窗口可以解决！！！思路为：
* 两个起点，相当于动态窗口的两边，根据其窗口内的值的和来确定窗口的位置和大小
* 由于是连续的，差为1的一个序列，那么求和公式是(a0+an)*n/2，*求和公式忘记了！！！
  * 相等，那么就将窗口范围的所有数添加进结果集
  * 如果当前窗口内的值之和小于sum，那么右边窗口右移一下
  * 如果当前窗口内的值之和大于sum，那么左边窗口右移一下


```python
class Solution:
    def FindContinuousSequence(self, tsum):
        # write code here
        left = 1
        right = 2
        res = []
        while left < right:
            tmp = (left+right)*(right-left+1)/2  # (a0+an)*n/2
            if tmp == tsum:
                res.append(list(range(left, right+1)))   # 需要学习一下这种写法
                left += 1            # 重点，这里需要更新一下下标，不然会无限循环！！！
            elif tmp < tsum:
                right += 1
            else:
                left += 1
        return res
```

# 解答二：暴力求解

两重循环进行求解，注意下标的范围。

```python
class Solution:
    def FindContinuousSequence(self, tsum):
        # write code here
        res = []
        for i in range(1, tsum // 2 + 1):
            tmp = i 
            for j in range(i+1, tsum // 2 + 2):
                tmp += j
                if tmp == tsum:
                    res.append(list(range(i,j+1)))     # 需要学习这种写法
        return res
```

# 感想

双指针解法真的很强大，这里自己怎么也不会想到用双指针进行求解，一定要掌握住！！！！另外需要学习的是
列表
