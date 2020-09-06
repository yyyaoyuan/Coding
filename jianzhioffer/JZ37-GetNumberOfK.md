# 题目描述

统计一个数字在升序数组中出现的次数。

# 解答一

整体思路是，先找到第一个目标数字出现的索引idxFirst，再找到最后一个目标数字出现的索引idxLast，然后次数=idxFirst-idxLast+1。

这里的问题是在于寻找idxFirst和idxLast，利用二分查找的思想进行解决。

需要特别注意判断条件。

```python
class Solution:
    def GetFirstK(self, data, k):
        low = 0
        high = len(data) - 1
        while low <= high:
            mid = (low + high) // 2
            if data[mid] < k:
                low = mid + 1
            elif data[mid] > k:
                high = mid - 1
            else:
                if mid == low or data[mid - 1] < k:  # 重点：当到list[0]或不为k的时候跳出函数
                    return mid
                else:
                    high = mid - 1
        return -1
    def GetLastK(self, data, k):
        low = 0
        high = len(data) - 1
        while low <= high:
            mid = (low + high) // 2
            if data[mid] > k:
                high = mid - 1
            elif data[mid] < k:
                low = mid + 1
            else:
                if mid == high or data[mid + 1] > k: # 重点：当到list[-1]或不为k的时候跳出函数
                    return mid
                else:
                    low = mid + 1
        return -1
    def GetNumberOfK(self, data, k):
        idxFirst = self.GetFirstK(data, k)
        idxLast = self.GetLastK(data, k)
        if idxLast >= idxFirst and idxLast != -1:
            return idxLast - idxFirst + 1
        else:
            return 0
```

# 感想

这道题整体的思路了解了，但是最后
