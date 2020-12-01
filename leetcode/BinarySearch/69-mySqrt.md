# x 的平方根

实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

## 示例 1:

输入: 4
输出: 2

## 示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。

# 解答：二分搜索法

典型的二分搜索问题，注意终止条件，以及左右边界问题。

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        if x == 0 or x == 1:
            return x
        left = 0
        right = x
        while left <= right:              # 这里是闭区间
            mid = (left + right) // 2
            if mid**2 <= x and (mid+1)**2 > x:
                return mid
            elif mid**2 < x:
                left = mid + 1
            elif mid**2 > x:
                right = mid - 1
```

# 感想

自己在这道题上还是有问题，竟然最简单的二分搜索还没有掌握！！！！继续加油！！！
