# 求一个正数的平方根

# 解法

面试中遇见了这道题，首先先看一个最简单的场景：求一个整数的平方根，并且该整数可以求出整数平方根。

思路：最简单的方法进行遍历，因为可以求出整数平方根，所以只需要循环遍历便可以求出结果。

```python
def mySqrt(N):
    for i in range(N):
        if abs(i*i - N) == 0:
            return i
```

在接下来对上述方法进行改进：上述时间复杂度为O(N)，一般这种改进就是想办法改成O(log N)，所以很自然的可以想到二分查找。

```python
def mySqrt(N):
    left = 0
    right = N
    while left < right:
        mid = (left+right) // 2         # 这里写错了，一定要记住是(left+right) // 2，而不是N // 2
        if mid*mid-N < 0:
            left = mid + 1
        elif mid*mid-N > 0:
            right = mid
        else:
            return mid
```

最后，是进阶版，考虑小数的情况，以及没有整数平方根的情况。**这里需要特别注意小于1的情况，此时需要在[0,1]区间进行二分，而不是[0,x]。**

```python
def mySqrt4(x, e):
    left = 0
    right = max(x, 1.0) # 这里需要注意分为两种情况处理：大于1和小于1

    while left < right:
        mid = (left + right) / 2.0
        if abs(mid**2-x) < e:
            break
        if mid**2 < x:
            left = mid
        else:
            right = mid
    return mid
```

# 感想
这是面试
