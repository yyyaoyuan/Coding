# 寻找某个数在数组中是第几大

给定一个无序数组，和数组中一个数字，判断该数字是数组中第几大的数字。（假设数组中没有重复的数字）

# 解答：计数

遍历一边数组，统计有多少个数字比该数字大，然后再加1便是结果。

```python
class Solution:
    def findTargetInArr(arr, target):
        if not arr:
            return -1
        res = 0
        for i in arr:
            if i > target:
               count += 1
        return count + 1
```

# 感想

旷视面试遇到了这道题，在面试官的提示下写出了O(n)复杂度的算法，加油！！！！！！！
