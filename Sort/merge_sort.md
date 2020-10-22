# 归并排序

先将数组进行拆分，然后进行合并，注意合并时需要进行大小的判断，依次来决定谁先放入结果数组。

```python
def merge_sort(data):
    if len(data) <= 1:
        return data
    n = len(data) // 2
    left = merge_sort(data[:n])     # 注意这里需要赋值给left
    right = merge_sort(data[n:])    # 注意这里需要赋值给right
    l, r = 0, 0
    res = []
    while l < len(left) and r < len(right):
        if left[l] < right[r]:
            res.append(left[l])
            l += 1
        else:
            res.append(right[r])
            r += 1
    res += left[l:]               # 注意在r == len(right)时，直接将剩余的数组添加进来即可
    res += right[r:]              # 注意在l == len(left)时，直接将剩余的数组添加进来即可
    return res
```
