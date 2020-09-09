# 题目描述

请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

# 解答一

采用一个新字符串，对原始字符串进行循环遍历，当遇见' '时换成'%20'，即可。

```python
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        if not s:
            return ''
        res = ''
        for i in s:
            if i == ' ':
                i = '%20'
            res += i
        return res
```

# 解答二

首先采用split(' ')函数将字符串分割，然后采用'%20'.join()函数进行连接。

```python
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        if not s:
            return ''
        return '%20'.join(s.split(' '))
```

# 解答三

直接采用replace()函数。

```python
class Solution:
    # s 源字符串
    def replaceSpace(self, s):
        # write code here
        if not s:
            return ''
        return s.replace(' ', '%20')
```
