# 最长回文子串

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

## 示例 1：

输入: "babad"

输出: "bab"

注意: "aba" 也是一个有效答案。

## 示例 2：

输入: "cbbd"

输出: "bb"

# 解答：动态规划

* 状态：dp[i][j]代表s[i][j]是否为回文串，1是，0不是
* 初始值：对角线的元素全部都是1
* 状态转移方程：
  * if s[i] == s[j]: if j - i < 3: dp[i][j] = 1
  * else: dp[i][j] = dp[i+1][j-1]
 
 *注意使用两个变量记录一下最长回文串的长度，以及起始位置*
 
 ```python
 class Solution:
    def longestPalindrome(self, s: str) -> str:
        if not str:
            return ''
        n = len(s)
        max_len = 1
        start = 0
        dp = [[0]*n for _ in range(n)]

        for i in range(n):
            dp[i][i] = 1

        for i in range(n-1, -1, -1): # 遍历顺利和最长回文子序列一致
            for j in range(i+1, n):
                if s[i] == s[j]:
                    if j - i < 3:      # 注意这个判断语句！！！！
                        dp[i][j] = 1
                    else:
                        dp[i][j] = dp[i+1][j-1]
                else:
                    dp[i][j] = 0
            
                if dp[i][j]:          # 对于每一个是回文子串的s[i][j]进行判断，是否是当前最长的！！！！
                    cur_len = j - i + 1
                    if cur_len > max_len:
                        max_len = cur_len
                        start = i 
        return s[start:start+max_len]  # 注意这里不需要start+max_len-1，因为python列表索引[start:start+max_len]正好到达start+max_len-1！！！
 ```
 
 # 感想：
 
 最长回文子串返回子串，感觉最难的一点是又加了一个j-i是否小于3的判断，以及遍历的顺序，是先遍历的列，后遍历的行！！！！
