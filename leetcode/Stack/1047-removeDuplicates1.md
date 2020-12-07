# 删除字符串中的所有相邻重复项

给出由小写字母组成的字符串 S，重复项删除操作会选择两个相邻且相同的字母，并删除它们。

在 S 上反复执行重复项删除操作，直到无法继续删除。

在完成所有重复项删除操作后返回最终的字符串。答案保证唯一。 

## 示例：

输入："abbaca"

输出："ca"

解释：例如，在 "abbaca" 中，我们可以删除 "bb" 由于两字母相邻且相同，这是此时唯一可以执行删除操作的重复项。之后我们得到字符串 "aaca"，其中又只有 "aa" 可以执行重复项删除操作，所以最后的字符串为 "ca"。

# 栈

使用一个栈帮助记录字符串中的元素，一旦遇见当前的元素和栈顶元素相同的情况，便将栈顶元素弹出，否则压入，直至字符串中的元素遍历完成。

```python
class Solution:
    def removeDuplicates(self, S: str) -> str:
        if not S:
            return S
        stack = []
        for c in S:
            if not stack or stack[-1] != c:   # 注意对于初始值（栈为空）的操作！！！
                stack.append(c)
            else:
                stack.pop()
        return ''.join(stack)  # 注意字符串列表转换成字符串的操作！！！
```

# 感想

这道题是[删除字符串中的所有相邻重复项 II](https://github.com/yyyaoyuan/Coding/blob/master/leetcode/Stack/1209-removeDuplicates.md)的简化版本，该题不需要记录每个字符出现的次数，
因此栈中元素只需要是字符即可。注意学习，继续加油！！！
