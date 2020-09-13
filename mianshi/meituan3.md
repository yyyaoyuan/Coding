# 美团第三题

# 题目描述：

小团和小美正在玩一个填数游戏，这个游戏是给一个等式，其中有一些数被挖掉了，你需要向其中填数字，使得等式成立。

比如 ——— + 12 = 34，那么横线天的一定是22.

现在，这个游戏到了最后一关，这一关的等式很奇特：_+_+...+_=n
这里可以填任意多个正整数（甚至可能是1个），只要这些数的和等于n即可。
但是，有一个额外的限制，填入的所有数必须小于等于k，大于等于1，填入的数的最大值必须大于等于d。
请你计算，有多少个不同的等式满足这些限制。由于答案可能很大，请将答案mod(998244353)后输出。

## 输入描述

输入包含三个数n, k, d (1 <= d <= k <= n <= 1000)

## 输出描述

输出包含一行，即方案数。

## 样例输入

5 3 2

## 样例输出

12

## 提示

样例解释：
2 + 3 = 5
3 + 2 = 5
1 + 1 + 3 = 5
1 + 3 + 1 = 5
3 + 1 + 1 = 5
1 + 2 + 2 = 5
2 + 1 + 2 = 5
2 + 2 + 1 = 5
1 + 1 + 1 + 2 = 5
1 + 1 + 2 + 1 = 5
1 + 2 + 1 + 1 = 5
2 + 1 + 1 + 1 = 5
共12种填法。

# 解答
```python
import collections
dic = collections.defaultdict(int)
def dfs(n,k,d,res, maxval):
    if res > n:
       return 0
    if res == n and maxval >= d:
        return 1
    key = str(n - res) + ' ' + str(maxval >= d)
    if key in dic:
        return dic[key]
    count = 0
    for i in range(1, k+1):
        res += i
        tmp = maxval
        if maxval < i:
            maxval = i
        count += dfs(n, k, d, res, maxval)
        res -= 1
        maxval = tmp
    dic[key] = count
    return count
n, k, d = [int(i) for i in input().split()]
r = [0]
print(dfs(n,k,d,0,0))
```

# 感想

这里需要学习两点，剪枝的使用，以及输入输出

