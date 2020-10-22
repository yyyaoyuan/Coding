# 选择排序

遍历数组，依次挑选最小的，次小的，直至结束。

```python
def select_sort(data):
    n = len(data)
    for i in range(n-1):          # 注意边界
        for j in range(i+1, n):   # 注意边界
            if data[i] > data[j]:
                data[i], data[j] = data[j], data[i]
    return data
```
