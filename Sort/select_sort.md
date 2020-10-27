# 选择排序

遍历数组，依次挑选最小的，次小的，直至结束。

```python
def select_sort(data):
    n = len(data)
    for i in range(n-1):          # 注意边界
        min_idx = i
        for j in range(i+1, n):   # 注意边界
            if data[min_idx] > data[j]:
                min_idx = j
        data[i], data[min_idx] = data[min_idx], data[i]
    return data
```
