# 题目描述

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，
如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

# 解答

* 设置4个指针，分别控制行的两边和列的两边。
* 然后判断两种特殊情况，一种是只有一行，一种是只有一列。
* 接着利用4个循环按照规则进行遍历，注意边界的处理。
* 最后更新指针。

```python
class Solution:
    # matrix类型为二维列表，需要返回列表
    def printMatrix(self, matrix):
        # write code here
        left = 0
        right = len(matrix[0]) - 1
        
        up = 0
        down = len(matrix) - 1
        
        res = []
        
        while left <= right and up <= down:
            if left == down:                     # 注意条件判断，只有一行的情况
                for i in range(left, right+1):
                    res.append(matrix[left][i])
                return res                       # return的位置不要弄错了
            if up == right:                      # 注意条件判断，只有一列的情况
                for i in range(up, down+1):
                    res.append(matrix[i][up])
                return res
                
            for i in range(left, right):         # 从左到右写入列表
                res.append(matrix[left][i])
                
            for i in range(up, down):            # 从上到下写入列表
                res.append(matrix[i][right])
                
            for i in range(right, left, -1):     # 从右到左写入列表
                res.append(matrix[down][i])
                
            for i in range(down, up, -1):        # 从下到上写入列表
                res.append(matrix[i][up])
                
            left += 1
            up += 1
            right -= 1
            down -= 1
        return res
```

# 感想

这个问题挺好的，一开始想到了使用4个指针，但是没搞清楚具体应该怎么赋值，还是需要多练习！加油！加油！加油！
