# 题目描述

每年六一儿童节,牛客都会准备一些小礼物去看望孤儿院的小朋友,今年亦是如此。HF作为牛客的资深元老,自然也准备了一些小游戏。

其中,有个游戏是这样的:首先,让小朋友们围成一个大圈。然后,他随机指定一个数m,让编号为0的小朋友开始报数。

每次喊到m-1的那个小朋友要出列唱首歌,然后可以在礼品箱中任意的挑选礼物,并且不再回到圈中,从他的下一个小朋友开始,继续0...m-1报数....这样下去....直到剩下最后一个小朋友,可以不用表演,

并且拿到牛客名贵的“名侦探柯南”典藏版(名额有限哦!!^_^)。请你试着想下,哪个小朋友会得到这份礼品呢？(注：小朋友的编号是从0到n-1)

如果没有小朋友，请返回-1

# 解答一

利用list做成循环链表，注意当遍历到末尾的时候修改指针为0。具体思路如下：
* 使用list模拟循环链表，用cur作为指向list的下标位置。
* 当cur移到list末尾直接指向list头部，当删除一个数后list的长度和cur的值相等则cur指向0

```python
class Solution:
    def LastRemaining_Solution(self, n, m):
        # write code here
        if n < 1 or m < 1:
            return -1
        children = list(range(n))
        cur = 0
        while len(children) != 1:
            for _ in range(1, m):   # 注意这里是从1开始到m-1
                cur += 1
                if cur == len(children):
                    cur = 0
            children.remove(children[cur])
            if cur == len(children):
                    cur = 0
        return children[0]
```

# 解答二

数学归纳法，一直没有看懂。。。。先过。
