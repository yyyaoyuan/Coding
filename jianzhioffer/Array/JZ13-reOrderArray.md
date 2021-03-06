# 题目描述

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

# 解答一

采用两个列表，一个用来装奇数，一个用来装偶数，然后拼接即可。

```python
class Solution:
    def reOrderArray(self, array):
        # write code here
        if not array:
            return []
        resOdd = []
        resEven = []
        for i in array:
            if i % 2 != 0:
                resOdd.append(i)
            else:
                resEven.append(i)
        return resOdd+resEven
```

# 解答二

采用冒泡排序的思想，两重循环，第一重循环从头到尾遍历所有的元素，第二重循环从后往前遍历，遇到先偶后奇的便交换位置。

```python
class Solution:
    def reOrderArray(self, array):
        # write code here
        if not array:
            return []
        for i in range(len(array)):
            for j in range(len(array)-1, i, -1):               # 这里特别需要注意索引
                if array[j-1] % 2 == 0 and array[j] % 2 != 0:  # 先偶后奇
                    array[j], array[j-1] = array[j-1], array[j]
        return array
```

采用冒泡排序的思想，两重循环，第一重循环从尾到头遍历所有的元素，第二重循环从前往后遍历，遇到先偶后奇的便交换位置。

```python
class Solution:
    def reOrderArray(self, array):
        # write code here
        if not array:
            return []
        for i in range(len(array), 0, -1):                   # 这里要特别注意索引
            for j in range(i-1):                             # 这里要特别注意索引
                if array[j] % 2 == 0 and array[j+1] % 2 != 0:
                    array[j], array[j+1] = array[j+1], array[j]
        return array
```

# 感想

这里用到了冒泡排序的思想，趁着复习一下，这里的关键一定要弄清楚索引的边界，面试的时候一定不要弄错边界情况。
最后，当编译通过的时候还是很有成就感的，并且感觉编程还是很有意思的，好好学习，加油！加油！加油！
