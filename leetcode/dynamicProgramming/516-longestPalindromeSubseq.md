# 最长回文子序列

给定一个字符串 s ，找到其中最长的回文子序列，并返回该序列的长度。可以假设 s 的最大长度为 1000 。

## 示例 1:

输入: "bbbab"

输出: 4

# 解答：动态规划

* 状态：在子串 s[i..j] 中，最长回文子序列的长度为 dp[i][j]。
* 初始情况：dp[i][i] = 1, dp[i][j] = 0 if i < j
* 状态转移方程: 
  * if s[i] == s[j]: dp[i][j] = dp[i + 1][j - 1] + 2
  * else: dp[i][j] = max(dp[i + 1][j], dp[i][j - 1])
  
```python
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        if not str:
            return 0
        n = len(s)
        dp = [[0 for i in range(n)] for j in range(n)]
        
        for i in range(n-1, -1, -1):     # 注意i是反着遍历！！！
            dp[i][i] = 1                 # 注意初始化
            for j in range(i+1,n):
                if s[i] == s[j]:
                    dp[i][j] = dp[i+1][j-1] + 2
                else:
                    dp[i][j] = max(dp[i+1][j], dp[i][j-1])
        return dp[0][-1]
```
