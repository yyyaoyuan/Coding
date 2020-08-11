# 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

# 解答一——记忆化搜索

此题非常经典，本来打算采用先写递归的方式进行，但是发现时间复杂度太高，无法通过测试，因此直接采用记忆化搜索的方法进行解决。
此外，鉴于递归的时间复杂度较高，且记忆化搜索也是在递归的基础上进行修改，因此，以后再遇见类似的题型，只进行记忆化搜索的解答以及动态规划的解答两种。
此问题解决的具体思路如下：因为该青蛙可以向上跳一阶或者两阶，所以跳n阶的方法总数为：f(n) = f(n-1) + f(n-2)，其中f(n-1)表示先跳上n-1阶，然后在直接跳上第n阶；此问题解决的具体思路如下：因为该青蛙可以向上跳一阶或者两阶，所以跳n阶的方法总数为：f(n) = f(n-1) + f(n-2)，其中f(n-2)表示先跳上n-2阶，然后在直接跳上第n阶。
根据上述递归表达式可以得出：
```python
class Solution:
    def jumpFloor(self, number):
        # write code here
        self.memo = [-1]*(number+1)
        return self.jump(number)
    def jump(self, number):
        if number < 0:
            print('Please input a integer')
        if number == 0 or number == 1 or number == 2:
            self.memo[number] = number
            return self.memo[number]
        if self.memo[number] == -1:
            steps = self.jump(number-1) + self.jump(number-2)
            self.memo[number] = steps
            return self.memo[number]
        return self.memo[number]
```

# 解答二——动态规划

按照解答一中的递推公式：f(n) = f(n-1) + f(n-2)，可知需要两个初始值，便可以实现自底向上的计算过程，具体实现如下：
```python
class Solution:
    def jumpFloor(self, number):
        # write code here
        if number < 0:
            print('Please input a positive integer')
        self.memo = [0]*(number+1)
        self.memo[0] = 1
        self.memo[1] = 1
        for i in range(2, number+1):
            self.memo[i] = self.memo[i-1] + self.memo[i-2]
        return self.memo[number]
```

# 解答三——循环求解

此题和**斐波那契数列**的递推公式一样，因此，该题的本质与斐波那契数列一致，接下来对其进行进一步的总结，对其斐波那契数列，python有一种非常简单的实现方法，具体如下：
```python
def jumpFloor(self, number):
        # write code here
        if number < 0:
            print('Please input a positive integer')
        if 0 < number <= 2:
            return number
        t1, t2 = 1, 2
        for _ in range(3, number+1):
            t1, t2 = t2, t1+t2
        return t2
```

# 类似的例题分析：
我们可以用2\*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2\*1的小矩形无重叠地覆盖一个2\*n的大矩形，总共有多少种方法？

## 思路：
因为每一个矩形具有两种覆盖形式（横着或者竖着），那么在覆盖一个2\*n的大矩形的最小一部分时也有两种情况，要么是（1）竖着将最后一个小矩形铺上去，要么是（2）横着将最后一个小矩形铺上去。
* 对于第一种情况，表明此时已经覆盖完该大矩形2\*(n-1)的部分，只剩下2\*1的部分，直接竖着放上去即可，此时对应的方法总数为f(n-1)；
* 对于第二种情况，表明此时已经覆盖完该大矩形2\*(n-2)的部分，且又将一个矩形按照1\*2的方式横着覆盖上去，此时仅剩下1\*2的部分，直接横着覆盖上去即可，此时对应的方法总数为f(n-2)；
* 综上，f(n) = f(n-1) + f (n-2)。
该递推公式与爬台阶以及斐波那契数列一致，即可采用上述代码的任意一种进行求解。

