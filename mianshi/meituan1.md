# 美团第一题

# 题目描述

小团有一个nxm的矩阵A，他知道这是小美用一种特殊的方法生成的，具体规则如下：小美首先写下一个nxm的矩阵，然后小妹每一次将这个矩阵上下翻转后接到原矩阵的下方。
小美重复这个过程若干次（甚至可能是0次，也就是没有进行郭这一操作），然后将操作后的矩阵交给小团。

小团想知道，小美一开始写下的矩阵是什么。因为小美可能有多种一开始的矩阵，小团想得到最小的矩阵（这里的最小值矩阵即nxm的面积最小）。

## 输入描述

输入包含两个整数n，m，表示小团矩阵的大小。
接下来n行，每行m个正整数，第i行第j列表示矩阵第i行第j列的数。
1 <= n <= 100000, 1 <= m <= 5，矩阵内的数小于等于10。

## 输出描述

输出包含一个矩阵，一共n行m列，表示小美一开始最小的矩阵。

## 样例输入

8 3

1 0 1

0 1 0

0 1 0

1 0 1

1 0 1

0 1 0

0 1 0

1 0 1

## 样例输出

1 0 1
0 1 0

## 样例解释

1.
1 0 1
0 1 0

2.
1 0 1
0 1 0
0 1 0
1 0 1

3.
1 0 1
0 1 0
0 1 0
1 0 1
1 0 1
0 1 0
0 1 0
1 0 1

其中最小的矩阵为第一种。

# 解答

```python
def process(matrix, n, m):
    def judge(matrix, i):
        reverse_matrix = matrix[:i][::-1]
        flag = True
        for idx in range(0, len(matrix), i):
            if (idx // i) % 2 == 0 and matrix[idx:idx+1] != matrix[0:i]:
                flage = False
            elif (idx // i) % 2 == 1 and matrix[idx:idx+i] != reverse_matrix:
                flag = False
        return flag
    min_rows = 2
    while min_rows < n:
       if n % min_rows != 0:
           min_rows += 1
           continue
       res = judge(matrix, min_rows)
       if res:
           break
       min_rows += 1
    for i in range(min_rows):
        print(' '.join([str(item) for item in matrix[i]]))
 
n, m = [int(item) for item in input().split(' ')]
matrix = []
for _ in range(n):
    matrix.append([int(item) for item in input().split(' ')])
process(matrix, n, m)
```
