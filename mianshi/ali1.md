# 题目描述

我们称一个数字的前导零为从最高位开始的连续一段0，但不包含最低位。例如，1234，1000，0都是没有前导零的，0000有三个前导零，00123有两个前导零。

定义函数F(x)为将01串x中的所有数字翻转（0变1，1变0），然后删除他的所有前导零。

给出一个不含前导零的01数字串S，求他经过k次F函数运算后得到的串。

## 输入描述：

第一行两个空格分隔的正整数n, k，分别代表S的长度和运算次数。
第二行一个只包含01的数字串S，保证不含前导零。
1 <= n <= 1000
1 <= k <= 10^9

## 输出描述

一行一个数字串代表答案

## 示例1:

输入：

9 3

110001001

输出：

110

# 解答：暴力+剪枝

```python
def process(string, k):
    for i in range(k):
        new_string = []
        for s in string:
            if s == '1':
                new_string.append('0')
            else:
                new_string.append('1')
        new_string = ''.join(new_string)
        string = list(str(int(new_string)))
        
        if len(string) == 1:
           print((int(string[0]) + k - i + 1) % 2)        # 根据剩余长度为偶数还是奇数来计算最终输出结果
           exit()
    print(''.join(string))

n, k = [int(i) for i in input().split(' ')]
string = list(input())
process(string, k)
```














