# 题目描述

输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

# 解答一

暴力求解：循环两次寻找，其中需要注意统计满足条件的两个数的乘积，每次根据乘积是否变小进行相应的更新。

```python
def FindNumbersWithSum(self, array, tsum):
        # write code here
        n = len(array)
        minN = 10000
        count = 0
        for i in range(n-1):
            for j in range(i+1, n):
                if array[i] + array[j] == tsum and array[i]*array[j] < minN:
                    count += 1
                    res = []                   # 这里需要注意每次都需要将列表清空，然后装入新的满足条件的元素值
                    res.append(array[i])
                    res.append(array[j])
                    minN = array[i]*array[j]
        if count == 0:                         # 这里需要注意如果循环结束都没有找到，需要返回空值
            return []
        return res
```

# 解答二

双指针求解：

假设：若b>a,且存在，
a + b = s;
(a - m ) + (b + m) = s
则：(a - m )(b + m)=ab - (b-a)m - m*m < ab；说明外层的乘积更小
也就是说依然是左右夹逼法！！！只需要2个指针
1.left开头，right指向结尾
2.如果和小于sum，说明太小了，left右移寻找更大的数
3.如果和大于sum，说明太大了，right左移寻找更小的数

```python
def FindNumbersWithSum(self, array, tsum):
        left = 0
        right = len(array)-1   # 这里需要注意是总共的长度减去1，因为python是从0开始索引的
        while left < right:
            if array[left] + array[right] < tsum:
                left += 1
            elif array[left] + array[right] > tsum:
                right -= 1
            else:
                res = []
                res.append(array[left])
                res.append(array[right])
                return res
        return []
```
