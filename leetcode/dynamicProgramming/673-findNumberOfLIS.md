# 最长递增子序列的个数

给定一个未排序的整数数组，找到最长递增子序列的个数。

## 示例 1:

输入: [1,3,5,4,7]

输出: 2

解释: 有两个最长递增子序列，分别是 [1, 3, 4, 7] 和[1, 3, 5, 7]。

# 解答：动态规划

* 状态：dp[i]代表数组arr[:i]的最长递增子序列（LIS）的长度，res[i]代表数组数组arr[:i]的LIS组合的长度
* 初始值：dp[i] = 1, res[i] = 1
* 状态转移方程：if nums[i] > nums[j]: 
  * if dp[j] + 1 > dp[i]: dp[i] = dp[j] + 1, res[i] = res[j]  % 此时意味着第一次找到长度为dp[j]+1的这个组合
  * if dp[j] + 1 > dp[i]: dp[i] = dp[j] + 1, res[i] = res[j]  % 此时意味着不是第一次找到长度为dp[j]+1的这个组合
  
```python
class Solution:
    def findNumberOfLIS(self, nums: List[int]) -> int:
        if not nums:
            return 0
        dp = []
        res = []
        for i in range(len(nums)):
            dp.append(1)
            res.append(1)
            for j in range(i):
                if nums[i] > nums[j]:
                    if dp[j] + 1 > dp[i]:
                        dp[i] = dp[j] + 1
                        res[i] = res[j]
                    elif dp[j] + 1 == dp[i]:
                        res[i] += res[j]

        max_len = max(dp)
        ans = 0
        for i in range(len(res)):
            if dp[i] == max(dp):
                ans += res[i]
        return ans
```
 # 感想
 
 在做完[最长递增子序列题][https://github.com/yyyaoyuan/Coding/blob/master/leetcode/dynamicProgramming/300-lengthOfLIS.md]以后，应该要有能力解决该问题，但是自己还是没有能独立想出解决方案，还是差很远，继续加油！！！！
 
 **此题的关键在于如何判断是否最长递增子序列是第一次出现：
 
 * if dp[j] + 1 > dp[i]，表示第一次出现
 * if dp[j] + 1 == dp[i]，表示不是第一次出现
 
 
