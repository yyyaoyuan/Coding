# 题目描述

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007

# 解答一：暴力求解

只需根据逆序对的定义进行判断即可（该题暴力求解超时）。

```python
class Solution:
    def InversePairs(self, data):
        # write code here
        n = len(data)
        count = 0
        for i in range(n-1):
            for j in range(i+1, n):
                if data[i] >= data[j]:     # 逆序对的定义
                    count += 1
        return count % 1000000007
```

# 解答二：归并排序

这题主要考察的知识点是归并排序，在归并排序的基础上增加一个统计逆序对个数的变量即可。

```python
class Solution:
    def __init__(self):
        self.count = 0

    def InversePairs(self, data):
        # write code here
        self.merge_sort(data)
        return self.count % 1000000007

    def merge_sort(self, data):
        if len(data) <= 1:
            return data
        n = len(data) // 2
        left = self.merge_sort(data[:n])
        right = self.merge_sort(data[n:])
        l, r = 0, 0
        res = []
        while l < len(left) and r < len(right):
            if left[l] < right[r]:
                res.append(left[l])
                l += 1
            else:
                res.append(right[r])
                r += 1
                self.count += len(left) - l    # 核心代码！！！，因为归并排序时，左右两边都是有序的，只要在顺序遍历时出现left[l]大于right[r]的情况，那么left[l]后面的所有数都是大于right[r]的        res += left[l:]
        res += right[r:]
        return res
```

# 感想

这题主要考察归并排序，但是仅仅会归并排序并不一定可以解决该问题，想到了归并排序的思路后，最核心的问题在于计算逆序对的个数，需要根据归并排序的规律进行计算。继续加油！
