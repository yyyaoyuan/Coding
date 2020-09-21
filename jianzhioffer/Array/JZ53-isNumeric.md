# 题目描述

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

# 解答一

写规则判断所有可能：
* 对于e的情况:
  * 不同出现两个e
  * e不能出现在最后面，因为e后面要接数字
* 对于符号位的情况:
  * 如果前面已经出现过了符号位，那么这个符号位，必须是跟在e后面的
  *  如果这是第一次出现符号位，而且出现的位置不是字符串第一个位置，那么就只能出现在e后面
* 对于小数点的情况：
  * 小数点不能出现两次；而且如果已经出现过e了，那么就不能再出现小数点，因为e后面只能是整数
  * 如果是第一次出现小数点，小数点不能在最后面

```python
class Solution:
    # s字符串
    def isNumeric(self, s):
        # write code here
        if len(s) <= 0:
            return False
        # 分别标记是否出现过正负号、小数点、e，因为这几个需要特殊考虑
        hasSign = False
        hasPoint = False
        hasE = False
        for i in range(len(s)):
            # 对于e的情况
            if s[i] == 'E' or s[i] == 'e':
                if hasE:                 # 不同出现两个e
                    return False
                else:                    # e不能出现在最后面，因为e后面要接数字
                    hasE = True
                    if i == len(s) - 1 or i == 0:
                        return False
            # 对于符号位的情况
            elif s[i] == '+' or s[i] == '-':
                # 如果前面已经出现过了符号位，那么这个符号位，必须是跟在e后面的
                if hasSign:
                    if s[i-1] != 'e' and s[i-1] != 'E':
                        return False
                # 如果这是第一次出现符号位，而且出现的位置不是字符串第一个位置，那么就只能出现在e后面
                else:
                    hasSign = True
                    if i > 0 and s[i-1] != 'e' and s[i-1] != 'E':
                        return False
            # 对于小数点的情况
            elif s[i] == '.':
                # 小数点不能出现两次；而且如果已经出现过e了，那么就不能再出现小数点，因为e后面只能是整数
                if hasPoint or hasE:
                    return False
                # 如果是第一次出现小数点，小数点不能在最后面
                else:
                    hasPoint = True
                    if i == len(s) - 1:
                        return False
            else:
                if s[i] < '0' or s[i] > '9':   # 其他字符必须是‘0’到‘9’之间的
                    return False
        return True
```

# 解答二

正则表达式：
* ^XXXXX$，^代表开头，$代表结尾
* 第一部分：[\+\-]?          # [\+\-]代表\+或者\-出现一次，?代表前一个字符出现0次或者1次
* 第二部分：\d*(\.\d+)?      # \*代表前一个字符出现0次或者无限次，\+代表前一个字符出现1次或者无限次
* 第三部分：([eE][\+\-]?\d+)?

```python
import re
class Solution:
    # s字符串
    def isNumeric(self, s):
        # write code here
        p = re.compile(r'^[\+\-]?\d*(\.\d+)?([eE][\+\-]?\d+)?$')
        return p.match(s)
```

# 感想
