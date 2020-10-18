# 题目描述

在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.（从0开始计数）

# 解答一：hash

首先遍历所有字符，并利用一个字典存储每个字符出现的次数；然后再遍历所有字符，寻找到字典中相应字符个数为1的字符，输出该字符的索引即可。

```python
class Solution:
    def FirstNotRepeatingChar(self, s):
        # write code here
        if not s:
            return -1
        dic = {}
        for i in s:
            if i not in dic:
                dic[i] = 1
            else:
                dic[i] += 1
        for d in s:                  # 注意这里是遍历字符串，不能遍历字典，因为python 2.7中默认对字典排序，但是python 3中不会进行此操作，所以python 3可以遍历字典
            if dic[d] == 1:
                return s.index(d)
        return -1
```

# 解答二：利用该字符的第一次出现的索引是否和最后一次出现的索引相同进行判断，非常巧妙！！！

遍历所有字符串，寻找到第一个字符，满足第一次出现的索引和最后一次出现的索引相同，即可返回该字符的索引。

```python
class Solution:
    def FirstNotRepeatingChar(self, s):
        # write code here
        if not s:
            return -1
        for i in s:
            if s.index(i) == s.rindex(i):    # 核心代码，非常简介和优美！！！
                return s.index(i)
        return -1
```

# 感想

该题和之前做的一道判断数字出现一次是类似的题目，朴素的解法是采用哈希表，记录每个字符出现的次数。巧妙的解法是**判断第一次出现的索引是否和最后一次出现的索引相同**，一定要记住这种解决方案！！！

需要学习的知识点：
* python 2.7 会默认对字典中的 key 进行排序，python 3 不会，需要记住！！！
* python中判断字符串中某个字符最后一次出现的索引函数是 rindex (e.g., '11234'.rindex('2'))，需要记住！！！
