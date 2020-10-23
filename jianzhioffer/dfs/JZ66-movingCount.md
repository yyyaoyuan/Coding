# 题目描述

地上有一个m行和n列的方格。一个机器人从坐标0,0的格子开始移动，每一次只能向左，右，上，下四个方向移动一格，但是不能进入行坐标和列坐标的数位之和大于k的格子。 例如，当k为18时，机器人能够进入方格（35,37），因为3+5+3+7 = 18。但是，它不能进入方格（35,38），因为3+5+3+8 = 19。请问该机器人能够达到多少个格子？

# 解答：深度优先遍历+回溯

核心思路：首先利用一个二维数组记录每一个方格是否可以到达，先初始化为0表示不可到达，如果可以到达将其改为1，并令计数+1，然后对上下左右进行递归遍历.

```python
class Solution:
    def __init__(self):
        self.count = 0            # 注意这种用法，先初始化一个count，令其为0，便可以达到全局变量的效果
    def movingCount(self, threshold, rows, cols):
        arr = [[0 for i in range(cols)] for j in range(rows)]   # 注意这种初始化而为数组的写法
        self.dfs(arr, 0, 0, threshold)   # dfs开始，先输入0, 0
        return self.count
    def dfs(self, arr, i, j, k):
        if i < 0 or j < 0 or i >= len(arr) or j >= len(arr[0]):  # 注意边界条件的写法
            return
        tmpi = list(map(int, list(str(i))))   # 重点学习对象，map进行改变格式
        tmpj = list(map(int, list(str(j))))
        if sum(tmpi) + sum(tmpj) > k or arr[i][j] != 0:  # 注意边界条件的写法
            return
        arr[i][j] = 1
        self.count += 1
        self.dfs(arr, i+1, j, k)    # 重点学习对象，dfs的递归遍历
        self.dfs(arr, i-1, j, k)
        self.dfs(arr, i, j+1, k)
        self.dfs(arr, i, j-1, k)
```

# 感想

第一次做深度优先遍历+回溯的题目，记住解决方案，并且这里有很多需要学习的知识点，先将其总结如下：
* 首先定义一个init函数，可以设置一个变量self.count，其可以起到全局变量的作用，所有函数中均可对其进行操作
* 二维数组的定义：arr = [[0 for i in range(cols)] for j in range(rows)]     rows*cols
* tmpi = list(map(int, list(str(i))))，map用来改变列表的格式，将其从字符串类型改成int型

这里需要学习的真的很多，好好记住，加油！！！
