# 题目描述

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4。

# 解答一：冒泡排序

利用冒泡排序的思想，注意截断，截断时需要注意边界条件。

```python
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        # write code here
        n = len(tinput)
        res = []
        if n == 0 or n < k or k == 0:         # 注意这里需要判断k==0
            return res
        for i in range(n-1, -1, -1):          # 注意这里是n-1, -1, -1
            for j in range(i):
                if tinput[j+1] > tinput[j]:
                    tinput[j+1], tinput[j] = tinput[j], tinput[j+1]
            res.append(tinput[i])
            if len(res) == k:
                return res
```

# 解答二：快速排序

```python
class Solution:
    def GetLeastNumbers_Solution(self, tinput, k):
        # write code here
        def quickSort(lst):
            if not lst:
                return lst
            p = lst[0]
            l = quickSort([i for i in lst[1:] if i < p])
            r = quickSort([i for i in lst[1:] if i >= p])
            return l + [p] + r 
        if not tinput or k > len(tinput):
            return []
        res = quickSort(tinput)
        return res[:k]
```
