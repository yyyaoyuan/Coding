# 有效的括号

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

* 左括号必须用相同类型的右括号闭合。
* 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

示例 1:

输入: "()[]{}"

输出: true

示例 2:

输入: "(]"

输出: false

# 解答一：栈

按照顺序依次进栈，如果出现右括号（右方括号，右大括号）的情况，判断栈顶元素与其是否配对，是的话则将栈顶元素弹出，否则将其压入。

```python
class Solution:
    def isValid(self, s: str) -> bool:
        if not s:
            return True 
        stack = []
        for c in s:
            if not stack:
                stack.append(c)
            elif (stack[-1] == '(' and c == ')') or (stack[-1] == '[' and c == ']') or (stack[-1] == '{' and c == '}'):
                stack.pop()
            else:
                stack.append(c)
        return not stack
```

# 解答二：栈+哈希表

```python
class Solution:
    def isValid(self, s: str) -> bool:
        dic = {')': '(',']': '[','}': '{'}   # 首先使用字典存放配对的字符数组
        stack = []
        for c in s:
            if stack and c in dic:
                if dic[c] != stack.pop():
                    return False
            else: 
                stack.append(c)
            
        return not stack
```

# 感想

腾讯面试时遇见了这道题，当时在面试官的提示下写完了，整体思想不难，但是手生，还是需要多加练习，加油！！！！
