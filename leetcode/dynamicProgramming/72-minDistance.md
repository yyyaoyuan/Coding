# 编辑距离

给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数。

你可以对一个单词进行如下三种操作：

* 插入一个字符
* 删除一个字符
* 替换一个字符

## 示例 1：

输入：word1 = "horse", word2 = "ros"

输出：3

解释：

horse -> rorse (将 'h' 替换为 'r')

rorse -> rose (删除 'r')

rose -> ros (删除 'e')

# 解答：动态规划

* 状态： dp[i][j] 代表 word1 的前 i 个字母和 word2 的前 j 个字母之间的编辑距离。
* 初始值：dp[i][0] = i
* 状态转移方程：
  * if word1[i-1] == word[j-1]: dp[i][j] = dp[i-1][j-1]                  % 此时不需要额外的操作
  * else: dp[i][j] = min(dp[i-1][j], min(dp[i][j-1], dp[i-1][j-1])) + 1  % 此时需要进行一步操作，所以加1

*注意：dp数组的大小是m+1行，n+1列的，这道题和最长公共子序列类似*

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        m, n = len(word1), len(word2)
        dp = [[0 for i in range(n+1)] for j in range(m+1)]
        for i in range(m+1):
            dp[i][0] = i      # 这是初始状态
        for j in range(n+1):
            dp[0][j] = j      # 这是初始状态
        for i in range(1,m+1):
            for j in range(1,n+1):
                if word1[i-1] == word2[j-1]:       # 注意这里是i-1，j-1，原因是因为i的变化范围是[1, m+1]，j的变化范围是[1, n+1]
                    dp[i][j] = dp[i-1][j-1]        # 注意这里不需要加1
                else:
                    dp[i][j] = min(dp[i][j-1], min(dp[i-1][j], dp[i-1][j-1])) + 1  # 注意这里需要加1
        return dp[-1][-1]
```

# 感想

常见的动态规划面试题，非常基础的动归问题，加油！！！
