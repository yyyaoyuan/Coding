# 盛最多水的容器

给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0) 。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器。

# 解答：双指针法

* 设置两个指针left, right
* 设置一个变量res用来存放最大值
* 如果当前指针所在的面积大于res，对res进行替换
* 否则，如果左边指针指向的高度低于右边，则left += 1，否则right -= 1。

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        if not height:
            return 0
        left = 0
        right = len(height) - 1
        res = 0
        while left <= right:
            if min(height[left], height[right]) * (right - left) > res:
                res = min(height[left], height[right]) * (right - left)
            elif height[left] < height[right]:
                left += 1
            else:
                right -= 1
        return res
```

# 感想

腾讯的面试题，本以为掌握了做题技巧，没想到今天做的时候竟然忘记了，还是要经常复习啊，下次绝对不能再忘记了！！！！加油！！！！
