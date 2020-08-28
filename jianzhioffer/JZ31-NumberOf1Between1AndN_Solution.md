#题目描述

求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。
ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的**求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）**。

# 解答一

这个题很多人的解答方案是找规律，不过我看了一下，有点懵，现在时间有限，直接按照暴力方法来解决，也算是学习一下python的用法。

思路：利用二重循环来分别判断，第一重循环遍历所有的数字，第二重循环将所有的数字转换成字符串然后统计'1'出现多少次。

```python
class Solution:
    def NumberOf1Between1AndN_Solution(self, n):
        # write code here
        count = 0
        for i in range(n+1):
            for j in str(i):
                if j == '1':
                    count += 1
        return count
```

# 解答二

利用一重循环，加上python的内部函数解决，首先对所有的数字进行遍历，然后将每个数字转换成字符串，利用**list.count('1')**来统计'1'出现的次数。

```python
def NumberOf1Between1AndN_Solution(self, n):
        # write code here
        count = 0
        for i in range(n+1):
            count += str(i).count('1')
        return count
```

# 感想

这道题找规律，如果面试中遇见，先写出暴力的就行了，找规律我感觉不好理解，并且感觉这样的题意义不大，这里出现了**一个错误是rang(n+1)而不应该是rang(n)**，下次一定要注意！！！！！
另外，**记住list.count(obj)的用法。**
