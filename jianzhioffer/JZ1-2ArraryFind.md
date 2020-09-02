# 题目描述

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。
请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

# 解答一

暴力求解，循环遍历即可。

```python
def Find(self, target, array):
        # write code here
        for i in range(len(array)):            # 注意学习python中行怎么统计（二维数组）
            for j in range(len(array[i])):     # 注意学习python中列怎么统计（二维数组）
                if target == array[i][j]:
                    return True
```

此外，可以利用python的内部接口实现内层循环，这应该是最简洁的版本。

```python
for arr in array:
            if target in arr:                 # 注意学习这种方式，真的很简洁和优美
                return True
        return False
```

# 解答二

对暴力求解进行改进，在内层循环中采用二分查找，将时间复杂度改为O(log N)。

```python
def Find(self, target, array):
        # write code here
        if len(array[0]) == 0:
            return False
        if array[0][0] <= target <= array[-1][-1]:  # 注意学习二维数组最后一个元素的索引
            for arr in array:
                if arr[0] <= target <= arr[-1]:
                    left = 0
                    right = len(arr)-1              # 注意边界的计算 
                    while left <= right:
                        mid = (left + right) // 2
                        if arr[mid] < target:
                            left = mid+1
                        elif arr[mid] > target:
                            right = mid-1
                        else:
                            return True
        return False
```

# 解答三

因为是该二维数组是从左到右递增以及从上倒下递增排列，因此可以从右上角的元素开始进行查找，分为以下三种情况：
* 当要查找数字比右上角数字大时。下移
* 当要查找数字比右下角数字小时，左移
* 当要查找数字等于右下角数字时，返回True

具体代码如下：
```python
def Find(self, target, array):
        # write code here
        r = 0
        l = len(array[0]) - 1  # 注意这是列的大小
        while r <= len(array) - 1  and l >= 0:
            if target > array[r][l]:
                r += 1
            elif target < array[r][l]:
                l -= 1
            else:
                return True
        return False
```

# 感想

这道题需要注意到一些基础的知识点，特别是python中关于二维数组的行和列的计算问题，接下来对上述用到的知识点进行统计：
* rows = len(array)      # 行数
* rows = len(array[0])   # 列数
* array[-1][-1]          # 二维数组最后一个索引
* array[-1]              # 一维数组最后一个索引
