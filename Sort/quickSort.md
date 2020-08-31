# 快速排序

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
