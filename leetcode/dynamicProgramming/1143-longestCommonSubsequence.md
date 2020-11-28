# 最长公共子序列

给定两个字符串 text1 和 text2，返回这两个字符串的最长公共子序列的长度。

一个字符串的 子序列 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。
例如，"ace" 是 "abcde" 的子序列，但 "aec" 不是 "abcde" 的子序列。两个字符串的「公共子序列」是这两个字符串所共同拥有的子序列。

若这两个字符串没有公共子序列，则返回 0。

## 示例 1:

输入：text1 = "abcde", text2 = "ace" 
输出：3  
解释：最长公共子序列是 "ace"，它的长度为 3。

# 解答：动态规划

* 状态：dp[i][j] 表示 text1[1...i]和text2[1...j]最长公共子序列的长度
* 初始情况：dp[0][...]和dp[...][0]初始化为0，表示一个字符串为空时与另一个字符串公共子序列的长度。
* 状态转移方程：dp[i+1][j+1]有两种情况
  * if text1[i] == text2[j]: dp[i+1][j+1] = dp[i][j] + 1
  * else: dp[i+1][j+1] = max(dp[i][j+1], dp[i+1][j])
* 最后的结果为dp[-1][-1]，需要特别注意的是，**dp数组是m+1行，n+1列**。


```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        if not text1 or not text2:
            return 0
        m, n = len(text1), len(text2)
        dp = [[0 for i in range(n+1)] for j in range(m+1)]
        for i in range(1, m+1):
            for j in range(1, n+1):
                if text1[i-1] == text2[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        return dp[-1][-1]
````

# 感想

这是一道非常经典的动态规划题，上周微软面试时遇到了一道类似的题目，但是自己没有任何头绪，现在把这种类型的题目好好的练习一下，继续加油！！！
