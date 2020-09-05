# leetcode 11. 盛最多水的容器(python)

给你 n 个非负整数 a1，a2，…，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。
找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

**说明：**你不能倾斜容器，且 n 的值至少为 2。

# 解答一：暴力解法

将所有数字按照顺序循环遍历两次，然后搜寻所有可能下的面积大小，最后记录最大值的面积即可。

```python
def mySolution(A):
    if not A:
        return 0
    m = 0
    for i in A:
        for j in A:
            if min(i,j)*(A.index(i)-A.index(j)) > m:
                m = min(i,j)*(A.index(i)-A.index(j))
    return m
```

# 解答二：双指针法

设置左右两个指针 left 和 right，盛水容量由矮的高度决定，所以我们每次移动矮的高度。

**这里移动矮的高度的原因在于，只有当移动矮的高度时才有可能寻找到更大的面积，如果移动长的高度，只能寻找到比当前面积还要小的面积**

这里相当于是暴力搜索法的剪枝方法。

```python
def mySolution(A):
    if not A:
        return None
    left = 0
    right = len(A) - 1
    m = 0
    while left <= right:
        if min(A[left], A[right])*(right-left) > m:
            m = min(A[left], A[right])*(right-left)
        if A[left] > A[right]:
            right -= 1
        else:
            left += 1
    return m
```

# 感想

这是今天腾讯一面的面试题，因为之前没有复习到双指针解法，所以并没有回答的很好，希望可以顺利进入下一轮吧～～～
