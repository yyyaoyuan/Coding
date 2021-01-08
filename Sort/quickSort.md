# 快速排序


## 解法一：递归

采用递归方法对一个数组进行排序。

```python
class Solution:
    def quickSort(self, arr):
        # write code here
        if not arr:
            return []
        pivot = arr[0]
        left = self.quickSort([x for x in arr[1:] if x < pivot])      # 对小于pivot的所有元素进行快速排序，注意需要去除掉数组的第一个元素，因为是以它为基准。
        right = self.quickSort([x for x in arr[1:] if x >= pivot])    # 对大于等于pivot的所有元素进行快速排序

        return left+[pivot]+right
```

**记住这样的形式，真的非常简洁和优美：[x for x in arr[1:] if x < pivot]**

## 解法二：非递归

快速排序非递归非常重要的思想是把**一个区间的左右索引放入一个栈中**，有多少区间，就把所有区间的左右索引全部放入栈中，每次进行处理的时候，同时弹出栈顶元素的两个区间，然后进行操作。

另一个重要的思想是将划分，将小于某个值（pivot）的元素放在pivot的左右，大于pivot的元素放在它的右边，然后记录pivot最后的索引。

```python
def quickSort(arr):
    if len(arr) <= 1:
        return arr
    stack = []
    stack.append(len(arr) - 1)   # 一个区间的右边界
    stack.append(0)              # 一个区间的左边界
    while stack:
        l = stack.pop()
        r = stack.pop()
        index = partition(arr, l, r)  # 非常重要的操作！！！，划分的同时也要记录pivot的索引
        if l < index - 1:             # 根据当前pivot的位置来判断是否还会有新的区间，如果有，继续将其添加到栈中，否则弹出栈中已有的区间继续进行上述操作，直至栈为空为止。
            stack.append(index - 1)
            stack.append(l)
        if r > index + 1:
            stack.append(r)
            stack.append(index + 1)
    return arr

:
    pivot = arr[l]
    while l < r:
        while l < r and arr[r] >= pivot:   # 判断数组右边哪一个元素小于pivot
            r -= 1
        arr[l] = arr[r]                    # 一旦发现小于pivot的元素，便替换最开始的元素，注意：最开始元素的值已经被记录在pivot中
        while l < r and arr[l] <= pivot:  # 判断数组左边哪一个元素大于pivot
            l += 1
        arr[r] = arr[l]                    # 一旦发现大于pivot的元素，便替换刚才小于pivot的右边元素
    arr[l] = pivot
    return l
```

# 感想：

面试中遇见了这道题，面试官要求写出非递归的快速排序，自己没有写出来，这里好好复习一下，希望以后面试中遇见的话，可以写出来，加油！！！
