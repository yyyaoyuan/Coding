# 题目描述

对一个输入的单词进行拼写检查，假设所有符合要求的单词在一个列表中。要求：不能通过替换，删除来改变输入的单词，只能通过交换字符顺序改变输入的单词。

## 样例:

输入：words = ['cat', 'dog', 'bee', 'act', 'horse', 'cow']
     s = 'tca'

输出：['cat', 'act']

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

首先利用字典中的所有单词进行建树，然后对新输入单词的所有组合进行查找，**这里需要注意剪枝，当发现某些前缀字符不在字典树上时，便可以排序以该前缀字符开头的所有组合**。

```python
class Trie:
    # word_end = -1
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = {}
        self.word_end = -1

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: void
        """
        curNode = self.root
        for c in word:
            if not c in curNode:
                curNode[c] = {}
            curNode = curNode[c]

        curNode[self.word_end] = True

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        curNode = self.root
        for c in word:
            if not c in curNode:
                return False
            curNode = curNode[c]

        # Doesn't end here
        if self.word_end not in curNode:
            return False

        return True

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        curNode = self.root
        for c in prefix:
            if not c in curNode:
                return False
            curNode = curNode[c]

        return True

class Solution:
    def __init__(self):
        self.res = []
        self.obj = Trie()

    def mySolution(self, words, strs):
        for w in words:
            self.obj.insert(w)
        self.dfs('', strs)
        return self.res

    def dfs(self, pre, strs):
        # print(pre, strs)
        if len(strs) == 0:
            if self.obj.search(pre):
                self.res.append(pre)
                return
            else:
                return

        for j in range(len(strs)):
            if j > 0 and strs[j] == strs[j - 1]:
                continue

            # 当前字母加入形成的前缀是否存在, 不存在则截断
            preCur = pre + strs[j]
            if not self.obj.startsWith(preCur):
                continue

            strs = strs[:j] + strs[j+1:]

            # dfs下一个字母
            self.dfs(preCur, strs)

            # 复原
            strs = strs[:j] + preCur[-1] + strs[j:]

words = ['cat', 'dog', 'bee', 'act', 'horse', 'cow']
s = 'tca'

s = ''.join(sorted(s))

sol = Solution()
print(sol.mySolution(words, s))
```

# 感想

这道题暴力的思路比较容易想出来，字典树+DFS+剪枝不太容易写出来，继续加油！！！
