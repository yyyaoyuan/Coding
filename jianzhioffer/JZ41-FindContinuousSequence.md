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
                tmpRes = []
                for i in range(left, right+1):
                    tmpRes.append(i)
                res.append(tmpRes)
                left += 1            # 重点，这里需要更新一下下标，不然会无限循环！！！
            elif tmp < tsum:
                right += 1
            else:
                left += 1
        return res
```

# 解答二：暴力求解

两重循环，一
