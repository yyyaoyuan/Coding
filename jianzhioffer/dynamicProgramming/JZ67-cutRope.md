# 题目描述

给你一根长度为n的绳子，请把绳子剪成整数长的m段（m、n都是整数，n>1并且m>1，m<=n），每段绳子的长度记为k[1],...,k[m]。
请问k[1]x...xk[m]可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

# 解答：动态规划

这里需要注意初始值的计算，**最低要先给出n = 3的情况**。

* n<=3的情况，m>1必须要分段，例如：3必须分成1、2；1、1、1 ，n=3最大分段乘积是2
* n>=4的情况，跟n<=3不同，4可以分很多段，比如分成1、3，这里的3可以不需要再分了，因为3分段最大才2，不分就是3。记录最大的。

```python
class Solution:
    def cutRope(self, number):
        # write code here
        if number == 2:
            return 1        # 注意这里是1的原因是因为一定要切割，m>1
        if number == 3:
            return 2        # 注意这里是2的原因是因为一定要切割，m>1
        dp = [0]*(number+1)
        dp[1] = 1
        dp[2] = 2           # 注意这里是2的原因是n > 2，那么长度为2的可以不切割，所以最大为2
        dp[3] = 3           # 注意这里是3的原因是n > 3，那么长度为3的可以不切割，所以最大为3；注意长度为4的时候不适用！！！！！    
        maxVal = 0
        for i in range(4, number+1):
            for j in range(1, i // 2 + 1):            # 注意这里只需算到一半即可。。。
                maxVal = max(maxVal, dp[j]*dp[i-j])
            dp[i] = maxVal
        return dp[number]
```

# 感想

这道题，目前的自己肯定是做不出来的，接下来系统复习和练习动态规划，加油！！！！！！！
