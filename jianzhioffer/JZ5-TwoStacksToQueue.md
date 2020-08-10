# 题目描述
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

# 解答
因为栈是先进后出，队列是先进先出，所以利用两个栈的话便可以实现先进先出，具体如下：
一个栈stack_1用来压（push）数据，一个栈stack_2用来弹（pop）数据；
在弹数据时，需要进行判断是否stack_2为空，如果非空，直接弹出stack_2中的数据；如果为空，则将所有stack_1中的数据全部弹出后压进stack_2，此时便可以实现先进去stack_1的数据便会先弹出来，实现先进先出的功能。
具体代码实现如下：
```
class Solution:
    def __init__(self):
        self.stack_1 = []
        self.stack_2 = []
    def push(self, node):
        # write code here
        self.stack_1.append(node)
    def pop(self):
        if self.stack_2 == []:
            while self.stack_1:
                  self.stack_2.append(self.stack_1.pop())
        return self.stack_2.pop()
```

# 感想
该题是我开始刷牛客网剑指offer的第一题，也是人生中刷的第一道题。首先我看到这道题时，整个人是很懵的，完全不懂如何下手。
因此，只能在网上搜寻答案，看到答案后，又去了解了一下python的基础知识，才算是稍微理解了这道题的解法，现在以此为记录，希望自己不要太快忘记。
另外，也希望自己刷两个星期的题后，再看到类似的题可以得心应手，万事开头难，我相信我可以过了刷题这一关，我一定可以！
