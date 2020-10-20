# 题目描述

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

保证base和exponent不同时为0

# 解答一

暴力求解，这里需要注意到exponent为负时的处理情况。

```python
class Solution:
    def Power(self, base, exponent):
        # write code here
        if base == 0 and exponent == 0:
            return -1
        res = 1
        if exponent > 0:
            for i in range(1, exponent+1):
                res *= base
        elif exponent == 0:
            return 1
        else:
            for i in range(1, abs(exponent)+1):
                res *= base
            res = 1. / res
        return res
```

# 解答二

递归加二分，这里需要用到一个求幂的小规律。

* 如果 n 是偶数的话，Power(x, 2n) = Power(x, n) * Power(x, n)，因此我们对给定 n，只需计算其 n / 2 次幂，再将其相乘即可；
* 如果 n 是奇数的话，例如 n = 5 时，先计算n // 2 = 2，向下取整，之后再计算Power(x, 5) = Power(x, 2) * Power(x, 2) * x。

这样就很容易地把时间复杂度降到了 O(log n) 级别。

```python
class Solution:
    def Power(self, base, exponent):
        if base == 0 and exponent == 0:
            return -1
        if exponent < 0:
            return self.Power(1. / base, -exponent)
        elif exponent == 0:
            return 1
        elif exponent == 1:
            return base
        else:
            return self.Power(base, exponent // 2) ** 2 if exponent % 2 == 0 else self.Power(base, exponent // 2) ** 2 * base # 记住这种写法
```

# 解答三

二分加循环。

```python
def myPower1(x, n):
    if n < 0:
        res = 1 / x
        n = -n
    else:
        res = x
    while n != 1:
        if n % 2 == 0:
            res *= res
        else:
            res = res * res * x
        n = n // 2
    return res
```

# 感想

这道题自己应该怎样也想不出采用递归和二分的思路进行求解，先记住吧，以后遇到类似的题注意找到规律或许可以解决出来。另外，需要学习一个简介的if else写法：
**A if x > y else B**


第四范式面试考到了！！！！幸好复习到了，但是不太好的一点是非递归的循环写法没有写出来，不过自己复习到的面试写出来了还是值得肯定的，继续加油！！！
