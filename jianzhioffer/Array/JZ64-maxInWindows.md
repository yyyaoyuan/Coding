# 题目描述

给定一个数组和滑动窗口的大小，找出所有滑动窗口里数值的最大值。例如，如果输入数组{2,3,4,2,6,2,5,1}及滑动窗口的大小3，那么一共存在6个滑动窗口，他们的最大值分别为{4,4,6,6,6,5}； 针对数组{2,3,4,2,6,2,5,1}的滑动窗口有以下6个： {[2,3,4],2,6,2,5,1}， {2,[3,4,2],6,2,5,1}， {2,3,[4,2,6],2,5,1}， {2,3,4,[2,6,2],5,1}， {2,3,4,2,[6,2,5],1}， {2,3,4,2,6,[2,5,1]}。
窗口大于数组长度的时候，返回空。

# 解答一：滑动窗口法

利用过两个指针记录满足条件的数组，然后利用max函数进行计算，注意边界条件的控制。

```python
class Solution:
    def maxInWindows(self, num, size):
        # write code here
        if size == 0 or not num:
            return []
        if size > len(num):
            return []
        res = []
        for i in range(len(num)):
            j = i + size - 1
            if j < len(num):
                res.append(max(num[i:j+1]))
        return res
```

# 解答二：双向队列法

用一个双端队列，队列第一个位置保存当前窗口最大值的索引，当窗口滑动一次
* 判断当前索引指向的最大值是否过期
* 新增加的值从队尾开始比较，把所有比他小的值丢掉

```python
class Solution:
    def maxInWindows(self, num, size):
        # write code here
        if not num or size <= 0:
            return []
        queue, res = [], []
        for i in range(len(num)):
            if len(queue) > 0 and queue[0] < i - size + 1:
                queue.pop(0)
            while len(queue) > 0 and num[queue[-1]] < num[i]:
                queue.pop()
            queue.append(i)
            if i >= size - 1:
                res.append(num[queue[0]])
        return res
```

# 感想

这道题应该主要考察双向队列的使用，队列头
