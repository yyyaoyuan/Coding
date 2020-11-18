# 岛屿数量

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。此外，你可以假设该网格的四条边均被水包围。

## 示例 1：

输入：grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
输出：1

# 解答

深度优先遍历，对所有相连接的岛进行附色，从0开始，最后染了几种染色，岛屿数便是几。

```python
class Solution:
    def __init__(self):
        self.shift = [[0, 1], [0, -1], [1, 0], [-1, 0]]
    def numIslands(self, grid):
        m, n = len(grid), len(grid[0])
        color = 2
        for i in range(m):
            for j in range(n):
                if grid[i][j] == '1':
                    self.dfs(grid, i, j, color)
                    color += 1
        return color - 2
    
    def dfs(self, grid, i, j, color):
        m, n = len(grid), len(grid[0])
        if i < 0 or i >= m or j < 0 or j >= n or grid[i][j] != '1':
            return
        grid[i][j] = color
        for d in self.shift:
            self.dfs(grid, i + d[0], j + d[1], color)
```

# 感想

这道题比最大海岛面积容易一点，最大海岛面积的求解思路包含了该问题的求解思路，仔细体会，现在基本了解了dfs算法的使用。继续加油！！！
