# 题目描述

输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则按字典序打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

# 解答一：递归求解

* 递归终止条件：len(ss) <= 1
* 递归主体：
  * 遍历字符串中的每一个元素ss[i]
  * 遍历字符串中除去ss[i]后的所有元素的全排列，然后与ss[i]拼接上即可装入结果集合中。

```python
class Solution:
    def Permutation(self, ss):
        # write code here
        if len(ss) <= 1:
            return ss
        res = set()
        for i in range(len(ss)):
            for j in self.Permutation(ss[:i] + ss[i+1:]):   # 这句代码非常巧妙，因为我们的函数就是要返回一个全排列，所以在这里对返回的全排列进行遍历！！！！
                res.add(ss[i] + j)
        return sorted(res)
```

# 解答二：递归求解，dfs

```python
# -*- coding:utf-8 -*-
class Solution:
    def Permutation(self, ss):
        # write code here
        if len(ss) <= 1:
            return ss
        self.res = set()
        ss = list(ss)
        self.dfs(ss, 0)
        return sorted(self.res)
    def dfs(self, ss, i):
        if i == len(ss) - 1:
            self.res.add(''.join(ss))
            return
        for j in range(i, len(ss)):       # 注意这里是从i开始遍历！！！
            ss[j], ss[i] = ss[i], ss[j]   # 将第j个元素与第i个元素交换位置，表示使用ss[j]作为开始元素，然后利用dfs去寻找出去ss[j]后的所有元素的全排列
            self.dfs(ss, i+1)
            ss[j], ss[i] = ss[i], ss[j]   # 这里对列表元素进行复原，以便进行下一次的替换操作！！！
```

# 感想

字符串全排列问题还是有些绕，后面继续思考一下，加油！！！！
