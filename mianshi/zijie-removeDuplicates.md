# 字节面试题：删除字符串中的所有相邻重复项（大于等于k）

给你一个字符串 s，从 s 中选择数量大于等于 k 个的相邻且相等的字母，并删除它们，使被删去的字符串的左侧和右侧连在一起。

你需要对 s 重复进行无限次这样的删除操作，直到无法继续为止。

在执行完所有删除操作后，返回最终得到的字符串。

本题答案保证唯一。

## 示例1:

输入：s = "4444111100", k = 4 

输出："00"

## 示例2:

输入：s = "001144441111005", k = 4 

输出："5"


# 解答：双栈处理

* 首先使用一个栈stack1存储每个字符以及出现的次数
* 然后使用一个栈stack2存储满足条件的字符以及出现的次数，此时需要注意字符的删除操作


```python
def removeDuplicates(s, k):
    if not s or k > len(s):
        return s
    stack1 = []
    stack2 = []

    for c in s:
        if not stack1 or stack1[-1][0] != c:
            stack1.append([c, 1])
        else:
            stack1[-1][1] += 1

    for c, n in stack1:             # 特别需要注意下面的判断条件！！！！
        if not stack2:
            stack2.append([c, n])
        elif n < k:
            if stack2[-1][0] != c:
                stack2.append([c, n])
            elif stack2[-1][1] + n >= k:
                stack2.pop()
        elif stack2[-1][0] == c:
            stack2.pop()

    ans = ''
    for c, n in stack2:
        ans += c * n

    return ans
```

# 感想

字节跳动面试中遇见了这道题，当时想到了用栈进行解决，但是没有写出答案，后面自己学习了题目[1209-删除字符串中的所有相邻重复项 II](https://github.com/yyyaoyuan/Coding/blob/master/leetcode/Stack/1209-removeDuplicates.md)，
然后仿照了写了出来，说实话还是有一些难度的，自己调试了很久猜得到正确的结果，继续加油！！！！！！
