# 删除字符串中的所有相邻重复项 II

给你一个字符串 s，「k 倍重复项删除操作」将会从 s 中选择 k 个相邻且相等的字母，并删除它们，使被删去的字符串的左侧和右侧连在一起。

你需要对 s 重复进行无限次这样的删除操作，直到无法继续为止。

在执行完所有删除操作后，返回最终得到的字符串。

本题答案保证唯一。

## 示例 1：

输入：s = "abcd", k = 2
输出："abcd"
解释：没有要删除的内容。

## 示例 2：

输入：s = "deeedbbcccbdaa", k = 3
输出："aa"
解释： 
先删除 "eee" 和 "ccc"，得到 "ddbbbdaa"
再删除 "bbb"，得到 "dddaa"
最后删除 "ddd"，得到 "aa"

# 解答：使用栈辅助进行处理

* 使用一个栈装元素，同时记录相同元素出现的个数！！！

```python
class Solution:
    def removeDuplicates(self, s: str, k: int) -> str:
        if not s or k > len(s):
            return s 
        stack = []
        for c in s:
            if not stack or stack[-1][0] != c:  # 对初始状态的判断可以使用这种方式，注意学习
                stack.append([c, 1])      # 特别要注意学习这种写法
            elif stack[-1][1] + 1 < k:
                stack[-1][1] += 1
            else:
                stack.pop()
        ans = ''
        for s, l in stack:   # 对元素对的存取方法！！！
            ans += s * l     # 对字符元素的处理方式
        return ans 
```

# 感想

这道题需要学习新的知识点：

* 栈刚开始的处理方法：if not stack or stack[-1][0] != c

* 将元素和元素个数一起放进栈中：stack.append([c, 1])，**第一次遇见这种写法，注意学习！！！栈中可以追加列表元素，注意活学活用！！！**

* '1' * 3 = '111'
