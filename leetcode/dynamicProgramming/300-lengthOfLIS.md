# 最长上升子序列

给定一个无序的整数数组，找到其中最长上升子序列的长度。

示例:

输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
说明:

可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
你算法的时间复杂度应该为 O(n2) 。

# 解答：动态规划

* 状态：dp[i]表示nums[:i]中最长上升子序列的长度
* 初始情况：dp[i] = 1
* 状态转移方程：if nums[i] > nums[j]: dp[i] = max(dp[i], dp[j] + 1)，0 <= j < i

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums:
            return 0
        dp = []
        for i in range(len(nums)):
            dp.append(1)
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
        return max(dp)
```

# 感想

leetcode刷的第三道动态规划题，继续好好刷题，用心来刷题，加油，加油，加油！
