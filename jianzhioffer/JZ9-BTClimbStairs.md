# 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

# 解答一——数学归纳法

该题按照数学思路进行解答，直接计算出总共的跳法，然后编程输入进去，具体如下：
**因为青蛙除最后一个台阶外都有两次选择：跳上去或者不跳上去，对于最后一个台阶，只有一种选择：跳上去，所以总共的跳法为2^(n-1)。**

# 代码
```python
class Solution:
    def jumpFloorII(self, number):
        # write code here
        if number == 0:
            return 0
        return 2 ** (number-1)
```

# 解答二——动态规划

这道问题上述解法虽然简单，确是采用数学的方法进行的求解，并不是采用计算机的思想进行的求解，接下来用计算机的动态规划思想对其进行解决。
具体如下：因为青蛙可以从跳任意高度的台阶，所以n阶台阶所产生的总共跳法为：f(n) = 1 + f(n-1) + f(n-2) + ... + f(1)，其中1表示直接跳上n阶，f(n-1)表示先跳上n-1阶，再直接跳上n阶（一种可能），
f(n-2)以此类推。有了上述通项公式，便可以按照动态规划的思想对其进行求解，即先算出f(1)，在利用f(2) = f(1) + 1算出f(2)，以此类推。这里需要注意的是，需要使用两次循环进行计算。

```python
class Solution:
    def jumpFloorII(self, number):
        # write code here
        if number <= 0:
            return 0
        sum = [0]*(number+1)
        for i in range(1, number+1):
            q = 0
            for j in range(i):
                q += sum[j]
            sum[i] = q + 1
        return sum[number]
```

# 解答三——递归

接下来按照递归的方法进行求解，同样的，根据解答二可以得知n阶台阶所产生的总共跳法为：f(n) = 1 + f(n-1) + f(n-2) + ... + f(1)，根据上述递推公式可得：

```python
class Solution:
    def jumpFloorII(self, number):
        # write code here
        if number <= 0:
            return 0
        if number == 1:
            return 1
        if number == 2:
            return 2
        sum = 0
        for i in range(1, number):
                sum += self.jumpFloorII(i)
        return sum + 1
```

# 解答四——记忆化搜索
接下来对解答三中的递归方法进行改造，采用记忆化搜索的方法节省计算时间，具体如下：
```python
class Solution:
    def jumpFloorII(self, number):
        # write code here
        self.memo = [-1]*(number+1)
        return self.jump(number)
    def jump(self, number):
        if number < 0:
            print('Please input a positive integer')
        if number == 0 or number == 1 or number == 2:
            self.memo[number] = number
            return self.memo[number]
        if self.memo[number] == -1:
            sum = 0
            for i in range(1, number):
                sum += self.jump(i)
            self.memo[number] = sum + 1
            return self.memo[number]
        else:
            return self.memo[number]
```

# 感想

该方法可以采用上述四种方法进行求解，其中速度最慢的是递归迭代，因为使用了大量的重复运算。数学归纳法比较适用于该方法，因为可以总结出通项公式，如果找不到通项公式，则不能采用该方法，因此我认为归纳法的使用范围是比较有限的，并且我个人并不建议练习的时候采用归纳法对问题进行求解，这样不太好训练自己的计算机思维。记忆化搜索和动态规划均是采用了空间换时间的方法，一个是自顶向下进行运算，一个是自底向上进行运算。
