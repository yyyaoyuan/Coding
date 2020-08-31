# 题目描述

给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。（注意：规定B[0] = A[1] * A[2] * ... * A[n-1]，B[n-1] = A[0] * A[1] * ... * A[n-2];）
对于A长度为1的情况，B无意义，故而无法构建，因此该情况不会存在。

# 解答一

暴力求解，两重循环遍历即可。

```python
def multiply(self, A):
        # write code here
        n = len(A)
        B = [0]*n
        if n <= 1:
            return -1
        for i in range(n):
            mul = 1
            for j in range(n):
                if i != j:
                    mul *= A[j]
            B[i] = mul
        return B
```

# 解答二

解答二需要发现规律，因为每次都是除掉自身位置，所以按照对角线的防线可以分成上三角和下三角两部分，然后分别进行求解。

```python
class Solution:
    def multiply(self, A):
        n = len(A)
        B = [1]*n
        C = [1]*n
        for i in range(n-1):        # 先求出下三角的部分
            B[i+1] = B[i]*A[i]
        
        for i in range(n-2,-1,-1):  # 再求出上三角的部分
            C[i] = C[i+1]*A[i+1]
        
        for i in range(n):          # 进行合并
            B[i] *= C[i]
        
        return B
```


