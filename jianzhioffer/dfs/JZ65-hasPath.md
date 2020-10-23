# 题目描述

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。
路径可以从矩阵中的任意一个格子开始，每一步可以在矩阵中向左，向右，向上，向下移动一个格子。如果一条路径经过了矩阵中的某一个格子，则该路径不能再进入该格子。 
例如"abcesfcsadee", 3行4列，矩阵中包含一条字符串"bcced"的路径，但是矩阵中不包含"abcb"路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入该格子。

# 解答一

该题思路就是判断第一个符合条件的字符后进行深度优先遍历，如果找到返回True，否则回溯回去，寻找下一个符合条件的字符，重复进行，直至全部搜索完毕。
自己实现的深度优先遍历和回溯算法，调试了很久，写得比较复杂和冗余，写在这里算是一个纪念吧。

```python
class Solution:
    def __init__(self):
        self.shift = [[0, 1], [0, -1], [1, 0], [-1, 0]] # 坐标位移数组，以后自己就用这种写法吧，比较简洁
        self.arr = []       # 该数组用于记录是否已经访问过

    def hasPath(self, newmatrix, rows, cols, path1):
        # write code here
        if not path1:
            return True
        path = list(path1)
        matrix = [['0' for i in range(cols)] for j in range(rows)]
        k = 0
        
        for i in range(rows):   # 将字符串转换成矩阵
            for j in range(cols):
                matrix[i][j] = list(newmatrix).pop(k)
                k += 1
        print(matrix)

        self.arr = [[0 for i in range(cols)] for j in range(rows)] # 初始化arr数组
        for i in range(rows):
            for j in range(cols):
                    if not path:
                        return True
                    if matrix[i][j] == path[0] and self.arr[i][j] == 0:
                        path.pop(0)
                        if self.dfs(matrix, self.arr, i, j, path):
                            return True
                        else:      # 进行回溯
                            self.arr = [[0 for m in range(cols)] for n in range(rows)]
                            path = list(path1)
                            continue
        return False
        
    def dfs(self, matrix, arr, i, j, path):
        m, n = len(arr), len(arr[0])
        if not path:  # 表明完全匹配了
            return True
        if i < 0 or i >= m or j < 0 or j >= n or arr[i][j] == 1: # 超出边界条件以及已经访问过
            return False
        arr[i][j] = 1  # 更改arr数组，代表i, j访问过
        for d in self.shift:
            x, y = i + d[0], j + d[1]
            if 0 <= x < m and 0 <= y < n and matrix[x][y] == path[0] and arr[x][y] == 0: # 注意判断x, y是否越界！！！
                tmp = path[:]
                path.pop(0)
                if self.dfs(matrix, arr, x, y, path):
                    return True
                else:    # 进行回溯
                    path = tmp
                    continue
```

# 解答二
