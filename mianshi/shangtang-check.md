# 题目描述

对一个输入的单词进行拼写检查，假设所有符合要求的单词在一个列表中。要求：不能通过替换，删除来改变输入的单词，只能通过交换字符顺序改变输入的单词。

## 样例:

输入：words = ['dsassfdaa', 'dsassfd', 'dsassdf', 'dsassf']

     instring = 'dsafdss'

输出：['dsassdf', 'dsassfd']

# 解答一：暴力求解

将新来的单词和词典中所有的单词进行一一匹配，如果找到符合条件A的单词，便将该单词装入一个结果列表中，否则返回空列表。

条件A用来判断单词1和单词2是否匹配：遍历单词1的所有字符，判断该字符是否在单词2中，若在便将该字符从单词2中删除，如果不在则返回False，如果遍历结束后单词2为空，则返回True，否则返回False。

```python
class Solution:
    def mySolution(self, words, strs):
        if not strs or strs in words:
            return strs

        res = []
        for w in words:
            if self.isMatch(w, strs):
                res.append(w)
        if res:
            return res
        else:
            return []

    def isMatch(self, w, strs):
        w = list(w)
        strs = list(strs)
        for i in strs:
            if i in w:
                w.remove(i)
            else:
                return False
        if not w:
            return True
        else:
            return False

words = ['cat', 'dog', 'bee', 'act', 'horse', 'cow']
sol = Solution()
s = 'tca'
print(sol.mySolution(words, s))
```

# 解答二：字典树+深度优先遍历+剪枝


