# 题目描述
LL今天心情特别好,因为他去买了一副扑克牌,发现里面居然有2个大王,2个小王(一副牌原本是54张^_^)...他随机从中抽出了5张牌,想测测自己的手气,
看看能不能抽到顺子,如果抽到的话,他决定去买体育彩票,嘿嘿！！“红心A,黑桃3,小王,大王,方片5”,“Oh My God!”不是顺子.....LL不高兴了,
他想了想,决定大\小 王可以看成任何数字,并且A看作1,J为11,Q为12,K为13。
上面的5张牌就可以变成“1,2,3,4,5”(大小王分别看作2和4),“So Lucky!”。LL决定去买体育彩票啦。 

现在,要求你使用这幅牌模拟上面的过程,然后告诉我们LL的运气如何，**如果牌能组成顺子就输出true，否则就输出false。为了方便起见,你可以认为大小王是0。**

# 解答一

分成三种情况：
* 数组为空，返回Flase；
* 不包含0，只要数组有重复便输出False，否则判断数组的最大值和最小值之差是否为4，是则返回True，否则返回False；
* 包含0，只要数组有非0的重复元素便输出False，否则数组的最大值和**最小值（不包括0）**之差是否小于等于4，是则返回True，否则返回False。

```python
class Solution:
    def IsContinuous(self, numbers):
        # write code here
        if not numbers:
            return False
        if 0 not in numbers:
            tmp = {}
            for n in numbers:
                if n in tmp:      # 注意这里字典计数的用法，使用n in tmp来判断该键值是否已经存在
                    tmp[n] += 1
                    return False
                else:
                    tmp[n] = 1
            minVal = min(numbers)
            maxVal = max(numbers)
            return maxVal - minVal == 4
        else:
            tmp = {}
            for n in numbers:
                if n in tmp and n != 0:     # 注意这里字典计数的用法，使用n in tmp来判断该键值是否已经存在 
                    tmp[n] += 1
                    return False
                elif n in tmp and n == 0:    # 注意这里字典计数的用法，使用n in tmp来判断该键值是否已经存在
                    tmp[n] += 1
                else:
                    tmp[n] = 1
            count = tmp[0]
            maxVal = max(numbers)
            minVal = 14
            for n in numbers:
                if n != 0 and n < minVal:
                    minVal = n 
            return maxVal - minVal <= 4
```

# 解答二

改进第一种情况，将不包含0和包含0的情况一起进行统计。

```python
class Solution:
    def IsContinuous(self, numbers):
        # write code here
        if not numbers:
            return False
        tmp = {}
        for n in numbers:
            if n in tmp and n != 0:      # 注意这里字典的用法
                return False
            elif n in tmp and n == 0:    # 注意这里字典的用法
                tmp[n] += 1
            else:
                tmp[n] = 1
        maxVal = max(numbers)
        minVal = 14
        for n in numbers:
            if n != 0 and n < minVal:
                minVal = n
        return maxVal - minVal <= 4
```

# 感想

这里主要需要学习的是字典计数的用法，之前用过了，但是这里却忘记了， 利用如下语句判断键值是否存在于字典中：
* if n in tmp
