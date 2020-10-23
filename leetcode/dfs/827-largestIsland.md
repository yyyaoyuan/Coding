# 最大人工岛

在二维地图上， 0代表海洋， 1代表陆地，我们最多只能将一格 0 海洋变成 1变成陆地。进行填海之后，地图上最大的岛屿面积是多少？（上、下、左、右四个方向相连的 1 可形成岛屿）

## 示例 1:

输入: [[1, 0], [0, 1]]
输出: 3
解释: 将一格0变成1，最终连通两个小岛得到面积为 3 的岛屿。

## 示例 2:

输入： [[1, 0, 0], [1, 0, 0]]
输出：3
解释: 将一格0变成1，最终连通两个小岛得到面积为 3 的岛屿。

# 解答：深度优先遍历

核心思想：
* 先深度优先搜索记录每个岛屿的面积，然后给每个岛屿标号（从2开始，因为0和1分别代表大海和小岛）。
* 再遍历0的位置，将这个0连着的岛屿面积加一起求最大值。

```python
class Solution:
    def __init__(self):
        self.land = {}
        
    def largestIsland(self, grid):
        m, n = len(grid), len(grid[0])
        res = 0
        
        color = 2
        for i in range(m):             # 深度优先遍历记录小岛的面积
            for j in range(n):
                if grid[i][j] == 1:
                    self.land[color] = self.dfs(grid, i, j, color)
                    res = max(res, self.land[color])   # 记录目前情况下最大小岛的面积
                    color += 1

        for i in range(m):
            for j in range(n):
                if grid[i][j] == 0:   # 遍历0的位置
                    seen = set()
                    S = 1
                    for d in [[0, 1], [0, -1], [1, 0], [-1, 0]]:      # 注意学习这种写法
                        x, y = i + d[0], j + d[1]                     # 注意学习这种写法
                        if 0 <= x < m and 0 <= y < n and grid[x][y] not in seen:
                            if grid[x][y] in self.land:
                                S += self.land[grid[x][y]]
                            seen.add(grid[x][y])   # 防止重复，比如land 2计算过，这里便不再需要计算land 2的面积
                    res = max(S, res)      # 记录算上当前岛屿后的最大面积
                            
        return res
    
    def dfs(self, grid, i, j, color):
        m, n = len(grid), len(grid[0])
        if grid[i][j] != 1:
            return 0
        res = 1
        grid[i][j] = color
        for d in [[0, 1], [0, -1], [1, 0], [-1, 0]]:
            x, y = i + d[0], j + d[1]       
            if 0 <= x < m and 0 <= y < n:
                res += self.dfs(grid, x, y, color)
        return res
```

# 感想

感觉深度优先遍历还是有点太难了，还是需要好好练习，明天继续复习一下！！！，主要需要学习的知识点：
```python
for d in [[0, 1], [0, -1], [1, 0], [-1, 0]]:      # 注意学习这种写法
    x, y = i + d[0], j + d[1]
```
