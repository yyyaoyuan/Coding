# 题目描述

牛客最近来了一个新员工Fish，每天早晨总是会拿着一本英文杂志，写些句子在本子上。同事Cat对Fish写的内容颇感兴趣，有一天他向Fish借来翻看，但却读不懂它的意思。例如，“student. a am I”。后来才意识到，这家伙原来把句子单词的顺序翻转了，正确的句子应该是“I am a student.”。Cat对一一的翻转这些单词顺序可不在行，你能帮助他么？

# 解答一

首先将字符串按照空格进行划分，然后逆序依次追加到结果数组中，最后连接成新字符串。

```python
class Solution:
    def ReverseSentence(self, s):
        # write code here
        if not s:
            return s
        tmp = s.split(' ')
        res = []
        for i in range(len(tmp)-1, -1, -1):
            res.append(tmp[i])
        return ' '.join(res)
```

# 解答二

思路和解答一相同，不过可以利用列表的逆序输出语句（[::-1]）直接输出。

```python
class Solution:
    def ReverseSentence(self, s):
        return ' '.join(s.split(' ')[::-1]) if s else s  # 这种写法
```
