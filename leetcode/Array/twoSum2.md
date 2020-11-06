# 两数之和 II - 输入有序数组

给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。

说明:

* 返回的**下标值（index1 和 index2）不是从零开始的**。
* 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

示例:

输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。

# 解答一：双指针法

一前一后两个指针，如果当前两个指针指向的元素之和小于target，前面的指针向前移一位，大于，后面的指针退后一位，相等，则返回向前索引加1后的值。

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left = 0
        right = len(numbers)-1
        while left <= right:
            if numbers[left] + numbers[right] < target:
                left += 1 
            elif numbers[left] + numbers[right] > target:
                right -= 1
            else:
                return [left+1, right+1]
        return []
```

# 解答二：二分搜索法

首先遍历该数组，然后对当前元素后面的数字进行二分搜索。

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        if not numbers:
            return
        n = len(numbers)
        for i in range(n):
            left = i+1
            right = n-1
            while left <= right:
                mid = (left + right) // 2
                if numbers[i] + numbers[mid] < target:
                    left = mid+1           # 特别要注意下标
                elif numbers[i] + numbers[mid] > target:
                    right = mid-1          # 特别要注意下标
                else:
                    return [i+1, mid+1]
        return []
```

# 感想

注意学习双指针方法在这里的使用，非常巧妙，和刚才无序场景下的哈希表一样巧妙。
